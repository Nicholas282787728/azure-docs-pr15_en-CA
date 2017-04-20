<properties 
    pageTitle="Tutorial: Azure Active Directory integration with Gigya | Microsoft Azure" 
    description="Learn how to use Gigya with Azure Active Directory to enable single sign-on, automated provisioning, and more!" 
    services="active-directory" 
    authors="jeevansd"  
    documentationCenter="na" 
    manager="femila"/>
<tags 
    ms.service="active-directory" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.tgt_pltfrm="na" 
    ms.workload="identity" 
    ms.date="09/01/2016" 
    ms.author="jeedes" />

#<a name="tutorial-azure-active-directory-integration-with-gigya"></a>Tutorial: Azure Active Directory integration with Gigya
  
The objective of this tutorial is to show the integration of Azure and Gigya.  
The scenario outlined in this tutorial assumes that you already have the following items:

-   A valid Azure subscription
-   A Gigya single sign on enabled subscription
  
After completing this tutorial, the Azure AD users you have assigned to Gigya will be able to single sign into the application at your Gigya company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).
  
The scenario outlined in this tutorial consists of the following building blocks:

1.  Enabling the application integration for Gigya
2.  Configuring single sign-on
3.  Configuring user provisioning
4.  Assigning users

![Configure Single Sign-On] (./media/active-directory-saas-gigya-tutorial/IC789512.png "Configure Single Sign-On")
##<a name="enabling-the-application-integration-for-gigya"></a>Enabling the application integration for Gigya
  
The objective of this section is to outline how to enable the application integration for Gigya.

###<a name="to-enable-the-application-integration-for-gigya-perform-the-following-steps"></a>To enable the application integration for Gigya, perform the following steps:

1.  In the Azure classic portal, on the left navigation pane, click **Active Directory**.

    ![Active Directory] (./media/active-directory-saas-gigya-tutorial/IC700993.png "Active Directory")

2.  From the **Directory** list, select the directory for which you want to enable directory integration.

3.  To open the applications view, in the directory view, click **Applications** in the top menu.

    ![Applications] (./media/active-directory-saas-gigya-tutorial/IC700994.png "Applications")

4.  Click **Add** at the bottom of the page.

    ![Add application] (./media/active-directory-saas-gigya-tutorial/IC749321.png "Add application")

5.  On the **What do you want to do** dialog, click **Add an application from the gallery**.

    ![Add an application from gallerry] (./media/active-directory-saas-gigya-tutorial/IC749322.png "Add an application from gallerry")

6.  In the **search box**, type **Gigya**.

    ![Application Gallery] (./media/active-directory-saas-gigya-tutorial/IC789513.png "Application Gallery")

7.  In the results pane, select **Gigya**, and then click **Complete** to add the application.

    ![Gigya] (./media/active-directory-saas-gigya-tutorial/IC789527.png "Gigya")
##<a name="configuring-single-sign-on"></a>Configuring single sign-on
  
The objective of this section is to outline how to enable users to authenticate to Gigya with their account in Azure AD using federation based on the SAML protocol.  
As part of this procedure, you are required to create a base-64 encoded certificate file.  
If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).

###<a name="to-configure-single-sign-on-perform-the-following-steps"></a>To configure single sign-on, perform the following steps:

1.  In the Azure classic portal, on the **Gigya** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.

    ![Configure Single Sign-On] (./media/active-directory-saas-gigya-tutorial/IC789528.png "Configure Single Sign-On")

2.  On the **How would you like users to sign on to Gigya** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.

    ![Configure Single Sign-On] (./media/active-directory-saas-gigya-tutorial/IC789529.png "Configure Single Sign-On")

3.  On the **Configure App URL** page, in the **Gigya Sign On URL** textbox, type your URL using the following pattern "*http://company.gigya.com*", and then click **Next**.

    ![Configure App URL] (./media/active-directory-saas-gigya-tutorial/IC789530.png "Configure App URL")

4.  On the **Configure single sign-on at Gigya** page, click **Download certificate**, and then save the certificate file on your computer.

    ![Configure Single Sign-On] (./media/active-directory-saas-gigya-tutorial/IC789531.png "Configure Single Sign-On")

5.  In a different web browser window, log into your Gigya company site as an administrator.

6.  Go to **Settings \> SAML Login**, and then click the **Add** button.

    ![SAML Login] (./media/active-directory-saas-gigya-tutorial/IC789532.png "SAML Login")

7.  In the **SAML Login** section, perform the following steps:

    ![SAML Configuration] (./media/active-directory-saas-gigya-tutorial/IC789533.png "SAML Configuration")

    1.  In the **Name** textbox, type a name for your configuration.
    2.  In the Azure classic portal, on the **Configure single sign-on at Gigya** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.
    3.  In the Azure classic portal, on the **Configure single sign-on at Gigya** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Single Sign-On Service URL** textbox.
    4.  In the Azure classic portal, on the **Configure single sign-on at Gigya** dialog page, copy the **Name Identifier Format** value, and then paste it into the **Name ID Format** textbox.
    5.  Create a **base-64 encoded** file from your downloaded certificate.
        
        >[AZURE.TIP]For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)

    6.  Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.
    7.  Click **Save Settings**.

8.  On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.

    ![Configure Single Sign-On] (./media/active-directory-saas-gigya-tutorial/IC789534.png "Configure Single Sign-On")
##<a name="configuring-user-provisioning"></a>Configuring user provisioning
  
In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.  
In the case of Gigya, provisioning is a manual task.

###<a name="to-provision-a-user-accounts-perform-the-following-steps"></a>To provision a user accounts, perform the following steps:

1.  Log in to your **Gigya** company site as an administrator.

2.  Go to **Admin \> Manage Users**, and then click **Invite Users**.

    ![Manage Users] (./media/active-directory-saas-gigya-tutorial/IC789535.png "Manage Users")

3.  On the Invite Users dialog, perform the following steps:

    ![Invite Users] (./media/active-directory-saas-gigya-tutorial/IC789536.png "Invite Users")

    1.  In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.
    2.  Click **Invite User**.
    
        >[AZURE.NOTE] The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.

>[AZURE.NOTE] You can use any other Gigya user account creation tools or APIs provided by Gigya to provision AAD user accounts.

##<a name="assigning-users"></a>Assigning users
  
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

###<a name="to-assign-users-to-gigya-perform-the-following-steps"></a>To assign users to Gigya, perform the following steps:

1.  In the Azure classic portal, create a test account.

2.  On the **Gigya **application integration page, click **Assign users**.

    ![Assign Users] (./media/active-directory-saas-gigya-tutorial/IC789537.png "Assign Users")

3.  Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.

    ![Yes] (./media/active-directory-saas-gigya-tutorial/IC767830.png "Yes")
  
If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).