<properties
    pageTitle="Get Started with Azure Mobile Apps for Xamarin.Android apps"
    description="Follow this tutorial to get started using Azure Mobile Apps for Xamarin Android development"
    services="app-service\mobile"
    documentationCenter="xamarin"
    authors="adrianhall"
    manager="erikre"
    editor="" />

<tags
    ms.service="app-service-mobile"
    ms.workload="mobile"
    ms.tgt_pltfrm="mobile-xamarin-android"
    ms.devlang="dotnet"
    ms.topic="hero-article"
    ms.date="10/01/2016"
    ms.author="adrianha" />

#<a name="create-a-xamarinandroid-app"></a>Create a Xamarin.Android App

[AZURE.INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

##<a name="overview"></a>Overview

This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app. For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).

A screenshot from the completed app is below:

![][0]

Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.

##<a name="prerequisites"></a>Prerequisites

To complete this tutorial, you need the following prerequisites:

* An active Azure account. If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps. For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).

* Visual Studio with Xamarin. See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.

>[AZURE.NOTE]If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://tryappservice.azure.com/?appServiceName=mobile).  You can immediately create a short-lived starter Mobile App in App Service. No credit cards required; no commitments.

## <a name="create-an-azure-mobile-app-backend"></a>Create an Azure Mobile App backend

Follow these steps to create a Mobile App backend.

[AZURE.INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications. Next, download a server project for a simple "todo list" backend and publish it to Azure.

## <a name="configure-the-server-project"></a>Configure the server project

[AZURE.INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a>Download and run the Xamarin.Android app

1. Under **Download and run your Xamarin.Android project**, click the **Download** button.

    Save the compressed project file to your local computer, and make a note of where you save it.

2. Press the **F5** key to build the project and start the app.

3. In the app, type meaningful text, such as _Complete the tutorial_ and then click the **Add** button.

    ![][10]

    Data from the request is inserted into the TodoItem table. Items stored in the table are returned by the mobile app backend, and the data appears in the list.

    > [AZURE.NOTE] You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.

##<a name="next-steps"></a>Next steps

* [Add Offline Sync to your app](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Add authentication to your app](app-service-mobile-xamarin-android-get-started-users.md)
* [Add push notifications to your Xamarin.Android app](app-service-mobile-xamarin-android-get-started-push.md)
* [How to use the managed client for Azure Mobile Apps](app-service-mobile-dotnet-how-to-use-client-library.md)


<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
