ms.TocTitle: Release notes
Title: Office 365 REST API release notes for April 2015
Description: Find information about new features and preview features for developers available in the April 2015 release of the Office 365 APIs, and find known issues.
ms.ContentId: 14c3c05f-313f-4bd0-802b-749adc074b8c
ms.topic: article (how-tos)
ms.date: June 2, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]

# Office 365 REST API release notes for April 2015

<p class="previewnote">This documentation covers features that are currently in preview. For information about working with preview features, see [Preview developer features on the Office 365 platform](.\platform-development-preview-features-overview.md).</p>

_**Applies to:** Office 365_

This article provides information about the new features for developers that are available in the April 2015 release of the Office 365 APIs, and any known issues that you might want to be aware of. For more information about developing for Office 365, see [Office 365 APIs platform overview](.\platform-development-overview.md).

## New GA features in Office 365 APIs

The following new Office 365 API features are generally available:

* Cross-origin resource sharing (CORS) support, including:
	* CORS support in Exchange
	* CORS support in SharePoint
	* CORS support in Microsoft Azure Active Directory (Azure AD)
* AppOnly support in Exchange
* AppOnly support in SharePoint
* Support for Auth scopes in SharePoint (Taxonomy, Search, UPA)
* Updates to the Outlook APIs, including:
	* [Sync for calendar views](..\howto\sync-calendar-view.md)
	* [Search](..\api\complex-types-for-mail-contacts-calendar.md#Search) for messages that meet a specified criterion
	* [Filters](..\api\complex-types-for-mail-contacts-calendar.md#Filter) for complex types
	* Windows **TimeZone** support for start and end times in the Calendar API. See the **StartTimeZone** and **EndTimeZone** properties of the [Event](..\api\complex-types-for-mail-contacts-calendar.md#EventResource) entity.
	* Opening a message or event in Outlook Web App. See the **WebLink** property of the [Message](..\api\complex-types-for-mail-contacts-calendar.md#MessageResource) and **Event** entities.
	
## New preview features in Office 365 APIs

The following new Office 365 API preview features are available:

* Notes API (preview)
* OneDrive API (preview)
* Office 365 unified API (preview)
* Office graph (preview)
* Video REST API (preview)
* For the Outlook APIs:
	* Outlook Notifications REST API (preview) to get notifications for mail, contacts and events 
	* Outlook User Photo REST API (preview) to get HD photos of authenticated users
	* Extended properties on mail


For details about the new preview features, see [Preview developer features on the Office 365 platform](.\platform-development-preview-features-overview.md).

## Office 365 unified API (preview) known issues

The following are known issues with the Office 365 unified API (preview).

### Unified groups and social activity insights availability

For the preview release, access to unified group events and conversations might take some time to become available worldwide through the unified API. 

### User entity limitations

*No instant access after creation*

Users can be created immediately through a POST on the user entity. An Office 365 license must first be assigned to a user, in order to get access to Office 365 services.  Even then, due to the distributed nature of the service, it might take in the order of 15 minutes before files, messages and events entities are available for use for this user, through the unified API. During this time, apps will receive a 404 HTTP error response. 

*Setting extended user profile properties*

Setting extended user profile properties like AboutMe and Skills is not currently supported. 

### Group entity limitations

*No instant access to content after creation*

Unified groups can be created immediately through a POST on the group entity. However, for a unified group that is created through the unified API, access to the associated content will not be readily available. Apps will be able to start adding content to the group (files, conversations, and events) after a set period of time, as follows: 

* For conversations and events, up to 40 minutes after group creation 
* For files, up to 24 hours after group creation 

Until that time, attempts to update the unified group with content will result in a 500 HTTP error response. For proof-of-concept applications that are using the Office 365 unified APIs, we recommend that you use Outlook or Outlook Web App to create unified group if immediate access to the content is required. 

*Policy*

Using the Office 365 unified APIs to create and name a unified group bypasses any unified group policies that are configured through Outlook Web App. For proof-of-concept applications that use the Office 365 unified APIs, we recommend that you use Outlook or Outlook Web App to create unified groups. 

*Permission scopes*

The Office 365 unified API exposes two permission scopes for unified groups: 
* Group.Read.All  
* Group.ReadWrite.All 

These scopes provide access to group management functions (enumerating groups, enumerating group members) as well as access to content in the group (conversations and events). However, in order to access files in a unified group, you must also request the Sites.Read.All or Site.ReadWrite.All permission scope.  For more information about these permission scopes, see [Get started with Office 365 unified API (preview)](https://msdn.microsoft.com/office/office365/HowTo/get-started-with-office-365-unified-api#msg_register_app).  

### Contacts

Personal contacts are not currently supported. Only organizational contacts are supported.

### OData operations

Cross-workload filtering/search is not available. Full-text search (using $search) is only available for users, groups, organization contacts, messages, and events.

### Performance SLA

The request latency for 95th percentile might be high.

### Schema inconsistencies

Canonical IDs for attendees and recipients are not available.

### Uploading files to a particular folder

Uploading a file to a specific folder requires an application to perform three steps: 

1. Create a new file in the root folder. 

2. Upload the file content.
 
3. Move the file to the target folder. 

Steps 2 and 3 are interchangeable. In addition, to create a folder under another folder, you must create the new folder under the root folder, and then you can move it to the applicable target folder. We will fix these issues so that these operations only require one call. 

### File and content streaming

Upload and download of files (files in unified groups, drives, or mail file attachments) is limited to 1 MB. 

### App registration compatibility

During the preview timeframe, you should register new apps to call the Office 365 unified API. Single- and multi-tenant apps are supported for web applications. Native client apps can only be used within the tenant that the application is registered in. 

## Outlook APIs known issues

### Cannot set reminders for events

Currently you can't set a reminder from the client library or directly via REST when you're creating or updating events. The event reminder field is not updated, but no error is returned.

## Additional resources

- [Office 365 APIs platform overview](https://msdn.microsoft.com/en-us/office/office365/howto/platform-development-overview)
- [Preview developer features on the Office 365 platform](.\platform-development-preview-features-overview.md)
- [OneDrive API (preview) release notes](http://aka.ms/odb-api-release-notes)
