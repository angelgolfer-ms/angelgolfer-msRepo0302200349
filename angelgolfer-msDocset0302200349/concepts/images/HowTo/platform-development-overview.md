ms.TocTitle: Platform overview
Title: Office 365 APIs platform overview
Description: Using Office 365 APIs, create custom solutions that access your customer's Office 365 data and build those apps across mobile, web, and desktop platforms.
ms.ContentId: 16fbf0c0-5470-466b-aab8-a0c9074c94e2
ms.topic: article (how-tos)
ms.date: July 20, 2015

<script src="https://cdn.optimizely.com/js/3043860527.js"></script>

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Office 365 APIs platform overview

_**Applies to:** Office 365_

[!INCLUDE [Use Microsoft Graph](../includes/use-msgraph-note.txt)]

Whether you want to incorporate the richness of Office 365 data into your app, or create a custom experience within Office 365 itself, or use custom reports to keep your Office 365 Enterprise environment running smoothly, you can use the developer features below to achieve your goals. 

<style>#mytable {border:none;} #mytable td {border:none;}</style>
<table id="mytable">
	<tr>
		<td>
			![Office 365 APIs.](images\O365_APIsAndSuiteApps_1.png)

		</td>
		<td>

				<p>**Integrate Office 365 data into your own apps**</p>
				
				<p>You can create custom solutions that access and interact with all the richness of a user’s Office 365 data—and you can build those solutions across all mobile, web, and desktop platforms. The new Office 365 APIs enable you to provide access to Office 365 data, including their mail, calendars, contacts, files, and folders. All right from within your app itself.</p> 
				
				<p>Whether you're building web applications using .NET, PHP, Java, Python, or Ruby on Rails, or creating apps for Windows 8, Universal Apps, iOS, Android, or on another device platform. It's your choice.</p>
				
				<p>See [Office 365 API overview](..\howto\rest-api-overview.md).</p>
		</td>
	</tr>
	<tr>
		<td>
			![Office 365 APIs.](images\O365_APIsAndSuiteApps_2.png)
		</td>
		<td>
			<p>**Create custom experiences within Office 365**</p>
			
			<p>Now, you can extend Office 365 itself. Customize how your data and experiences are displayed within and interact with Office 365 to provide a seamless user experience.</p> 	
					
			<ul>
				<li>[Create a FileHandler add-in](..\howto\using-cross-suite-apps.md) to control how Office 365 displays and interacts with your custom file types, including custom file type icons, file preview within the Office 365 UI, creating and opening the file type in a custom editor. And since FileHandler add-ins host their data and logic remotely, you can develop your add-in using the language, tools, and web development stack of your choice.
				</li>
				<li>[Add your app to the app launcher](..\howto\connect-your-app-to-o365-app-launcher.md) to give it visibility and make it accessible right from the Office 365 home page. Take advantage of Azure AD single sign-on to provide seamless access to your app for authorized users.
				</li>
			</ul>

		</td>
	</tr>
	<tr>
		<td>
			![Office 365 APIs.](images\O365_APIsAndSuiteApps_3.png)
		</td>
		<td>
			<p>**Analyze and manage the health of your Office 365 Enterprise environment**</p>
			
			<p>Office 365 Enterprise provides administrators a variety of developer features to keep their domains and subscriptions effective and well-tuned.</p>
			
			<ul>
				<li>[Access the Reporting web service](https://msdn.microsoft.com/en-us/library/office/jj984325.aspx) to build reporting dashboards, charts, and graphs to help their organization manage their subscription usage.
				</li>
				<li>[Use the Office 365 Service Communications API (preview)](https://msdn.microsoft.com/library/office/dn707386.aspx) to retrieve real-time service health information and Message Center communications for the domains that they own or manage. This enables them to monitor service health, manage communications, and develop plans to respond to upcoming service maintenance.
				</li>
				<li>[Use the Office 365 Management Activity API (preview)](https://msdn.microsoft.com/library/office/mt227394.aspx) to retrieve information about various user, admin, system, and policy actions and events from Office 365 and Azure AD  activity logs. Use this information to build solutions that provide monitoring, analysis, and data visualizations. 
				</li>
			</ul>

		</td>
	</tr>
	
</table>

You can also create custom experiences within the Office clients, such as Word, Excel, and PowerPoint, and within SharePoint 2013 and SharePoint Online. To learn more, see [Office add-ins](https://msdn.microsoft.com/library/jj220060.aspx) and [SharePoint add-ins](https://msdn.microsoft.com/library/fp179930.aspx).
  

## Additional resources
<a name="bk_addresources"> </a>


### General
-  [Code samples on dev.office.com](http://dev.office.com/code-samples#?filters=office%20365%20app)

-  [Set up your Office 365 development environment](..\howto\setup-development-environment.md)
    
-  [Office 365 app authentication and resource authorization](..\howto\common-app-authentication-tasks.md)

-  [Blog: .NET and JavaScript libraries for Office 365 APIs](http://blogs.office.com/2014/05/12/net-and-javascript-libraries-for-office-365-apis/)

-  [Office 365 API Tools for Visual Studio and Office 365 Client Libraries](http://aka.ms/clientlibrary)

-  [Getting familiar with the Office 365 API Client Libraries](http://chakkaradeep.com/index.php/getting-familiar-with-the-office-365-api-client-libraries/)

-  [Office 365 API Client Libraries - Authenticating your client to Office 365](http://chakkaradeep.com/index.php/office-365-api-client-libraries-authenticating-your-client-to-office-365/)

-  [Changes to Office 365 API Authentication Library in the Summer Update](http://chakkaradeep.com/index.php/changes-to-office-365-api-authentication-library-in-the-summer-update/)

-  [Training videos on the Office Dev Center](http://dev.office.com/training)

-  [Getting started with the Office 365 APIs (training video)](http://www.microsoftvirtualacademy.com/training-courses/introduction-to-office-365-development?m=10072&ct=31602) 

### Android apps

-  [Develop Office 365 REST API apps for Android](..\howto\getting-started-Office-365-APIs.md)

### Web applications
-  [Building an Office 365 ASP.NET MVC app](..\howto\getting-started-Office-365-APIs.md)

-  [Office 365 APIs and Python Part 1: OAuth2](http://blogs.msdn.com/b/exchangedev/archive/2015/01/05/office-365-apis-and-python-part-1-oauth2.aspx)
    
-  [Office 365 APIs and Python Part 2: Contacts API](http://blogs.msdn.com/b/exchangedev/archive/2015/01/09/office-365-apis-and-python-part-2-contacts-api.aspx)
    
-  [Office 365 APIs and Python Part 3: Mail and Calendar API](http://blogs.msdn.com/b/exchangedev/archive/2015/01/15/office-365-apis-and-python-part-3-mail-and-calendar-api.aspx)

    

