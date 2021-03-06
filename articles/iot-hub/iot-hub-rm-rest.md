<properties
    pageTitle="Create an IoT Hub using the REST API | Microsoft Azure"
    description="Follow this tutorial to get started using the REST API to create an IoT Hub."
    services="iot-hub"
    documentationCenter=".net"
    authors="dominicbetts"
    manager="timlt"
    editor=""/>

<tags
     ms.service="iot-hub"
     ms.devlang="dotnet"
     ms.topic="article"
     ms.tgt_pltfrm="na"
     ms.workload="na"
     ms.date="08/16/2016"
     ms.author="dobett"/>

# <a name="tutorial-create-an-iot-hub-using-a-c-program-and-the-rest-api"></a>Tutorial: Create an IoT hub using a C# program and the REST API

[AZURE.INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introduction

You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically. This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.

> [AZURE.NOTE] Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../resource-manager-deployment-model.md).  This article covers using the Azure Resource Manager deployment model.

To complete this tutorial, you need the following:

- Microsoft Visual Studio 2015.
- An active Azure account. <br/>If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.
- [Microsoft Azure PowerShell 1.0][lnk-powershell-install] or later.

[AZURE.INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Prepare your Visual Studio project

1. In Visual Studio, create a Visual C# Windows project using the **Console Application** project template. Name the project **CreateIoTHubREST**.

2. In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.

3. In Nuget Package Manager, check **Include prerelease**, and search for **Microsoft.Azure.Management.ResourceManager**. Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.

4. In Nuget Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.

6. In Program.cs, replace the existing **using** statements with the following:

    ```
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```
    
7. In Program.cs, add the following static variables replacing the placeholder values. You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial. **Resource group name** is the name of the resource group you use when you create the IoT hub, it can be a pre-existing resource group or a new one. **IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub** (this name must be globally unique, so it should include your name or initials). **Deployment name** is a name for the deployment, such as **Deployment_01**.

    ```
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    
    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```

[AZURE.INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-the-rest-api-to-create-an-iot-hub"></a>Use the REST API to create an IoT hub

Use the [IoT Hub REST API][lnk-rest-api] to create an IoT hub in your resource group. You can also use the REST API to make changes to an existing IoT hub.

1. Add the following method to Program.cs:
    
    ```
    static void CreateIoTHub(string token)
    {
        
    }
    ```

2. Add the following code to the **CreateIoTHub** method to create an **HttpClient** object with the authentication token in the headers:

    ```
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. Add the following code to the **CreateIoTHub** method to describe the IoT hub to create and generate a JSON representation (for the current list of locations that support IoT Hub see [Azure Status][lnk-status]):

    ```
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };
    
    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. Add the following code to the **CreateIoTHub** method to submit the REST request to Azure, check the response, and retrieve the URL you can use to monitor the state of the deployment task:

    ```
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;
      
    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }
    
    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. Add the following code to the end of the **CreateIoTHub** method to use the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:

    ```
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. Add the following code to the end of the **CreateIoTHub** method to retrieve the keys of the IoT hub you created and print them to the console:

    ```
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2015-08-15-preview", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;
    
    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```
    
## <a name="complete-and-run-the-application"></a>Complete and run the application

You can now complete the application by calling the **CreateIoTHub** method before you build and run it.

1. Add the following code to the end of the **Main** method:

    ```
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```
    
2. Click **Build** and then **Build Solution**. Correct any errors.

3. Click **Debug** and then **Start Debugging** to run the application. It may take several minutes for the deployment to run.

4. You can verify that your application added the new IoT hub by visiting the [Azure portal][lnk-azure-portal] and viewing your list of resources, or by using the **Get-AzureRmResource** PowerShell cmdlet.

> [AZURE.NOTE] This example application adds an S1 Standard IoT Hub for which you are billed. When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.

## <a name="next-steps"></a>Next steps

Now you have deployed an IoT hub using the REST API, you may want to explore further:

- Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].
- Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.

To learn more about developing for IoT Hub, see the following:

- [Introduction to C SDK][lnk-c-sdk]
- [IoT Hub SDKs][lnk-sdks]

To further explore the capabilities of IoT Hub, see:

- [Simulating a device with the IoT Gateway SDK][lnk-gateway]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: ../powershell-install-configure.md
[lnk-rest-api]: https://msdn.microsoft.com/library/mt589014.aspx
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
