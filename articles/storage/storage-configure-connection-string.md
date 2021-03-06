<properties 
    pageTitle="Configure a Connection String to Azure Storage | Microsoft Azure"
    description="Configure a connection string to an Azure storage account. A connection string includes the information needed to authenticate access to a storage account from your application at runtime."
    services="storage"
    documentationCenter=""
    authors="tamram"
    manager="carmonm"
    editor="tysonn"/>

<tags
    ms.service="storage"
    ms.workload="storage"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/18/2016"
    ms.author="tamram"/>

# <a name="configure-azure-storage-connection-strings"></a>Configure Azure Storage Connection Strings

## <a name="overview"></a>Overview

A connection string includes the authentication information needed to access data in an Azure storage account from your application at runtime. You can configure a connection string to:

- Connect to the Azure storage emulator.
- Access a storage account in Azure.
- Access specified resources in Azure via a shared access signature (SAS).

[AZURE.INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>Storing your connection string

Your application will need to access the connection string at runtime in order to authenticate requests made to Azure Storage. You have a few different options for storing your connection string:

- For an application running on the desktop or on a device, you can store the connection string in an `app.config `file or a `web.config` file. Add the connection string to the **AppSettings** section.
- For an application running in an Azure cloud service, you can store your connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx). Add the connection string to the **ConfigurationSettings** section of the service configuration file.
- You can also use your connection string directly in your code. For most scenarios, however, we recommend that you store your configuration string in a configuration file.

Storing your connection string within a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud. You only need to edit the connection string to point to your target environment.

You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) class to access your connection string at runtime regardless of where your application is running.

## <a name="create-a-connection-string-to-the-storage-emulator"></a>Create a connection string to the storage emulator

[AZURE.INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

See [Use the Azure Storage Emulator for Development and Testing](storage-use-emulator.md) for more information about the storage emulator.

## <a name="create-a-connection-string-to-an-azure-storage-account"></a>Create a connection string to an Azure storage account

To create a connection string to your Azure storage account, use the connection string format below. Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:

    DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey

For example, your connection string will look similar to the following sample connection string:

    DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>

> [AZURE.NOTE] Azure Storage supports both HTTP and HTTPS in a connection string; however, using HTTPS is highly recommended.

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>Create a connection string using a shared access signature

[AZURE.INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="creating-a-connection-string-to-an-explicit-storage-endpoint"></a>Creating a connection string to an explicit storage endpoint

You can explicitly specify the service endpoints in your connection string instead of using the default endpoints. To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:

    DefaultEndpointsProtocol=[http|https];
    BlobEndpoint=myBlobEndpoint;
    QueueEndpoint=myQueueEndpoint;
    TableEndpoint=myTableEndpoint;
    FileEndpoint=myFileEndpoint;
    AccountName=myAccountName;
    AccountKey=myAccountKey

One scenario where you may wish to do specify an explicit endpoint is if you have mapped your Blob storage endpoint to a custom domain. In that case, you can specify your custom endpoint for Blob storage in your connection string, and optionally specify the default endpoints for the other service if your application uses them.

Here are examples of valid connection strings that specify an explicit endpoint for the Blob service:

    # Blob endpoint only
    DefaultEndpointsProtocol=https;
    BlobEndpoint=www.mydomain.com;
    AccountName=storagesample;
    AccountKey=account-key

    # All service endpoints
    DefaultEndpointsProtocol=https;
    BlobEndpoint=www.mydomain.com;
    FileEndpoint=myaccount.file.core.windows.net;
    QueueEndpoint=myaccount.queue.core.windows.net;
    TableEndpoint=myaccount;
    AccountName=storagesample;
    AccountKey=account-key

The endpoint value that is listed in the connection string is used to construct the request URIs to the Blob service, and it dictates the form of any URIs that are returned to your code.

Note that if you choose to omit a service endpoint from the connection string, then you will not be able to use that connection string to access data in that service from your code.

### <a name="creating-a-connection-string-with-an-endpoint-suffix"></a>Creating a connection string with an endpoint suffix

To create a connection string for storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Governance, use the following connection string format. Indicate whether you want to connect to the storage account through HTTP or HTTPS, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:


    DefaultEndpointsProtocol=[http|https];
    AccountName=myAccountName;
    AccountKey=myAccountKey;
    EndpointSuffix=mySuffix;


For example, your connection string should look similar to the following connection string:

    DefaultEndpointsProtocol=https;
    AccountName=storagesample;
    AccountKey=<account-key>;
    EndpointSuffix=core.chinacloudapi.cn;

## <a name="parsing-a-connection-string"></a>Parsing a connection string

[AZURE.INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]


## <a name="next-steps"></a>Next steps

- [Use the Azure Storage Emulator for Development and Testing](storage-use-emulator.md)
- [Azure Storage Explorers](storage-explorers.md)
- [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md)
