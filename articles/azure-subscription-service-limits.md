<properties
    pageTitle="Microsoft Azure Subscription and Service Limits, Quotas, and Constraints"
    description="Provides a list of common Azure subscription and service limits, quotas, and constraints. This includes information on how to increase limits along with maximum values."
    services=""
    documentationCenter=""
    authors="rothja"
    manager="jeffreyg"
    editor=""
    tags="billing"
    />

<tags
    ms.service="billing"
    ms.workload="na"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="08/29/2016"
    ms.author="btardif"/>

# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a>Azure subscription and service limits, quotas, and constraints

## <a name="overview"></a>Overview

This document specifies some of the most common Microsoft Azure limits. This does not currently cover all Azure services. Over time, these limits will be expanded and updated to cover more of the platform.

Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) to learn more about Azure pricing. There, you can estimate your costs using the [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting the pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).

> [AZURE.NOTE] If you want to raise the limit above the **Default Limit**, you can [open an online customer support request at no charge](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). The limits cannot be raised above the **Maximum Limit** value in the tables below. If there is no **Maximum Limit** column, then the specified resource does not have adjustable limits.

## <a name="limits-and-the-azure-resource-manager"></a>Limits and the Azure Resource Manager

It is now possible to combine multiple Azure resources in to a single Azure Resource Group. When using Resource Groups, limits that once were global become managed at a regional level with the Azure Resource Manager. For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).

In the limits below, a new table has been added to reflect any differences in limits when using the Azure Resource Manager. For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table. When a limit applies to both scenarios, it is only shown in the first table. Unless otherwise indicated, limits are global across all regions.

