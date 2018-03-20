ms.TocTitle: Connect to the app launcher
Title: Have your app appear in the Office 365 app launcher
Description: Learn how to connect your app to the Office 365 app launcher via the My apps page and how to give a single sign-on experience using Office 365 credentials.
ms.ContentId: 089d8e30-a9d3-423f-acf8-c727b32ac36f
ms.topic: article (how-tos)
ms.date: June 30, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]


# Have your app appear in the Office 365 app launcher

_**Applies to:** Office 365_
 
The app launcher is a new feature in Office 365 that makes it easier for users to find and access their apps. This article describes the ways you as a developer can get your apps to appear in users’ launchers, and also give them a single sign-on experience using their Office 365 credentials.
 
<a name="section_0"> </a>
## The app launcher connects to apps, quick task tiles, and a user's My apps page
 
To start the launcher, select the launcher icon on the top navigation bar:

![The default tiles displayed from a user's app launcher include basic apps in a tenancy and quick links to functions, such as Outlook tasks or the Office 365 Admin Portal.](images\Office365_AppLauncher_Launcher.png)
 
The user’s app launcher not only defaults to some basic apps within a given tenancy, but has links to other functions that may be needed quickly, such as Outlook tasks or the Office 365 Admin Portal. The launcher icon appears no matter what application is running, so that other apps can be quickly started. Selecting **My apps** from the lower right corner of the launcher brings up the **My apps** page – home to all of a user’s apps.

The launcher is both customizable and extensible. Users can pin any app from their **My apps** page to the launcher, and they can pin up to three of the default apps to the top navigation bar for quick access. For more information on the launcher, see [Finding help for the latest changes in Office 365](https://support.office.com/en-us/article/Find-help-for-the-latest-changes-in-Office-365-22E9A8BF-EF08-4B95-B10F-6E839440339C).
 
<a name="section_1"> </a>
## You integrate with Azure AD to get your app into a user’s My apps page
 
You can use the integration between **Office 365** and **Azure Active Directory** to get your app assigned to specific users, and show up on their **My apps** page. Every Office 365 tenant has an associated Azure AD, which is the source for all app registration, configuration, and permissions for the tenant. The associated Azure AD is available free of charge with an Office 365 subscription, but to administer you must complete Azure registration; see [additional information on Azure registration](http://technet.microsoft.com/en-us/library/dn832618).

As a developer, you build apps that authenticate using Azure AD in a number of different [scenarios](https://msdn.microsoft.com/en-us/library/azure/dn499820.aspx). Then, an app can be assigned to a user (and appear on their **My apps** page) in several different ways:

- Develop an app for a single organization, and register it in the organization’s Azure AD. Or, as an independent software vendor (ISV), write a multi-tenant app that is registered in the Azure application gallery. An organization’s Azure AD administrator then configures the app and assigns it to individual users, and the app will show up on their **My apps** pages. To learn more about the admin option, skip to [An admin can configure custom apps or shared apps in Azure AD](#section_3).

- Develop an app that registers in a user’s Azure AD without admin assignment, by allowing users to sign on with their Office 365 credentials. See [Apps with single sign-on flow](#section_2).

- Develop a Web app that users can install directly from the **Office Store**. See the next section, [Single sign-on Web apps in the Office Store](#section_1_5).

<a name="section_1_5"> </a>
## Single sign-on Web apps in the Office Store

You can create a Web app using single sign-on flow and submit it to the **Office Store**. A user then selects the **Office Store** default icon in the app launcher, and installs the app using their Office 365 credentials. Building the app is similar to the steps in [Apps with single sign-on flow](#section_2), except the action of installation takes place from the store rather than from the vendor's website. To submit apps to the store see [Submit Web apps for Office 365 to the Seller Dashboard](https://msdn.microsoft.com/office/office365/HowTo/submit-web-apps-seller-dashboard).  

<a name="section_2"> </a>
## Apps with single sign-on flow

Developers can create applications using **Office 365 API Tools for Visual Studio** that let users install the app using their Office 365 credentials. After installation, the app will appear on the user’s **My apps** page, and be launched from then on without further authentication. Such applications are developed by independent software vendors (ISVs) to be run by many different organizations (multi-tenant). Users can visit the ISV’s website, and install the app using their Office 365 credentials.

###From sign-on to launcher: user experience

1. The user selects a link on the provider’s website to sign on with Office 365 credentials.
2. Azure AD presents a sign-on page with the app name and request for specific resources (profile, contacts, etc.). User consents by choosing **OK**.
3. Provider initiates session with the user, requesting and receiving information (terms of service agreement, confirmation of email address, etc.).
4. User is now signed in to provider’s app. The user can now find the app on the **My apps** page, and pin it to the launcher.

###Authentication and Authorization

Azure AD can use the standard **OAuth 2.0** protocol to authorize Office 365 apps. The app gets an **auth code** from the Azure AD **Authorization Endpoint**, and then sends it to the **Token Endpoint** to get access and refresh tokens for requests using Office 365 APIs. For more information and flow diagrams, see [Office 365 app authentication and resource authorization](https://msdn.microsoft.com/office/office365/howto/common-app-authentication-tasks).

Apps with single sign-on flow use an additional protocol: [**OpenID Connect**](http://msdn.microsoft.com/en-us/library/azure/dn645541.aspx). While **OAuth** requests an **auth code**, **OpenID Connect** requests an **identity token**. This token enables single sign-on and other elements of the sign-on flow, such as matching identity claims with user profile information. As of late 2015 we also support the submission of valid SAML based applications to the Office Store.

###Key concepts for building single sign-on apps

- **Office 365 API Tools for Visual Studio** provides all you need to enable single sign-on flow. Add references to **OpenID Connect**, and the [**Open Web Interface for .NET (OWIN)**](http://owin.org/) framework. Request permissions for user resources through the **Add -> Connected Service** dialog. A related code sample to explore the tooling required may be found on GitHub at: [https://github.com/OfficeDev/O365-WebApp-MultiTenant](https://github.com/OfficeDev/O365-WebApp-MultiTenant).

- The app launcher initiates sign-on to the sign-on URL for the application; if this value is blank, the launcher will default to the **Reply URL** in the [Application Object Properties](https://msdn.microsoft.com/library/azure/dn132633.aspx#BKMK_AppObject). To deliver a seamless single sign-on experience it is important to set this value to a destination that will initiate your application’s user authentication flow.

- To effectively move your app from development to pre-production and production, let the **BaseUrl** of the **Redirect URI** be calculated at runtime (see an example in **startup.auth.cs** of the previously mentioned code sample)

- The syntax for calling the Authorization Endpoint in Azure AD using **OAuth** is: `https://login.windows.net/<tenant>/oauth2/<use>`, where `<tenant>` can be replaced with a verified domain, a tenant Identifier, or **Common** (for multi-tenant apps). 

- Apps can support either a combination of anonymous and authenticated experiences for the user, or authenticated-only experiences. Wherever a function requires authentication, use the **[Authorize]** attribute at the beginning of that section of code.

<a name="section_3"> </a>
##An admin can configure custom apps or shared apps in Azure AD

An Azure AD administrator can configure two types of applications:

- A Line-of-business (LoB) application for a single organization (single-tenant app), written by an enterprise developer and registered in the organization’s Azure AD.

- A software-as-a-service (SaaS) application for multiple organizations (multi-tenant app), written by an independent software vendor (ISV), and stored in the Azure **application gallery**.

For guidance in developing and registering these types of applications, see [Adding, Updating, and Removing an Application](https://msdn.microsoft.com/en-us/library/azure/dn132599). A guide to authentication in Azure AD for Office 365 may be found in [Office 365 app authentication and resource authorization](https://msdn.microsoft.com/office/office365/howto/common-app-authentication-tasks).

An administrator signs on to Azure AD either from the [**Azure Management Portal**](https://manage.windowsazure.com/) or from the **Office 365 admin center** via the **Azure AD** menu item on the left Dashboard. Once on Azure AD, an admin selects the appropriate directory, then **Applications** from the menu, then the **ADD** button on the command bar. The following options are displayed:

- **Add an application my organization is developing**
- **Add an application from the gallery**

If the admin selects the first option, the **Add Application wizard** captures several fields, including the app **Name**, **Type**, **App ID URI**, and **Sign-on URL** (the **App URL** in the [Application Object Properties](https://msdn.microsoft.com/library/azure/dn132633.aspx#BKMK_AppObject)). There is also a **Logo wizard** to upload a custom logo if desired.

When the second option, **Add an application from the gallery** is selected, the **Application Gallery** is shown:

![After a signed-in Azure AD admin selects Add an Application from the Gallery, the admin can search for available apps in the Application Gallery or install an organization's custom app.](images\Office365_AppLauncher_AppGallery.png)

The admin can search for a particular app in the Gallery, or select **CUSTOM** to install other apps that the organization is using. When selected, the app is installed, and a configuration menu is shown, giving options from among the following:
 
- **Enable single sign-on with Windows Azure AD**
- **Enable automatic user provisioning to [appname] (shown depending on the app)**
- **Assign users to [appname]**

If **Enable single sign-on with Windows Azure AD** is selected, the following options are shown:

- **Windows Azure AD Single Sign-On** (used for all apps with federated sign-on)
- **Password Single Sign-On**
- **Existing Single Sign-On**

Choosing one of these options allows Azure AD to store and manage the access needed for applications, so that the users only need Office 365 credentials to access all their assigned apps. For more information on each of the single sign-on options, see [Support for single sign-on](https://msdn.microsoft.com/library/azure/dn308588.aspx#bkmk_supportsso). 

The next step is to assign users to the application. On the previous configuration menu, select **Assign users to [appname]**. The following screen is shown:

![After an Azure AD admin selects Assign Users, the admin can select currently unassigned users and then choose ASSIGN on the command bar at the bottom of the screen.](images\Office365_AppLauncher_AssignUser.png)

The admin can select one or more users who are **Unassigned**, and then choose **ASSIGN** on the command bar. For federated apps, there may be pre-set user roles, which can be matched to specific user roles as part of the assignment. For non-federated apps, the admin has the option of entering credentials on behalf of the user; if omitted, the user will be prompted to enter their username and password on first use of the app.

The app icon is now displayed on the user’s **My apps** page, and can be pinned to the launcher, and the user will no longer have to re-enter credentials whenever the app is launched.

<a name="bk_addresources"> </a>
##Additional resources

- [Find help for the latest changes in Office 365](https://support.office.com/en-us/article/Find-help-for-the-latest-changes-in-Office-365-22E9A8BF-EF08-4B95-B10F-6E839440339C)
- [Office 365 app authentication and resource authorization](http://msdn.microsoft.com/en-us/office/office365/howto/common-app-authentication-tasks)
- [Authentication scenarios for Azure AD](https://msdn.microsoft.com/en-us/library/azure/dn499820)
- [Adding, Updating, and Removing an Application](https://msdn.microsoft.com/en-us/library/azure/dn132599)
- [Application access enhancements for Azure AD](http://msdn.microsoft.com/en-us/library/azure/dn308588.aspx)
- [Azure AD Authentication Library for .NET](http://msdn.microsoft.com/en-us/library/azure/jj573266.aspx)
- [Application Submissions to the Azure Gallery](http://blogs.msdn.com/b/azureappgallery/archive/2014/07/23/application-submissions-to-the-azure-gallery.aspx)




