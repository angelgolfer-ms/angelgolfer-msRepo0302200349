ms.TocTitle: Create an app with Office 365 APIs
Title: Create an app with Office 365 APIs
Description: Create an example iOS, Android, JavaScript, or ASP.NET app using Office 365 APIs to connect to your customers’ document, email, contacts, or calendar data.
ms.ContentId: 907209f2-ed2a-4c81-b7d1-9b1a5ef497a5
ms.topic: article (how-tos)
ms.date: August 13, 2015

<script src="https://cdn.optimizely.com/js/3043860527.js"></script> 

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]

# Create an app with Office 365 APIs

_**Applies to:** Office 365_

<<<<<<< HEAD
[!INCLUDE [Add the Platform filter bar](../includes/controls/addplatformsfilter.xml)]

The Office 365 APIs are REST services that provide access to Office 365 data, such as: mail, calendars, and contacts from Exchange Online; files and folders from SharePoint Online and OneDrive for Business; users and groups from Azure Active Directory.
=======
[!INCLUDE [Use Microsoft Graph](../includes/use-msgraph-note.txt)]
>>>>>>> staging

The Office 365 APIs are REST services that provide access to Office 365 data, such as: mail, calendars, and contacts from Exchange Online; files and folders from SharePoint Online and OneDrive for Business; users and groups from Azure Active Directory.


[!INCLUDE [BEGIN iOS section](../includes/controls/iossection.xml)]


**Not developing iOS apps?** Use the control in the upper right corner of this page to select the type of app you're developing.


##Create an iOS app with Office 365 APIs

<p class="previewnote">This documentation covers features that are currently in preview. For information about working with preview features, see [Preview developer features on the Office 365 platform](..\howto\platform-development-preview-features-overview.md).</p>


