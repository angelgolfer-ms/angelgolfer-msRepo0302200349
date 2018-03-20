ms.TocTitle: Manually register your app
Title: Manually register your app with Azure AD so it can access Office 365 APIs
Description: Manually add Azure Active Directory common consent to your ASP.NET application so it can access OneDrive for Business files or other secured resources.
ms.ContentId: 95479f73-15d7-426e-abdf-ae2c72b5cd33
ms.topic: article (how-tos)
ms.date: September 9, 2015
<<<<<<< HEAD

=======
redirect_url: https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-scenarios/#basics-of-registering-an-application-in-azure-ad
---
>>>>>>> staging
[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Manually register your app with Azure AD so it can access Office 365 APIs   

_**Applies to:** Office 365_
 

<a name="bk_intro"> </a>

The Office 365 API services use Azure Active Directory (Azure AD) to provide secure authentication to users' Office 365 data. To access the Office 365 APIs, you need to register your app with Azure AD. 


<a name="bk_RegistrationPrereqs"> </a>
##Prerequisites for registering your apps with Azure AD

To register your apps, you'll need two accounts:

- An Office 365 business account

	If you don't have an existing Office 365 business account, there are several ways to create one. For more information, see [Get an Office 365 account](..\howto\setup-development-environment.md#bk_Office365Account).

- An Azure AD subscription associated with your Office 365 business account

	This is where you'll actually register your app. You can use an existing Azure AD tenancy, or create a new one.
	When you sign up for an Office 365 business account, a Microsoft Azure subscription is automatically created and associated with that Office 365 account.
	
	So, if you have an existing Microsoft Azure subscription, you can associate your Office 365 business account with it. If not, you'll need to create an association to the Azure subscription that was created when you signed up for your Office 365 business account.
	
	For more information, see [Associate your Office 365 account with Azure AD to create and manage apps](..\howto\setup-development-environment.md#bk_CreateAzureSubscription).
	



<a name="bk_RegisterApp"> </a>
## Register your app with the Azure Management Portal 

As part of registration, you specify whether your app is a Web application, such as an MVC or Web Forms solution, or a native app, such as a smart phone or other mobile device. Azure AD uses this information to generate resources your app will need to authenticate with Azure. For web applications, Azure generates both a client ID and app secret. For native apps, Azure generates a client ID.

After you register your app, you can configure its properties, including:

- Specifying the app endpoint(s) Azure will use for redirection during authentication.
- For web applications, whether to make your app available only in the Azure tenancy you registered it in, or across multiple tenancies.
- For web applications, generating the app secret and its duration.

Once your app is registered, you can then specify which Office 365 services your app requires access to. This includes specifying the permissions level for the Office 365 APIs your app requires.


<a name="bk_RegisterNativeApp"> </a>
### Register your native app with the Azure Management Portal 

The following instructions are for native apps, which includes iOS and Android apps. 

1. Sign into the [Azure Management Portal](https://manage.windowsazure.com/), using your Office 365 business account credentials.

2. Click the **Active Directory** node in the left column and select the directory linked to your Office 365 subscription.

	![A screenshot of the Azure Management Portal website. The item 'Active Directory' is selected in the left navigation pane. In the main pane, the Directory tab is selected. The name of the current directory is highlighted.](images\O365APIs_RegisterApp_1.png)

3. Select the **Applications** tab and then **Add** at the bottom of the page.
	
	![A screenshot of the directory information page. In the menu bar at the bottom of the page, the New icon is highlighted.](images\O365APIs_RegisterApp_2.png)

4. On the pop-up, select **Add an application my organization is developing**. Then click the arrow to continue.

5. Choose a name for your app and select **Native client application** as its Type. Then click the arrow to continue.
	
6. Next, specify a redirect URI. This is the URI to which Azure AD will redirect the user-agent in response to an OAuth 2.0 request. The value does not need to be a physical endpoint, but must be a valid URI. You can think of the redirect URL as a unique identifier for your app.
	
7. Click the check mark to complete your app registration.
	
Your native app is now registered with Azure AD. Now you can proceed to [Specifying the permission levels your app requires from the Office 365 API services](#bk_ConnectAppToO365).




<a name="bk_RegisterWebApp"> </a>
### Register your brower-based web app with the Azure Management Portal 

The following instructions are for browser-based web apps. These types of apps run entirely in the browser after loading the source code from a server.

1. Sign into the [Azure Management Portal](https://manage.windowsazure.com/), using your Office 365 business account credentials.

2. Click the **Active Directory** node in the left column and select the directory linked to your Office 365 subscription.

	![A screenshot of the Azure Management Portal website. The item 'Active Directory' is selected in the left navigation pane. In the main pane, the Directory tab is selected. The name of the current directory is highlighted.](images\O365APIs_RegisterApp_1.png)

3. Select the **Applications** tab and then **Add** at the bottom of the page.
	
	![A screenshot of the directory information page. In the menu bar at the bottom of the page, the New icon is highlighted.](images\O365APIs_RegisterApp_2.png)

4. On the pop-up, select **Add an application my organization is developing**. Then click the arrow to continue.

5. Choose a name for your app and select **Web application and/or web API** as its Type. Then click the arrow to continue.

6. The **Sign-on URL** is the address of a web page where users can sign in and use your app. The value set for this property is also set as the value of the **Reply URL**.
	
7. The **App ID URI** is a unique identifier for Azure AD to identify your app. It must be a unique value in your organization’s Azure AD.
	
7. Click the check mark to complete your app registration.
	
Your browser-based web app is now registered with Azure AD. However, you have to configure your app to allow the OAuth 2.0 implicit grant flow and configure the Azure tenancy scope of your app. After you complete the configuration, proceed to [Specifying the permission levels your app requires from the Office 365 API services](#bk_ConnectAppToO365).

#### Configure your app to allow the OAuth 2.0 implicit grant flow

Because browser-based web apps can't secure an application secret, your application will use the OAuth implicit grant flow. You need to update the application's manifest to allow the OAuth implicit grant flow because it is not allowed by default.

1. Select the **Configure** tab of your application's entry in the Azure Management Portal.

2. Using the **Manage Manifest** button in the drawer, download the manifest file for the application and save it to your computer.

3. Open the manifest file with a text editor. Search for the *oauth2AllowImplicitFlow* property. By default it is set to *false*; change it to *true* and save the file.

4. Using the **Manage Manifest** button, upload the updated manifest file.

#### Specify whether your web app is single or multi-tenant

For browser-based web apps, you can also configure the Azure tenancy scope of your app: whether the app should be available only within the single Azure tenancy in which you register it, or if it should be available across multiple Azure tenancies. 

The default is **No**. You can change the tenancy scope later, if necessary.

1. In the Azure Management Portal, select your application and choose **Configure** in the top menu. Scroll down to **Application is multi-tenant**, and select **Yes** or **No**.






<a name="bk_RegisterServerApp"> </a>
### Register your web server app with the Azure Management Portal 

The following instructions are for web server apps, such as Node.js apps.

1. Sign into the [Azure Management Portal](https://manage.windowsazure.com/), using your Office 365 business account credentials.

2. Click the **Active Directory** node in the left column and select the directory linked to your Office 365 subscription.

	![A screenshot of the Azure Management Portal website. The item 'Active Directory' is selected in the left navigation pane. In the main pane, the Directory tab is selected. The name of the current directory is highlighted.](images\O365APIs_RegisterApp_1.png)

3. Select the **Applications** tab and then **Add** at the bottom of the page.
	
	![A screenshot of the directory information page. In the menu bar at the bottom of the page, the New icon is highlighted.](images\O365APIs_RegisterApp_2.png)

4. On the pop-up, select **Add an application my organization is developing**. Then click the arrow to continue.

5. Choose a name for your app and select **Web application and/or web API** as its Type. Then click the arrow to continue.

6. The **Sign-on URL** is the address of a web page where users can sign in and use your app. The value set for this property is also set as the value of the **Reply URL**.
	
7. The **App ID URI** is a unique identifier for Azure AD to identify your app. It must be a unique value in your organization’s Azure AD.
	
7. Click the check mark to complete your app registration.
	
Your web server app is now registered with Azure AD. However, you have to generate an app secret so clients can authenticate with your server app. After that, you can proceed to [Specifying the permission levels your app requires from the Office 365 API services](#bk_ConnectAppToO365).

<a name="bk_ConfigureApp_Secret"> </a>
#### Generate a new app secret for your web application

1. In the Azure Management Portal, select your application and choose **Configure** in the top menu. Scroll down to **keys**.

2. Select the duration for your client secret, and click the Save icon.

	![A screenshot of the app configuration page for your app, on the Azure Management Portal website. Under the page section titled 'keys', a drop-down list is shown for selecting the duration of the new key. In the menu bar at the bottom of the page, the SAVE icon is highlighted.](images\O365APIs_RegisterApp_7.png)
	
	Azure displays the app secret.

3. Click the Clipboard icon to copy the client secret to the Clipboard.

	![A screenshot of the app configuration page for your app, on the Azure Management Portal website. Under the page section titled 'keys', the new client secret is now displayed. Next to the client secret, the Clipboard icon is highlighted.](images\O365APIs_RegisterApp_8.png)

	**Important** Azure only displays the client secret at the time you initially generate it. You cannot navigate back to this page and retrieve the client secret later. 



<a name="bk_ConnectAppToO365"> </a>
## Specify the Office 365 API permissions your app requires 

Finally, you'll need to specify exactly what permissions your app requires of the Office 365 APIs. To do so, you add access to the Office 365 service containing the API you require to your app, and then specify the permission(s) you need from the APIs in that service. See [Office 365 application manifest and permission details](..\howto\application-manifest.md) for a complete listing of Office 365 API permissions.  

1. In the Azure Management Portal, on the configuration page for your app, scroll to the bottom of the page and, under **permissions to other applications**, select **Add application**.
 
	![A screenshot of the app configuration page for your app, on the Azure Management Portal website. Under the page section titled 'permission to other applications', the 'Add application' button is highlighted.](images\O365APIs_RegisterApp_4.png)

2. Select the Office 365 service for which your app requires permissions.
	

	1. Select the service name, and click the plus symbol to add the service. 
	2. The service is then listed under the **Selected** column. 
	3. Click the check mark icon to save your choices.
	![A screenshot of the 'permissions to other applications' page. The available services are listed in a table. Next to the name of the selected service is a plus icon. At the far right is a column that will list the applications you add to your app. The check mark icon that you click to save your choices is highlighted at the top of the page.](images\O365APIs_RegisterApp_5.png)

	You are returned to your app's configuration page.

4. Under **permissions to other applications**, click the **Delegated Permissions** column for each service you added, and specify the permissions your app needs.

	![A screenshot of the app configuration page for your app, on the Azure Management Portal website. Under the page section titled 'permissions to other applications', the services that you just added are listed in a table. Next to the name of each application is a column titled 'Delegated Permissions'. This column displays a drop-down menu of the permissions you can request for your app from each application you added.](images\O365APIs_RegisterApp_6.png)

	These are the permissions that will be displayed to your app user when  Azure prompts them to consent to your app's permission request. In general, request only the services your app actually requires, and specify the least level of permissions in each service that still enable your app to perform its functions.

	Also, be aware that permission levels are additive. There is no need to request multiple permission levels for a given API, as the more expansive permission level already includes the more restricted permission. For example, for the Mail API, the **Send email as a user** permission already includes the **Read and write access to users' email** permission.
	
	For more information on specific permissions, see [Office 365 application manifest and permission details](..\howto\application-manifest.md).


<a name="bk_NextSteps"> </a>
## Next steps

Now, with your app registered, configured, and connected to the Office 365 services, you're ready to add code to your app that authenticates with Azure AD and accesses your user's Office 365 data.

Use the starter projects, code samples, procedural topics, and reference material listed in the next section get your app up and running.

<a name="bk_AdditionalResources"> </a>
## Additional resources

- [Office 365 API starter projects, code samples, and videos](..\howto\starter-projects-and-code-samples.md)

- [Office 365 API contents](..\howto\rest-api-overview.md)

- [Outlook Mail API reference](..\api\mail-rest-operations.md)

- [Outlook Calendar API reference](..\api\calendar-rest-operations.md)

- [Outlook Contacts API reference](..\api\contacts-rest-operations.md)

- [Files API reference](..\api\files-rest-operations.md)

- [Overview of developing on the Office 365 platform](..\howto\platform-development-overview.md)

- [Office 365 application manifest and permission details](..\howto\application-manifest.md)
