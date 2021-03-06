<properties
   pageTitle="Create a Linux VM with multiple NICs | Microsoft Azure"
   description="Learn how to create a Linux VM with multiple NICs attached to it using the Azure CLI or Resource Manager templates."
   services="virtual-machines-linux"
   documentationCenter=""
   authors="iainfoulds"
   manager="timlt"
   editor=""/>

<tags
   ms.service="virtual-machines-linux"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="vm-linux"
   ms.workload="infrastructure"
   ms.date="10/27/2016"
   ms.author="iainfou"/>

# <a name="creating-a-linux-vm-with-multiple-nics"></a>Creating a Linux VM with multiple NICs
You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it. A common scenario would be to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution. This article provides quick commands to create a VM with multiple NICs attached to it. For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Different [VM sizes](virtual-machines-linux-sizes.md) support a varying number of NICs, so size your VM accordingly.

>[AZURE.WARNING] You must attach multiple NICs when you create a VM - you cannot add NICs to an existing VM. You can [create a VM based on the original virtual disk(s)](virtual-machines-linux-copy-vm.md) and create multiple NICs as you deploy the VM.

## <a name="quick-commands"></a>Quick commands
Make sure that you have the [Azure CLI](../xplat-cli-install.md) logged in and using Resource Manager mode:

```bash
azure config mode arm
```

In the following examples, replace example parameter names with your own values. Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myVM`.

First, create a resource group. The following example creates a resource group named `myResourceGroup` in the `WestUS` location:

```bash
azure group create myResourceGroup -l WestUS
```

Create a storage account to hold your VMs. The following example creates a storage account named `mystorageaccount`:

```bash
azure storage account create mystorageaccount -g myResourceGroup \
    -l WestUS --kind Storage --sku-name PLRS
```

Create a virtual network to connect your VMs to. The following example creates a virtual network named `myVnet` with an address prefix of `192.168.0.0/16`:

```bash
azure network vnet create -g myResourceGroup -l WestUS \
    -n myVnet -a 192.168.0.0/16
```

Create two virtual network subnets - one for front-end traffic and one for back-end traffic. The following example creates two subnets, named `mySubnetFrontEnd` and `mySubnetBackEnd`:

```bash
azure network vnet subnet create -g myResourceGroup -e myVnet \
    -n mySubnetFrontEnd -a 192.168.1.0/24
azure network vnet subnet create -g myResourceGroup -e myVnet \
    -n mySubnetBackEnd -a 192.168.2.0/24
```

Create two NICs, attaching one NIC to the front-end subnet and one NIC to the back-end subnet. The following example creates two NICs, named `myNic1` and `myNic2`, and attaches them to your subnets:

```bash
azure network nic create -g myResourceGroup -l WestUS \
    -n myNic1 -m myVnet -k mySubnetFrontEnd
azure network nic create -g myResourceGroup -l WestUS \
    -n myNic2 -m myVnet -k mySubnetBackEnd
```

Finally, create your VM, attaching the two NICs you previously created. The following example creates a VM named `myVM`:

```bash
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location WestUS \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username ops \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="creating-multiple-nics-using-azure-cli"></a>Creating multiple NICs using Azure CLI
If you have previously created a VM using the Azure CLI, the quick commands should be familiar. The process is the same to create one NIC or multiple NICs. You can read more details about [deploying multiple NICs using the Azure CLI](../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.

The following example creates two NICs, named `myNic1` and `myNic2`, with one NIC connecting to each subnet:

```bash
azure network nic create --resource-group myResourceGroup --location WestUS \
    -n myNic1 --subnet-vnet-name myVnet --subnet-name mySubnetFrontEnd
azure network nic create --resource-group myResourceGroup --location WestUS \
    -n myNic2 --subnet-vnet-name myVnet --subnet-name mySubnetBackEnd
```

Typically you also create a [Network Security Group](../virtual-network/virtual-networks-nsg.md) or [load balancer](../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs. Again, the commands are the same when working with multiple NICs. The following example creates a Network Security Group named `myNetworkSecurityGroup`:

```bash
azure network nsg create --resource-group myResourceGroup --location WestUS \
    --name myNetworkSecurityGroup
```

Bind your NICs to the Network Security Group using `azure network nic set`. The following example binds `myNic1` and `myNic2` with `myNetworkSecurityGroup`:

```bashazure 
azure network nic set --resource-group myResourceGroup --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set --resource-group myResourceGroup --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

When creating the VM, you now specify multiple NICs. Rather using `--nic-name` to provide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs. You also need to take care when you select the VM size. There are limits for the total number of NICs that you can add to a VM. Read more about [Linux VM sizes](virtual-machines-linux-sizes.md). The following example shows how to specify multiple NICs and then a VM size that supports using multiple NICs (`Standard_DS2_v2`):

```bash
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location WestUS \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username ops \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="creating-multiple-nics-using-resource-manager-templates"></a>Creating multiple NICs using Resource Manager templates
Azure Resource Manager templates use declarative JSON files to define your environment. You can read an [overview of Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs. You use *copy* to specify the number of instances to create:

```bash
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Read more about [creating multiple instances using *copy*](../resource-group-create-multiple.md). 

You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:

```bash
"name": "[concat('myNic', copyIndex())]", 
```

You can read a complete example of [creating multiple NICs using Resource Manager templates](../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Next steps
Make sure to review [Linux VM sizes](virtual-machines-linux-sizes.md) when trying to creating a VM with multiple NICs. Pay attention to the maximum number of NICs each VM size supports. 

Remember that you cannot add additional NICs to an existing VM, you must create all the NICs when you deploy the VM. Take care when planning your deployments to make sure that you have all the required network connectivity from the outset.