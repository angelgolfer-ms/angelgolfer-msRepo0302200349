ms.TocTitle: Integrate Office 365 APIs into Visual Studio
Title: Integrate Office 365 APIs into .NET Visual Studio projects
Description: Use ADAL to authenticate with Azure Active Directory, then use Office 365 Discovery Service to determine resource endpoints to access Office 365 user data.
ms.ContentId: 8c30ca03-6433-4fcf-a01d-fd142620d12f
ms.topic: article (how-tos)
ms.date: June 2, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Integrate Office 365 APIs into .NET Visual Studio projects

_**Applies to:** Office 365_


After you've [added an Office 365 service to your project](..\howto\adding-service-to-your-Visual-Studio-project.md), you'll need to write code that authenticates the app user and accesses their Office 365 data. 

The authentication process is different based on whether you are building a web application, such as an MVC, or a native application, such as a Windows Store app. Select one of the links below to walk through an example of building an application that uses the Office 365 APIs: 

- [Integrating Office 365 APIs into an MVC application](#bk_IntegrateMVC)
- [Integrating Office 365 APIs into a Windows Store app](#bk_IntegrateWindowsStore)

**Note** These walkthroughs use the latest version of the [Office Developer Tools for Visual Studio](http://aka.ms/OfficeDevToolsForVS2013). If you're using earlier versions of the tools, you'll want to upgrade to the latest version to ensure the code in these examples works correctly for you.


<a name="bk_IntegrateMVC"> </a>
##Integrating Office 365 APIs into an MVC Visual Studio Project


The example we'll build will be a single-tenant MVC that uses Azure AD Single Sign-on to authenticate and read the user's Contact information from Office 365. We'll use the [Office 365 single-tenant MVC project](https://github.com/OfficeDev/O365-WebApp-SingleTenant) on GitHub as a model. 

The application will employ a persistent [Active Directory Authentication Library](https://msdn.microsoft.com/en-us/library/azure/jj573266.aspx) (ADAL) token cache that uses a database for caching. ADAL enables you to  authenticate users to Active Directory (AD), in this case Azure AD, and then obtain access tokens for securing API calls. 

In order to successfully build this example, you'll need to have set the following permissions for the Office 365 APIs. 

- For the **Users and Groups** APIs, set permissions to **Enable sign-on and read users' profile**.

- For the **Contacts** APIs, set permissions to **Read users' contacts**.

To open the Office 365 tools to make sure you have set the above permissions, in **Solution Explorer**, right-click the project and select **Add** > **Connected Service**.

From there, building the example consists of three major steps:

 - [Configure your project for authentication with Azure AD](#bk_AuthenticateAzure)

 - [Authenticate with Azure Active Directory](#bk_AuthenticateAzureAD)

 - [Access Office 365 APIs](#bk_accessOffice365APIs)


<a name="bk_AuthenticateAzure"> </a>
###Configure your project for authentication with Azure Active Directory

Since the example we're building requires only Office 365 credential authentication, we'll be using [OWIN](http://owin.org/) [Katana](http://katanaproject.codeplex.com/documentation) and [Active Directory Authentication Library](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) (ADAL).

But first, we'll configure the project to use Secure Socket Layers (SSL).

####Enable SSL for your project 

Visual Studio does not configure your project for SSL by default. If you haven't already enabled SSL in your project, you'll want to now, and then update the Office 365 services with the appropriate Redirect URL.

To enable SSL:

1. In **Solution Explorer**, click on the project.
2. In **Properties**, set **SSL Enabled** to **True**.
	
	Visual Studio specifies a value for the **SSL URL**.

Next, we'll want to update the application to use the HTTPS endpoint for the home page:

1.	In **Solution Explorer**, right-click the project, and select **Properties**.
2.	Select the **Web** tab. Under **Servers**, set **Project URL** to the HTTPS endpoint Visual Studio created for the **SSL URL**.

Lastly, we'll update the Office 365 services:

3. In **Solution Explorer**, right-click the project, and select **Add** > **Connected Service**. Sign in if necessary.

	Visual Studio prompts you that one or more Redirect URLs in your project do not exist in your application entry in Azure AD.

4. Click **Yes** to add the secure redirect URL to your application entry in Azure AD.
5. Click **OK** to exit **Services Manager**.


<a name="bk_AuthenticateDownloadNuGets"> </a>
####Manage NuGet packages necessary for authentication

You will need to install the following Azure AD and OWIN Katana packages for authentication:

- [Active Directory Authentication Library](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory)
- [EntityFramework](https://www.nuget.org/packages/EntityFramework)
- [Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)
- [Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)
- [Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect)

These packages may also install selected NuGet packages as dependencies.

To download and install the NuGet packages:

1. In the **Solution Explorer**, right-click the project.
2. Select **Manage NuGet Packages...** 
3. In **Manage NuGet Packages**, click **Online**.
4. Use the Search box to find the necessary package.
5. Select the package and click **Install**.
6. In **Select Projects**, click **OK**.
7. Accept any licenses as prompted.

####Update the web.config file to enable authentication

When you added Office 365 services to your project, Visual Studio added the following properties to your application's registry in Azure AD, and to the **web.config** file in your solution:

    <add key="ida:ClientId" value="app-azure-ad-client-id" />
    <add key="ida:ClientSecret" value="app-azure-ad-password" />
    <add key="ida:TenantId" value="azure-tenant-where-app-is-registered" />
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/" 

<!--
In addition, to successfully authenticate against Azure AD, a single-tenant web application must be able to specify the login authority, including the appropriate tenant ID. The authority follows the pattern

	https://login.windows.net/[tenantId]

where [tenantId] is the ID of the Azure tenant in which the application is registered.

Because of this, you'll need to add the tenant ID to the project's web.config file. You can retrieve the tenant ID for your application from the [Azure Management Portal](https://manage.windowsazure.com).
 

1. Sign into the [Azure Management Portal](https://manage.windowsazure.com/), using your Office 365 subscription credentials.

2. In the left navigation panel, select **Active Directory**. Make sure the **Directory** tab is selected, and then click on the directory name for the Office 365 tenancy is which your app is registered.

	At this point, the URL in the browser window will include a GUID that is the tenant ID of your directory.

3. Copy only the GUID from the browser URL. This is the ID for the tenancy in which your application is registered.

After you have copied the tenant ID, you can add it to the project's web.config file. 

1. In **Solution Explorer**, double-click **Web.config**.
2. In the Web.config file, in the **appSettings** section, add a new key, containing the tenant ID, directly under the ida:AuthorizationUri key:

		<add key="ida:TenantId" value="your-Office-365-tenant-ID"/>

3. Save the file.
-->



####Create a database to manage ADAL authentication tokens

Next, we'll add a database to the project, to act as our ADAL token cache.

For more information about the ADAL token cache, see [The New Token Cache in ADAL v2](http://www.cloudidentity.com/blog/2014/07/09/the-new-token-cache-in-adal-v2/).


To add the database that will act as the ADAL token cache:

1. In **Solution Explorer**, right-click the **App_Data** folder and select **Add** > **New Item...**
2. Make sure **Data** is selected, and then select **SQL Server Database**. Name the database **ADALTokenCacheDb**, and click **Add**.

Make sure the database connection has been added to the project web.config:

1. In **Solution Explorer**, double-click **web.config**.
2. Make sure the following section has been added to the web.config file, after the **appSettings** section. If it's not there, add it:

<connectionStrings>
  <add name="DefaultConnection"
    connectionString="Data Source=(LocalDB)\v11.0;AttachDbFilename=|DataDirectory|\ADALTokenCacheDb.mdf;Integrated Security=True" providerName="System.Data.SqlClient" />
</connectionStrings>

  	<connectionStrings>
    	<add name="DefaultConnection"
         connectionString="Data Source=(LocalDB)\v11.0;AttachDbFilename=|DataDirectory|\ADALTokenCacheDb.mdf;Integrated Security=True" providerName="System.Data.SqlClient" />
  	</connectionStrings>



<ol start="3">
<li>Save the file.</li>
</ol>


####Copy over files needed for authentication

Next, we'll import some files from the [Office 365 single-tenant MVC project](https://github.com/OfficeDev/O365-WebApp-SingleTenant) GitHub project. We'll explain what each file is used for as we go.

To copy files from the GitHub project:

1. In a browser, navigate to the file you want to copy over. (The files are listed below).
2. Right-click the **Raw** button, and select **Save target as...**
3. Save the file to your computer.
4. In Visual Studio, in **Solution Explorer**, under the project node, right-click the specified folder as described below and select **Add** > **Existing Item...**
5. Select the file from where you saved it on your computer. 

Copy the following files into the **Models** folder in the project. These classes demonstrate how a persistent ADAL token cache can be constructed and used to store tokens.

- [ADALTokenCache.cs](https://github.com/OfficeDev/O365-WebApp-SingleTenant/blob/master/O365-WebApp-SingleTenant/Models/ADALTokenCache.cs)
- [ApplicationDbContext.cs](https://github.com/OfficeDev/O365-WebApp-SingleTenant/blob/master/O365-WebApp-SingleTenant/Models/ApplicationDbContext.cs)

Create a new folder, **Utils**.

1. In **Solution Explorer**, right-click your project and select **Add** > **New Folder**.
2. Name the folder **Utils**. 

Copy the following file into it. This helper class contains member variables that read the values from your project's web.config file that you'll need to create the ADAL authentication object during start up. 

- [SettingsHelper.cs](https://github.com/OfficeDev/O365-WebApp-SingleTenant/blob/master/O365-WebApp-SingleTenant/Utils/SettingsHelper.cs)


Finally, copy the  [_LoginPartial.cshtml](https://github.com/OfficeDev/O365-WebApp-SingleTenant/blob/master/O365-WebApp-SingleTenant/Views/Shared/_LoginPartial.cshtml) file into the **Views** > **Shared** folder of your project.


<a name="bk_AuthenticateAzureAD"> </a>
###Authenticate with Azure Active Directory

Now that we have the project configured for authentication, we can actually add the functionality that handles authentication with Azure AD.

####Configure Azure AD single sign-on

Next, we'll need to add an OWIN startup class to the project, to actually handle authentication. To add the OWIN startup class:

1. In Solution Explorer, right-click the project name and select **Add** > **New Item...**
2. In **Add New Item**, under **Web**, select **General**, then select **OWIN Startup class**.
3. For **Name**, enter **Startup**.
3. Click **Add**.

A new start-up class is added to your project. 

Next, we'll add the code that handles authentication:

1. Replace the namespace references in the file with the following:


		using Microsoft.IdentityModel.Clients.ActiveDirectory;
		using Microsoft.Owin.Security;
		using Microsoft.Owin.Security.Cookies;
		using Microsoft.Owin.Security.OpenIdConnect;
		using O365_WebApp_SingleTenant.Models;
		using O365_WebApp_SingleTenant.Utils;
		using Owin;
		using System;
		using System.IdentityModel.Claims;
		using System.Threading.Tasks;
		using System.Web;
		using Microsoft.Owin;



<ol start="2">
<li>Add the following method, ConfigureAuth, to the Startup class.</li>
</ol>

        public void ConfigureAuth(IAppBuilder app)
        {
            app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

            app.UseCookieAuthentication(new CookieAuthenticationOptions());

            app.UseOpenIdConnectAuthentication(
                new OpenIdConnectAuthenticationOptions
                {
                    ClientId = SettingsHelper.ClientId,
                    Authority = SettingsHelper.Authority,

                    Notifications = new OpenIdConnectAuthenticationNotifications()
                    {                       
                        // If there is a code in the OpenID Connect response, redeem it for an access token and refresh token, and store those away.
                        AuthorizationCodeReceived = (context) =>
                        {
                            var code = context.Code;
                            ClientCredential credential = new ClientCredential(SettingsHelper.ClientId, SettingsHelper.AppKey);
                            String signInUserId = context.AuthenticationTicket.Identity.FindFirst(ClaimTypes.NameIdentifier).Value;

                            AuthenticationContext authContext = new AuthenticationContext(SettingsHelper.Authority, new ADALTokenCache(signInUserId));
                            AuthenticationResult result = authContext.AcquireTokenByAuthorizationCode(code, new Uri(HttpContext.Current.Request.Url.GetLeftPart(UriPartial.Path)), credential, SettingsHelper.AADGraphResourceId);

                            return Task.FromResult(0);
                        },
                        RedirectToIdentityProvider = (context) =>
                        {
                            // This ensures that the address used for sign in and sign out is picked up dynamically from the request
                            // this allows you to deploy your app (to Azure Web Sites, for example)without having to change settings
                            // Remember that the base URL of the address used here must be provisioned in Azure AD beforehand.
                            string appBaseUrl = context.Request.Scheme + "://" + context.Request.Host + context.Request.PathBase;
                            context.ProtocolMessage.RedirectUri = appBaseUrl + "/";
                            context.ProtocolMessage.PostLogoutRedirectUri = appBaseUrl;

                            return Task.FromResult(0);
                        },
                        AuthenticationFailed = (context) =>
                        {
                            // Suppress the exception if you don't want to see the error
                            context.HandleResponse();
                            return Task.FromResult(0);
                        }
                    }

                });
        }

<ol start="3">
<li>Add code to the Startup.Configuration method that calls the ConfigureAuth method.</li>
</ol>

        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }


####Add a controller for sign-in and sign-out of Office 365

Add an account controller to handle sign-in and sign-out:

1. In **Solution Explorer**, right-click the **Controllers** folder and select **Add** > **Controller...**
2. Select **MVC 5 Controller - Empty** and click **Add**.
3. For Controller name, enter **AccountController**, and click **Add**.
4. Replace the namespace references in the controller file with the following:


		using Microsoft.IdentityModel.Clients.ActiveDirectory;
		using Microsoft.Owin.Security;
		using Microsoft.Owin.Security.Cookies;
		using Microsoft.Owin.Security.OpenIdConnect;
		using O365_WebApp_SingleTenant.Utils;
		using System.Security.Claims;
		using System.Web;
		using System.Web.Mvc;


<ol start="5">
<li>Delete the Index() method.</li>
<li>Add the following methods to the AccountController class, to handle sign-in and sign-out.</li>
</ol>
 

        public void SignIn()
        {
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        public void SignOut()
        {
            string callbackUrl = Url.Action("SignOutCallback", "Account", routeValues: null, protocol: Request.Url.Scheme);

            HttpContext.GetOwinContext().Authentication.SignOut(
                new AuthenticationProperties { RedirectUri = callbackUrl },
                OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
        }

        public ActionResult SignOutCallback()
        {
            if (Request.IsAuthenticated)
            {
                // Redirect to home page if the user is authenticated.
                return RedirectToAction("Index", "Home");
            }

            return View();
        }

<a name="bk_accessOffice365APIs"> </a>
###Access Office 365 APIs

Now we're ready to add the code that will access the user's Office 365 data.

####Create the model for the contacts information view 

First, we need to create the class on which we will base the Contacts view:

1. In **Solution Explorer**, right-click the **Models** folder and select **Add** > **Class...**
2. Select **Class**, enter **MyContact** as the name, and click **Add**.
3. In the class, add the following line of code.


	    public class MyContact
	    {
	        public string Name { get; set; }
	    }

<ol start="4">
<li>Save the file.</li>
</ol>



####Add a controller for contact information

Next, add a controller for the users' contact information:

1. In **Solution Explorer**, right-click the **Controllers** folder and select **Add** > **Controller...**
2. Select **MVC 5 Controller - Empty** and click **Add**.
3. For Controller name, enter **ContactsController**, and click **Add**.

	Visual Studio adds a new empty controller to the project.

4. Replace the namespace references in the controller file with the following:

		using Microsoft.IdentityModel.Clients.ActiveDirectory;
		using Microsoft.Office365.Discovery;
		using Microsoft.Office365.OutlookServices;
		using O365_WebApp_SingleTenant.Models;
		using O365_WebApp_SingleTenant.Utils;
		using System.Collections.Generic;
		using System.Security.Claims;
		using System.Threading.Tasks;
		using System.Web.Mvc;


	Be sure to add a namespace reference for the Models namespace of your project:


			using [projectname].Models;


<ol start="5">
<li>Add the [Authorize] attribute to the ContactsController class.</li>
</ol>

The [Authorize] attribute requires that the user be authenticated before they can access this controller. 


    	[Authorize]
		public class ContactsController : Controller

<ol start="6">
<li>Change the Index() method to be asynchronous.</li>
</ol> 

		public async Task<ActionResult> Index()

<ol start="7">
<li>Add the following code to the Index() method.</li>
</ol>   

This code creates the authentication context, using the signed-in Office 365 user Id and the authority for your Office 365 tenancy.


            List<MyContact> myContacts = new List<MyContact>();

            var signInUserId = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier).Value;
            var userObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;

            AuthenticationContext authContext = new AuthenticationContext(SettingsHelper.Authority, new ADALTokenCache(signInUserId));

<ol start="8">
<li>Add a <b>try-catch</b> block directly below the above code in the Index() method.</li>
</ol>


            try
            {
 
            }
            catch (AdalException exception)
            {
                //handle token acquisition failure
                if (exception.ErrorCode == AdalError.FailedToAcquireTokenSilently)
                {
                    authContext.TokenCache.Clear();

                    //handle token acquisition failure
                }
            }

            return View(myContacts);

<ol start="9">
<li>In the <b>try</b> block of the above code, add the following code to the Index() method.</li>
</ol>

This code attempts to acquire an access token to the Discovery Service, passing the application's client id and app password, as well the user's credentials. Because the user authentication token has been cached, the controller is able to acquire the necessary access token silently, without having to prompt the user again for their credentials.

With the access token, the application can create a Discovery Service client object, and use the discovery client object to determine the resource endpoint for the Office 365 service Contacts APIs.

                DiscoveryClient discClient = new DiscoveryClient(SettingsHelper.DiscoveryServiceEndpointUri,
                    async () =>
                    {
                        var authResult = await authContext.AcquireTokenSilentAsync(SettingsHelper.DiscoveryServiceResourceId, new ClientCredential(SettingsHelper.ClientId, SettingsHelper.AppKey), new UserIdentifier(userObjectId, UserIdentifierType.UniqueId));

                        return authResult.AccessToken;
                    });

                var dcr = await discClient.DiscoverCapabilityAsync("Contacts");


<ol start="10">
<li>Finally, directly below the above code in the <b>try</b> block, add the following code to the Index() method.</li>
</ol> 


This code contacts the resource endpoint for the Office 365 service Contacts APIs, again silenlty passing the application and user credentials to acquire an access token to the Outlook service.
	
Once the access token is recieved, the code can initialize an Outlook client object. The code then uses the **Me** property of the Outlook client object to retrieve contacts information for this user.	

Lastly, the controller reads through the list of user contacts and returns a view listing their display names.


                OutlookServicesClient exClient = new OutlookServicesClient(dcr.ServiceEndpointUri,
                    async () =>
                    {
                        var authResult = await authContext.AcquireTokenSilentAsync(dcr.ServiceResourceId, new ClientCredential(SettingsHelper.ClientId, SettingsHelper.AppKey), new UserIdentifier(userObjectId, UserIdentifierType.UniqueId));

                        return authResult.AccessToken;
                    });

                var contactsResult = await exClient.Me.Contacts.ExecuteAsync();

                do
                {
                    var contacts = contactsResult.CurrentPage;
                    foreach (var contact in contacts)
                    {
                        myContacts.Add(new MyContact { Name = contact.DisplayName });
                    }

                    contactsResult = await contactsResult.GetNextPageAsync();

                } while (contactsResult != null);

 

The completed Index() method should now read as follows:

        public async Task<ActionResult> Index()
        {
            List<MyContact> myContacts = new List<MyContact>();

            var signInUserId = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier).Value;
            var userObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;

            AuthenticationContext authContext = new AuthenticationContext(SettingsHelper.Authority, new ADALTokenCache(signInUserId));
            
            try
            {
                DiscoveryClient discClient = new DiscoveryClient(SettingsHelper.DiscoveryServiceEndpointUri,
                    async () =>
                    {
                        var authResult = await authContext.AcquireTokenSilentAsync(SettingsHelper.DiscoveryServiceResourceId, new ClientCredential(SettingsHelper.ClientId, SettingsHelper.AppKey), new UserIdentifier(userObjectId, UserIdentifierType.UniqueId));

                        return authResult.AccessToken;
                    });

                var dcr = await discClient.DiscoverCapabilityAsync("Contacts");                

                OutlookServicesClient exClient = new OutlookServicesClient(dcr.ServiceEndpointUri,
                    async () =>
                    {
                        var authResult = await authContext.AcquireTokenSilentAsync(dcr.ServiceResourceId, new ClientCredential(SettingsHelper.ClientId, SettingsHelper.AppKey), new UserIdentifier(userObjectId, UserIdentifierType.UniqueId));

                        return authResult.AccessToken;
                    });

                var contactsResult = await exClient.Me.Contacts.ExecuteAsync();

                do
                {
                    var contacts = contactsResult.CurrentPage;
                    foreach (var contact in contacts)
                    {
                        myContacts.Add(new MyContact { Name = contact.DisplayName });
                    }

                    contactsResult = await contactsResult.GetNextPageAsync();

                } while (contactsResult != null);
            }
            catch (AdalException exception)
            {
                //handle token acquisition failure
                if (exception.ErrorCode == AdalError.FailedToAcquireTokenSilently)
                {
                    authContext.TokenCache.Clear();

                    //handle token acquisition failure
                }
            }

            return View(myContacts);
        }


####Create the view for the Contacts data

Next, we can create the view for the user's contact information. We'll do so by basing the view on the **MyContact** class that we created earlier.

1. In **Solution Explorer**, right-click the **Contacts** folder and select **Add** > **View**.
2. In the **Add View** dialog box, define the new view:
	- For **View name**, enter **Index**. 
	- For **Template**, select **List**. 
	- For **Model class**, select **MyContact**.
	- Click **Add**.



####Add the MyContacts link to the navigation bar

1. In **Solution Explorer**, in the **Shared** folder, double-click the _Layout.cshtml file.

2. Add an action link for the MyContacts page, and inject the partial class for the user log-in. Update the HTML of the navigation bar from what's auto-generated: 

            <div class="navbar-collapse collapse">
                <ul class="nav navbar-nav">
                    <li>@Html.ActionLink("Home", "Index", "Home")</li>
                    <li>@Html.ActionLink("About", "About", "Home")</li>
                    <li>@Html.ActionLink("Contact", "Contact", "Home")</li>
                </ul>
            </div>


		
To the following, to add an action link for the MyContacts page, and inject the partial class for the user log-in:

            <div class="navbar-collapse collapse">
                <ul class="nav navbar-nav">
                    <li>@Html.ActionLink("Home", "Index", "Home")</li>
                    <li>@Html.ActionLink("About", "About", "Home")</li>
                    <li>@Html.ActionLink("Contact", "Contact", "Home")</li>
                    <li>@Html.ActionLink("My Contacts", "Index", "Contacts")</li>
                </ul>
                @Html.Partial("_LoginPartial")
            </div>




###Debug your application


You are now ready to run the solution. Press F5 to debug your web application.

If this is a new development environment, Visual Studio may prompt you to configure IIS SSL certificate. Click **Yes** twice to continue.

1. Visual Studio will launch the web application in the brower you selected in Visual Studio.

2. Click **Sign in**, at the top right corner of the page, and sign in to your Office 365 tenant where you registered your web application.

	Since only your organization users are allowed to sign-in to a single tenant application, there is no need to consent. If your application was multi-tenant, Azure AD would display a consent page listing the permissions the app was requested, so you could consent to giving the app those permissions.


5. Once you're signed in, you should see your email address  and **Sign out** displayed in the navigation bar across the top of the home page.

6. Click on **My Contacts**

	The **My Contacts** page will retrieve and display the names of any Exchange contacts from your tenant.


You now have a web application project that you can customize and integrate Office 365 APIs.

[Next steps](#bk_nextsteps)


<a name="bk_IntegrateWindowsStore"> </a>
##Integrating Office 365 APIs into a Windows Visual Studio Project

For an example of how to integrate the Office 365 APIs into a native client application, such as a Windows Store or Phone app, you can refer to the [Office 365 Windows app project](https://github.com/OfficeDev/O365-Windows) on GitHub. The project retrieves a list of the user's files.

The [AuthenticationHelper.cs](https://github.com/OfficeDev/O365-Windows/blob/master/O365-Windows/O365-Windows/Helpers/AuthenticationHelper.cs)  class contains the code to authenticate and acquire tokens from Azure AD for Office 365 resources. In the sample, we acquire a token for the My Files resource. 

This occurs in the **GetAccessToken** method: in order to acquire tokens, we first query Office 365 Discovery Service to discover the app capabilities. As we configured the app to request My Files permissions, Office 365 discovery service will return My Files capabilityÃ¢â‚¬â„¢s information, such as the Resource Id and Endpoint URI. With these, we then acquire  an access token for the My Files resource.

###Storing Last Tenant Id

As device applications are by default multi-tenant applications, the app initially does not know which user from which tenant is signing into the app until the user successfully signs in and gives the app consent.

Note that multi-tenant applications allow external Office 365 users to sign in and use the application. If the app is published to Windows Store, users can download the app, sign in to their Office 365 tenants and use the application. Azure AD will register the Windows application on behalf of the user in the respective tenant of the signed-in user.

Once the user consents, the app can then get the signed-in usersÃ¢â‚¬â„¢ tenant ID, which it stores in the App settings. The app can then use this tenant ID to initialize the authentication context next time the user opens the app or makes a request. This eliminates the need for the user to consent every time a request is made; they need only consent once, when they first access the app. This is true until the access token expires.


<a name="bk_nextsteps"> </a>
## Next steps

After you've accessed the Office 365 APIs, you can then work with the user resources available through the APIs. For more information and code snippets showing how to perform common tasks using client libraries provided by Visual Studio, see:

- [Outlook Mail API reference](..\api\mail-rest-operations.md)
- [Outlook Calendar API reference](..\api\calendar-rest-operations.md)
- [Outlook Contacts API reference](..\api\contacts-rest-operations.md)
- [Files API reference](..\api\files-rest-operations.md)

<a name="bk_addresources"> </a>
## Additional resources

**Code Samples**

-  [Office 365 APIs starter projects and code samples](..\howto\Starter-projects-and-code-samples.md) 
-  [Office Developer on github](https://github.com/OfficeDev)


**Visual Studio development**

-  [Set up your Office 365 development environment](..\howto\setup-development-environment.md)


-  [Getting started with the Office 365 APIs](http://www.microsoftvirtualacademy.com/training-courses/introduction-to-office-365-development?m=10072&ct=31602): training video 


**Reference**

-  [Office 365 API reference](..\api\API-Catalog.md)




  













<!--
After you've [added an Office 365 service to your project](..\howto\adding-service-to-your-Visual-Studio-project.md), you'll need to write code that authenticates the app user and accesses their Office 365 data. This includes: 



1. [Authenticating with Azure Active Directory](#bk_AuthenticateAzure)
2. [Use the Office 365 Discovery Service to determine resource endpoints](#bk_discoveryContext)
3. [Use endpoints to access Office 365 user data and resources](#bk_accessOffice365resources)



<a name="bk_AuthenticateAzure"> </a>
## Authenticate with Azure Active Directory

The Office 365 APIs use the Active Directory Authentication Library (ADAL) with Azure Active Directory for authentication. Use the [Active Directory Authentication Library](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) (ADAL) to authenticate with Azure Active Directory for Office 365. 


The authentication requirements your code needs to address can vary greatly, depending on:

- Whether the application you're building is a web application or native app
- Whether you want to make your application available to a single or multiple tenants
- Any specific business scenarios your application might be addressing

For detailed examples of how to handle various authentication scenarios, see [Microsoft Azure Active Directory Samples and Documentation](https://github.com/AzureADSamples) on [github](https://github.com). The following examples are especially relevant to Office 365 authentication scenarios:

- [WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
- [WebApp-WebAPI-OpenIDConnect-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-OpenIDConnect-DotNet)
- [WebApp-WebAPI-OAuth2-UserIdentity-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-UserIdentity-DotNet)
- [Client Applications Samples](https://github.com/AzureADSamples?query=windows)

For more information on ADAL, see [Azure AD Authentication Library for .NET](http://msdn.microsoft.com/en-us/library/azure/jj573266.aspx)




<a name="bk_discoveryContext"> </a>
##Use the Office 365 Discovery Service to determine resource endpoints


Many of the endpoints that your application may need to call vary by user, such as the endpoints for the user's files and folders. To obtain the URLs of the desired Office 365 endpoints, it's best practice for your application to call the Office 365 Discovery Service.  Typically, this will be the first Office 365 service that your solution calls. 


For more details about the Office 365 Discovery Service, see [Use the Discovery Service API to find endpoints for your Office 365 app](..\howto\discover-service-endpoints.md) and [Discovery Service REST API operations reference](..\API\Discovery-Service-REST-operations.md).

<a name="bk_accessOffice365resources"> </a>
##Use endpoints to access Office 365 user data and resources

You can then use the endpoints returned by the Office 365 Discovery Service to actually access your user's Office 365 data. You do so by creating the appropriate client object in your code. The type of client object you create depends on the Office 365 API service you access.

- For calendar, contacts, and email, create an Outlook Services client of the appropriate type:
	- Mail: [Get the Outlook Service Mail client](..\howto\common-mail-tasks-client-library.md#GetClient)
	- Calendar: [Get the Outlook Service Calendar client](..\howto\common-calendar-tasks-client-library.md#GetClient)
	- Contacts: [Get the Outlook Service Contacts client](..\howto\common-contacts-tasks-client-library.md#GetClient)


- For SharePoint Online and OneDrive for Business files, create a [SharePoint client object](..\howto\common-file-tasks-client-library.md#GetClient).

- For user information, create an Azure AD client object.

<a name="bk_nextsteps"> </a>
## Next steps

After you've accessed the Office 365 APIs, you can then work with the user resources available through the APIs. For more information and code snippets showing how to perform common tasks in Visual Studio, see:

- [Common mail tasks using an Office 365 client library](..\howto\common-mail-tasks-client-library.md)
- [Common calendar tasks using an Office 365 client library](..\howto\common-calendar-tasks-client-library.md)
- [Common contacts tasks using an Office 365 client library](..\howto\common-contacts-tasks-client-library.md)
- [Common file tasks using an Office 365 client library](..\howto\common-file-tasks-client-library.md)

<a name="bk_addresources"> </a>
## Additional resources

**Code Samples**

-  [Office 365 API starter projects, code samples, and videos](..\howto\Starter-projects-and-code-samples.md) 
-  [Office Developer on GitHub](https://github.com/OfficeDev)


**Visual Studio development**

-  [Set up your Office 365 development environment](..\howto\setup-development-environment.md)


-  [Getting started with the Office 365 APIs](http://www.microsoftvirtualacademy.com/training-courses/introduction-to-office-365-development?m=10072&ct=31602): training video 


**Reference**

-  [Office 365 REST APIs reference](..\api\API-Catalog.md)

-->




    

