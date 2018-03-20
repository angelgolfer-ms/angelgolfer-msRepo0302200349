ms.TocTitle: Configure and update file handlers
Title: Configure and update file handlers in Office 365
Description: Configure a new file handler or update an existing file handler configuration.
ms.ContentId: ae338417-ced2-49f1-93e5-8afa05c03a5e
ms.topic: article (how-tos)
ms.date: December 10, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Configure and update file handlers in Office 365

<!-- Learn how to register new file handlers, and update configuration for existing file handlers. -->


_**Applies to:** Office 365_



## App manifest and the addIns property
<a name="sectionSection0"> </a>

The [Application entity](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#ApplicationEntity) in the Azure active directory (AD) contains a new property, **addIns**, to support file handlers. The **addIns** property itemizes the file handlers contained in an app, and the associated properties. These details are used to configure a file handler for an extension with Office 365, specifying the new file, open and preview behavior for that extension. 

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

**Note** The property keys are case sensitive.

The schema is described in the following table.

|**Member**|**Description**|**Data type**|**Parent**|**Child members**|
|:-----|:-----|:-----|:-----|:-----|
| **addIns**|Root element; contains an array of objects defining file handlers in the application.|array|none|**type**<br/> **properties**|
| **id**|Identifies an individual add-in within the add-ins collection; you can use a GUID generating tool to generate the value.|GUID|**addIns**|none|
| **type**|The add-in type. For file handlers, value is "FileHandler".|string| **addIns**|none|
| **properties**|Defines the file handler properties|object| **addIns**|**extension**<br/> **fileIcon**<br/> **newFileUrl**<br/> **previewUrl**<br/> **openUrl**|
| **extension**|The file handler extension without a leading "." character; for example, "psd". Multiple file extensions, separated by semicolon, can be specified.|string| **properties**|none|
| **fileIcon**|URL for the icon representing the file type; for example, "https://fabrikam.com/SampleFileHandler/psdicon.png". Protocol must be https and can be any image format that will render in an HTML page. The image will automatically resize and  the recommended dimension for image is 32x32 pixels.|string| **properties**|none|
| **newFileUrl** |URL for the new file function; for example, "https://fabrikam.com/SampleFileHandler/newFile". Protocol must be https.|string| **properties**|none|
| **previewUrl**|URL for the preview function; for example, "https://fabrikam.com/SampleFileHandler/preview". Protocol must be https.|string| **properties**|none|
| **openUrl**|URL for the function that opens the file for editing; for example, "https://fabrikam.com/SampleFileHandler/open". Protocol must be https.|string| **properties**|none|

To configure a file handler, you need to add the file handler details via the **addIns** property to the app manifest in Azure AD. There is currently no UI in the Azure management portal to do this, so you need to do this using [Azure AD Graph API](https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api-quickstart/) queries. 

With the first query, you need to retrieve the **objectId** for the application. To do this, you use a **GET** request with the **appId** as a filter parameter for the query.
**Note** The **objectId** and **appId** are both GUIDs that identify the application, but they are not the same value.

You can find the **appId**, also known as the Client ID, in the configuration page for your app in the Azure Management portal, in the **Client ID** property. You can also find it in **ClientID** key of the **appSettings** section of the web.config for your application.

To retrieve the **objectId**, send the following **GET** request to the Azure AD Graph.

```
GET https://graph.windows.net/contoso.com/applications?api-version=1.6&$filter=appId%20eq%20'appId'
```

Replace contoso.com with your tenant domain and *appId* with the Client ID value. This query will return the application object, which contains the **objectId** property.

Now you're ready to construct the  query to update the file handler configuration, as follows:

```
PATCH https://graph.windows.net/contoso.com/applications/objectId/?api-version=1.6
```

Replace contoso.com with your tenant domain and *objectId* with the **objectId** value you retrieved with the first query. Set the content type to application/json, and pass the json specifying the file handler configuration details in the request body.


**Note** The **addIns** property is part of the [Azure AD Graph 1.6 schema](https://graph.windows.net/microsoft.com/$metadata?api-version=1.6), so you need to specify 1.6 for the api-version parameters, as shown in the preceding examples.

For more information, see [Azure AD Graph API Versioning](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning).

**Note** After updating the application configuration, your changes won’t be visible if you download the manifest file.

<a name="sectionSection1"> </a>
## AddIns Manager sample tool

You can use the [AddIns Manager sample tool](https://addinsmanager.azurewebsites.net/) to make the Azure AD Graph queries to configure and update a file handler once you have registered the file handler application with Azure AD. Using the AddIns Manager tool will update the app configuration in Azure AD.

**Note** The AddIns Manager sample tool is for demonstration and testing purposes only, and should not be used in production environments. 

####To use the AddIns Manager tool to configure a file handler
1. Navigate to [AddIns Manager sample tool](https://addinsmanager.azurewebsites.net/).
2. When the page loads in the browser, click **Sign in** in the top right side of the page.
3. Enter the credentials for the tenant admin, and click **sign in**.
4. Select the name of your file handler app in **My Applications** in the left navbar.
5. Click **Register Add-In**.
6. In the **Register Add-In** dialog, select **File Handler**.
7. Click the drop-down for **File Handler Add-In**.
8. Enter the details for your file handler. **Note** The protocol must be https.
9. Click **Update Add-In**. 


If the file handler was configured successfully you will see a message box confirming the successful update.