> [AZURE.NOTE] It is important to emphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as the service management quotas are. Let's use core quotas as an example. If you need to request a quota increase with support for cores, you need to decide how many cores you want to use in which regions, and then make a specific request for Azure Resource Group core quotas for the amounts and regions that you want. Therefore, if you need to use 30 cores in West Europe to run your application there; you should specifically request 30 cores in West Europe. But you will not have a core quota increase in any other region -- only West Europe will have the 30-core quota.
<!-- -->
As a result, you may find it useful to consider deciding what your Azure Resource Group quotas need to be for your workload in any one region, and request that amount in each region into which you are considering deployment. See [troubleshooting deployment issues](./resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.

## <a name="service-specific-limits"></a>Service-specific limits

- [Active Directory](#active-directory-limits)
- [API Management](#api-management-limits)
- [App Service](#app-service-limits)
- [Application Gateway](#application-gateway-limits)
- [Application Insights](#application-insights-limits)
- [Automation](#automation-limits)
- [Azure Redis Cache](#azure-redis-cache-limits)
- [Azure RemoteApp](#azure-remoteapp-limits)
- [Backup](#backup-limits)
- [Batch](#batch-limits)
- [BizTalk Services](#biztalk-services-limits)
- [CDN](#cdn-limits)
- [Cloud Services](#cloud-services-limits)
- [Data Factory](#data-factory-limits)
- [Data Lake Analytics](#data-lake-analytics-limits)
- [DNS](#dns-limits)
- [DocumentDB](#documentdb-limits)
- [Event Hubs](#event-hubs-limits)
- [IoT Hub](#iot-hub-limits)
- [Key Vault](#key-vault-limits)
- [Media Services](#media-services-limits)
- [Mobile Engagement](#mobile-engagement-limits)
- [Mobile Services](#mobile-services-limits)
- [Monitoring](#monitoring-limits)
- [Multi-Factor Authentication](#multi-factor-authentication)
- [Networking](#networking-limits)
- [Notification Hub Service](#notification-hub-service-limits)
- [Operational Insights](#operational-insights-limits)
- [Resource Group](#resource-group-limits)
- [Scheduler](#scheduler-limits)
- [Search](#search-limits)
- [Service Bus](#service-bus-limits)
- [Site Recovery](#site-recovery-limits)
- [SQL Database](#sql-database-limits)
- [Storage](#storage-limits)
- [StorSimple System](#storsimple-system-limits)
- [Stream Analytics](#stream-analytics-limits)
- [Subscription](#subscription-limits)
- [Traffic Manager](#traffic-manager-limits)
- [Virtual Machines](#virtual-machines-limits)
- [Virtual Machine Scale Sets](#virtual-machine-scale-sets-limits)


### <a name="subscription-limits"></a>Subscription limits
#### <a name="subscription-limits"></a>Subscription limits
[AZURE.INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a>Subscription limits - Azure Resource Manager

The following limits apply when using the Azure Resource Manager and Azure Resource Groups. Limits that have not changed with the Azure Resource Manager are not listed below. Please refer to the previous table for those limits.

For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).

[AZURE.INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]


### <a name="resource-group-limits"></a>Resource Group limits

[AZURE.INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a>Virtual Machines limits
#### <a name="virtual-machine-limits"></a>Virtual Machine limits
[AZURE.INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]


#### <a name="virtual-machines-limits---azure-resource-manager"></a>Virtual Machines limits - Azure Resource Manager

The following limits apply when using the Azure Resource Manager and Azure Resource Groups. Limits that have not changed with the Azure Resource Manager are not listed below. Please refer to the previous table for those limits.

[AZURE.INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a>Virtual Machine Scale Sets limits

[AZURE.INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="networking-limits"></a>Networking limits

[AZURE.INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a>Networking limits
[AZURE.INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a>Application Gateway limits

[AZURE.INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="traffic-manager-limits"></a>Traffic Manager limits

[AZURE.INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a>DNS limits

[AZURE.INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a>Storage limits

For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](../articles/storage/storage-scalability-targets.md).

#### <a name="storage-service-limits"></a>Storage Service limits

[AZURE.INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

#### <a name="virtual-machine-disk-limits"></a>Virtual Machine disk limits

[AZURE.INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

See [Virtual machine sizes](../articles/virtual-machines/virtual-machines-linux-sizes.md) for additional details.

**Standard storage accounts**

[AZURE.INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

**Premium storage accounts**

[AZURE.INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a>Storage Resource Provider limits

[AZURE.INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]


### <a name="cloud-services-limits"></a>Cloud Services limits

[AZURE.INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]


### <a name="app-service-limits"></a>App Service limits
The following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.

[AZURE.INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a>Scheduler limits

[AZURE.INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a>Batch limits

[AZURE.INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

###<a name="biztalk-services-limits"></a>BizTalk Services limits
The following table shows the limits for Azure Biztalk Services.

[AZURE.INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]


### <a name="documentdb-limits"></a>DocumentDB limits

[AZURE.INCLUDE [azure-documentdb-limits](../includes/azure-documentdb-limits.md)]

Quotas listed with an asterisk (*) [can be adjusted by contacting Azure support](./documentdb/documentdb-increase-limits.md).

### <a name="mobile-engagement-limits"></a>Mobile Engagement limits

[AZURE.INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]


### <a name="search-limits"></a>Search limits

Pricing tiers determine the capacity and limits of your search service. Tiers include:

- *Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.
- *Basic* provides dedicated computing resources for production workloads at a smaller scale, with up to three replicas for highly available query workloads.
- *Standard (S1, S2, S3, S3 High Density)* is for larger production workloads. Multiple levels exist within the standard tier so that you can choose a resource configuration for specific scenarios.

**Limits per subscription**

[AZURE.INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

**Limits per search service**

[AZURE.INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

For more granular information about other limits, including document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).

### <a name="media-services-limits"></a>Media Services limits

[AZURE.INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a>CDN limits

[AZURE.INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a>Mobile Services limits

[AZURE.INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitoring-limits"></a>Monitoring limits

[AZURE.INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a>Notification Hub Service limits

[AZURE.INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a>Event Hubs limits

[AZURE.INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a>Service Bus limits

[AZURE.INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a>IoT Hub limits

[AZURE.INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a>Data Factory limits

[AZURE.INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a>Data Lake Analytics Limits
[AZURE.INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="stream-analytics-limits"></a>Stream Analytics limits
[AZURE.INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a>Active Directory limits

[AZURE.INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]


### <a name="azure-remoteapp-limits"></a>Azure RemoteApp limits

[AZURE.INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a>StorSimple System limits

[AZURE.INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]


### <a name="operational-insights-limits"></a>Operational Insights limits

[AZURE.INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a>Backup limits

[AZURE.INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a>Site Recovery limits

[AZURE.INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a>Application Insights limits

[AZURE.INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a>API Management limits

[AZURE.INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a>Azure Redis Cache limits

[AZURE.INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a>Key Vault limits

[AZURE.INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
[AZURE.INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a>Automation limits
[AZURE.INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a>SQL Database limits

For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).

## <a name="see-also"></a>See also

[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[Virtual Machine and Cloud Service Sizes for Azure](virtual-machines/virtual-machines-linux-sizes.md)

[Sizes for Cloud Services](cloud-services/cloud-services-sizes-specs.md)