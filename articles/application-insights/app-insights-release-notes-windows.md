<properties 
    pageTitle="Release notes for Application Insights for Windows" 
    description="The latest updates for Windows Store SDK." 
    services="application-insights" 
    documentationCenter=""
    authors="alancameronwills" 
    manager="douge"/>
<tags 
    ms.service="application-insights" 
    ms.workload="tbd" 
    ms.tgt_pltfrm="ibiza" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.date="02/12/2016" 
    ms.author="joshweb"/>
 
# <a name="release-notes-for-application-insights-sdk-for-windows-phone-and-store"></a>Release Notes for Application Insights SDK for Windows Phone and Store

The Application Insights SDK sends telemetry about your live app to [Application Insights](https://azure.microsoft.com/services/application-insights/), where you can analyze its usage and performance.


## <a name="version-111"></a>Version 1.1.1

### <a name="windows-sdk"></a>Windows SDK

- Fix a hang during crash when using the Windows Phone's Silverlight SDK. After this change, any crash that happens later than ~2 seconds after the call to WindowsAppInitialier.InitializeAsync(...) will be persisted to disk and will be sent the next time the app is started. If a crash happens before ~2 seconds after the call, it will be ignored.  
- Set the NuGet's dependencies to a specific version of Core and Microsoft.ApplicationInsights.PersistenceChannel (v1.2.3).   

### <a name="core-sdk"></a>Core SDK

- Core is managed in github. Future release notes of the Core SDK can be found [in github](http://github.com/Microsoft/ApplicationInsights-dotnet/releases)

## <a name="version-11"></a>Version 1.1

### <a name="core-sdk"></a>Core SDK

- SDK now introduces new telemetry type ```DependencyTelemetry``` which contains information about dependency call from application
- New method ```TelemetryClient.TrackDependency``` allows to send information about dependency calls from application

## <a name="version-100"></a>Version 1.0.0

### <a name="windows-app-sdk"></a>Windows App SDK

- New initialization for Windows Apps. New `WindowsAppInitializer` class with `InitializeAsync()` method allows for bootstrapping initialization of SDK collection. This change allow more precise control and significant app initialization performance improvements over previous ApplicationInsights.config technique.
- DeveloperMode is no longer automatically set. To change DeveloperMode behavior you must specify in code.
- NuGet package no longer injects ApplicationInsights.config. Recommend to use the new WindowsAppInitializer when manually adding NuGet package.
- ApplicationInsights.config only reads `<InstrumentationKey>`, all other settings are ignored in preference for WindowsAppInitializer settings.
- Store Market will be auto collected by SDK.
- Lots of bug fixes, stability improvements, and performance enhancements.

### <a name="core-sdk"></a>Core SDK

- ApplicationInsights.config file is no longer requiered. And not added by the NuGet package. Configuration can be fully specified in code.
- NuGet package will no longer add a targets file to your solution. This removes the automatic setting of DeveloperMode during a debug build. DeveloperMode should be manually set in code.

## <a name="version-017"></a>Version 0.17

### <a name="windows-app-sdk"></a>Windows App SDK

- Windows App SDK now supports Universal Windows Apps created against Windows 10 technical preview and with VS 2015 RC.

### <a name="core-sdk"></a>Core SDK

- TelemetryClient defaults to initialize with the InMemoryChannel.
- New API added, `TelemetryClient.Flush()`. This Flush method will trigger an immediate blocking upload of all telemetry logged to that client. This enables manual triggering of upload before process shutdown.
- NuGet package added a .Net 4.5 target. This target has no external dependencies (removed BCL and EventSource dependencies).

## <a name="version-016"></a>Version 0.16 

2015-04-28 preview

- SDK now supports DNX target platform to enable monitoring of [.NET Core framework](http://www.dotnetfoundation.org/NETCore5) applications.
- Instances of ```TelemetryClient``` do not cache Instrumentation Key anymore. Now if instrumentation key wasn't set in ```TelemetryClient``` explicitly ```InstrumentationKey``` will return null. It fixes an issue when you set ```TelemetryConfiguration.Active.InstrumentationKey``` after some telemetry was already collected, telemetry modules like dependency collector, web requests data collection and performance counters collector will use new instrumentation key.

## <a name="version-015"></a>Version 0.15

- New property ```Operation.SyntheticSource``` now available on ```TelemetryContext```. Now you can mark your telemetry items as "not a real user traffic" and specify how this traffic was generated. As an example by setting this property you can distinguish traffic from your test automation from load test traffic.
- Channel logic was moved to the separate NuGet called Microsoft.ApplicationInsights.PersistenceChannel. Default channel is now called InMemoryChannel
- New method ```TelemetryClient.Flush``` allows to flush telemetry items from the buffer synchronously

## <a name="version-013"></a>Version 0.13

No release notes for older versions available. 