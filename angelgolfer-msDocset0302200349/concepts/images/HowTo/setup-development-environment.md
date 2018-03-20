ms.TocTitle: Set up your dev environment
Title: Set up your Office 365 development environment
Description: Confirm or create your Office 365 Developer Site, connect to an Azure tenant so you can register apps, and get tools for developing with the Office 365 APIs.
ms.ContentId: c9fe7f08-bd9d-479c-9fa6-84f17d6a9826
ms.topic: article (how-tos)
ms.date: July 20, 2015

<script src="https://cdn.optimizely.com/js/3097170014.js"></script>

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



[!INCLUDE [Add the platforms filter bar](../includes/controls/addplatformsfilter.xml)]

# Set up your Office 365 development environment

_**Applies to:** Office 365_

[!INCLUDE [Use Microsoft Graph](../includes/use-msgraph-note.txt)]

Before you can create applications that access the Office 365 APIs, you'll need to set up your developer environment. This consists of three one-time tasks to make sure you've got the tools and environment to be successful.

<!--

1. [Download the developer tools](#bk_VisualStudio) you'll be using to create your apps.
3. [Get an Office 365 for business account](#bk_Office365Account), to access the Office 365 APIs.
2. [Associate your Office 365 account with Azure AD](#bk_CreateAzureSubscription), so you can create and manage apps.

-->

<svg xmlns:xlink="http://www.w3.org/1999/xlink" height="63px" width="531px">

<style type="text/css">
	.st0{fill:#A7C7E3;}
	.st1{fill:#2273B9;}
	.st2{fill:none;}
	.st3{font-family:'Segoe UI';}
	.st4{font-size:12px;}
	.st5{fill:#FFFFFF;}
	.st6{font-family:'Segoe UI';}
	.st7{font-size:36px;}
</style>
<g id="Shapes">
	<rect x="48.6" y="9" class="st0" width="124.4" height="44"/>
	<rect x="4" y="9" class="st1" width="45" height="44"/>
	<rect x="352" y="9" class="st1" width="44.9" height="44"/>
	<rect x="396.9" y="9" class="st0" width="125.1" height="44"/>
	<rect x="222" y="9" class="st0" width="126" height="44"/>
	<rect x="177" y="9" class="st1" width="45.1" height="44"/>
</g>
<g id="TEXT">
	<a xlink:href="#bk_VisualStudio">
	<rect x="48.6" y="17.4" class="st2" width="123.8" height="26"/>
	<text transform="matrix(1 0 0 1 83.532 26.3218)"><tspan x="0" y="0" class="st3 st4">Download </tspan><tspan x="-14.1" y="14.4" class="st3 st4">developer tools</tspan></text>
	</a>

	<a xlink:href="#bk_CreateAzureSubscription">
	<rect x="397.9" y="18" class="st2" width="123.8" height="26"/>
	<text transform="matrix(1 0 0 1 406.2534 26.8691)"><tspan x="0" y="0" class="st3 st4">Associate Office 365  </tspan><tspan x="15.8" y="14.4" class="st3 st4">with Azure AD</tspan></text>
	</a>

	<a xlink:href="#bk_Office365Account">
	<rect x="222.1" y="17.7" class="st2" width="125.8" height="26"/>
	<text transform="matrix(1 0 0 1 239.0165 26.5959)"><tspan x="0" y="0" class="st3 st4">Get an Office 365  </tspan><tspan x="-8.2" y="14.4" class="st3 st4">for business account</tspan></text>
	</a>

	<a xlink:href="#bk_VisualStudio">
	<text transform="matrix(1 0 0 1 20 44)" class="st5 st6 st7">1</text>
	</a>

	<a xlink:href="#bk_Office365Account">
	<text transform="matrix(1 0 0 1 191 44)" class="st5 st6 st7">2</text>
	</a>

	<a xlink:href="#bk_CreateAzureSubscription">
	<text transform="matrix(1 0 0 1 362 44)" class="st5 st6 st7">3</text>
	</a>

</g>
</svg>


<a name="bk_VisualStudio"> </a>


[!INCLUDE [BEGIN iOS section](../includes/controls/iossection.xml)]

## Install iOS developer tools for building your app

**Not developing iOS apps?** Use the control in the upper right corner to select the type of app you're developing.


You use [Xcode](https://developer.apple.com/xcode/downloads/) to develop iOS apps. See **Get the tools** in [Start Developing iOS Apps Today](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/RoadMapiOS/) for more details.

You can use the [Office 365 SDK for iOS](https://github.com/OfficeDev/Office-365-SDK-for-iOS) to develop iOS apps that access the Office 365 APIs. To more easily integrate the SDK into your app, you can use the [CocoaPods](http://cocoapods.org/) dependency manager. CocoaPods is based on Ruby, and is available with the default Ruby install on OS X. Prior to using Cocoapods for the first time, you need to run the following two commands from Terminal to install and set up the environment for Cocoapods, so that it is available to use for you Xcode projects:

```
sudo gem install cocoapods
pod setup
```

If the install and setup were successful, you should see the message **Setup completed** in Terminal.

**Note**: These commands only needs to be run once.
  

[!INCLUDE [END iOS section](../includes/controls/iossection.xml)]

[!INCLUDE [BEGIN Android section](../includes/controls/androidsection.xml)]

## Install Android developer tools for building your app

**Not developing Android apps?** Use the control in the upper right corner to select the type of app you're developing.

You have two choices for Android development, [Android Studio](#bk_useAndroidStudio) or the [Android Developer Tools including Eclipse](#bk_useEclipse). The two are similar, but Android Studio takes advantage of Gradle support to manage the library dependencies that you have to manage by hand when you use Eclipse.

<a name="bk_useAndroidStudio" ></a>

* **Android Studio** Follow the instructions on the Android developers site to [download and install Android Studio](https://developer.android.com/sdk/index.html). Follow the instructions in [Add dependencies for Android Studio](#bk_dependenciesForStudio) to add libraries to your project. 

<a name="bk_useEclipse"></a>

* **Android Developer Tools and Eclipse** Follow the instruction on the Android developers site to download and install the [Android Developer Tools including Eclipse](http://developer.android.com/tools/help/adt.html). Follow the instructions in [Add dependencies for Eclipse](#bk_dependenciesForEclipse) to add libraries to your project.


[!INCLUDE [END Android section](../includes/controls/androidsection.xml)]

[!INCLUDE [BEGIN JavaScript section](../includes/controls/javascriptsection.xml)]

## Install Angular developer tools for building your app

**Not developing Angular apps?** Use the control in the upper right corner to select the type of app you're developing.


You can write Angular applications in many different IDEs and since none provide a significant advantage for developing with the Office 365 APIs, choose your favorite and get started. [Brackets](http://brackets.io/), [Sublime Text](http://www.sublimetext.com/), [WebStorm](https://www.jetbrains.com/webstorm/), and [Visual Studio](http://www.visualstudio.com/downloads) are popular choices.

You don't need any other tools to develop Angular applications using the Office 365 APIs. However, if you are following the [Create an Angular app with Office 365 APIs](.\getting-started-Office-365-APIs.md?javascript) tutorial, you'll need to install a couple additional utilities to download and configure the sample, including [Git](http://git-scm.com/) and [Node.js](http://nodejs.org/).

[!INCLUDE [END JavaScript section](../includes/controls/javascriptsection.xml)]

[!INCLUDE [BEGIN ASP.NET MVC section](../includes/controls/aspnetmvcsection.xml)]

## Install Visual Studio developer tools for building your app

**Not developing apps with Visual Studio?** Use the control in the upper right corner to select the type of app you're developing.
 
The Office Developer Tools for Visual Studio include client libraries and UI enhancements to Visual Studio. The client libraries make it easier for you to interact with the Office 365 REST APIs from the device or platform of your choice by using libraries available for .NET Framework and JavaScript. The Visual Studio UI enhancements make it easy to add Office 365 services to your app projects.

Install the [Office Developer Tools for Visual Studio](http://aka.ms/officedevtoolsatvscom). 

####If you don't have Visual Studio

If you don't have a version of Visual Studio installed, you can:


- Install [Visual Studio 2015 Community or Enterprise Editions](http://go.microsoft.com/fwlink/?LinkId=517106) 
    
	Visual Studio Community is available if you're an individual developer, or part of a organization using Visual Studio in a classroom learning environment, for academic research, or for contributing to open source projects. Developers at non-enterprise organizations may qualify as well. For more information, please refer to the [Visual Studio Community License Terms](https://www.visualstudio.com/support/legal/dn877550) and the [Visual Studio Licensing Whitepaper](https://www.microsoft.com/en-us/download/details.aspx?id=13350).

- Install Visual Studio  [via your MSDN subscription](http://msdn.microsoft.com/en-us/subscriptions/downloads/).
    

<!--
####To install the Office Developer Tools for Visual Studio 2013

- Download and install the [Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013).

####If you have Visual Studio 2012

If you have Visual Studio 2012 installed, you can download and install the [Office Developer Tools for Visual Studio 2012](http://aka.ms/OfficeDevToolsForVS2012).

-->    
 

[!INCLUDE [END ASP.NET MVC section](../includes/controls/aspnetmvcsection.xml)]



<a name="bk_Office365Account"> </a>
## Get an Office 365 account to access Office 365 APIs

To access Office 365 APIs such as mail, contacts, calendar, and files, you need to have an Office 365 business account with global administrator privileges. 

<!--
Tech reviewers: Is this correct, that you currently need global admin privileges to a) associate your O365 account with Azure AD, and b) manage apps through the Azure managment portal? I've gotten conflicting answers from various product team members. I know this'll change once the new MSA-enabled registration portal goes live, but is this accurate currently? Thanks!
-->

This can be one of the following plans:

- Office 365 Midsize Business
- Office 365 Enterprise E1, E3, E4, or K1
- Office 365 Education
- Office 365 Developer 

<!--
- Office 365 Government G1, G3, G4, or K1
-->

### If you already have an Office 365 for business account

If you already have one of the Office 365 accounts listed above, you're set. The next step is to  [associate your Office 365 account with an Azure AD subscription](#bk_CreateAzureSubscription), so you can create and manage apps that use the Office 365 APIs.


### If you don't currently have an Office 365 for business account

If you don't have an existing Office 365 for business account, you can:

- Sign up for one of the [Office 365 for business plans](http://products.office.com/en-us/business/compare-office-365-for-business-plans) listed above, or
- Sign up for an Office 365 Developer account, as described below.

<!--
Follow up with PMG about their plan to give away 10,000 O365 Developers subscriptions through dev.office.com. If/when that program happens, make sure to update the topic to link to that offer.
-->

#### Signing up for an Office 365 Developer account

**If you have an MSDN subscription, ** [redeem your Office 365 Developer account benefit](https://msdn.microsoft.com/subscriptions/manage/default.aspx). This benefit is available to Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers.

**Otherwise,** start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK), or buy an  [Office 365 Developer account](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK) (with one user license for either option). This account costs $99.00 per year.

<!--
Follow up with PMG about their plan to give away 10,000 O365 Developers subscriptions through dev.office.com. If/when that program happens, make sure to update the topic to link to that offer.
-->


When you sign up for a new Office 365 Developer account, follow these instructions.

    
During signup, you'll be asked to supply a subdomain of  **.onmicrosoft.com** and a user ID to assign to the domain that you're creating, as shown in Figure 1. After signup, you have to use the resulting **userid** (in the format _userid@yourdomain_.onmicrosoft.com) to sign in to your portal site where you administer your account. 


**Note**  If you're logged on to another Microsoft account when you try to sign up for a Developer subscription, you might get this message: "Sorry, that user ID you entered didn't work. It looks like it's not valid. Be sure you enter the user ID that your organization assigned to you. Your user ID usually looks like  _someone@example.com_ or _someone@example.onmicrosoft.com_." If you see this message, log out of the Microsoft account you were using and try again. If you still get the message, clear your browser cache or switch to a private browser session and then fill out the form.


**Figure 1. Office 365 Developer account domain name**

![During signup to create your Office 365 Developer subscription, you're asked to supply a unique subdomain of .onmicrosoft.com and a user ID.](images\SP15_app_O365Signup_bordered.png)
    

After you finish the signup process, your browser opens the Office 365 installation page. Choose the **Admin** icon to open the admin center page.


<a name="bk_CreateAzureSubscription"> </a>
## Associate your Office 365 account with Azure AD to create and manage apps

To authenticate your applications, you need to register them in Microsoft Azure Active Directory (Azure AD). This is where Office 365 user account and application information is stored. To manage Azure AD through the Azure Management Portal, you need a Microsoft Azure subscription. Using the management portal in Microsoft Azure enables you to manage users, roles, and apps. 

- **If you can have an existing Microsoft Azure subscription**, you can [associate your Office 365 for business subscription with it](#bk_AssociateExistingAzureSubscription). 

- **Otherwise**, you'll need to [create a new Azure subscription and associate it with your Office 365 account](#bk_AssociateNewAzureSubscription) in order to register and manage apps.


<a name="bk_AssociateExistingAzureSubscription"> </a>
### To associate an existing Azure subscription with your Office 365 account


1. Log on to the  [Microsoft Azure Management portal](https://manage.windowsazure.com) with your existing Azure credentials (for example, your Microsoft ID such as user@live.com).
	    
2. Select the  **Active Directory** node, then select the **Directory** tab and, at the bottom of the screen, select **New**. 
	 
4. On the **New** menu, select **Active Directory** > **Directory** > **Custom Create**.
	
5. In **Add directory**, in the **Directory** drop-down box, select  **Use existing directory**. Check **I am ready to be signed out**, and then select the check mark in the lower-right corner. 
	
	This brings you back to the Azure Management Portal.
	    
3. Log in with your Office 365 account information. 
	
	You will be prompted whether to use your directory with Azure. 
	
	**Important** To associate your Office 365 account with Azure AD, you'll need  an Office 365 business account with global administrator privileges. 
	
	    
4. Select  **continue**, and then **Sign out now**.
	    
5. Close the browser and reopen the  [portal](https://manage.windowsazure.com). Otherwise, you will get an access denied error.
	
	    
6. Log on again with your existing Azure credentials (for example, your Microsoft ID such as user@live.com). Navigate to the  **Active Directory** node and, under **Directory**, you should now see your Office 365 account listed.
	
	
<a name="bk_AssociateNewAzureSubscription"> </a>
### To create a new Azure subscription and associate it with your Office 365 account


1. Log on to Office 365. From the **Home** page, select the **Admin** icon to open the Office 365 admin center.
2. In the menu page along the left side of the page, scroll down to **Admin** and select **Azure AD**.

	**Important** To open the Office 365 admin center, and access Azure AD, you'll need  an Office 365 business account with global administrator privileges. 
	
3. Create a new subscription.
		
	If you're using a trial version of Office 365, you'll see a message telling you that Azure AD is limited to customers with paid services. You can still create a trial 30-day Azure subscription at no charge, but you'll need to perform a few extra steps:
	
	1. Select your country or region, and then choose **Azure subscription**.
	2. Enter your personal information. For verification purposes, enter a telephone number at which you can be reached, and specify whether you want to be sent a text message or called.
	3. Once you've received your verification code, enter it and choose **Verify code**.
	4. Enter payment information, check the agreement, and select **Sign up**.
		
		Your credit card will not be charged.
		
		Do not close or refresh your browser while your Azure subscription is being created.
		    
4. Once your Azure subscription is created, choose  **Portal**.
	    
5. The Azure Tour appears. You can view it, or choose  **X** to close it.
	    
	You should now see all items in your Azure subscription. It lists a directory with the name of your Office 365 tenant.
	


[!INCLUDE [BEGIN iOS section](../includes/controls/iossection.xml)]


##Next steps

Now, you're ready to  [build and run your first app](..\howto\getting-started-Office-365-APIs.md). 
    


- [iOS SDK for Office 365](https://github.com/OfficeDev/Office-365-SDK-for-iOS) 


[!INCLUDE [END iOS section](../includes/controls/iossection.xml)]

[!INCLUDE [BEGIN Android section](../includes/controls/androidsection.xml)]


##Next steps

Now, you're ready to  [build and run your first app](..\howto\getting-started-Office-365-APIs.md). 


[!INCLUDE [END Android section](../includes/controls/androidsection.xml)]

[!INCLUDE [BEGIN JavaScript section](../includes/controls/javascriptsection.xml)]

##Next steps

Now, you're ready to  [build and run your first app](..\howto\getting-started-Office-365-APIs.md). 
    


[!INCLUDE [END JavaScript section](../includes/controls/javascriptsection.xml)]

[!INCLUDE [BEGIN ASP.NET MVC section](../includes/controls/aspnetmvcsection.xml)]

##Next steps

Now, you're ready to  [build and run your first app](..\howto\getting-started-Office-365-APIs.md). 
    


[!INCLUDE [END ASP.NET MVC section](../includes/controls/aspnetmvcsection.xml)]

## Additional resources


-  [Office 365 API starter projects, code samples, and videos](..\howto\starter-projects-and-code-samples.md) 

-  Try writing code against the Office 365 APIs using the [API Sandbox](http://apisandbox.msdn.microsoft.com)


-  [Office 365 API reference](..\api\API-Catalog.md)


    
    
[!INCLUDE [Enable filtering functionality ](../includes/controls/enablefiltering.xml)]


