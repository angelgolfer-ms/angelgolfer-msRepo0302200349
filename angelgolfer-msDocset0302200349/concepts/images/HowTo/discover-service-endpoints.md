ms.TocTitle: Discovery tasks
Title: Common endpoint discovery tasks using the Discovery Service API
Description: Use the Office 365 Discovery Service to dynamically find endpoints for Microsoft services and user resources and get the information needed to obtain access.
ms.ContentId: ef8f781f-31c3-4871-929d-ab6155b02917
ms.topic: article (how-tos)
ms.date: June 30, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]


# Common endpoint discovery tasks using the Discovery Service API
    
_**Applies to:** Office 365_

<<<<<<< HEAD
=======
[!INCLUDE [Use Microsoft Graph](../includes/use-msgraph-note.txt)]
>>>>>>> staging

The Office 365 APIs provide access to events, contacts, mail, and files through Microsoft services. Before users of your application can access Microsoft services and user resources, the application needs their endpoints. Discovery Service lets you discover these endpoints dynamically and get the information needed to obtain access.

The Discovery Service exposes a RESTful API. Client SDKs are available for the [.NET platform](..\howto\getting-started-Office-365-APIs.md), [Android](http://msdn.microsoft.com/en-us/office/office365/howto/develop-apps-for-android), and [iOS](http://dev.office.com/iOS). Discovery Service supports discovering **Calendar**,  **Contacts**,  **Mail**,  **MyFiles** (for OneDrive and OneDrive for Business service endpoints), **Notes** (for OneNote), and **RootSite** (for SharePoint).

**Note** The Discovery Service only provides functionality for Office 365 online environment and does not work for on-premises deployments.

To learn more about Discovery Service operations, see [Discovery Service REST API operations reference](..\api\discovery-service-rest-operations.md).  For code samples on how to use the Discovery Service API to find endpoints for services that you access using the Office 365 APIs, see [Office 365 APIs: How to use Discovery Service](https://code.msdn.microsoft.com/Office-365-APIs-How-to-use-609102ea#content) and 
[Office 365 Discovery Service sample](https://github.com/OfficeDev/Office365-Discovery-Service-Sample).

The API endpoint URI for Discovery Service are as follows.

Version v1.0:
```
ApiEndpoint = "https://api.office.com/discovery/v1.0/me/;

```

Version v2.0:
```
ApiEndpoint = "https://api.office.com/discovery/v2.0/me/;

```

The Resource ID for Discovery Service:
```
ResourceId = "https://api.office.com/discovery/";

```

## Discovery Service requirements

Before using Discovery Service, you need to  [Set up your Office 365 development environment](..\howto\setup-development-environment.md).


## Discovery Service process

The following is the workflow for an app using Discovery Service.


**Table 1. Interactions among your app, Discovery Service, and Azure AD to call Office 365 APIs**


|**Step**|**Description**|**Workflow**|
|:-----|:-----|:-----|
|1|Register your app in the Azure Management Portal and configure the app's code with the client Id and redirect URI. Then, in the Azure Management Portal, configure the permissions for the app.| |
|2|Your app gets the user's email address. It contacts Discovery Service with email address and the set of scopes the app wants to access.|![Your app requests authorization code for Discovery Service.](images\O365APIs_DiscoveryFlow_Step1.png)|
|3|The app goes to the Azure AD authorization endpoint and the user authenticates and grants consent (if consent has not been granted before). Azure AD issues an authorization code.|![The user authenticates and grants consent. Azure AD issues an authorization code.](images\O365APIs_DiscoveryFlow_Step2.png)|
|4|Your app redeems the authorization code. Azure returns an access token and a refresh token.|![Your app redeems the authorization code. Azure returns an access token and a refresh token.](images\O365APIs_DiscoveryFlow_Step3.png)|
|5|Your app calls Discovery Service using the access token. Discovery Service returns Http Response with resource IDs and endpoint URIs for Office 365 services.|![Your app calls Discovery Service using the access token. Discovery Service returns Http Response with resource IDs and endpoint URIs for Office 365 services.](images\O365APIs_DiscoveryFlow_Step4.png)|
|6|Your app redeems the refresh token with Azure AD token endpoint, to get the access token for the desired Office 365 resource. The Azure AD token endpoint returns an access token for the specified resource and a refresh token.|![Your app redeems the refresh token with the Azure AD token endpoint, to get an access token for the desired Office 365 resource. The Azure AD token endpoint returns an access token and a refresh token.](images\O365APIs_DiscoveryFlow_Step5.png)|
|7|Your app can now call Office 365 APIs using the URI from Discovery Service and the access token. Office 365 returns Http Response.|![Your app can now call Office 365 APIs using the URI from Discovery Service and the access token.](images\O365APIs_DiscoveryFlow_Step6.png)|

For a sample that shows how to use Discovery Service, see  [Office 365 APIs: How to use Discovery Service](http://code.msdn.microsoft.com/Office-365-APIs-How-to-use-609102ea).

For information about the APIs that Discovery Service uses, see  [Discovery Service REST API operations reference](..\api\discovery-service-rest-operations.md).


## Additional resources
<a name="bk_addresources"> </a>


-  [Set up your Office 365 development environment](..\howto\setup-development-environment.md)
    
-  [Building an Office 365 ASP.NET MVC app](..\howto\getting-started-Office-365-APIs.md)
    
-  [Discovery Service REST API operations reference](..\api\discovery-service-rest-operations.md)
    
-  [Office 365 APIs: How to use Discovery Service](http://code.msdn.microsoft.com/Office-365-APIs-How-to-use-609102ea)

-  [Getting started with the Office 365 APIs](http://www.microsoftvirtualacademy.com/training-courses/introduction-to-office-365-development?m=10072&ct=31602): training video 

