<properties
    pageTitle="Add Push Notifications to iOS App with Azure Mobile Apps"
    description="Learn how to use Azure Mobile Apps to send push notifications to your iOS app."
    services="app-service\mobile"
    documentationCenter="ios"
    manager="yochayk"
    editor=""
    authors="ysxu"/>

<tags
    ms.service="app-service-mobile"
    ms.workload="mobile"
    ms.tgt_pltfrm="mobile-ios"
    ms.devlang="objective-c"
    ms.topic="article"
    ms.date="10/10/2016"
    ms.author="yuaxu"/>


# <a name="add-push-notifications-to-your-ios-app"></a>Add Push Notifications to your iOS App

[AZURE.INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Overview
In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.

If you do not use the downloaded quick start server project, you will need the push notification extension package. See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.

The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html). You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).

##<a name="configure-hub"></a>Configure Notification Hub

[AZURE.INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Register app for push notifications

[AZURE.INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a>Configure Azure to send push notifications

[AZURE.INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

##<a id="update-server"></a>Update backend to send push notifications

[AZURE.INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a>Add push notifications to app

[AZURE.INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a>Test push notifications

[AZURE.INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

##<a id="more"></a>More

* Templates give you flexibility to send cross-platform pushes and localized pushes. [How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS quick start]: app-service-mobile-ios-get-started.md
