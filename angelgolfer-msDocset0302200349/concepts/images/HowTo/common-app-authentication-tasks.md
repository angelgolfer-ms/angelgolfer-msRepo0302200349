ms.TocTitle: Understand authentication
Title: Office 365 app authentication concepts
Description: Understand app authorization flow among Azure AD, the user, and Office 365 API endpoints, and the roles of user consent, access codes, tokens, and scopes.
ms.ContentId: aff11bd0-62ae-4579-a459-faaa236eec26
ms.topic: article (how-tos)
ms.date: October 6, 2015
<<<<<<< HEAD

=======
redirect_url: https://graph.microsoft.io/en-us/docs/authorization/auth_overview
---
>>>>>>> staging
[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Understanding authentication with Office 365 APIs

_**Applies to:** Office 365_

In order for your app to gain access to a user's Office 365 data, your app must first prove it is the app it says it is, and that it has permission to access the user's data. This topic provides a brief overview of how this authentication process is implemented by Office 365 services, and includes pointers to resources where you can learn more about handling authentication for your apps.


## Authentication concepts

Before discussing authorization, there are several terms with which you should be familiar.

- _Authentication_ refers to verifying the identity of an application or user.
	
	 All user accounts, application registrations, and permissions are stored in Azure AD. This allows you to provide logon credentials and be confirmed as a valid user. 

	For information about authentication, see  [Authentication Scenarios for Azure AD](http://msdn.microsoft.com/en-US/library/azure/dn499820.aspx).

- _Authorization_ is the process of granting access to resources, as well as specifying the level of access allowed. 
	
	For example, your application might need access to list a user's calendar events. When you specify  **Read** permission to the calendar, the application will have permission to generate a list of the user's calendar events.

	For more information about authorization, see  [Use Active Directory for authentication in Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/web-sites-authentication-authorization/)

- _Consent_, like authorization, refers to granting permission for an application or user to use certain resources. It gives _the user_ the opportunity to grant or deny access to specific resources.
	
	An example is when a user installs an app. The consent framework will ask the user if they want to allow the app to access their mailbox. The user will see the request for the app to access their mailbox in a dialog box. The user agrees or declines the request.

##Office 365 uses Azure AD for authentication

The Office 365 API services use Azure Active Directory (Azure AD) to provide secure authentication and authorization to users' Office 365 data. Azure AD implements authorization flows according to the [OAuth 2.0 protocol](http://tools.ietf.org/html/rfc6749).

Therefore, enabling your app to authenticate in order to access Office 365 data consists of two basic steps:

- Register your app with Azure AD
- Implement code in your app that handles the appropriate authentication flow 

### Register your app with Azure AD to access Office 365 API services
<a name="bk_register"> </a>

When you create an application that needs access to the Office 365 API services, you need to provide a way to let the service know your application has rights to access it. The Office 365 APIs use Azure AD to provide authentication services that you can use to grant rights for the application to access those services. 

To allow your application access to the Office 365 APIs, you need to [register your application with Azure AD](..\howto\add-common-consent-manually.md). Registering your app allows you to:

- Establish an identity for your application. This includes a client ID, a unique identifier for your app within Azure.
- Specify the app endpoint(s) Azure will use for redirection during authentication.
- Specify what resources it needs access to, and setting permission levels, or _scopes_, for accessing those resources. 
	
	For a complete list of available Office 365 API scopes, see [Office 365 API permissions reference](..\howto\application-manifest.md).


## Authentication flow overview
<a name="bk_authenticate"> </a>

Azure AD implements the [OAuth 2.0 protocol](http://tools.ietf.org/html/rfc6749) for authorizing access from your application to Office 365 resources. The OAuth 2.0 protocol defines several authorization flows. Which flow you implement will vary on the type of app you build, be it a Web application, such as an MVC or Web Forms solution, or a native app, such as a smart phone or other mobile device.

As an introduction, below is a high-level overview of a typical authentication flow; in this case, the [authorization code grant flow](http://msdn.microsoft.com/en-US/library/azure/dn645542.aspx), which is often used for Web applications.

Successfully handling authorization in your app requires that you understand the authentication flow for your type of app. For detailed information about how Azure AD implements OAuth 2.0, see  [OAuth 2.0 in Azure AD](http://msdn.microsoft.com/en-us/library/azure/dn645545.aspx).

### Example: authorization code grant flow
<a name="sectionSection4"> </a>


|**Description**|**Flow**|
|:-----|:-----|
|The user visits your web app, which requires information from Office 365. Your app redirects them to the Azure AD authentication endpoint.|![The user calls the application, and the application calls the authorization endpoint in Azure AD.](images\O365APIs_AuthFlow_Step1.png)|
|<p>The user authenticates and grants consent, if the application is configured with restricted access rights.</p><p>Azure AD issues an authorization code. Authorization codes are used to request access codes for specific resources.</p> |![After the user grants consent, Azure AD issues an authorization code to the app.](images\O365APIs_AuthFlow_Step2.png)|
|<p>After your application has the authorization code, the application can request access and refresh tokens. Your app passes the authorization code to the Azure AD token issuance endpoint.</p><p>Azure AD returns access and refresh tokens.</p>|![The app passes the authorization code to Azure AD, and Azure AD returns an access and a refresh token to the app.](images\O365APIs_AuthFlow_Step3.png)|
|<p>Your app can then use the access and refresh tokens to access the Office 365 API endpoints and return data.</p><p>Your app can then present these tokens, on behalf of the user, to the Office 365 API service(s). The specified resource then returns the information requested by the application.</p> |![The app then uses the access token and the refresh token to access the Office 365 API endpoints.](images\O365APIs_AuthFlow_Step4.png)|


In order to reduce the number of calls an application has to make to Azure AD, and also to reduce the number of consents a user has to make, a multiple resource refresh token is issued by the authorization service. After this refresh token is received, it can be used to request access tokens (and additional refresh tokens) to multiple resources. 

For more information about refresh tokens, see  [Refresh Tokens for Multiple Resources](http://msdn.microsoft.com/en-us/library/azure/dn645538.aspx).


## Exploring how OAuth 2.0 works in the Office 365 OAuth Sandbox
<a name="sectionSection5"> </a>

If you want to explore how OAuth 2.0 works with the Office 365 REST APIs, we've created a web application, the [Office 365 OAuth Sandbox](https://oauthplay.azurewebsites.net/), that lets you observe the messages and tokens passed as the application authenticates with Azure AD. You can also make sample calls to the Office 365 APIs and observe the data returned. For more information on using the Sandbox, see [OAuth2 in action with Office 365 Calendar, Contacts, and Mail](http://blogs.msdn.com/b/exchangedev/archive/2014/10/28/oauth2-in-action-with-the-release-of-office-365-calendar-contacts-and-mail.aspx).

## Office 365 API code samples that implement authorization

The [Office Developer Repo](https://github.com/OfficeDev) on GitHub includes numerous code samples that access Office 365 APIs using Azure AD, including:

- [Office 365 iOS Connect sample](https://github.com/OfficeDev/O365-iOS-Connect) 
- [Office 365 Android Connect sample](https://github.com/OfficeDev/O365-Android-Connect)
- [Office 365 Windows Connect sample](https://github.com/OfficeDev/O365-Win-Connect)

In addition, the [Azure Active Directory developer's guide](http://aka.ms/aaddev) includes quick starts and how-to's that illustrate how to implement Azure AD authentication on various developer platforms, including [iOS](https://azure.microsoft.com/en-us/documentation/articles/active-directory-devquickstarts-ios/), [Android](https://azure.microsoft.com/en-us/documentation/articles/active-directory-devquickstarts-android/), [.NET](https://azure.microsoft.com/en-us/documentation/articles/active-directory-devquickstarts-dotnet/), [Xamarin](https://azure.microsoft.com/en-us/documentation/articles/active-directory-devquickstarts-xamarin/), and [Cordova](https://azure.microsoft.com/en-us/documentation/articles/active-directory-devquickstarts-cordova/).

## Additional resources
<a name="ConNavExample_resources"> </a>

-  [Azure Active Directory developer's guide](http://aka.ms/aaddev)

-  [Office 365 OAuth Sandbox](https://oauthplay.azurewebsites.net/)

- [OAuth2 in action with Office 365 Calendar, Contacts, and Mail](http://blogs.msdn.com/b/exchangedev/archive/2014/10/28/oauth2-in-action-with-the-release-of-office-365-calendar-contacts-and-mail.aspx)
    
-  [Office Developer Repo](https://github.com/OfficeDev) 
    
-  [Azure AD Authentication Library for .NET ](http://msdn.microsoft.com/en-us/library/jj573266.aspx)
    

    
