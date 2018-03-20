ms.TocTitle: Create file handlers in Office 365
Title: Create file handlers in Office 365
Description: Create an Office 365 file handler with basic functionality, based on modifying a project template.
ms.ContentId: d8f4bc98-118c-444a-9e64-e16fb36bf605
ms.topic: article (how-tos)
ms.date: December 10, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Create file handlers in Office 365

    
_**Applies to:** Office 365_


This walkthrough demonstrates creating a basic file handler for a custom file type using the File Handler application project template. You can download the template for Visual Studio 2013 and Visual Studio 2015 from [File Handler Application](https://visualstudiogallery.msdn.microsoft.com/16013099-a1c2-4718-b111-c581a095996e), or locate it from the **Online Templates** section in the **New Project** dialog.


<a name="sectionSection102"> </a>
## Create and customize the Office 365 app

As mentioned previously, this sample is based on the File Handler application project template, so to start you'll need to create a new project using that template. You can either download it from [File Handler Application](https://visualstudiogallery.msdn.microsoft.com/16013099-a1c2-4718-b111-c581a095996e), or locate it from the **Online Templates** section in the **New Project** dialog.

###To download the template and create the project

1. On the **File** menu, click **New** and then click **Project**.
2. In the left pane, select **Online**, and in the **Visual C#** category, select **Office**.
3. **File Handler Application** should appear as on option in the middle pane; select it, enter basicfilehandler for the name, and click **OK** to create the project.

If you have not installed the template yet, you will be prompted to install the template.

Next you'll register the app with Azure AD and then modify it to add the file handler extension functionality.

###To register and configure the app with Azure AD

1. In the Solution Explorer, right-click the project name and choose **Add** > **Connected Service**.

2. Select **Office 365 APIs**, and click **Configure**.

3. Click **Register your app**. 

    **Note** The text in the **Add Connected Service** dialog may differ depending on Visual Studio version you are working in. Also, if **Register your app** is not available, you may need to remove placeholder values for the ClientId and ClientSecret in the web.config. To do this, search for the following keys and remove them from the web.config:
    
    ```xml
    <add key="ida:ClientId" value="[ClientId placeholder]" />
    <add key="ida:ClientSecret" value="[ClientSecret placeholder]" />
    ```

4. Sign in with a tenant administrator account for your Office 365 developer organization.

6. Click **App Properties**.

7. Add the following to the **redirect URIs** list:

	- `http://basicfilehandler.azurewebsites.net` 

	- `https://basicfilehandler.azurewebsites.net` 

	**Note** The basicfilehandler.azurewebsites.net site is where the file handler application will be hosted. You will create this when you publish this project to Azure in a later step.

8. Click **Apply** to close the **App Properties** dialog, and then **OK** to close the **Services Manager** dialog.

At this point, Visual Studio adds the required NuGet packages to the project. Now you're ready to configure permissions for your app, which must be done in the Azure AD management portal.

9. Sign into the [Azure Management Portal](https://manage.windowsazure.com/).

10. In the left navigation panel, select **Active Directory**. Make sure the **Directory** tab is selected, and then click on the directory name.

11. On the directory page, select Applications. You should see your file handler application listed. If you don't see it in the list, select **Applications my company owns** in the **Show** dropdown.

12. Select your application, and then click **Configure** in the top menu.

13. Scroll to the bottom of the page and, under **permissions to other applications**, select **Add application**.

14. Select **Microsoft Graph**, and then click the checkmark icon.

15. Under **permissions to other applications**, click the **Delegated Permissions** column and select **Read and write files that the user selects**.

16. Click **Save** in the bottom navigation bar.




<a name="sectionSection0"> </a>
## Code the file handler application

Now you're ready to add the file handler specific code to the application. If you've used the File Handler application project template to create the project, a lot of this work is already done for you. The primary tasks remaining are for you to add code to the NewFile, Open and Preview methods to specify what should happen for the custom file type.

You can find these methods in the FileHandlerController.cs file in the Controllers folder of the project solution.

For the Preview method, look for the following method declaration:

```cs
public async Task<ActionResult> Preview()
```

For the Open method, look for the following method declaration:

```cs
public async Task<ActionResult> Open()
```

For the New file method, look for the following method declaration:

```cs
public async Task<ActionResult> NewFile()
```

**Note** The first part of the code in these methods loads the activation parameters. Activation parameters contain information that Office 365 includes as part of the **POST** request made to the file handler. 
The code included with the project template accesses and caches these values as soon as the file handler is invoked. For more information about the parameters available, see File handler activation parameters.



<a name="sectionSection4"> </a>
## Publish application

Now you're ready to publish the application to Azure.

1. In **Solution Explorer**, right-click the project and select **Publish**.

2. Select **Microsoft Azure Websites**.

3. When you are prompted for credentials, enter the credentials you use to manage your Azure subscription.

4. In **Select Existing Websites**, click **New**.

5. Enter **basicfilehandler** as the **Site name**.

6. If you don't have a database server set up, specify **Create new server**; otherwise, select the database server to use.

7. Click **Create**.

8. Once the site is created, click **Publish**.


<a name="sectionSection5"> </a>
## Configure the file handler

After publishing the file handler application, you are ready to configure it in Office 365. 

1. Navigate to the [AddIns Manager sample tool](https://addinsmanager.azurewebsites.net/), which is a sample tool you can use to make the necessary queries to the Azure AD Graph API to configure the file handler. Using the AddIns Manager tool will update the app configuration in Azure AD.

   **Note** The AddIns Manager sample tool is for demonstration and testing purposes only, and should not be used in production environments. 

2. When the page loads in the browser, click **Sign in** in the top right side of the page.

3. Enter the credentials for the tenant admin, and click **sign in**.

4. Select the name of your file handler app in **My Applications** in the left navbar.

5. Click **Register Add-In**.

6. In the **Register Add-In** dialog, select **File Handler**.

7. Click the drop-down for **File Handler Add-In**.

8. Enter the details for your file handler. **Note** The protocol must be https.

9. Click **Update Add-In**.   

<a name="sectionSection103"> </a>
## Test the file handler

To test your application, upload some sample files using the custom file type to your SharePoint site. 
When you view the document library, these files should be displayed with the image you specified for the custom file icon.
If you make add-in metadata changes in Azure Active Directory, you can see the changes in Office 365 by refreshing your browser.

<a name="sectionSection100"> </a>


<a name="sectionSection101"> </a>