You can create iOS apps that integrate with Office 365 APIs. When creating your iOS app, you can program directly against the [REST APIs](..\API\API-Catalog.md) to interact with Office 365, or you can use the [Office 365 iOS SDK](https://github.com/OfficeDev/Office-365-SDK-for-iOS), which is an object model built on top of the REST APIs to create the app. In this topic, we'll walk you through creating a basic iOS app that uses the Office 365 iOS SDK to retrieve a user's email and display it on their device. The walkthrough is based on the Office 365 Connect sample.

See the following for Office 365 iOS code samples:

- [Office 365 Connect app for iOS](https://github.com/OfficeDev/O365-iOS-Connect#office-365-connect-app-for-ios)

- [Office 365 Code snippets for iOS](https://github.com/OfficeDev/O365-iOS-Snippets)

- [Email Peek - An iOS app built using Office 365](https://github.com/OfficeDev/O365-iOS-EmailPeek/)

**Note** These code samples use the [Office 365 SDK for iOS](https://github.com/OfficeDev/Office-365-SDK-for-iOS) to connect to Office 365.

<a name="bk_prerequisites"> </a>
##Before you start

Before you can create applications that access the Office 365 APIs, you'll need to set up your developer environment. This consists of three one-time tasks to make sure you've got the tools and environment to be successful:

1. Set up the iOS app development environment that you'll be using to create your apps. This includes installing and setting up the [CocoaPods](http://cocoapods.org) environment.

2. Get an Office 365 for business subscription, to access the Office 365 APIs.

3. Associate your Office 365 subscription with Azure Active Directory, so you can create and manage apps.

If you still need to complete any of these steps, take a look at [Set up your Office 365 development environment](..\howto\setup-development-environment.md) for detailed instructions on getting set up.

<a name="bk_createApp"> </a>
##Create your app and add dependencies
For this, you'll create an iOS project and use CocoaPods to add dependencies to the Office 365 SDK for iOS and the [Azure Active Directory Authentication Library (ADAL) for iOS](https://github.com/AzureAD/azure-activedirectory-library-for-objc).

###Create the SimpleMailApp project
1.	Open Xcode
2.	Choose **File > New > Project**.
3.	Select the **Single View Application** template in the ***Applications** section of the **iOS** project templates, and then choose **Next**.
4.	Specify **SimpleMailApp** for the **Product Name**, select **Objective-C** for **Language**, **Universal** for **Devices**, a value for **Organization Identifier**, and then choose **Next**.
5.	Select the location for your project, specify whether it should be under version control, and then choose **Create**.
6.	Once the project has been created, close Xcode. 
 
The Cocoapods commands need to be run from the root of your project folder, so from Terminal, navigate to the project directory. If you did not change the default location when creating the project, the project will be located in the **SimpleMailApp** directory on the **Desktop**.

###Enable Cocoapods for the SimpleMailApp project
1.	Run the following command to initialize the Podfile for your project.

    ```objective-c
		pod init
```

2.	Open the Podfile using the following command.

    ```objective-c
		Open podfile
```

3.	Declare the dependencies for the Office 365 SDK for iOS and the ADAL SDK for iOS by adding the following definitions to the open Podfile.

    ```objective-c
    pod 'ADALiOS', '~> 1.2.0'
    pod 'Office365', '= 0.9.0'
```
    These definitions should between the target and end statements, so the result will look like the following.

    ```objective-c
    target 'SimpleMailApp' do
    pod 'ADALiOS', '~> 1.2.0'
    pod 'Office365', '= 0.9.0'
    end
    ```
     
4.	Close the Podfile.

**Note**  The Office 365 SDK for iOS is currently in developer preview, which means that it is subject to change prior to finalization, possibly even changes that would break code written using the SDK. The SDK uses the [Semantic Versioning](http://semver.org/) convention in which compatibility is specified using a three part version number: major.minor.patch. Until version 1.0 is reached, the minor version number will be incremented for breaking and other significant changes.

###Configure the dependencies for the SimpleMailApp project
To configure these dependencies and add them and the existing project to a new workspace, from Terminal, run the following command.

    pod install

###Register your application with Azure Active Directory
1.	Sign into the [Azure Management Portal](https://manage.windowsazure.com/) using your Office 365 Developer Site credentials.

2.	Click **Active Directory** on the left menu, then click on the directory for your Office 365 developer site. 
    ![Azure Management Portal](images/O365APIs_RegisterApp_1.png)

3.	On the top menu, click **Applications**.

4.	Click **Add** from the bottom menu.  
	![Azure Management Portal Add Application](images/O365APIs_RegisterApp_2.png)

5.	On the **What do you want to do** page, click **Add an application my organization is developing**.

6.	On the **Tell us about your application** page, specify **SimpleMailApp** for the application name and select **NATIVE CLIENT APPLICATION** for **Type**.

7.	Click the arrow icon on the bottom-right corner of the page.

8.	On the **Application information** page, specify a Redirect URI, for this example, you can specify `http://localhost/simplemailappproject`. Make note of the URI, since you'll need this later when coding the SimpleMailApp project. Click the checkbox in the bottom right corner of the page.

9.	Once the application has been successfully added, you will be taken to the Quick Start page for the application. From here, click **Configure** in the top menu.

10.	In **permissions to other applications**, click **Add application**.

11.	Click **Office 365 Exchange Online**, and then click the check mark icon.
    ![Azure Management Portal Add Application](images/O365APIs_RegisterApp_5.png)

12.	Under **permissions to other applications**, click the **Delegated Permissions** column for **Office 365 Exchange Online**, and select **Send mail as a user**.  
    ![Azure Management Portal Add Application](images/O365APIs_RegisterApp_6.png)

    These are the permissions that will be displayed to your app user when Azure prompts them to consent to your app's permission request. In general, request only the services your app actually requires, and specify the least level of permissions in each service that still enable your app to perform its functions.

13.	Copy the value specified for **Client ID**; you will need this later when coding the SimpleMailApp project.

14.	Click **Save** in the bottom menu.

<a name="bk_codeYourApp"></a>
## Code your app 
Open the **SimpleMailApp** workspace in Xcode. 

###Authenticate with Azure AD and get the access token
An access token is required to access Office 365 APIs, so your application needs to implement the logic to retrieve and manage access tokens. The [Azure Active Directory authentication library (ADAL) for iOS and OSX](https://github.com/AzureAD/azure-activedirectory-library-for-objc) provides you with the ability to manage authentication in your application with just a few lines of code. Learn more about authentication with Azure Active Directory in [What is Azure Active Directory?](https://azure.microsoft.com/en-us/documentation/articles/active-directory-whatis/) on Azure.com. The first thing you'll do is create a header file and class, AuthenticationManager that uses the ADAL for iOS and OSX to manage authentication for your app.

####To create the AuthenticationManager class
1. Right-click the SimpleMailApp project folder, select **New File**, and in the **iOS** section, click **Cocoa Touch Class**, and then click **Next**.

2. Specify **AuthenticationManager** as the **Class**, **NSObject** for **Subclass of:**, and then click **Next**.

3. Click **Create** to create the class and header files.

####To code the AuthenticationManager header file

1. Import the necessary Office 365 iOS SDK and ADAL SDK header files by adding the following code directives to AuthenticationManager.h.

    ```objective-c
#import <Foundation/Foundation.h>
#import <ADALiOS/ADAuthenticationContext.h>
#import <ADALiOS/ADAuthenticationSettings.h>
#import <ADALiOS/ADLogger.h>
#import <ADALiOS/ADInstanceDiscovery.h>
#import <office365_odata_base/office365_odata_base.h>
```

6. Declare a property for the **ADALDependencyResolver** object from the ADAL SDK which uses dependency injection to provide access to the authentication objects.

    ```objective-c
@property (readonly, nonatomic) ADALDependencyResolver *dependencyResolver;
```

7. Specify the **AuthenticationManager** class as a singleton.

    ```objective-c
+(AuthenticationManager *)sharedInstance;
```

8. Declare the methods for retrieving and clearing the access and refresh tokens.

    ```objective-c
//retrieve token
-(void)acquireAuthTokenWithResourceId:(NSString *)resourceId completionHandler:(void (^)(BOOL authenticated))completionBlock;
//clear token
-(void)clearCredentials;
```

####To code the AuthenticationManager class

1. Above the **@implementation** declaration, declare static variables for the redirect URI, client ID and the authority.

    ```objective-c
static NSString * const REDIRECT_URL_STRING = @"redirectUri";
static NSString * const CLIENT_ID           = @"clientID";
static NSString * const AUTHORITY           = @"https://login.microsoftonline.com/common";
```

    Replace the *redirectUri* with the value you copied from step 8 when registering your app with Azure AD, and the *clientID* with the value you specified in step 13 of the same procedure.

2. In the ***interface** declaration, above **@implementation**, declare the following properties.

    ```objective-c
@interface AuthenticationManager ()
@property (strong,    nonatomic) ADAuthenticationContext *authContext;
@property (readwrite, nonatomic) ADALDependencyResolver  *dependencyResolver;
@property (readonly, nonatomic) NSURL    *redirectURL;
@property (readonly, nonatomic) NSString *authority;
@property (readonly, nonatomic) NSString *clientId;
@end
```
3. Add code for the constructor to the implementation. 

	```objective-c
-(instancetype)init
{
    self = [super init];
    if (self) {
        // These are settings that you need to set based on your
        // client registration in Azure AD.
        _redirectURL = [NSURL URLWithString:REDIRECT_URL_STRING];
        _authority = AUTHORITY;
        _clientId = CLIENT_ID;
    }
    return self;
}
```

4. Add the following code to use a single authentication manager for the application.

	```objective-c
+(AuthenticationManager *)sharedInstance
{
    static AuthenticationManager *sharedInstance;
    static dispatch_once_t onceToken;
 
    // Initialize the AuthenticationManager only once.
    dispatch_once(&onceToken, ^{
        sharedInstance = [[AuthenticationManager alloc] init];
    });
 
    return sharedInstance;
}
```
5. Acquire access and refresh tokens from Azure AD for the user.

    ```objective-c
-(void)acquireAuthTokenWithResourceId:(NSString *)resourceId completionHandler:(void (^)(BOOL authenticated))completionBlock
{
        ADAuthenticationError *error;
    self.authContext = [ADAuthenticationContext authenticationContextWithAuthority:self.authority error:&error];
[self.authContext acquireTokenWithResource:resourceId
                                      clientId:self.clientId
                                   redirectUri:self.redirectURL
                               completionBlock:^(ADAuthenticationResult *result) {
                                   if (AD_SUCCEEDED != result.status) {
                                       completionBlock(NO);
                                   }
                                   else {
                                       NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults];
                                       [userDefaults setObject:result.tokenCacheStoreItem.userInformation.userId
                                                        forKey:@"LogInUser"];
                                       [userDefaults synchronize];
                                       self.dependencyResolver = [[ADALDependencyResolver alloc] initWithContext:self.authContext
                                                                                                      resourceId:resourceId
                                                                                                        clientId:self.clientId
                                                                                                     redirectUri:self.redirectURL];
                                       completionBlock(YES);
                                   }
                               }];
}
```

    The first time the application runs, a request is sent to the URL specified for the AUTHORITY const (see step 1), which the redirects you to a login page where you can enter your credentials. If your login is successful, the response contains the access and refresh tokens. Subsequent times when the application runs, the authentication manager will use the access or refresh token for authenticating client requests, unless the token cache is cleared.

6. Finally, add code to log out the user by clearing the token cache and removing the application's cookies.

    ```objective-c
-(void)clearCredentials{
    id<ADTokenCacheStoring> cache = [ADAuthenticationSettings sharedInstance].defaultTokenCacheStore;
    ADAuthenticationError *error;
 
       if ([[cache allItemsWithError:&error] count] > 0)
        [cache removeAllWithError:&error];
        NSHTTPCookieStorage *cookieStore = [NSHTTPCookieStorage sharedHTTPCookieStorage];
    for (NSHTTPCookie *cookie in cookieStore.cookies) {
        [cookieStore deleteCookie:cookie];
    }
}
```

###Connect to Office 365
Next you need to add class to your project to connect to Office 365, and use the Discovery service to retrieve the Exchange service endpoints.

####To create the Office365ClientFetcher class and header files
1. Right-click the SimpleMailApp project folder, , select **New File**, and in the **iOS** section, click **Cocoa Touch Class**, and then click **Next**.

2. Specify **Office365ClientFetcher** as the **Class**, **NSObject** for **Subclass of:**, and then click **Next**.

3. Click **Create** to create the class and header files.

####To code the Office365ClientFetcher header file
1. Import the necessary Office 365 iOS SDK header files by adding the following code directives to Office365ClientFetcher.h.

    ```objective-c
#import <Foundation/Foundation.h>
#import <office365_odata_base/office365_odata_base.h>
#import <office365_exchange_sdk/office365_exchange_sdk.h>
#import "MSDiscoveryClient.h"
#import <MSOutlookServicesClient.h>
```

2. Declare the methods for fetching the Outlook and Discovery service clients.

    ```objective-c
-(void)fetchOutlookClient:(void (^)(MSOutlookServicesClient *outlookClient))callback;
-(void)fetchDiscoveryClient:(void (^)(MSDiscoveryClient *discoveryClient))callback;
```

####To code the Office365ClientFetcher class

1. Import the Office365ClientFetcher and AuthenticationManager header files.

	```objective-c
#import "Office365ClientFetcher.h"
#import "AuthenticationManager.h"
```

5. Add the implementation code to the Office365ClientFetcher class.

	```objective-c
-(void)fetchOutlookClient:(void (^)(MSOutlookServicesClient *outlookClient))callback
{
    // Get an instance of the authentication controller.
    AuthenticationManager *authenticationManager = [AuthenticationManager sharedInstance];
    [authenticationManager acquireAuthTokenWithResourceId:@"https://outlook.office365.com/"
                                           completionHandler:^(BOOL authenticated) {
        if(authenticated){
            NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults];
            NSDictionary *serviceEndpoints = [userDefaults objectForKey:@"O365ServiceEndpoints"];
            // Gets the MSOutlookServicesClient with the URL for the Mail service.
            callback([[MSOutlookServicesClient alloc] initWithUrl:serviceEndpoints[@"Mail"]
                                       dependencyResolver:authenticationManager.dependencyResolver]);
        }
        else{
            //Display an alert in case of an error
            dispatch_async(dispatch_get_main_queue(), ^{
                NSLog(@"Error in the authentication");
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Error"
                                                                message:@"Authentication failed. Check the log for errors."
                                                               delegate:self
                                                      cancelButtonTitle:@"OK"
                                                      otherButtonTitles:nil];
                [alert show];
            });
        }
    }];
}
-(void)fetchDiscoveryClient:(void (^)(MSDiscoveryClient *discoveryClient))callback
{
    AuthenticationManager *authenticationManager = [AuthenticationManager sharedInstance];
    [authenticationManager acquireAuthTokenWithResourceId:@"https://api.office.com/discovery/"
                                        completionHandler:^(BOOL authenticated) {
        if (authenticated) {
            callback([[MSDiscoveryClient alloc] initWithUrl:@"https://api.office.com/discovery/v1.0/me/"
                                         dependencyResolver:authenticationManager.dependencyResolver]);
        }
        else {
            dispatch_async(dispatch_get_main_queue(), ^{
                NSLog(@"Error in the authentication");
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Error"
                                                                message:@"Authentication failed. This may be because the Internet connection is offline  or perhaps the credentials are incorrect. Check the log for errors and try again."
                                                               delegate:self
                                                      cancelButtonTitle:@"OK"
                                                      otherButtonTitles:nil];
                [alert show];
            });
        }
    }];
}
```

###The View Controller
Next you  need to call the methods to connect to the Office 365 services, triggering authentication, and then display the results in the UI. Here you're going to create a View Controller class containing UI controls using the same names as the View Controller and UI controls in the Office 365 iOS Connect sample. This enables you to download and use the storyboard from the Connect sample, allowing you to skip the steps normally required to connect the storyboard to a View Controller.

####To add the View Controller
1. Right-click the SimpleMailApp project, , select **New File**, and in the **iOS** section, click **Cocoa Touch Class**, and then click **Next**.

2. Select **UIViewController** for **Subclass of:**, and specify **SendMailViewController** as the **Class** and then click **Next**.

3. Click **Create** to create the class and header files. 

####To code the View Controller
To start, import the necessary header files by adding the following code directives to SendMailViewController.m.

```objective-c
#import "SendMailViewController.h"
#import "Office365ClientFetcher.h"
#import "AuthenticationManager.h"
#import "MSDiscoveryServiceInfoCollectionFetcher.h"
```

Next, declare the following properties and methods in the **SendMailViewController** interface.

```objective-c
@interface SendMailViewController ()

@property (weak, nonatomic) IBOutlet UILabel *headerLabel;
@property (weak, nonatomic) IBOutlet UITextView *mainContentTextView;
@property (weak, nonatomic) IBOutlet UITextView *statusTextView;
@property (weak, nonatomic) IBOutlet UITextField *emailTextField;
@property (weak, nonatomic) IBOutlet UIBarButtonItem *disconnectBarButtonItem;
@property (weak, nonatomic) IBOutlet UIButton *sendMailButton;
@property (weak, nonatomic) IBOutlet UIActivityIndicatorView *activityIndicator;

@property (strong, nonatomic) Office365ClientFetcher *baseController;
@property (strong, nonatomic) NSMutableDictionary *serviceEndpointLookup;

-(IBAction)sendMailTapped:(id)sender;
-(IBAction)disconnectTapped:(id)sender;

@end
```

Now add the following code for the **SendMailViewController** implementation.

```objective-c
@implementation SendMailViewController

#pragma mark - Properties
-(Office365ClientFetcher *)baseController
{
    if (!_baseController) {
        _baseController = [[Office365ClientFetcher alloc] init];
    }

    return _baseController;
}

#pragma mark - Lifecycle Methods
- (void)viewDidLoad
{
    [super viewDidLoad];

    self.disconnectBarButtonItem.enabled = NO;
    self.sendMailButton.hidden = YES;
    self.emailTextField.hidden = YES;
    self.mainContentTextView.hidden = YES;
    self.headerLabel.hidden = YES;

    [self connectToOffice365];
}

#pragma mark - IBActions
//Send a mail message when the Send button is clicked
-(IBAction)sendMailTapped:(id)sender
{
    [self sendMailMessage];
}

// Clear the token cache and update the UI when the Disconnect button is tapped
-(IBAction)disconnectTapped:(id)sender
{
    self.disconnectBarButtonItem.enabled = NO;
    self.sendMailButton.hidden = YES;
    self.mainContentTextView.text = @"You're no longer connected to Office 365.";
    self.headerLabel.hidden = YES;
    self.emailTextField.hidden = YES;
    self.statusTextView.hidden = YES;

    // Clear the access and refresh tokens from the credential cache. You need to clear cookies
    // since ADAL uses information stored in the cookies to get a new access token.
    AuthenticationManager *authenticationManager = [AuthenticationManager sharedInstance];
    [authenticationManager clearCredentials];
}

#pragma mark - Helper Methods
-(void)connectToOffice365
{
    [self.baseController fetchDiscoveryClient:^(MSDiscoveryClient *discoveryClient) {
        MSDiscoveryServiceInfoCollectionFetcher *servicesInfoFetcher = [discoveryClient getservices];

        // Call the Discovery Service and get back an array of service endpoint information
        NSURLSessionTask *servicesTask = [servicesInfoFetcher readWithCallback:^(NSArray *serviceEndpoints, MSODataException *error) {
            if (serviceEndpoints) {

                self.serviceEndpointLookup = [[NSMutableDictionary alloc] init];

                for(MSDiscoveryServiceInfo *serviceEndpoint in serviceEndpoints) {
                    self.serviceEndpointLookup[serviceEndpoint.capability] = serviceEndpoint.serviceEndpointUri;
                }

                // Keep track of the service endpoints in the user defaults
                NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults];

                [userDefaults setObject:self.serviceEndpointLookup
                                 forKey:@"O365ServiceEndpoints"];

                [userDefaults synchronize];

                dispatch_async(dispatch_get_main_queue(), ^{
                   
                    NSString *userEmail = [userDefaults stringForKey:@"LogInUser"];
                    NSArray *parts = [userEmail componentsSeparatedByString: @"@"];

                    self.headerLabel.text = [NSString stringWithFormat:@"Hi %@!", parts[0]];
                    self.headerLabel.hidden = NO;
                    self.mainContentTextView.hidden = NO;
                    self.emailTextField.text = userEmail;
                    self.statusTextView.text = @"";
                    self.disconnectBarButtonItem.enabled = YES;
                    self.sendMailButton.hidden = NO;
                    self.emailTextField.hidden = NO;
                });
            }
            else {
                dispatch_async(dispatch_get_main_queue(), ^{
                    NSLog(@"Error in the authentication: %@", error);

                    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Error"
                                                                    message:@"Authentication failed. This may be because the Internet connection is offline  or perhaps the credentials are incorrect. Check the log for errors and try again."
                                                                   delegate:nil
                                                          cancelButtonTitle:@"OK"
                                                          otherButtonTitles:nil];
                    [alert show];
                });
            }
        }];
        
        [servicesTask resume];
    }];
}

-(void)sendMailMessage
{
    MSOutlookServicesMessage *message = [self buildMessage];

    [self.baseController fetchOutlookClient:^(MSOutlookServicesClient *outlookClient) {
        dispatch_async(dispatch_get_main_queue(), ^{
            // Show the activity indicator
            [self.activityIndicator startAnimating];
        });

        MSOutlookServicesUserFetcher *userFetcher = [outlookClient getMe];
        MSOutlookServicesUserOperations *userOperations = [userFetcher operations];

        // Send the mail message. This results in a call to the service.
        NSURLSessionTask *task = [userOperations sendMailWithMessage:message
                                                     saveToSentItems:YES
                                                            callback:^(int returnValue, MSODataException *error) {
            NSString *statusText;

            if (error == nil) {
                statusText = @"Check your inbox, you have a new message. :)";
            }
            else {
                statusText = @"The email could not be sent. Check the log for errors.";
                NSLog(@"%@",[error localizedDescription]);
            }

            // Update the UI.
            dispatch_async(dispatch_get_main_queue(), ^{
                self.statusTextView.text = statusText;
                [self.activityIndicator stopAnimating];
            });
        }];

        [task resume];
    }];
}

//Compose the mail message
-(MSOutlookServicesMessage *)buildMessage
{
    // Create a new message. Set properties on the message.
    MSOutlookServicesMessage *message = [[MSOutlookServicesMessage alloc] init];
    message.Subject = @"Welcome to Office 365 development on iOS with the Office 365 Connect sample";

    // Get the recipient's email address.
    // See the helper method getRecipients to understand the usage.
    NSString *toEmail = self.emailTextField.text;

    MSOutlookServicesRecipient *recipient = [[MSOutlookServicesRecipient alloc] init];

    recipient.EmailAddress = [[MSOutlookServicesEmailAddress alloc] init];
    recipient.EmailAddress.Address = [toEmail stringByTrimmingCharactersInSet:[NSCharacterSet whitespaceCharacterSet]];

    message.ToRecipients = (NSMutableArray<MSOutlookServicesRecipient> *)[[NSMutableArray alloc] initWithObjects:recipient, nil];

    // Get the email text and put in the email body.
    NSString *filePath = [[NSBundle mainBundle] pathForResource:@"EmailBody" ofType:@"html" ];
    NSString *body = [NSString stringWithContentsOfFile:filePath encoding:NSUTF8StringEncoding error:nil];
    message.Body = [[MSOutlookServicesItemBody alloc] init];
    message.Body.ContentType = MSOutlookServices_BodyType_HTML;
    message.Body.Content = body;

    return message;
}

@end
```
####Main.storyboard
Since the View Controller you've created is named the same as the one in the [Office 365 iOS Connect sample](https://github.com/OfficeDev/O365-iOS-Connect), with the code specifying controls with the same names as the ones in the sample, you can use the sample's storyboard. To get the storyboard, [download](https://github.com/OfficeDev/O365-iOS-Connect/archive/master.zip) the sample, locate the **Main.storyboard** file in the O365-iOS-Connect-master\Sample\O365-iOS-Connect\Base.lproj folder of the download.

Copy this file to the SimpleMailApp\SimpleMailApp\Base.lproj folder in your project, overwriting the existing version of the file in that location.

###Email source
The final step is to create an HTML file that the sample uses to construct the body of the email. Add an HTML file to your project and name it EmailBody.html. You can customize it however you want, or use the following code for a basic test.

```html
<html>
    <body>
        <p>Sent from SimpleMailApp iOS sample</p>
    </body>
</html>
```

<a name="bk_test" />
##Testing the app
Build and run the application from Xcode. This launches the iOS Simulator, and you'll see a **Connect to Office 365** link. Click it, and you will be prompted to enter your credentials. Once you have successfully logged in, you will see a textbox with the email address for the account you logged in as and a **Send** link. Click **Send** to send an email message to the address specified in the textbox.

<a name="bk_nextsteps"> </a>
## Next steps

Now that you've built an app that uses the Mail API, you can explore the other Office 365 REST APIs available for use in your apps.

- [Office 365 API reference](..\api\api-catalog.md)

<a name="bk_addresources"> </a>
## Additional resources

- [Office 365 iOS SDK](https://github.com/OfficeDev/Office-365-SDK-for-iOS)
- [Set up your Office 365 development environment](..\howto\setup-development-environment.md)
- [Office 365 Connect app for iOS](https://github.com/OfficeDev/O365-iOS-Connect)
- [Office 365 code snippets for iOS](https://github.com/OfficeDev/O365-iOS-Snippets)





[!INCLUDE [END iOS section](../includes/controls/iossection.xml)]

[!INCLUDE [BEGIN Android section](../includes/controls/androidsection.xml)]

**Not developing Android apps?** Use the control in the upper right corner of this page to select the type of app you're developing.

## Create an Android app with Office 365 APIs

To give you a taste of what you can do with the Office 365 REST APIs, this topic shows you how to create a simple application that gets information from an Exchange Online server.

![A screenshot of the app running in an emulator window. The available actions are shown on buttons.](images\O365APIs_RunningApp1-50Percent.png)

Before you can start work on your first Office 365 application, there are a few one-time tasks that you need to take care of, plus you'll need to be sure that you have your tools. After that you can get started on your first app.

<a name="bk_setup"></a>
##Before you start

Before you can create applications that access the Office 365 APIs, you'll need to set up your developer environment. This consists of three one-time tasks to make sure you've got the tools and environment to be successful:

1. Set up the Android app development environment that you'll be using to create your apps.
1. Get an Office 365 for business subscription, to access the Office 365 APIs.
1. Associate your Office 365 subscription with Azure AD, so you can create and manage apps.

<<<<<<< HEAD
If you still need to complete any of these steps, take a look at <a href="setup-development-environment?android">Set up your Office 365 development environment</a> for detailed instructions on getting set up.
=======
If you still need to complete any of these steps, take a look at [Set up your Office 365 development environment](..\howto\setup-development-environment.md) for detailed instructions on getting set up.
>>>>>>> staging

<a name="bk_createApp"></a>
##Create your app and add dependencies
In this step, you'll create an app and add the Office 365 SDK for Android and Azure Active Directory Authentication Library for Android to the project. Source for both of these libraries is available from GitHub, and you can download the binaries for the Office 365 SDK from [Bintray](https://bintray.com/msopentech/Maven/Office-365-SDK-for-Android/view), if you prefer.

<a name="bk_dependenciesForStudio"></a>
###Add dependencies for Android Studio

You can use Android Studio's built-in support for Gradle to manage the dependencies for your application. To add the dependencies to your application:

1. Create a new Android application in Android Studio.
1. Locate `app/build.gradle` in your app module and add the following dependencies. We'll use only "outlook-services", however, they're all listed here for reference.

```no-highlight
dependencies {
    // base OData library:
    compile group: 'com.microsoft.services', name: 'odata-engine-core', version: '+'
    compile group: 'com.microsoft.services', name: 'odata-engine-android-impl', version: '+', ext:'aar'

    // choose the discovery and outlook services
    compile group: 'com.microsoft.services', name: 'discovery-services', version: '+'
    compile group: 'com.microsoft.services', name: 'outlook-services', version: '+'

    // Azure Active Directory Authentication Library
    compile group: 'com.microsoft.aad', name: 'adal', version: '+'
    }
```

<a name="bk_dependenciesForEclipse"></a>
###Add dependencies for Eclipse

If you use Eclipse, you'll need to do a little more work by hand to add the Azure Active Directory Authentication Library for Android and Office 365 SDK libraries to your workspace. To add the dependencies to your workspace: 

1. Download or clone the
   [Azure Active Directory Authentication Library](https://github.com/AzureAD/azure-activedirectory-library-for-android).

1. Start Eclipse and create a new workspace for your app.

1. Import the AuthenticationActivity project from the Azure Active Directory Authentication Library into your new workspace.

1. Add the Android support library to the AuthenticationActivity project. To do this, right-click the project, choose **Android Tools**, and then **Add Support Library**.

1.  Download the latest version of the [gson library](https://code.google.com/p/google-gson/).

1. Add the gson jar file to the libs folder of the AuthenticationActivity project.

1. Add the jar files from the Office 365 SDK for Android. Either download the jar files from Bintray, or clone and build the Office 365 SDK for Android, and then copy the jar files to your project.

	**To download the jar files:**

   Download the jar files for the [Office 365 SDK for Android](https://github.com/OfficeDev/Office-365-SDK-for-Android) from [Bintray](https://bintray.com/msopentech/Maven/Office-365-SDK-for-Android/view). You need to add the following jar files to the libs folder:
    * odata-engine-android-impl-0.11.1jar
    * outlook-services-0.11.1.jar
    * file-services-0.11.1.jar
    * discovery-services-0.11.1.jar
	<br />**Note** You can use version 0.11.1 or later of the jars.
	
	**To build the jar files:**
	
	1. Clone the [Office 365 SDK for Android](https://github.com/OfficeDev/Office-365-SDK-for-Android).
	2. Go to the sdk directory.
	3. Run `.\gradlew clean`.
	4. Run `.\gradlew assemble`.

###Update the manifest
You'll need to add two permissions to your **AndroidManifest.xml** file so that your application can access Azure AD and Office 365.

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

###Integrate Office 365 services
Before you start writing the code for your Office 365 application, you have to do a little work to register your application with Azure AD and to set permissions for your application to access Office 365 services. You need to do this only once for each application.

<a name="bk_register"></a>
####Register your app with Azure AD
1. Sign into the [Azure Management Portal](https://manage.windowsazure.com/), using your Office 365 Developer Site credentials.

1. Click **Active Directory** on the left menu, then click on the directory for your Office 365 Developer Site.

    ![A screenshot of the Azure Management Portal website. The item 'Active Directory' is selected in the left navigation pane. In the main pane, the Directory tab is selected. The name of the current directory is highlighted.](images\O365APIs_RegisterApp_1.png)

1. On the top menu, select **Applications**.

1. Click **Add** in the bottom menu.

	![A screenshot of the directory information page. In the menu bar at the bottom of the page, the New icon is highlighted.](images\O365APIs_RegisterApp_2.png)
1. On the **What do you want to do** page, click **Add an application my organization is developing**.

1. On the **Tell us about your application** page, give your application a name and select **NATIVE CLIENT APPLICATION** for **Type**.

1. Click the arrow icon on the bottom-right corner of the page.

1. On the **Application information** page, specify a Redirect URI. For this example, you can specify **http://localhost/simplemailapp** and then click the checkbox in the bottom-right corner of the page.

1. Once the application has been successfully added, the Quick Start page for the application is displayed. 

Your app is now registered with Azure AD, and has been assigned a client ID. You'll need this information later [when you set up your application](#bk_context). However, there are several important aspects of your app left to configure.	

####Add Office 365 services and set permissions

Next, you'll need to specify exactly what permissions your app requires of the Office 365 APIs. To do so, you add access to the Office 365 service containing the API you require to your app, and then specify the permissions you need from the APIs in that service. The example application needs to read the users' Inbox, so set up the required permission as follows.

1. In the Azure Management Portal, on the configuration page for your app, scroll to the bottom of the page and, under **permissions to other applications**, select **Add application**.
 
	![A screenshot of the app configuration page for your app, on the Azure Management Portal website. Under the page section titled 'permission to other applications', the 'add application' button is highlighted.](images\O365APIs_RegisterApp_4.png)

1. Select the **Office 365 Exchange Online** service.
	
	1. Select the service name, and click the plus symbol to add the service. 
	1. The service is then listed under the **Selected** column. 
	1. Click the check mark icon to save your choices.
	![A screenshot of the 'permissions to other applications' page. The available applications are listed in a table. Next to the name of each is the plus icon. At the far right is a column that lists the applications you have added to your app. A check mark icon at the bottom of the page is highlighted.](images\O365APIs_RegisterApp_5.png)

	You are returned to your app's configuration page.

1. Under **permissions to other applications**, click the **Delegated Permissions** column for **Office 365 Exchange Online**, and specify the **Read users' mail** permission.

	![A screenshot of the app configuration page for your app, on the Azure Management Portal website. Under the page section titled 'permission to other applications', the application you have just added are listed in a table. Next to the name of each application is a column titled 'Delegated permissions'. This column displays a drop-down menu of the permissions you can request for your app from each application you added.](images\GetStarted_DelegatedPermissions.png)

	These are the permissions that will be displayed to your app user when Azure prompts them to consent to your app's permission request. In general, request only the services your app actually requires, and specify the least level of permissions in each service that still enable your app to perform its functions.

<a name="bk_codeYourApp"></a>
## Code your app
The following code sample is a simple application that uses all of the Azure AD and Office 365 functions that you need to create an Android application. 

###Connect to Office 365
Before you can call an Office 365 service, you must authenticate your application with Azure AD. Learn more about authentication with Azure Active Directory in [What is Azure Active Directory?](https://azure.microsoft.com/en-us/documentation/articles/active-directory-whatis/) on Azure.com.

The following code defines an **AuthenticationController** object that uses two objects from the Azure Active Directory Authentication Library to manage authenticating your application. 

The first, **ADALDependencyResolver**, uses dependency injection to provide the rest of your application access to the **AuthenticationController** object. The second, **AuthenticationContext** manages authentication with Azure AD. It does the following:

1. Presents an authentication UI to the user the first time that the user logs into Office 365.

2. Stores the access token for the application so that service clients can access the tokens.

3. Refreshes the access token as needed. If necessary, it will present the authentication UI again.

When you run the application, information about the token in sent to the application log. This information would normally be used within an application instead of being displayed. 

    package com.microsoft.office365.auth_discover_snack;

    import android.app.Activity;
    import android.util.Log;

    import com.google.common.util.concurrent.SettableFuture;
    import com.microsoft.aad.adal.AuthenticationCallback;
    import com.microsoft.aad.adal.AuthenticationContext;
    import com.microsoft.aad.adal.AuthenticationResult.AuthenticationStatus;
    import com.microsoft.aad.adal.PromptBehavior;
    import com.microsoft.services.odata.impl.ADALDependencyResolver;
    import com.microsoft.services.odata.interfaces.DependencyResolver;

    public class AuthenticationController {
        private AuthenticationContext authContext;
        private ADALDependencyResolver dependencyResolver;
        private Activity contextActivity;
        private String resourceId;

        public static synchronized AuthenticationController getInstance() {
            if (INSTANCE == null) {
                INSTANCE = new AuthenticationController();
            }
            return INSTANCE;
        }
        private static AuthenticationController INSTANCE;

    private AuthenticationController() {
        resourceId = Constants.DISCOVERY_RESOURCE_ID;
    }

    public void setContextActivity(final Activity contextActivity) {
        this.contextActivity = contextActivity;
    }

    public void setResourceId(final String resourceId) {
        this.resourceId = resourceId;
        this.dependencyResolver.setResourceId(resourceId);
    }

    public SettableFuture<Boolean> initialize() {

        final SettableFuture<Boolean> result = SettableFuture.create();

        if (verifyAuthenticationContext()) {
            getAuthenticationContext().acquireToken(
                    this.contextActivity,
                    this.resourceId,
                    Constants.CLIENT_ID,
                    Constants.REDIRECT_URI,
                    PromptBehavior.Auto,
                    new AuthenticationCallback<AuthenticationResult>() {

                        @Override
                        public void onSuccess(final AuthenticationResult authenticationResult) {
                            if (authenticationResult != null && authenticationResult.getStatus() == AuthenticationStatus.Succeeded) {
                                dependencyResolver = new ADALDependencyResolver(
                                        getAuthenticationContext(),
                                        resourceId,
                                        Constants.CLIENT_ID);
                                Log.i("AuthenticationController", "initialize - Token acquired\n" +
                                                "    Token info:\n" +
                                                "      TenantId - " + authenticationResult.getTenantId() + "\n" +
                                                "      AccessToken - " + authenticationResult.getAccessToken() + "\n" +
                                                "      AccessTokenType - " + authenticationResult.getAccessTokenType() + "\n" +
                                                "      RefreshToken - " + authenticationResult.getRefreshToken() + "\n" +
                                                "      ExpiresOn - " + authenticationResult.getExpiresOn() + "\n" +
                                                "      IsMultiResourceRefreshToken - " + authenticationResult.getIsMultiResourceRefreshToken() + "\n" +
                                                "      IdToken - " + authenticationResult.getIdToken() + "\n" +
                                                "    User info:\n" +
                                                "      DisplayableId - " + authenticationResult.getUserInfo().getDisplayableId() + "\n" +
                                                "      UserId - " + authenticationResult.getUserInfo().getUserId() + "\n" +
                                                "      FamilyName - " + authenticationResult.getUserInfo().getFamilyName() + "\n" +
                                                "      GivenName - " + authenticationResult.getUserInfo().getGivenName()
                                );
                                result.set(true);
                            }
                        }

                        @Override
                        public void onError(Exception t) {
                            Log.e("AuthenticationController", "initialize - " + t.getMessage());
                            result.setException(t);
                        }
                    }
            );
        } else {
            result.setException(new Throwable("Auth context verification failed. Did you set a context activity?"));
        }
        return result;
    }

    public AuthenticationContext getAuthenticationContext() {
        if (authContext == null) {
            try {
                authContext = new AuthenticationContext(this.contextActivity, Constants.AUTHORITY_URL, false);
            } catch (Throwable t) {
                Log.e("AuthenticationController", "getAuthenticationContext - " + t.toString());
            }
        }
        return authContext;
    }

    public DependencyResolver getDependencyResolver() {
        return getInstance().dependencyResolver;
    }

    private boolean verifyAuthenticationContext() {
        if (this.contextActivity == null) {
            Log.e("AuthenticationController", "verifyAuthenticationContext - " + "Must set context activity");
            return false;
        }
        return true;
    }
    }

###Use Discovery Service

The Discovery Service provides your application with the endpoint locations for Office 365 services. You can get information about the provider, the API version, and the service endpoint URI, and other information.

The **DiscoveryController** object uses the **DiscoveryClient** object from the Office 365 SDK for Android to get a list of services from Office 365. It sends the list to the application's log file, but in your application you'll use the list of services to find the endpoints for Office 365 services.

    package com.microsoft.office365.auth_discover_snack;

    import android.util.Log;

    import com.google.common.util.concurrent.FutureCallback;
    import com.google.common.util.concurrent.Futures;
    import com.google.common.util.concurrent.ListenableFuture;
    import com.google.common.util.concurrent.SettableFuture;
    import com.microsoft.discoveryservices.ServiceInfo;
    import com.microsoft.discoveryservices.odata.DiscoveryClient;
    import com.microsoft.services.odata.impl.ADALDependencyResolver;

    import java.util.List;

    public class DiscoveryController {
    private List<ServiceInfo> mServices;

    public static synchronized DiscoveryController getInstance() {
        if (INSTANCE == null) {
            INSTANCE = new DiscoveryController();
        }
        return INSTANCE;
    }
    private static DiscoveryController INSTANCE;

    public SettableFuture<Boolean> initialize() {

        final SettableFuture<Boolean> result = SettableFuture.create();

        AuthenticationController.getInstance().setResourceId(Constants.DISCOVERY_RESOURCE_ID);
        ADALDependencyResolver dependencyResolver = (ADALDependencyResolver) AuthenticationController
                .getInstance().getDependencyResolver();

        DiscoveryClient discoveryClient = new DiscoveryClient(Constants.DISCOVERY_RESOURCE_URL, dependencyResolver);

        try {
            ListenableFuture<List<ServiceInfo>> services = discoveryClient.getservices().read();
            Futures.addCallback(services,
                    new FutureCallback<List<ServiceInfo>>() {
                        @Override
                        public void onSuccess(final List<ServiceInfo> services) {
                            getInstance().mServices = services;
                            StringBuilder servicesLogDescription = new StringBuilder();
                            servicesLogDescription.append("initialize - Services discovered\n");
                            servicesLogDescription.append("    Service info:\n");

                            String serviceProperty;
                            for (ServiceInfo service : services){
                                serviceProperty = "      ServiceName - " + service.getserviceName() + "\n";
                                servicesLogDescription.append(serviceProperty);
                                serviceProperty = "      ServiceId - " + service.getserviceId() + "\n";
                                servicesLogDescription.append(serviceProperty);
                                serviceProperty = "      Capability - " + service.getcapability() + "\n";
                                servicesLogDescription.append(serviceProperty);
                                serviceProperty = "      EntityKey - " + service.getentityKey() + "\n";
                                servicesLogDescription.append(serviceProperty);
                                serviceProperty = "      ProviderName - " + service.getproviderName() + "\n";
                                servicesLogDescription.append(serviceProperty);
                                serviceProperty = "      ProviderId - " + service.getproviderId() + "\n";
                                servicesLogDescription.append(serviceProperty);
                                serviceProperty = "      ServiceApiVersion - " + service.getserviceApiVersion() + "\n";
                                servicesLogDescription.append(serviceProperty);
                                serviceProperty = "      ServiceEndpointUri - " + service.getserviceEndpointUri() + "\n";
                                servicesLogDescription.append(serviceProperty);
                                serviceProperty = "      ServiceResourceId - " + service.getserviceResourceId() + "\n";
                                servicesLogDescription.append(serviceProperty);
                                serviceProperty = "      ServiceAccountType - " + service.getserviceAccountType() + "\n";
                                servicesLogDescription.append(serviceProperty);
                            }

                            Log.i("DiscoveryController", servicesLogDescription.toString());
                            result.set(true);
                        }

                        @Override
                        public void onFailure(final Throwable t) {
                            Log.e("DiscoveryController", "discoverServices - " + t.getMessage());
                            result.setException(t);
                        }
                    });
        } catch (Exception e) {
            Log.e("DiscoveryController", "discoverServices - " + e.getMessage());
            result.setException(e);
        }
        return result;
    }

    public ServiceInfo getService(String capability) {
        if (mServices == null)
            throw new NullPointerException("Services have not been discovered. "
                    + "Use discoverServices function first.");
        for (ServiceInfo service : mServices)
            if (service.getcapability().equals(capability))
                return service;

        return null;
    }
    }


###Access Office 365 API data

With an **AuthenticationController** to manage authentication with the Azure AD, and a **DiscoveryController** to provide the endpoints for Office 365 services, your application can start making calls to retrieve information from Office 365. 

The **MailController** object uses both to get a list of email in the user's Inbox. Once again, this simple application merely writes the subject lines to the application log file.

    package com.microsoft.office365.auth_discover_snack;

    import android.util.Log;

    import com.google.common.util.concurrent.FutureCallback;
    import com.google.common.util.concurrent.Futures;
    import com.google.common.util.concurrent.ListenableFuture;
    import com.google.common.util.concurrent.SettableFuture;
    import com.microsoft.discoveryservices.ServiceInfo;
    import com.microsoft.outlookservices.Message;
    import com.microsoft.outlookservices.odata.OutlookClient;
    import com.microsoft.services.odata.impl.ADALDependencyResolver;

    import java.util.List;

    public class MailController {

    public static synchronized MailController getInstance() {
        if (INSTANCE == null) {
            INSTANCE = new MailController();
        }
        return INSTANCE;
    }
    private static MailController INSTANCE;

    public SettableFuture<Boolean> initialize() {

        final SettableFuture<Boolean> result = SettableFuture.create();

        ServiceInfo service = DiscoveryController.getInstance().getService(Constants.MAIL_CAPABILITY);

        AuthenticationController.getInstance().setResourceId(service.getserviceResourceId());
        ADALDependencyResolver dependencyResolver = (ADALDependencyResolver) AuthenticationController
                .getInstance().getDependencyResolver();

        OutlookClient mailClient = new OutlookClient(service.getserviceEndpointUri(), dependencyResolver);

        try {
            ListenableFuture<List<Message>> mailItems = mailClient
                    .getMe()
                    .getFolder("Inbox")
                    .getMessages()
                    .read();
            Futures.addCallback(mailItems,
                    new FutureCallback<List<Message>>() {
                        @Override
                        public void onSuccess(final List<Message> mailItems) {
                            StringBuilder mailItemsLogDescription = new StringBuilder();
                            mailItemsLogDescription.append("initialize - Mail retrieved\n");
                            mailItemsLogDescription.append("    Mail items::\n");

                            String mailItemSubject;
                            for (Message mailItem : mailItems){
                                mailItemSubject = "      Subject: " + mailItem.getSubject() + "\n";
                                mailItemsLogDescription.append(mailItemSubject);
                            }

                            Log.i("MailController", mailItemsLogDescription.toString());
                            result.set(true);
                        }

                        @Override
                        public void onFailure(final Throwable t) {
                            Log.e("MailController", "initialize - " + t.getMessage());
                            result.setException(t);
                        }
                    });
        } catch (Exception e) {
            Log.e("MailController", "initialize - " + e.getMessage());
            result.setException(e);
        }
        return result;
    }
    }

<a name="bk_context"></a>
###Context and the application activity

There are two other classes that you need for this first Office 365 application. The first is a constants class that contains information that defines your application. The first three constants provide the endpoints for Azure AD authentication and the Office 365 Discovery Service. The next two constants are the identifying information that you created when you [registered your app in Azure AD](#bk_register). The final constant specifies that your app needs access to Office 365 mail services.

    package com.microsoft.office365.auth_discover_snack;

    interface Constants {
    public static final String AUTHORITY_URL = "https://login.microsoftonline.com/common";
    public static final String DISCOVERY_RESOURCE_URL = "https://api.office.com/discovery/v1.0/me/";
    public static final String DISCOVERY_RESOURCE_ID = "https://api.office.com/discovery/";
    public static final String CLIENT_ID = "<Assigned by Azure AD when you registered your app.>";
    public static final String REDIRECT_URI = "<Defined when you registered your app.>";

    public static final String MAIL_CAPABILITY = "Mail";
    
    }

The second class in the activity class that provides the UI for the application. The UI consists of three buttons, one to authenticate the app, one to get endpoint information from the Discovery Service, and one to get the email in your Inbox from th email service. The only other required method is the **onActivityResult** method that is called when the **AuthenticationActivity** completes.

    package com.microsoft.office365.auth_discover_snack;

    import android.content.Intent;
    import android.os.Bundle;
    import android.support.v7.app.ActionBarActivity;
    import android.util.Log;
    import android.view.View;

    import com.google.common.util.concurrent.FutureCallback;
    import com.google.common.util.concurrent.Futures;
    import com.google.common.util.concurrent.SettableFuture;

    public class MainActivity extends ActionBarActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void onAuthenticateButtonClick(View v){
        AuthenticationController.getInstance().setContextActivity(this);
        SettableFuture<Boolean> authenticated = AuthenticationController.getInstance().initialize();

        Futures.addCallback(authenticated, new FutureCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {
                Log.i("MainActivity", "onAuthenticateButtonClick - Authentication successful");
            }
            @Override
            public void onFailure(final Throwable t) {
                Log.e("MainActivity", "onAuthenticateButtonClick - " + t.getMessage());
            }
        });
    }

    public void onDiscoverButtonClick(View v){
        SettableFuture<Boolean> discovered = DiscoveryController.getInstance().initialize();

        Futures.addCallback(discovered, new FutureCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {
                Log.i("MainActivity", "onDiscoverButtonClick - Services discovered");
            }
            @Override
            public void onFailure(final Throwable t) {
                Log.e("MainActivity", "onDiscoverButtonClick - " + t.getMessage());
            }
        });
    }

    public void onGetMailButtonClick(View v) {
        SettableFuture<Boolean> mailRetrieved = MailController.getInstance().initialize();

        Futures.addCallback(mailRetrieved, new FutureCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {
                Log.i("MainActivity", "onGetMailButtonClick - Mail retrieved");
            }
            @Override
            public void onFailure(final Throwable t) {
                Log.e("MainActivity", "onGetMailButtonClick - " + t.getMessage());
            }
        });
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        Log.i("MainActivity", "onActivityResult - AuthenticationActivity has come back with results");
        super.onActivityResult(requestCode, resultCode, data);
        AuthenticationController
                .getInstance()
                .getAuthenticationContext()
                .onActivityResult(requestCode, resultCode, data);
    }
    }

###UI

The last piece that you'll need is a user interface that exercises the Azure AD and Office 365 services. This layout provides three buttons that do just that.

    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
        android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
        android:paddingRight="@dimen/activity_horizontal_margin"
        android:paddingTop="@dimen/activity_vertical_margin"
        android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="AUTHENTICATE TO OFFICE 365"
            android:id="@+id/authenticateButton"
            android:layout_alignParentLeft="true"
            android:layout_alignParentStart="true"
            android:layout_marginTop="21dp"
            android:onClick="onAuthenticateButtonClick" />

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="DISCOVERY SERVICES"
            android:id="@+id/discoverButton"
            android:layout_below="@+id/authenticateButton"
            android:layout_alignParentLeft="true"
            android:layout_alignParentStart="true"
            android:layout_marginTop="21dp"
            android:onClick="onDiscoverButtonClick" />

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="GET MAIL"
            android:id="@+id/getMailButton"
            android:layout_below="@+id/discoverButton"
            android:layout_alignParentLeft="true"
            android:layout_alignParentStart="true"
            android:layout_marginTop="21dp"
            android:onClick="onGetMailButtonClick" />
    </RelativeLayout>

##Test your app

Run the application from within your IDE to see the code in action. When you start the application, you'll see three buttons. When you click each of the buttons, information will be sent to the log window of your IDE.

![A screenshot of the app running in an emulator window. The available actions are shown on buttons.](images\O365APIs_RunningApp1-50Percent.png)

When you click the **Authenticate to Office 365** button, the app will call the **AuthenticationController** object which in turn will call the authentication workflow provided by the Azure Active Directory Authentication Library for Android. If a valid token is not available, a form to log in to Office 365 is shown.

![A screenshot of the Office 365 login page.](images\O365APIs_RunningApp2-50Percent.png)

After you've logged in, the **AuthenticationController** will write information about the authentication token to the log window.

![A screenshot of the token information returned from Office 365. The information includes the token, the expiration date, and information about the user, including the email address, family name, and given name.](images\O365APIs_RunningApp3.png)

Click the **DISCOVER SERVICES** button to get a list of the REST service endpoints that are available from your Office 365 server.

![A screenshot of the Office 365 REST service list. The list includes the service name, service ID, capability, entity key, provider name, provider ID, service API version, service endpoint URI, service resource ID and service account type.](images\O365APIs_RunningApp4.png)

Click the **Get mail** button to get a list of email messages in the user's Inbox. This example only lists the subject of each email message.

![A screenshot of a list of email subject lines from the user's Inbox.](images\O365APIs_RunningApp5.png)

<a name="bk_nextstep"> </a>

## Next steps

Now that you've built a simple app that gets email from Office 365, you're ready to take a look at a more complicated application that shows how to use the entire REST API.

* [Office 365 APIs Starter Project for Android](https://github.com/OfficeDev/O365-Android-Start)

<a name="bk_addresources"> </a>
## Additional resources


-  [Overview of developing on the Office 365 platform](..\howto\platform-development-overview.md)
-  [Office 365 code samples for Android](http://dev.office.com/code-samples?filters=Android)
    


[!INCLUDE [END Android section](../includes/controls/androidsection.xml)]

[!INCLUDE [BEGIN JavaScript section](../includes/controls/javascriptsection.xml)]

**Not developing Angular apps?** Use the control in the upper right corner to select the type of app you're developing.

## Create an Angular app with Office 365 APIs

 
<<<<<<< HEAD
Before you can start working on your first Angular application with Office 365, there are a few one-time tasks that you need to complete, including <a href="setup-development-environment?javascript">setting up your Office 365 development environment</a> and grabbing the right tools.
=======
Before you can start working on your first Angular application with Office 365, there are a few one-time tasks that you need to complete, including [Set up your Office 365 development environment](..\howto\setup-development-environment.md) and grabbing the right tools.
>>>>>>> staging

After setup, we'll walk you through creating a simple [Angular](https://angularjs.org/) app, **SimpleMailApp** that uses the [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js) to authenticate a user and REST calls to retrieve that user's email using [cross-origin resource sharing (CORS)](.\create-web-apps-using-CORS-to-access-files-in-Office-365.md).

![App Screenshot](images/AngularGettingStartedScreenshot.png)

This article focuses on an Angular front-end because ADAL JS was designed with single-page applications (SPAs) and Angular in mind. The library assumes the interaction pattern that SPAs require. While it is possible to use the library without Angular, it requires you to write much more code. Check out [Create JavaScript web apps using CORS to access Office 365 APIs](.\create-web-apps-using-CORS-to-access-files-in-Office-365.md) if you're interested in using the Office 365 APIs without ADAL JS.

## Before you start

Before you can create applications that access the Office 365 APIs, you'll need to set up your developer environment. This consists of three one-time tasks to make sure you've got the tools and environment to be successful:

1. Download tools to create your Angular application, including an IDE, Git, and Node.js. 
2. Get an Office 365 for business subscription, to access the Office 365 APIs.
3. Associate your Office 365 subscription with Azure AD, so you can create and manage apps.

<<<<<<< HEAD
If you still need to complete any of these steps, take a look at <a href="setup-development-environment?javascript">Set up your Office 365 development environment</a> for detailed instructions on getting set up.
=======
If you still need to complete any of these steps, take a look at [Set up your Office 365 development environment](..\howto\setup-development-environment.md) for detailed instructions on getting set up.
>>>>>>> staging

**Note**  Node.js, and specifically its package manager (npm), is needed for this article to install project dependencies. It's not necessary for development with the Office 365 APIs.

## Create your app and add dependencies 

In this step, you'll set up an Angular app by leveraging an empty project we developed, add the Azure Active Directory Authentication Library (ADAL) for JavaScript to it, and set up your application to communicate with Azure by registering it in your Azure Management Portal.

### Set up the SimpleMailApp project

To get you up and running as quickly as possible, you'll leverage an empty project we created, which can be found on [GitHub](https://github.com/OfficeDev/O365-Angular-GettingStarted). 

1. Using Git, clone the empty project from the command line.
 
    ```git clone https://github.com/OfficeDev/O365-Angular-GettingStarted.git```

    **Note**  If you are unfamiliar with Git, you can download the code directly from [GitHub](https://github.com/OfficeDev/O365-Angular-GettingStarted). 

2. Then switch to your new project folder and install your project dependencies using npm, the package manager for Node.js. 

    ```cd O365-Angular-GettingStarted/Starter```    
    ```npm install```     

**Note**  There's also a *Completed* folder in the repository. The project in that folder is ready to deploy once you configure it with your Azure tenant information and install the dependencies. 

### Add ADAL JS to the SimpleMailApp project

ADAL JS is a JavaScript library which provides you with complete support for both signing on Azure AD users in single-page applications (SPAs) like this one, and consuming directly from JavaScript Web APIs secured by Azure AD.

ADAL.js has two layers, in two files:

* **adal.js** Use for all JavaScript applications. It contains low-level functions, such as domain-specific logic, building and parsing OAuth2 messages, and caching tokens. For more information, see [Introducing ADAL JS v1](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/).
* **adal-angular.js** Include along with adal.js for Angular applications. It contains specific functions compatible with the Angular framework.

Include both of these files in your project to get access to a programming model for Azure AD authentication and calling APIs secured by Azure AD like the Outlook Mail REST API we will call later on in this article. 

You can get the bits from our CDN.

* [adal.min.js](https://secure.aadcdn.microsoftonline-p.com/lib/1.0.0/js/adal.min.js) ([non-minified version](https://secure.aadcdn.microsoftonline-p.com/lib/1.0.0/js/adal.js))
* [adal-angular.min.js](https://secure.aadcdn.microsoftonline-p.com/lib/1.0.0/js/adal-angular.min.js) ([non-minified version](https://secure.aadcdn.microsoftonline-p.com/lib/1.0.0/js/adal-angular.js))

The easiest way to include the ADAL dependencies is to add ```script``` tags using the CDN links as the ```src``` attribute at the end of the ```<head>``` tag in the **index.html** file located in *Starter/public*. 

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.0/js/adal.min.js"></script>
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.0/js/adal-angular.min.js"></script>
```

### Register your app with Azure AD

Before you start writing the code for your Office 365 application, you're required to do a little work to register your application with Azure Active Directory and to set permissions for your application to use Office 365 services. You only need to do this once for each application.

1. Sign into the [Azure Management Portal](https://manage.windowsazure.com/), using your Office 365 business account credentials.

2. Click the **Active Directory** node in the left column and select the directory linked to your Office 365 subscription.
    
    ![Azure Management Portal](images/O365APIs_RegisterApp_1.png)

3. Select the **Applications** tab and then **Add** at the bottom of the screen.
    
    ![Azure Management Portal Add Application](images/O365APIs_RegisterApp_2.png)

4. On the pop-up, select **Add an application my organization is developing**. Then click the arrow to continue. 

5. Choose a name for your app, such as *SimpleMailApp*, and select **Web application and/or web API** as its Type. Then click the arrow to continue.

6. The value of **Sign-on URL** is the URL where your application will be hosted. Use *http://127.0.0.1:8080/* for the sample project.

7. The value of **App ID URI** is a unique identifier for Azure AD to identify your app. You can use http://{your_subdomain}/SimpleMailApp, where {your_subdomain} is the subdomain of .onmicrosoft you specified while signing up for your Office 365 Office 365 business account. Then click the check mark to provision your application.

8. Once the application has been successfully added, you will be taken to the Quick Start page for the application. From here, select the **Configure** tab.

9. Scroll down to the **permissions to other applications** section and click the **Add application** button.

    ![Add application for web app](images/GettingStartedJavaScriptAddPermissionsMail.png)

10. In this article, we'll demonstrate how to get a user's email so add the **Office 365 Exchange Online** application. Click the plus sign in the application's row and then click the check mark at the top right to add it. Then click the check mark at the bottom right to continue.

    ![Add Exchange permissions](images/O365APIs_RegisterApp_5.png)

11. In the **Office 365 Exchange Online** row, select **Delegated Permissions**, and in the selection list, choose **Read user mail**.

    ![Add application for web app](images/GetStarted_DelegatedPermissions.png)

    These are the permissions that will be displayed to your app user when Azure prompts them to consent to your app's permission request. In general, request only the services your app actually requires, and specify the least level of permissions in each service that still let your app perform its functions.

12. Click **Save** to save the app's configuration.

### Configure your app to allow the OAuth 2.0 implicit grant flow

To get an access token for Office 365 API requests, your application will use the OAuth implicit grant flow. You need to update the application's manifest to allow the OAuth implicit grant flow because it is not allowed by default. 

1. Select the **Configure** tab of your application's entry in the Azure Management Portal. 

2. Using the **Manage Manifest** button in the drawer, download the manifest file for the application and save it to your computer.

3. Open the manifest file with a text editor. Search for the *oauth2AllowImplicitFlow* property. By default it is set to *false*; change it to *true* and save the file.

4. Using the **Manage Manifest** button, upload the updated manifest file.

You've now successfully created your app and registered it with Azure AD. The final step is to add code to make requests to the Outlook Mail REST API. 

## Code your app

Before we continue, check that you're still in the *Starter* directory of the project and you've included **adal.js** and **adal-angular.js** in **index.html**. After that, continue on to authenticating with Azure AD.   

### Authenticate with Azure AD and get an access token

[ADAL for JS](https://github.com/AzureAD/azure-activedirectory-library-for-js) provides the functionality to manage authentication in your application. You can use it for caching and retrieving access and refresh tokens. We need to edit only the **app.js** file in *public/scripts* to get authentication working.

To start, add *AdalAngular* as a required module for your *app* module on line 8.

```javascript
angular
  .module('app', [
    'ngRoute', 
    'AdalAngular'
  ])
```

Next, we'll configure the service that the *AdalAngular* provides us with by passing it in as an argument in your module's config function on line 13. We'll also add Angular's *$http* module at this time because we need it to configure the service.

```javascript
function config($routeProvider, $httpProvider, adalAuthenticationServiceProvider) {
```

The next step is to initialize *adalAuthenticationServiceProvider* in the *config* function so that the ADAL API is exposed and configured for your application. There are three arguments needed to initialize the provider: *tenant*, *clientId*, and *cacheLocation*. The *tenant* value is the subdomain of **.onmicrosoft** you specified while signing up for your Office 365 business account. The *clientId* is the client ID of your application that can be found in the Azure Management Portal under the **Configure** tab of your application's page. Finally, include *cacheLocation* with the value of *localStorage* if your app will run in Internet Explorer. 

```javascript
// Initialize the ADAL provider with your tenant name and clientID (found in the Azure Management Portal).
adalAuthenticationServiceProvider.init(
  {
    tenant: '{your_subdomain}.onmicrosoft.com',
    clientId: 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX',
    cacheLocation: 'localStorage'
  },
  $httpProvider
  );
```

At this point, you've configured the *AdalAngular* module and can use it to authenticate users in your application. An efficient way to do this in Angular applications is to set up which routes require the user to be authenticated. In our example, we want only authenticated users to be able to see our app, so protect the root route in the *$routeProvider* configuration by adding the *requireADLogin* member to the object you pass to the *.when* method.

```javascript
$routeProvider
  .when('/', {
    templateUrl: 'views/home.html',
    controller: 'HomeController',
    controllerAs: 'home',
    requireADLogin: true     // Designates that the user must be authenticated to view this page.
  })
  .otherwise({
    redirectTo: '/'
  });
```

### Retrieve a user's email from Office 365

Now that you have authenticated your user, you can make HTTP requests to the [Mail](https://msdn.microsoft.com/en-us/office/office365/api/mail-rest-operations) REST API using an authentication token. CORS support for the [Files](https://msdn.microsoft.com/office/office365/APi/files-rest-operations) REST API, the [Calendar](https://msdn.microsoft.com/office/office365/APi/calendar-rest-operations) REST API, and the [Contacts](https://msdn.microsoft.com/office/office365/APi/contacts-rest-operations) REST API is also available. 

To make the HTTP request to the Mail REST API to retrieve the user's email, you need to declare the URL of the Mail REST API at init time so ADAL JS knows to trust it, using cross-origin resource sharing (CORS). You can do this by passing an *endpoints* object to our *adalAuthenticationServiceProvider.init* code in **app.js**. The endpoint you need to add is *https://outlook.office365.com*.

```javascript 
var endpoints = {
  'https://outlook.office365.com': 'https://outlook.office365.com'
};
	
// Initialize the ADAL provider with your tenant name and clientID (found in the Azure Management Portal).
adalAuthenticationServiceProvider.init(
  {
    tenant: '{your_subdomain}.onmicrosoft.com',
    clientId: 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX',
    cacheLocation: 'localStorage',
    endpoints: endpoints
  },
  $httpProvider
  );
```

Now that ADAL JS is set up to make HTTP requests to the Mail REST API using CORS, the only thing left to do is make the HTTP request to retrieve the user's email. We'll do this in **homeController.js**, which is located in the *public/controllers* folder. 

Add the following code to your empty controller. It sets up the HTTP request and executes it. When the response is received, it attaches the data from the response to the view model to make it accessible from the view (**public/views/home.html**). 

```javascript
// Pass in the resource URL that you're requesting.
$http.get("https://outlook.office365.com/api/v1.0/me/messages")
  .then(function(response) {
    $log.debug('HTTP request to Mail API returned successfully.');
    vm.emails = response.data.value;
  }, function(error) {
    $log.error('HTTP request to Mail API failed.');
  });
```

Finally, let's add some HTML to show the data you just received. Add the following code to **home.html** located in the *public/views* folder. 

```html
<div class="container-fluid">
  <row>
    <div class="col-md-8 col-md-offset-2" style="margin-top: 20px;">
      <table class="table table-hover">
        <thead>
          <tr>
            <th>From</th>
            <th>Subject</th>
            <th>Body Preview</th>
            <th>Web Link</th>
          </tr>
        </thead>
        <tbody>
          <tr ng-repeat="email in home.emails">
            <td>{{email.Sender.EmailAddress.Name}} ({{email.Sender.EmailAddress.Address}})</td>
            <td>{{email.Subject}}</td>
            <td>{{email.BodyPreview}}</td>
            <td><a href={{email.WebLink}}>View on OWA</a></td>
          </tr>

          <tr ng-if="home.emails.length == 0">
            <td colspan="4" align="center">Your inbox is empty.</td>
          </tr>
        </tbody>
      </table>
    </div>
  </row>
</div>
```

## Test your app

Let's test your application to make sure it's successfully authenticating the user with Azure AD and fetching the user's email. From a command prompt within your the *Starter* directory, enter the command `node server.js`. This will start a development server listening on port 8080. Navigate to *http://127.0.0.1:8080/* in a web browser. If you've followed the steps correctly, your application should direct you to an Azure Active Directory sign-in page. Sign in using your Office 365 credentials (**user@{your_subdomain}.onmicrosoft.com**) and verify that you return to the application where you'll find your email.

Congratulations! You just built an Angular app using the Office 365 APIs. 

![App Screenshot](images/AngularGettingStartedScreenshot.png)

## Next steps

Now that you've built an app that uses the Mail API, you can explore the other Office 365 REST APIs available for use in your apps.

- [Office 365 API reference](.\rest-api-overview.md)

## Additional resources

-  [Office 365 APIs starter projects and code samples](..\howto\Starter-projects-and-code-samples.md) 
-  [Office Developer on GitHub](https://github.com/OfficeDev)


[!INCLUDE [END JavaScript section](../includes/controls/javascriptsection.xml)]


[!INCLUDE [BEGIN ASP.NET MVC section](../includes/controls/aspnetmvcsection.xml)]

**Not developing ASP.NET MVC web apps?** Use the control in the upper right corner to select the type of app you're developing.

## Create an ASP.NET MVC app with Office 365 APIs


When creating your app, you can program directly against the REST APIs to interact with Office 365, or you can use the Office Developer Tools for Visual Studio.

The Office Developer Tools for Visual Studio include client libraries and UI enhancements to access the Office 365 API services. The .NET Framework and JavaScript client libraries make it easier for you to interact with the Office 365 REST APIs from the device or platform of your choice. The Visual Studio UI enhancements make it easy to add Office 365 services to your app projects.

In this topic, we'll walk you through creating a simple MVC (model-view-controller) web application that uses the Office 365 APIs in Visual Studio. This includes:

1. [Create your app and add dependencies](#bk_createApp)
2. [Code your app](#bk_codeYourAppVS)
3. [Test your app](#bk_test)




<a name="bk_prerequisites" />
##Before you start

Before you can create applications that access the Office 365 APIs, you'll need to set up your developer environment. This consists of three one-time tasks to make sure you've got the tools and environment to be successful:

3. Download Visual Studio and the Office Developer Tools you'll be using to create your apps.
1. Get an Office 365 for business subscription, to access the Office 365 APIs.
2. Associate your Office 365 subscription with Azure AD, so you can create and manage apps.

<<<<<<< HEAD
If you still need to complete any of these steps, take a look at <a href="setup-development-environment?aspnet">Set up your Office 365 development environment</a> for detailed instructions on getting set up.
=======
If you still need to complete any of these steps, take a look at [Set up your Office 365 development environment](..\howto\setup-development-environment.md) for detailed instructions on getting set up.
>>>>>>> staging




<a name="bk_createApp"> </a>
## Create your app and add dependencies

After you've set up your development environment, you're ready to use Visual Studio to create a web application that uses the Office 365 APIs.

The example we'll build will be a single-tenant MVC that uses Azure AD Single Sign-on to authenticate and read the user's Contact information from Office 365. We'll use the [Office 365 single-tenant MVC project](https://github.com/OfficeDev/O365-WebApp-SingleTenant) on GitHub as a model. 

Select the version of Visual Studio you are using:

[!INCLUDE [Add the VS versions filter bar](../includes/controls/vsversionsfilter.xml)]


1. In Visual Studio, select **File** > **New**.
2. Under **Visual C#** > **Web**, select **ASP.NET web application**. Name the project and select **Ok**.
3. Select **MVC**.
4. Select **Change authentication**, select **No authentication**, and select **OK** twice to create the project.

The Office 365 API services use Azure AD to provide secure authentication to users' Office 365 data. To access the Office 365 APIs, you need to register your app with Azure AD. 

<a name="bk_intro"> </a>
### When you add an Office 365 service to your project, Visual Studio helps you register your app

If you're creating a Visual Studio project, app registration is handled for you when you add an Office 365 service to your project. During the process of adding an Office 365 service to your project, Visual Studio enables you to:

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

The following project templates support adding Office 365 APIs as a connected service:

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


<a name="addO365APIs"> </a>
### Use the Visual Studio Service Manager to register your app and add Office 365 APIs to your project


You add and configure Office 365 APIs by using the  **Services Manager** in Visual Studio.

[!INCLUDE [BEGIN VS2013 section](../includes/controls/vs2013section.xml)]

1. In the **Solution Explorer**, choose the project node.
    
2. Right-click or press and hold the project node and choose **Add** > **Connected Service**.
    
3. Register your app:
	
	At the top of the  **Services Manager** dialog box, choose the **Office 365** link, and then choose **Register your app**. Sign in with a tenant administrator account for your Office 365 developer organization. 

	This starts the app registration in Azure Active Directory, which allows your app to authenticate via OAuth.
    
    After you've logged on to Office 365, a list of available Office 365 APIs services appears. You will see a list of Office 365 APIs.

	You will see that the **Permissions** column to the right of each service is empty.
    
4. Select the Office 365 APIs to which you want to connect, and specify permission levels for each.

	1. For this example, select **Users and Groups**. Choose **Permissions**.

		![A screenshot that shows the Services Manager dialog box with the Users and Groups service Office 365 API selected and the Permissions link highlighted.](..\howto\images\O365_RegisterApp_User.png)

	2. Select **Enable sign-on and read users' profile** and choose **Apply**.

		![A screenshot that shows the Users and Groups Permissions dialog box with the Enable sign-on and read users' profile permission selected.](..\howto\images\O365_RegisterApp_UserPerms.png)

	1. Next, select **Contacts**. Choose **Permissions**.
	2. Select **Read users' contacts** and choose **Apply**.
	
		When you do this, Visual Studio adds the Office 365 services that contain the APIs you selected to your app in Azure AD, and sets the permission levels for the APIs to those you specified.

6. Set properties for your app:
	
	Choose  **App Properties** in the **Services Manager** dialog box. 
	
	The app properties you can set differ depending on whether your app project is a web service or web application, or a native application, such as a mobile phone project.
	
	For example, for web applications such as the one we're building, you could choose to make this sample app available to Office 365 organizations other than your developer organization.

	For now, we'll leave the app properties as they are by default.
	
	The  **Services Manager** dialog box now lists:
	
	- The service(s) you've selected to add to your project.
	- The permissions for each service. 
	
		![A screenshot of the Services Manager dialog box after the Users and Groups and Contact APIs have been configured, showing that both APIs have Read permissions.](..\howto\images\O365_RegisterApp_ServiceManager.png)
	
6. Choose **OK**.

At this point, Visual Studio adds the required **NuGet packages** to the project. The NuGet packages added vary based on the Office 365 APIs you add.

[!INCLUDE [END VS2013 section](../includes/controls/vs2013section.xml)]

[!INCLUDE [BEGIN VS2015 section](../includes/controls/vs2015section.xml)]

1. In the **Solution Explorer**, choose the project node to which you want to add an Office 365 service.
    
2. Right-click or press and hold the project node and choose **Add** > **Connected Service**.

3. On the **Microsoft** tab, choose **Office 365 APIs**, and choose **Configure**.

	The **Configure Office 365 API Services** dialog box appears.
    
3. Register your app:
	
	On the **Select Domain** page, enter or select the Office 365 domain in which you want your app to be registered; for example, <i>contoso.onmicrosoft.com</i>. Choose **Next**. You may be required to sign into Office 365, if you are not already currently signed in. 
	
	On the **Configure Application** page, choose to create a new Azure AD application.
	
	Check the box to use Single Sign-On with your application. Since Single Sign-On requires SSL, selecting this option automatically enables SSL in your project. 
	
	Choose **Next**. 

	Visual Studio registers your app.
    
4. Select the Office 365 APIs to which you want to connect, and specify permission levels for each. For this example:
	
	1. Select **Contacts**.
		
	2. Check **Read your contacts**.
		
	2. Select **Users and groups**.
		
	4. Check **Sign in and read your profile**.
		
6. Select **Finish**.
	
At this point, Visual Studio adds the required **NuGet packages** to the project. The NuGet packages added vary based on the Office 365 APIs you added.
    

[!INCLUDE [END VS2015 section](../includes/controls/vs2015section.xml)]


<a name="bk_codeYourAppVS"> </a>
    
## Code your app

After you've added the Office 365 services to your project, you'll need to write code that authenticates the app user and accesses their Office 365 data. 

The authentication process is different based on whether you are building a web application, such as an MVC, or a native application, such as a Windows Store app. 

This ASP.NET MVC example will employ a persistent [Active Directory Authentication Library](https://msdn.microsoft.com/en-us/library/azure/jj573266.aspx) (ADAL) token cache that uses a database for caching. ADAL enables you to  authenticate users to Active Directory (AD), in this case Azure AD, and then obtain access tokens for securing API calls. 

From there, building the example consists of three major steps:

 - [Configure your project for authentication with Azure AD](#bk_AuthenticateAzure)

 - [Authenticate with Azure Active Directory](#bk_AuthenticateAzureAD)

 - [Access Office 365 APIs](#bk_accessOffice365APIs)


<a name="bk_AuthenticateAzure"> </a>
###Configure your project for authentication with Azure Active Directory

Because the example you're building requires only Office 365 credential authentication, you'll be using [OWIN](http://owin.org/) &nbsp; [Katana](http://katanaproject.codeplex.com/documentation) and [Active Directory Authentication Library](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) (ADAL).

But first, you need to configure the project to use Secure Sockets Layer (SSL).

####Enable SSL for your project 

Visual Studio does not configure your project for SSL by default. If you haven't already enabled SSL in your project, you'll want to now, and then update the Office 365 services with the appropriate Redirect URL.

To enable SSL:

1. In **Solution Explorer**, choose on the project.
2. In **Properties**, set **SSL Enabled** to **True**.
	
	Visual Studio specifies a value for the **SSL URL**.

Next, update the application to use the HTTPS endpoint for the home page:

1.	In **Solution Explorer**, right-click the project, and select **Properties**.
2.	Select the **Web** tab. Under **Servers**, set **Project URL** to the HTTPS endpoint Visual Studio created for the **SSL URL**.

Lastly, update the Office 365 services:

3. In **Solution Explorer**, right-click the project, and select **Add** > **Connected Service**. Sign in if necessary.

	Visual Studio prompts you that one or more Redirect URLs in your project do not exist in your application entry in Azure AD.

4. Choose **Yes** to add the secure redirect URL to your application entry in Azure AD.
5. Choose **OK** to exit **Services Manager**.


<a name="bk_AuthenticateDownloadNuGets"> </a>
####Manage NuGet packages necessary for authentication

You'll need to install the following Azure AD and OWIN Katana packages for authentication:

- [Active Directory Authentication Library](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory)
- [EntityFramework](https://www.nuget.org/packages/EntityFramework)
- [Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)
- [Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)
- [Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect)

These packages may also install selected NuGet packages as dependencies.

To download and install the NuGet packages:

1. In the **Solution Explorer**, right-click the project.
2. Select **Manage NuGet Packages...** 
3. In **Manage NuGet Packages**, choose **Online**.
4. Use the Search box to find the necessary package.
5. Select the package and choose **Install**.
6. In **Select Projects**, choose **OK**.
7. Accept any licenses as prompted.

####Update the web.config file to enable authentication

When you added Office 365 services to your project, Visual Studio added the following properties to your application's registry in Azure AD, and to the **web.config** file in your solution.


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

2. In the left navigation panel, select **Active Directory**. Be sure the **Directory** tab is selected, and then choose the directory name for the Office 365 tenancy in which your app is registered.

	At this point, the URL in the browser window will include a GUID that is the tenant ID of your directory.

3. Copy only the GUID from the browser URL. This is the ID for the tenancy in which your application is registered.

After you have copied the tenant ID, you can add it to the project's web.config file. 

1. In **Solution Explorer**, double-click **Web.config**.
2. In the web.config file, in the **appSettings** section, add a new key, containing the tenant ID, directly under the ida:AuthorizationUri key.

		<add key="ida:TenantId" value="your-Office-365-tenant-ID"/>

3. Save the file.

-->

####Create a database to manage ADAL authentication tokens

Next, add a database to the project, to act as the ADAL token cache.

For more information about the ADAL token cache, see [The New Token Cache in ADAL v2](http://www.cloudidentity.com/blog/2014/07/09/the-new-token-cache-in-adal-v2/).


To add the database that will act as the ADAL token cache:

1. In **Solution Explorer**, right-click the **App_Data** folder and select **Add** > **New Item...**
2. Be sure **Data** is selected, and then select **SQL Server Database**. Name the database **ADALTokenCacheDb**, and choose **Add**.

Be sure the database connection has been added to the project web.config:

1. In **Solution Explorer**, double-click **web.config**.
2. Make sure the following section has been added to the web.config file, after the **appSettings** section. If it's not there, add it.
	
	```XML
	<connectionStrings>
  	<add name="DefaultConnection"
    	connectionString="Data Source=(LocalDB)\v11.0;AttachDbFilename=|DataDirectory|\ADALTokenCacheDb.mdf;Integrated Security=True" providerName="System.Data.SqlClient" />
	</connectionStrings>
	```
	
3. Save the file.

####Copy over files needed for authentication

Next, you'll import some files from the [Office 365 single-tenant MVC project](https://github.com/OfficeDev/O365-WebApp-SingleTenant) GitHub project.

To copy files from the GitHub project:

1. In a browser, navigate to the file you want to copy over. (The files are listed below).
2. Right-click the **Raw** button, and select **Save target as**
3. Save the file to your computer.
4. In Visual Studio, in **Solution Explorer**, under the project node, right-click the specified folder as described below and select **Add** > **Existing Item**.
5. Select the file from where you saved it on your computer. 

Copy the following files into the **Models** folder in the project. These classes demonstrate how a persistent ADAL token cache can be constructed and used to store tokens.

- [ADALTokenCache.cs](https://github.com/OfficeDev/O365-WebApp-SingleTenant/blob/master/O365-WebApp-SingleTenant/Models/ADALTokenCache.cs)
- [ApplicationDbContext.cs](https://github.com/OfficeDev/O365-WebApp-SingleTenant/blob/master/O365-WebApp-SingleTenant/Models/ApplicationDbContext.cs)

Create a new folder, **Utils**.

1. In **Solution Explorer**, right-click your project and select **Add** > **New Folder**.
2. Name the folder **Utils**. 

Copy the following file into it. This helper class contains member variables that read the values from your project's web.config file that you'll need to create the ADAL authentication object during startup. 

- [SettingsHelper.cs](https://github.com/OfficeDev/O365-WebApp-SingleTenant/blob/master/O365-WebApp-SingleTenant/Utils/SettingsHelper.cs)


Finally, copy the  [_LoginPartial.cshtml](https://github.com/OfficeDev/O365-WebApp-SingleTenant/blob/master/O365-WebApp-SingleTenant/Views/Shared/_LoginPartial.cshtml) file into the **Views** > **Shared** folder of your project.


<a name="bk_AuthenticateAzureAD"> </a>
###Authenticate with Azure Active Directory

Now that you have the project configured for authentication, you can actually add the functionality that handles authentication with Azure AD.

####Configure Azure AD single sign-on

Next, you'll need to add an OWIN startup class to the project, to actually handle authentication. To add the OWIN startup class:

1. In Solution Explorer, right-click the project name and select **Add** > **New Item...**
2. In **Add New Item**, under **Web**, select **General**, then select **OWIN Startup class**.
3. For **Name**, enter **Startup**.
3. Choose **Add**.

A new startup class is added to your project. 

Next, add the code that handles authentication:

1. Replace the namespace references in the file with the following.

	```C#
		
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
	```
	
2. Add the following method, **ConfigureAuth**, to the Startup class.
	
	```C#

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
	```
	
3. Add code to the **Startup.Configuration** method that calls the **ConfigureAuth method**.
	
	```C#
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
	```
	
####Add a controller for sign-in and sign-out of Office 365

Add an account controller to handle sign-in and sign-out:

1. In **Solution Explorer**, right-click the **Controllers** folder and select **Add** > **Controller...**
2. Select **MVC 5 Controller - Empty** and choose **Add**.
3. For Controller name, enter **AccountController**, and choose **Add**.
4. Replace the namespace references in the controller file with the following.
	
	```C#
		using Microsoft.IdentityModel.Clients.ActiveDirectory;
		using Microsoft.Owin.Security;
		using Microsoft.Owin.Security.Cookies;
		using Microsoft.Owin.Security.OpenIdConnect;
		using O365_WebApp_SingleTenant.Utils;
		using System.Security.Claims;
		using System.Web;
		using System.Web.Mvc;
	```
	
5. Delete the **Index() method**.
6. Add the following methods to the **AccountController** class, to handle sign-in and sign-out.
	 
	```C#
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
	```

<a name="bk_accessOffice365APIs"> </a>
###Access Office 365 APIs

Now you're ready to add the code that will access the user's Office 365 data.

####Create the model for the contacts information view 

First, you need to create the class on which we'll base the Contact view:

1. In **Solution Explorer**, right-click the **Models** folder and select **Add** > **Class...**
2. Select **Class**, enter **MyContact** as the name, and choose **Add**.
3. In the class, add the following line of code.
	
	```C#

	    public class MyContact
	    {
	        public string Name { get; set; }
	    }
	```
	
4. Save the file.
	
####Add a controller for contact information

Next, add a controller for the users' contact information:

1. In **Solution Explorer**, right-click the **Controllers** folder and select **Add** > **Controller**.
2. Select **MVC 5 Controller - Empty** and choose **Add**.
3. For Controller name, enter **ContactsController**, and choose **Add**.
	
	Visual Studio adds a new empty controller to the project.
	
4. Replace the namespace references in the controller file with the following.

	```C#
		using Microsoft.IdentityModel.Clients.ActiveDirectory;
		using Microsoft.Office365.Discovery;
		using Microsoft.Office365.OutlookServices;
		using O365_WebApp_SingleTenant.Models;
		using O365_WebApp_SingleTenant.Utils;
		using System.Collections.Generic;
		using System.Security.Claims;
		using System.Threading.Tasks;
		using System.Web.Mvc;
	```
	
	Be sure to add a namespace reference for the Models namespace of your project.
	
	```C#
			using [projectname].Models;
	```
	
5. Add the **[Authorize]** attribute to the **ContactsController** class.
	
	The **[Authorize]** attribute requires that the user be authenticated before they can access this controller. 
	
	```C#
    	[Authorize]
		public class ContactsController : Controller
	```
	
6. Change the Index() method to be asynchronous.
	 
	```C#
		public async Task<ActionResult> Index()
	```
	
7. Add the following code to the Index() method.
	   
	This code creates the authentication context, using the signed-in Office 365 user ID and the authority for your Office 365 tenancy.
	
	```C#
            List<MyContact> myContacts = new List<MyContact>();

            var signInUserId = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier).Value;
            var userObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;

            AuthenticationContext authContext = new AuthenticationContext(SettingsHelper.Authority, new ADALTokenCache(signInUserId));
	```
	
8. Add a **try-catch** block directly below the above code in the **Index()** method.
	
	```C#

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
	```
	
9. In the **try** block of the code above, add the following code to the **Index()** method.
	
	This code attempts to acquire an access token to the Discovery Service, passing the application's client ID and app password, and the user's credentials. Because the user authentication token has been cached, the controller is able to acquire the necessary access token silently, without having to prompt the user again for their credentials.
	
	With the access token, the application can create a Discovery Service client object, and use the discovery client object to determine the resource endpoint for the Office 365 service Contact APIs.
	
	```C#
                DiscoveryClient discClient = new DiscoveryClient(SettingsHelper.DiscoveryServiceEndpointUri,
                    async () =>
                    {
                        var authResult = await authContext.AcquireTokenSilentAsync(SettingsHelper.DiscoveryServiceResourceId, new ClientCredential(SettingsHelper.ClientId, SettingsHelper.AppKey), new UserIdentifier(userObjectId, UserIdentifierType.UniqueId));

                        return authResult.AccessToken;
                    });

                var dcr = await discClient.DiscoverCapabilityAsync("Contacts");
	```
	
10. Finally, directly below the above code in the <b>try</b> block, add the following code to the **Index()** method.
	
	This code contacts the resource endpoint for the Office 365 service Contact APIs, again silently passing the application and user credentials to acquire an access token to the Outlook service.
		
	Once the access token is received, the code can initialize an Outlook client object. The code then uses the **Me** property of the Outlook client object to retrieve contacts information for this user.	
	
	Lastly, the controller reads through the list of user contacts and returns a view listing their display names.
	
	```C#

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
	```
	
	The completed **Index()** method should now read as follows.
	
	```C#
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
	```
	
####Create the view for the Contacts data

Next, you can create the view for the user's contact information. You'll do so by basing the view on the **MyContact** class that you created earlier.

1. In **Solution Explorer**, right-click the **Contacts** folder and select **Add** > **View**.
2. In the **Add View** dialog box, define the new view:
	- For **View name**, enter **Index**. 
	- For **Template**, select **List**. 
	- For **Model class**, select **MyContact**.
	- Choose **Add**.



####Add the MyContacts link to the navigation bar

1. In **Solution Explorer**, in the **Shared** folder, double-click the _Layout.cshtml file.

2. Add an action link for the MyContacts page, and inject the partial class for the user log-in. 
3. Update the HTML of the navigation bar from what's autogenerated. 
	
	```ASP
            <div class="navbar-collapse collapse">
                <ul class="nav navbar-nav">
                    <li>@Html.ActionLink("Home", "Index", "Home")</li>
                    <li>@Html.ActionLink("About", "About", "Home")</li>
                    <li>@Html.ActionLink("Contact", "Contact", "Home")</li>
                </ul>
            </div>
	```
	
	To the following, to add an action link for the MyContacts page, and inject the partial class for the user log-in.
	
	```ASP
            <div class="navbar-collapse collapse">
                <ul class="nav navbar-nav">
                    <li>@Html.ActionLink("Home", "Index", "Home")</li>
                    <li>@Html.ActionLink("About", "About", "Home")</li>
                    <li>@Html.ActionLink("Contact", "Contact", "Home")</li>
                    <li>@Html.ActionLink("My Contacts", "Index", "Contacts")</li>
                </ul>
                @Html.Partial("_LoginPartial")
            </div>
	```
	
<a name="bk_test" />
##Test your app

Now you're ready to run the solution. Press F5 to debug your web application.

If this is a new development environment, Visual Studio may prompt you to configure the IIS SSL certificate. Choose **Yes** twice to continue.

1. Visual Studio will launch the web application in the browser you selected in Visual Studio.

2. Choose **Sign in**, at the top right corner of the page, and sign in to your Office 365 tenant where you registered your web application.
	
	Since only your organization users are allowed to sign-in to a single tenant application, there is no need to consent. If your application was multi-tenant, Azure AD would display a consent page listing the permissions the app was requested, so you could consent to giving the app those permissions.
	
3. Once you're signed in, you should see your email address  and **Sign out** displayed in the navigation bar across the top of the home page.
4. Choose on **My Contacts**.
	
	The **My Contacts** page will retrieve and display the names of any Exchange contacts from your tenant.
	
You now have a web application project that you can customize and integrate Office 365 APIs.

<a name="bk_nextstepsVS"> </a>
## Next steps

Explore the Office 365 REST APIs available for use in your apps.

- [Office 365 API reference](..\api\api-catalog.md)

Visit the [Office code sample repository](https://github.com/OfficeDev) on GitHub to download or explore code samples that use the Office 365 APIs in a wide range of project types, including:

- [Office 365 Starter Project for Windows Store App](https://github.com/OfficeDev/O365-Windows-Start)
- [Connecting to Office 365 in Windows Store, Phone, and universal apps](https://github.com/OfficeDev/O365-Win-Connect)
- [Office 365 Starter Project for ASP.NET MVC](https://github.com/OfficeDev/O365-ASPNETMVC-Start)

<a name="bk_addresources"> </a>
## Additional resources

- [Office 365 single-tenant MVC project](https://github.com/OfficeDev/O365-WebApp-SingleTenant)
- [Office 365 ASP.NET MVC starter project](https://github.com/OfficeDev/O365-ASPNETMVC-Start)
-  [Office 365 APIs starter projects and code samples](..\howto\Starter-projects-and-code-samples.md) 
 




[!INCLUDE [END ASP.NET MVC section](../includes/controls/aspnetmvcsection.xml)]



[!INCLUDE [Enable filtering functionality ](../includes/controls/enablefiltering.xml)]

