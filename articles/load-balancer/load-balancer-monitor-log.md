<properties
   pageTitle="Monitor operations, events, and counters for Load Balancer | Microsoft Azure"
   description="Learn how to enable alert events, and probe health status logging for Azure Load Balancer"
   services="load-balancer"
   documentationCenter="na"
   authors="sdwheeler"
   manager="carmonm"
   editor="tysonn"
   tags="azure-resource-manager"
/>
<tags
   ms.service="load-balancer"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="infrastructure-services"
   ms.date="10/24/2016"
   ms.author="sewhee" />

# <a name="log-analytics-for-azure-load-balancer-preview"></a>Log analytics for Azure Load Balancer (Preview)

You can use different types of logs in Azure to manage and troubleshoot load balancers. Some of these logs can be accessed through the portal. All logs can be extracted from an Azure blob storage, and viewed in different tools, such as Excel and PowerBI. You can learn more about the different types of logs from the list below.

- **Audit logs:** You can use [Azure Audit Logs](../../articles/monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status. Audit logs are enabled by default, and can be viewed in the Azure portal.
- **Alert event logs:** You can use this log to view what alerts for load balancer are raised. The status for the load balancer is collected every five minutes. This log is only written if a load balancer alert event is raised.
- **Health probe logs:** You can use this log to check for probe health check status, how many instances are online in the load balancer back-end and percentage of virtual machines receiving network traffic from the load balancer. This log is written on probe status event change.

>[AZURE.IMPORTANT] Log analytics currently works only for Internet facing load balancers. Logs are only available for resources deployed in the Resource Manager deployment model. You cannot use logs for resources in the classic deployment model. For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../../articles/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Enable logging

Audit logging is automatically enabled for every Resource Manager resource. You need to enable event and health probe logging to start collecting the data available through those logs. Use the following steps to enable logging.

Sign-in to the [Azure portal](http://portal.azure.com). If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.

1. In the portal, click **Browse**.
2. Select **Load Balancers**.

    ![portal - load-balancer](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Select an existing load balancer >> **All Settings**.
4. On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.

    ![portal - load-balancer-settings](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. In the **Diagnostics** pane, under **Status**, select **On**.
6. Click **Storage Account**.
7. Under **LOGS**, select an existing storage account, or create a new one. Use the slider to determine how many days event dat will be kept in the event logs. 8. Click **Save**.

    ![Portal - Diagnostics logs](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

>[AZURE.INFORMATION] Audit logs do not require a separate storage account. The use of storage for event and health probe logging will incur service charges.

## <a name="audit-log"></a>Audit log

The audit log is generated by default. The logs are preserved for 90 days in Azure’s Event Logs store. Learn more about these logs by reading the [View events and audit logs](../../articles/monitoring-and-diagnostics/insights-debugging-with-events.md) article.

## <a name="alert-event-log"></a>Alert event log

This log is only generated if you've enabled it on a per load balancer basis. The events are logged in JSON format and stored in the storage account you specified when you enabled the logging. The following is an example of an event.

    {
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }

The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert. In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).

## <a name="health-probe-log"></a>Health probe log

This log is only generated if you've enabled it on a per load balancer basis as detailed above. The data is stored in the storage account you specified when you enabled the logging. A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:

    {
        "records":
        {
            "time": "2016-01-26T10:37:46.6024215Z",
            "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
            "category": "LoadBalancerProbeHealthStatus",
            "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
            "operationName": "LoadBalancerProbeHealthStatus",
            "properties": {
                "publicIpAddress": "40.83.190.158",
                "port": "81",
                "totalDipCount": 2,
                "dipDownCount": 1,
                "healthPercentage": 50.000000
            }
        },
        {
            "time": "2016-01-26T10:37:46.6024215Z",
            "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
            "category": "LoadBalancerProbeHealthStatus",
            "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
            "operationName": "LoadBalancerProbeHealthStatus",
            "properties": {
                "publicIpAddress": "40.83.190.158",
                "port": "81",
                "totalDipCount": 2,
                "dipDownCount": 0,
                "healthPercentage": 100.000000
            }
        }
    }

The JSON output shows in the properties field the basic information for the probe health status. The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.

## <a name="view-and-analyze-the-audit-log"></a>View and analyze the audit log

You can view and analyze audit log data using any of the following methods:

- **Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal. Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../../articles/resource-group-audit.md) article.
- **Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free. Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.

## <a name="view-and-analyze-the-health-probe-and-event-log"></a>View and analyze the health probe and event log

You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs. Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.

>[AZURE.TIP] If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from Github.

## <a name="additional-resources"></a>Additional resources

- [Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.
- [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.

## <a name="next-steps"></a>Next steps

[Understand load balancer probes](load-balancer-custom-probe-overview.md)