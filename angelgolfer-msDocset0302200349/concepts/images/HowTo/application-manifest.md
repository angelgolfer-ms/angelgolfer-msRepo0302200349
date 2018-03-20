ms.TocTitle: Office 365 permissions reference
Title: Office 365 API permissions reference
Description: Use the application manifest to define app permissions and the scopes that grant and limit access to Office 365 data.
ms.ContentId: 2d2d68a8-b64a-4c1f-bd19-5550478f1f4f
ms.topic: article (how-tos)
ms.date: September 9, 2015

<<<<<<< HEAD
=======
redirect_url: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest

---
>>>>>>> staging
[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Office 365 API permissions reference


_**Applies to:** Office 365_

    
<a name="AppManifest_Scopes"> </a>
## Use scopes to specify access to Office 365 data 

Scopes are used to limit access to Office 365 data to a specific level in SharePoint, Exchange, and Microsoft Azure Active Directory. A scope is a combination of a resource or capability and an operation in the format _resource.operation_. For example, "MyFiles.Read" specifies the resource "MyFiles" and the operation "Read". There are no default scopes. 

You can specify scopes for your app in the [Azure Management Portal](https://manage.windowsazure.com/), or declare them in your app's application manifest. Scope information is stored in the app's application manifest. The format of the manifest is JSON. 

To modify the application manifest directly

1. Log on to the the [Azure Management Portal](https://manage.windowsazure.com/).   
2. View the application definition.   
3. Download the application manifest.    
4. Open the manifest and modify it according to the needs of the app. 

To learn more about configuring apps, see [Adding, Updating, and Removing an Application](http://msdn.microsoft.com/en-us/library/azure/dn132599.aspx).

**Note**  The tables describing service app permissions do not include a **Requires admin consent** column, as permissions for service apps always require admin consent. For more information about service apps, see [Building service and daemon apps in Office 365](..\howto\building-service-apps-in-office-365.md).

<a name="AppManifest_SharePointScopes"> </a>
## SharePoint scope permissions

|**Scope**|**Permission**|**Description**|**Requires Admin Consent**|
|:-----|:-----|:-----|:-----|
|Files.Read|Read user files |Allows the app to read current signed-in user's files.|No|
|Files.ReadWrite|Edit or delete user files |Allows the app to edit or delete current signed-in user's files.|No|
|Sites.Read.All|Read items in all site collections|Allows the app to read documents and list items in all site collections on behalf of the signed-in user.|No|
|Sites.ReadWrite.All|Read and write items in all site collections|Allows the app to create, read, update, and delete documents and list items in all site collections on behalf of the signed-in user.|No|
|Sites.Manage.All|Read and write items and lists in all site collections|Allows the app to read, create, update, and delete document libraries and lists in all site collections on behalf of the signed-in user.|No|
|Sites.FullControl.All|Have full control of all site collections|Allows the app to have full control of all site collections on behalf of the signed-in user.|Yes|
|Sites.Search.All|Run search queries as a user|Allows the app to run search queries and to read basic site info on behalf of the signed-in user.<br>**Note** Search results are based on the user's permissions instead of the app's permissions.</br>|Yes|
|User.Read.All|Read user profiles|Allows the app to read user profiles and to read basic site info on behalf of the signed-in user.|Yes|
|User.ReadWrite.All|Read and write user profiles|Allows the app to read and update user profiles and to read basic site info on behalf of the signed-in user.|Yes|
|TermStore.Read.All|Read managed metadata|Allows the app to read managed metadata and to read basic site info on behalf of the signed-in user.|Yes|
|TermStore.ReadWrite.All|Read and write managed metadata|Allows the app to read, create, update, and delete managed metadata and to read basic site info on behalf of the signed-in user.|Yes|

<a name="AppManifest_SharePointAppScopes"> </a>
### SharePoint scope permissions for service apps

|**Scope**|**Permission**|**Description**|
|:-----|:-----|:-----|
|Sites.Read.All|Read items in all site collections|Allows the app to read documents and list items in all site collections without a signed in user.|
|Sites.ReadWrite.All|Read and write items in all site collections|Allows the app to create, read, update, and delete documents and list items in all site collections without a signed in user.|
|Sites.Manage.All|Read and write items and lists in all site collections|Allows the app to read, create, update, and delete document libraries and lists in all site collections without a signed in user.|
|Sites.FullControl.All|Have full control of all site collections|Allows the app to have full control of all site collections without a signed in user.|
|User.Read.All|Read user profiles|Allows the app to read user profiles without a signed in user.|
|User.ReadWrite.All|Read and write user profiles|Allows the app to read and update user profiles and to read basic site info without a signed in user.|
|TermStore.Read.All|Read managed metadata|Allows the app to read managed metadata and to read basic site info without a signed in user.|
|TermStore.ReadWrite.All|Read and write managed metadata|Allows the app to write managed metadata and to read basic site info without a signed in user.|

<a name="AppManifest_ExchangeScopes"> </a>
## Exchange scope permissions

|**Scope**|**Permission**|**Description**|**Requires Admin Consent**|
|:-----|:-----|:-----|:-----|
|Contacts.Read|Read user contacts|Allows the app to read user contacts.|No|
|Contacts.ReadWrite|Have full access to user contacts |Allows the app to read, update, create and delete user contacts.|No|
|Calendars.Read|Read user calendars|Allows the app to read events in user calendars.|No|
|Calendars.ReadWrite|Have full access to user calendars |Allows the app to read, update, create, and delete events in user calendars.|No|
|Mail.Send|Send mail as a user|Allows the app to send messages as users in the organization.|No|
|Mail.Read|Read user mail |Allows this app to read messages in user mailboxes.|No|
|Mail.ReadWrite|Read and write access to user mail |Allows the app to read, update, create, and delete messages in user mailboxes.|No|
|Group.Read.All|Read all groups (preview)|Allows the app to read all groups properties and read group memberships on behalf of the signed-in user.|No|
|Group.ReadWrite.All|Read and write all groups (preview)|Allows the app to read all groups properties and memberships, and to create groups on-behalf of signed-in users.<br>Additionally allows the app to update and delete group properties and memberships on behalf of signed-in users, for groups the signed-in users own.</br>|No|
|full_access_as_user|Have full access to a user mailbox|Allows the application full access to mailboxes on behalf of users in the organization. <br>**Note**  This scope is applicable to the  [EWS Managed API](http://msdn.microsoft.com/library/c2267733-6f4f-49e5-9614-1e4a24c3af1a%28Office.15%29.aspx) and [Exchange Web Services (EWS)](http://msdn.microsoft.com/library/e6fd5c23-0ba5-4a7b-bdde-4a553447069f%28Office.15%29.aspx) only. It does not apply to the Office 365 APIs.</br>|No|

<a name="AppManifest_ExchangeAppScopes"> </a>
### Exchange scope permissions for service apps

|**Scope**|**Permission**|**Description**|
|:-----|:-----|:-----|
|full_access_as_app|Full access to all mailboxes|Allows the app to have full access via EWS to all mailboxes without a signed-in user.|
|Contacts.Read|Read contacts in all mailboxes|Allows the app to read all contacts in all mailboxes without a signed-in user.|
|Contacts.ReadWrite|Read and write contacts in all mailboxes|Allows the app to create, read, update, and delete all contacts in all mailboxes without a signed-in user.|
|Calendars.Read|Read calendars in all mailboxes|Allows the app to read events of all calendars without a signed-in user.|
|Calendars.ReadWrite|Read and write calendars in all mailboxes|Allows the app to create, read, update, and delete events of all calendars without a signed-in user.|
|Mail.Read|Read users' mail|Allows the app to read messages in user mailboxes.|
|Mail.ReadWrite|Read and Write access to user mail|Allows the app to read, update, create, and delete messages in user mailboxes.|
|Mail.Send|Send mail as a user|Allows the app to send messages as users in the organization.|


<a name="AppManifest_AzureScopes"> </a>
## Azure Active Directory scope permissions

|**Scope**|**Permission**|**Description**|**Requires Admin Consent**|
|:-----|:-----|:-----|:-----|
|User.ReadBasic.All|Read all users' basic profiles|Allows the app to read a basic set of profile properties of other users in your company or school on behalf of the signed-in user. Includes display name, first and last name, photo, and email address.|No|
|User.Read|Enable sign-in and read user profile|Allows users to sign-in to the app, and allows the app to read the profile, group membership, reports and manager of signed-in users. It also allow the app to read basic company information of signed-in users.|No|
|User.Read.All|Read all users' full profiles|Allows the app to read the full set of profile properties, group membership, reports and managers of other users in your company or school, on behalf of the signed-in user|Yes|
|Directory.Read.All|Read directory data|Allows the app to read data in your organization's directory. <br>**Note** Access rights are based on the user's permissions.</br>|Yes, unless the app is registered in the same tenant as the user, in this scenario, the user can consent to the app.|
|Directory.ReadWrite.All|Read and write directory data|Allows the application to read and write directory data, such as users and groups. <br>**Note** Access rights are based on the user's permissions, and does not allow user or group deletion.</br>|Yes|
|Directory.AccessAsUser.All|Access the directory as the signed-in user|Allows the app to have the same access to information in the directory as the signed-in user.|No, except for web applications, which require admin consent.|
|Group.Read.All|Read all groups (preview)|Allows the app to read all group properties and memberships on behalf of the signed-in user.|No|
|Group.ReadWrite.All|Read and write all groups (preview)|Allows the app to create groups on behalf of the signed-in user and read all group properties and memberships.  Additionally allows the app to update group properties and memberships for groups the signed-in user owns.|No|

<a name="AppManifest_AzureAppScopes"> </a>
### Azure Active Directory scope permissions for service apps

|**Scope**|**Permission**|**Description**|
|:-----|:-----|:-----|
|Directory.Read.All|Read directory data|Allows the app to read data in your organization's directory, such as users, groups, and apps.<br>**Note** Access rights are based on the user's permissions.</br>|
|Directory.ReadWrite.All|Read and write directory data|Allows the application to read and write directory data, such as users and groups.|

<a name="AppManifest_YammerScopes"> </a>
## Microsoft Yammer scope permissions

|**Scope**|**Permission**|**Description**|**Requires Admin Consent**|
|:-----|:-----|:-----|:-----|
|user_impersonation|Access the Yammer platform|Allows the app to access the Yammer platform on behalf of the signed-in user.|No|

For more details about activating Yammer for your organization, see the [Yammer activation guide](https://support.office.com/en-us/article/Yammer-activation-guide-4f924c74-87d2-49d0-a4f6-cba3ce2b0e7c).

## Additional resources
<a name="bk_addresources"> </a>

- [Manually register your app with Azure AD so it can access Office 365 APIs](..\howto\add-common-consent-manually.md)
   
-  [Office 365 app authentication concepts](..\howto\common-app-authentication-tasks.md)
    

-  [Overview of developing on the Office 365 platform](..\howto\platform-development-overview.md)
 
