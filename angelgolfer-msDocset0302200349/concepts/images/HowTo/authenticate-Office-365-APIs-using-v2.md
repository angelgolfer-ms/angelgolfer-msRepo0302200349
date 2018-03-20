ms.TocTitle: Authenticate using v2.0
Title: Authenticate Office 365 and Outlook.com APIs using the v2.0 app model
Description: Use the v2.0 authentication endpoint preview to sign in both Azure AD and Microsoft account users to your apps and Office 365 API endpoints.
ms.ContentId: 30286232-50d7-4155-8112-121ce412a705
ms.topic: article (how-tos)
ms.date: December 1, 2015

<<<<<<< HEAD
=======
redirect_url: https://graph.microsoft.io/en-us/docs/authorization/auth_overview

---
>>>>>>> staging
[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Authenticate Office 365 and Outlook.com APIs using the v2.0 authentication endpoint preview

_**Applies to:** Office 365 | Outlook.com_



|**Preview documentation** | 
|:-----|   
| There are features and functionality of the v2.0 authentication endpoint that are not yet supported in the public preview period. You should be aware of them if you are building applications during the public preview. For more information, see [Limitations and restrictions of the V2.0 app model preview](https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-limitations/). |


##Signing in Microsoft account and Azure AD users with a single authentication model

The v2.0 authentication endpoint preview enables you to create apps that accept both work and school (Azure AD) as well as personal (Microsoft account) identities. 

In the past, an app developer who wanted to support both Microsoft accounts and Azure Active Directory was required to integrate with two completely separate systems. Now you can build apps using the v2.0 authentication endpoint, which allows you to sign users in with both types of accounts. One simple process allows you to immediately reach an audience that spans millions of users with both personal and work/school accounts.   

Currently, your apps can access the following APIs using the v2.0 authentication endpoint preview:

- Outlook mail 
- Outlook contacts 
- Outlook calendars

with more Microsoft services being added in the near future.


<a name="bk_samples"> </a>

##Code samples

Explore the following code sample to learn how to create apps that use the v2.0 authentication endpoint preview to access Office APIs.

- [.NET MVC web app](https://dev.outlook.com/RestGettingStarted/Tutorial/dotnet)

<!--
- [Android](https://github.com/OfficeDev)
- [iOS](https://github.com/OfficeDev)
- [JavaScript](https://github.com/OfficeDev)
-->


<a name="bk_scopes"> </a>

##Office API authentication scopes

The table below lists the authentication scopes to use with the v2 authentication endpoint preview. For more information about using scopes with the v2.0 endpoint, and how it differs from using resources in Azure AD, see [Scopes, not resources](https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-compare/#scopes-not-resources).

<a name="bk_Outlookscopes"> </a>

###Outlook mail, calendar, and contacts scopes

|**Scope** | **Permission** | **Description** | 
|:-----|:-----|:-----|
| `https://outlook.office.com/mail.read` |Read user mail|Allows this app to read messages in user mailboxes.| 
| `https://outlook.office.com/mail.readwrite` |Read and write access to user mail|Allows the app to read, update, create, and delete messages in user mailboxes.|
| `https://outlook.office.com/mail.send`  |Send mail as a user|Allows the app to send messages as users in the organization.|
| `https://outlook.office.com/contacts.read` |Read user contacts|Allows the app to read user contacts.|
| `https://outlook.office.com/contacts.readwrite` |Have full access to user contacts|Allows the app to read, update, create and delete user contacts.|
| `https://outlook.office.com/calendars.read` |Read user calendars|Allows the app to read events in user calendars.|
| `https://outlook.office.com/calendars.readwrite` |Have full access to user calendars|Allows the app to read, update, create, and delete events in user calendars.|



## Outlook APIs

- These APIs work for all Office 365 users. We are gradually enabling these APIs for outlook.com users. When an app makes a request targeting an outlook.com mailbox not yet enabled for REST APIs, we return a special error "UserNotSupported" with Http Status 404. Your app must gracefully handle this case.

- For optimal performance, we recommend adding x-AnchorMailbox header for every request and set it to email address of the target mailbox.

- Currently, you must directly make REST API requests to the endpoint. The Office 365 SDKs continue to use the Azure AD endpoint.

- Refer to the following code sample for using v2.0 app model preview with Outlook APIs:
	- [.NET MVC web app](https://dev.outlook.com/RestGettingStarted/Tutorial/dotnet)



##Next steps

[Register an app to use the v2.0  authentication endpoint](https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-app-registration/).

##Learn more

[Limitations and restrictions in the v2.0 endpoint preview](https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-limitations/)

[What's new about the v2.0 endpoint preview](https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-compare)

More [v2.0 authentication endpoint preview documentation](https://azure.microsoft.com/en-us/documentation/articles/?service=active-directory&term=app+model+v2.0) on [azure.microsoft.com](https://azure.microsoft.com/)

