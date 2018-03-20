ms.TocTitle: Add Office 365 services in Visual Studio
Title: Using Visual Studio to register your app and add Office 365 APIs
Description: Learn how to register your app with Microsoft Azure Active Directory, add an Office 365 API service to your Visual Studio project, and set app permissions.
ms.ContentId: 5a2fbbba-dd0f-4cfe-b27a-dcd2ede82884
ms.topic: article (how-tos)
ms.date: July 20, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Using Visual Studio to register your app and add Office 365 APIs
   
_**Applies to:** Office 365_

    
After you've [set up your development environment](..\howto\setup-development-environment.md), you're ready to add an Office 365 API service to your Visual Studio project.


**In this article**

-  [Prerequisites for registering your apps with Azure AD using Visual Studio](#bk_RegistrationPrereqs)
-  [Use the Visual Studio Service Manager to register your app and add Office 365 APIs](#addO365APIs)
-  [Manually add optional Office 365 API Client Library NuGet Packages to your project](#O365NuGets)
-  [Next steps](#NextSteps)

<a name="bk_intro"> </a>
## When you add an Office 365 service to your project, Visual Studio helps you register your app

The Office 365 API services use Azure AD to provide secure authentication to users' Office 365 data. To access the Office 365 APIs, you need to register your app with Azure AD. 

If you are creating a Visual Studio project, app registration is handled for you when you add an Office 365 service to your project. 

Select the version of Visual Studio you're using:

[!INCLUDE [Add the VS versions filter bar](../includes/controls/vsversionsfilter.xml)]

During the process of adding an Office 365 service to your project, Visual Studio enables you to:

[!INCLUDE [BEGIN VS2013 section](../includes/controls/vs2013section.xml)]

-  Register your app with Azure AD, including specifying whether your app is a web application or native app
-  Configure app properties, such as app name, redirection/response endpoints, and tenancy scope

[!INCLUDE [END VS2013 section](../includes/controls/vs2013section.xml)]

[!INCLUDE [BEGIN VS2015 section](../includes/controls/vs2015section.xml)]

-  Register your app with Azure AD

[!INCLUDE [END VS2015 section](../includes/controls/vs2015section.xml)]

-  Connect to Office 365 services
-  Specify the permission levels your app requires for the APIs in those Office 365 services
-  Add the required **NuGet packages** to the project, based on the Office 365 services to which your app connects

The following projet templates support adding Office 365 APIs as a connected service:

- .NET Windows Store 8.1 Apps
- .NET Windows Store 8.1 Universal Apps
- .NET Windows Phone 8.1 Apps
- .NET Windows Phone 8.1 Silverlight Apps
- Windows Forms Applications
- WPF Applications
- ASP.NET MVC Web Applications
- ASP.NET Web Forms Applications
- Xamarin Android and iOS Applications
- Multi-device Hybrid (Cordova) Apps

If you don't have an existing Visual Studio project in which you want to use Office 365 APIs, or you'd like to try out completed projects that use the Office 365 APIs, download one of the projects listed on the [Office 365 APIs starter projects and code samples](..\howto\Starter-projects-and-code-samples.md) page.

<a name="bk_RegistrationPrereqs"> </a>
##Prerequisites for registering your apps with Azure AD using Visual Studio

To register your apps, you'll need:

- An [Office 365 Developer Site](..\howto\setup-development-environment.md#bk_Office365Account)
- An Azure AD tenant [associated with your Office 365 Developer Site](..\howto\setup-development-environment.md#bk_CreateAzureSubscription)
- [Visual Studio and the Office Developer Tools for Visual Studio](..\howto\setup-development-environment.md#bk_VisualStudio) 


<a name="addO365APIs"> </a>
## Use the Visual Studio Service Manager to register your app and add Office 365 APIs to your project

You add and configure Office 365 APIs by using the  **Services Manager** in Visual Studio.

[!INCLUDE [BEGIN VS2013 section](../includes/controls/vs2013section.xml)]

1. In the **Solution Explorer**, choose the project node  to which you want to add an Office 365 service.
    
2. Right-click or press and hold the project node and choose **Add** > **Connected Service**.
    
3. Register your app:
	
	At the top of the  **Services Manager** dialog box, choose the **Office 365** link, and then choose **Register your app**. Sign in with a tenant administrator account for your Office 365 developer organization. 

	This starts the app registration in Microsoft Azure Active Directory, which allows your app to authenticate via OAuth.
    
    After you've logged on to Office 365, a list of available Office 365 APIs services appears. You will see a list of Office 365 APIs.

	You will see that the **Permissions** column to the right of each service is empty.
    
4. Select the Office 365 APIs to which you want to connect, and specify permission levels for each:
	
	In the list:
	1. Select the Office 365 APIs you want to add
	1. Choose  **Permissions**.

		![A screenshot that shows the Services Manager dialog box with the Calendar service Office 365 API selected and the Permissions link highlighted.](images\Office365_AddServiceToYourProject_ServiceManager1.png)

	In the  **[Office 365 service] Permissions** dialog box:

	1. Select the permissions your project requires
	2. Choose  **Apply**.

		![A screenshot that shows the Calendar Permissions dialog box with the Read users' calendars permission selected.](images\Office365_AddServiceToYourProject_Permissions.png)

	When you do this, Visual Studio adds the Office 365 service(s) that contain the APIs you selected to your app in Azure AD, and sets the permission levels for the APIs to those you specified.
	
6. Set properties for your app:

	Choose  **App Properties** in the **Services Manager** dialog box. 

	The app properties you can set differ depending on whether your app project is a web service or web application, or a native application, such as a mobile phone project.

	For example, for web applications, to make this sample app available to Office 365 organizations other than your developer organization:
	1. Change the **Make this app available to:** setting to **Multiple Organizations** 
	2. Choose  **Apply**.
    
	![A screenshot of the Office 365 App Properties dialog box showing the setting to select to make your app available to multiple organizations.](images\Office365_AddServiceToYourProject_AppProperties.png)
	
	The  **Services Manager** dialog box now lists:
	
	- The service(s) you've selected to add to your project
	- The permissions for each service. 

		![A screenshot of the Services Manager dialog box after the Calendar service is configured, showing that the Calendar service has Read permissions.](images\Office365_AddServiceToYourProject_ServiceManager2.png)
	
6. Choose **OK**.
	
	
At this point, Visual Studio adds the required **NuGet packages** to the project. The NuGet packages added vary based on the Office 365 APIs you added.
    
[!INCLUDE [END VS2013 section](../includes/controls/vs2013section.xml)]

[!INCLUDE [BEGIN VS2015 section](../includes/controls/vs2015section.xml)]

1. In the **Solution Explorer**, choose the project node to which you want to add an Office 365 service.
    
2. Right-click or press and hold the project node and choose **Add** > **Connected Service**.

3. On the **Microsoft** tab, choose **Office 365 APIs**, and choose **Configure**.

	The **Configure Office 365 API Services** dialog box appears.
    
3. Register your app:
	
	On the **Select Domain** page, enter or select the Office 365 domain in which you want your app to be registered; for example, <i>contoso.onmicrosoft.com</i>. Choose **Next**. You may be required to sign into Office 365, if you are not already currently signed in. 
	
	On the **Configure Application** page, choose to create a new Azure AD application, or use an existing one. If you choose to use an existing Azure AD application, enter that application's client ID.
	
	If you want to use Single Sign-On with your application, check the box. Since Single Sign-On requires SSL, selecting this option automatically enables SSL in your project. 
	
	Choose **Next**. 

	Visual Studio registers your app.
    
4. Select the Office 365 APIs to which you want to connect, and specify permission levels for each:
	
	1. Select the Office 365 API; for example, Contacts or My Files.
	
	2. Choose the permission(s) your app requires.
		
		Remeber that permissions are additive in scope. For example, for the Mail API, the **Read and write to your mail** permission includes the **Read your mail** permission, so you don't need to select both. In general, select the least expansive permission that still enables your app to accomplish all it needs to do.
		
	2. Choose  **Next**.
	
	When you do this, Visual Studio adds the Office 365 service(s) that contain the APIs you selected to your app in Azure AD, and sets the permission levels for the APIs to those you specified.
	
6. When you have added all the APIs your app requires, choose **Finish**.
	
At this point, Visual Studio adds the required **NuGet packages** to the project. The NuGet packages added vary based on the Office 365 APIs you added.
    

[!INCLUDE [END VS2015 section](../includes/controls/vs2015section.xml)]



<a name="O365NuGets"> </a>
## Manually add optional Office 365 API Client Library NuGet Packages to your project

While the Office 365 tools automatically add the necessary NuGet packages when you add an Office 365 service, you can also manually add and manage NuGet packages by using the [Manage NuGet Packages dialog box](http://docs.nuget.org/consume/package-manager-dialog) or the [NuGet Package Manager console and PowerShell](http://docs.nuget.org/consume/package-manager-console). 

The following table lists the required NuGet packages, based on which Office 365 API service you add, and the type of project you've created.


|**Office 365 service**|.NET Windows Store Apps (Windows Store and Windows Phone)|Windows Desktop Apps (WPF and Windows Forms)|ASP.NET Web Applications (MVC and Web Forms)|Xamarin Applications (iOS and Android)|Cordova Applications|
|:-----|:-----|:-----|:-----|:-----|:-----|
|Users and Graphs|[Microsoft.Azure.ActiveDirectory.GraphClient](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)|[Microsoft.Azure.ActiveDirectory.GraphClient](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)|[Microsoft.Azure.ActiveDirectory.GraphClient](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)|[Microsoft.Azure.ActiveDirectory.GraphClient](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)|[Microsoft.Azure.ActiveDirectory.GraphClient.JS](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient.JS/)|
|Outlook Services|[Microsoft.Office365.OutlookServices](http://www.nuget.org/packages/Microsoft.Office365.OutlookServices/)|[Microsoft.Office365.OutlookServices](http://www.nuget.org/packages/Microsoft.Office365.OutlookServices/)|[Microsoft.Office365.OutlookServices](http://www.nuget.org/packages/Microsoft.Office365.OutlookServices/)|[Microsoft.Office365.OutlookServices](http://www.nuget.org/packages/Microsoft.Office365.OutlookServices/)| |
|SharePoint Services|[Microsoft.Office365.SharePoint](http://www.nuget.org/packages/Microsoft.Office365.SharePoint/)|[Microsoft.Office365.SharePoint](http://www.nuget.org/packages/Microsoft.Office365.SharePoint/)|[Microsoft.Office365.SharePoint](http://www.nuget.org/packages/Microsoft.Office365.SharePoint/)|[Microsoft.Office365.SharePoint](http://www.nuget.org/packages/Microsoft.Office365.SharePoint/)| |
|Discovery client|[Microsoft.Office365.Discovery](http://www.nuget.org/packages/Microsoft.Office365.Discovery/)|[Microsoft.Office365.Discovery](http://www.nuget.org/packages/Microsoft.Office365.Discovery/)|[Microsoft.Office365.Discovery](http://www.nuget.org/packages/Microsoft.Office365.Discovery/)|[Microsoft.Office365.Discovery](http://www.nuget.org/packages/Microsoft.Office365.Discovery/)||
|Any service| | | |[Microsoft.Office365.OAuth.Xamarin](http://www.nuget.org/packages/Microsoft.Office365.OAuth.Xamarin)|[Microsoft.Office365.ClientLib.JS](http://www.nuget.org/packages/Microsoft.Office365.ClientLib.JS/)|



Depending on your project type, certain NuGet packages are required when adding any Office 365 service:

- For Cordova projects, the [Microsoft.Office365.ClientLib.JS](http://www.nuget.org/packages/Microsoft.Office365.ClientLib.JS/) NuGet package is always required. 

	This package includes the necessary files for adding Outlook Services or SharePoint Services to your Cordova project.

- For Xamarin projects, the [Microsoft.Office365.OAuth.Xamarin](http://www.nuget.org/packages/Microsoft.Office365.OAuth.Xamarin) NuGet package is always required. 

<!--
- For MVC, WPF and WinForms, Windows Store and Phone projects, the [Microsoft.Office365.Discovery](http://www.nuget.org/packages/Microsoft.Office365.Discovery/) is always required.
- -->



Xamarin Studio now offers support for managing NuGet packages.

<a name="NextSteps"> </a>
## Next steps

After you're added an O365 service to your app, you'll need to authenticate the app with Office 365 in order to gain access to your user's data. See [Integrate Office 365 APIs into .NET Visual Studio projects](..\howto\Authenticate-and-use-services.md) for more details. 


[!INCLUDE [Enable filtering functionality ](../includes/controls/enablefiltering.xml)]


