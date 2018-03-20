ms.TocTitle: File handlers overview
Title: Overview of Office 365 file handlers
Description: File handlers enable non-Microsoft file types to integrate into Office 365 so they display icons, create new files, preview, and open in a non-Microsoft editor.
ms.ContentId: 78826f1a-6aa2-46ca-b2b4-a6caf5ee9040
ms.topic: article (how-tos)
ms.date: December 10, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Overview of Office 365 file handlers


<!-- Get an overview of Office 365 file handler add-in for Office 365. -->

_**Applies to:** Office 365_

  
File handlers are a new type of Office add-in that integrate non-Microsoft file types into Office 365 in the same way that that Office file types are.

With file handlers, you can enable the following user experiences for non-Microsoft file types:
-  customized file icons
-  create new files in the browser
-  file preview
-  rich view/edit capability


<a name="sectionSection0"> </a>
## What's in an Office 365 file handler

A file handler is comprised of the following: 
-  **File handler endpoint** A cloud-hosted app that optionally provides creating, previewing and editing functionality for new file types supported by the file handler.
-  **File icon** The image that represents the file type in Office 365.

<a name="sectionSection1"> </a>
### File handler application

The file handler application is a cloud-hosted application that contains the functional logic for creating, previewing, opening, and saving files of the type that it handles. It can be hosted on any stack, including non-Microsoft stacks. File handlers uses Azure AD to gain authorized access to Office 365 resources, so the application needs to be registered with Azure AD. For more information about registering an application with Azure AD, see:
[Using Visual Studio to register your app and add Office 365 APIs](https://msdn.microsoft.com/office/office365/HowTo/adding-service-to-your-Visual-Studio-project) and 
[Manually register your app with Azure AD so it can access Office 365 APIs](https://msdn.microsoft.com/en-us/office/office365/howto/add-common-consent-manually).

See [Create file handlers in Office 365](..\howto\create-file-handler-extensions.md) for a walkthrough of the steps using Visual Studio to create, deploy, and register a basic file handler.

For a more complex file handler example, see the [GPX-FileHandler](https://github.com/OfficeDev/GPX-FileHandler) on GitHub.


<a name="sectionSection2"> </a>
#### File handlers at runtime

 The file handler is invoked with the **newFileUrl**, **openUrl** or **previewUrl** URL specified in the addIns property of the Azure AD app manifest. To understand what happens, let's take a look at the scenario where a user clicks on the ellipses (**...**) to open the file callout. If there is a registered file handler for that file type, Office 365 invokes the file handler app by making a **POST** request to the URL specified in the **previewUrl** for the app manifest, passing the file location, along with other details in the request. The **previewUrl** points to a method in the file handler application that will retrieve a file stream for the file, and then uses this stream to provide a preview of the file in the browser.
 
 It's the same approach for the open functionality. In the scenario where the user clicks on **Edit in Browser**, or directly on the document title in the library, Office 365 makes a **POST** request to the **openUrl** URL. This endpoint loads the file stream into an appropriate editor, allowing the user to edit the file. The application should also allow the user to save the file by passing the updated file stream back to the file location, which is specified in the **filePut** activation parameter.

When a user clicks on **New file**, Office 365 makes a **POST** request to the **newFileUrl**. This endpoint
opens the appropriate editor so that the user can add content to the new file. The application should enable
the user to save the file back to the file location specified in the **filePut** activation parameter.

<a name="sectionSection3"> </a>
#### Activation parameters

In create new, open and preview scenarios, your application requires details, called activation parameters, about the file, tenant, Office 365 client, etc... to work with the file. Office 365 includes these details as form data sent in the initial **POST** request to the open or preview methods.

**Table 1. Descriptions for the activation parameters that Office 365 sends when the file handler is launched.**

|**Parameter**|**Description**|
|:-----|:-----|:-----|
| **Client**|The Office 365 client from which the file is opened or previewed; for example, "SharePoint".|
| **CultureName**|The culture name of the current thread, used for localization.|
| **FileGet**|The full URL of the REST endpoint your app calls to retrieve the file from Office 365. Your app must call this with the HTTP GET method.|
| **FilePut**|The full URL of the REST endpoint your app calls to save the file back to Office 365. Your app must call this with the HTTP POST method.|
| **ResourceId**|The URL of the Office 365 tenant used to get the access token from Azure AD.|
| **FileId**|The document ID for a specific document; allows your application to open more than one document at the same time.| 


Access these values from the request body, using the Request.Form collection. For example:

```cs
Request.Form["FileId"];
```

The application must cache these values as soon as the file handler is invoked because the first time the application is invoked for a user it doesn't have an access token, so it will be redirected to Azure AD, triggering the OAuth authorization code flow. Caching them immediately makes them available after Azure AD authorization is complete, and the browser is redirected back to the file handler. You can see an example of using a data model object and handler method for caching the activation parameter in a cookie, in the [GPX-FileHandler sample](https://github.com/OfficeDev/GPX-FileHandler), specifically [ActivationParameters.cs](https://github.com/OfficeDev/GPX-FileHandler/blob/7182d942a738564a53aa06362669dc074be40df6/MVCO365DemoMT/Models/ActivationParameters.cs) and [FileHandlerController.cs](https://github.com/OfficeDev/GPX-FileHandler/blob/7182d942a738564a53aa06362669dc074be40df6/MVCO365DemoMT/Controllers/FileHandlerController.cs).

<a name="sectionSection4"> </a>
#### App manifest and the addIns property


You specify the file handler details in the addIns property in the app manifest. The addIns property itemizes the file handlers contained in an app, and the associated properties. These details are used to configure a file handler for an extension with Office 365, specifying the new file, open and preview behavior for that extension. 

The manifest syntax is:

```json
{
    "addIns": [
        {
            "id": "unique guid",
            "type": "FileHandler",
            "properties": [
                {
                    "key": "extension",
                    "value": "List of file extensions separated by semicolons"
                },
                {
                    "key": "fileIcon",
                    "value": "URL of icon for the file type"
                },
                {
                    "key": "newFileUrl",
                    "value": "URL for the new file function"
                },
                {
                    "key": "openUrl",
                    "value": "URL for the file open function"
                },
                {
                    "key": "previewUrl",
                    "value": "URL for the file preview function"
                }
            ]
        }
    ]
}
```

To configure the file handler, you need to update the app manifest in Azure AD. There is currently no UI in the Azure management portal to do this, so you need to do this using Azure AD Graph API queries. See [Configure and update file handlers in Office 365](..\howto\programmatically-install-update-or-delete-apps.md) for more information.


<a name="sectionSection101"> </a>
## File handler availability

The following table lists the Office 365 services that support file handlers.

|**Service name**|**Availability**|
|:-----|:-----|:-----|
|SharePoint Online|Generally available (GA)|
|OneDrive for Business|GA|
|Outlook Web App|GA|

<a name="bk_addresources"> </a>
## In this section


    

-  [Create File Handlers in Office 365](..\howto\create-file-handler-extensions.md)
    
-  [Install, update, and delete file handlers in Office 365](..\howto\programmatically-install-update-or-delete-apps.md)
    

