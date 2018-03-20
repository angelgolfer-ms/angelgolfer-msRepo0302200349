ms.TocTitle: Build service and daemon apps in Office 365
Title: Build service and daemon apps in Office 365
Description: Office 365 supports using the OAuth2 client credentials grant flow so daemon or service web apps can request app-only tokens, without requiring user sign-in.
ms.ContentId: 14967061-1dfb-4d4b-9668-a7ac60343a55
ms.topic: article (how-tos)
ms.date: May 19, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Build service and daemon apps in Office 365

_**Applies to:** Office 365_

Device and web server applications usually require a user to sign-in and consent to allow the application to access and work with their information in Office 365. The underlying protocol to gain access is based on the [OAuth2 authorization code grant flow](https://msdn.microsoft.com/en-us/library/azure/dn645542.aspx). As part of this OAuth2 flow, the application gets an access token/refresh token pair that represents a delegation given to the application by an individual user for a set of permissions. Essentially before the application can access data for a user, it has to get an access token/refresh token for each user, and to get those, the user has to sign-on to the application at least once.

This is not possible for applications that run in the background, such as a daemon or service app. These apps need access without a user having to sign-in. OAuth2 provides the [client credentials grant flow](https://msdn.microsoft.com/en-us/library/azure/dn645543.aspx) for these types of applications, and Office 365 supports using this flow.

When using this flow, the app presents its client credentials to the OAuth2 token issuing endpoint, and in return gets an access token that represents the application itself without any user information. The token in this scenario is known as an app-only access token.

There is no need for the app to get a refresh token as when the access token expires, it simply goes back to the OAuth2 token issuing endpoint to get a new one. Also, since there is no user information in the app-only token, the app must specify the user within the API call when using this token.


## Defining permissions
To configure your app for app-only tokens, you first need to specify which permissions your app requires. You specify these permissions in application registration for your app in the Azure management portal for Microsoft Azure Active Directory (Azure AD). Select the application permissions type, as these are directly assigned to the application. See figure 1 for a screenshot of the Azure AD application registration permissions section.

**Figure 1. Configuring application permissions in Azure AD**
![A screenshot that shows the application permissions in the Azure management console.](images\O365_BuildingSvcApps_AppPerms.png)

**Note**  When registering the app in Azure AD, you must select the **Web Application and/or Web API** type, as app-only permissions are not available for native client applications.

## Granting consent and app authentication strength 
Once permissions are specified within the app registration, the app can ask for consent to be available in another Office 365 organization. App permissions must be consented to by an Office 365 tenant administrator. This is because these applications are quite powerful in terms of the data they can access within an Office 365 organization. For example, a service application with the Mail.Read permission that acquires access tokens via the client credential flow can read mail in any mailbox within the Office 365 organization.

Because of the broad access available to these apps, to successfully obtain an access token, apps must also use an X.509 certificate with a public/private key pair. Usage of simple symmetric keys are not allowed, and while the app could get an access token using a symmetric key, the API will return an access denied error for these access tokens. Self-issued X.509 certificates are accepted, but the app must register the public X.509 certificate with the application definition in Azure AD. The app then maintains the private key and uses it to assert its identity to the token issuing endpoint.

You implement the consent flow in a similar way as the authorization code grant flow by sending a request to the OAuth2 authorize endpoint. However once the authorize endpoint redirects back with an authorization code to the app, the remaining code can be ignored; for getting tokens, only the client credentials are necessary. You could build an experience like "Sign-up my Organization" in your app to accomplish the initial one-time consent. The key takeaway here is that you need to make one-time consent part of your daemon or service app configuration.  Once the consent is given, the app can get access tokens and start calling the Office 365 APIs.
### Revoking consent
You can revoke consent to service apps just like any other apps installed by an Office 365 tenant administrator. The administrator can either go to the [Azure management portal](https://manage.windowsazure.com/), find the application in the Application view, select and delete it, or alternatively the administrator can use the [Remove-MSOLServicePrincipal cmdlet](https://msdn.microsoft.com/en-us/library/azure/dn194113.aspx) from the Azure AD module for Windows PowerShell.
## Acquiring an access token with the client credential flow
When requesting app-only tokens, you must use a tenant-specific token issuing endpoint. If you use the common (tenant-independent) endpoint an error is returned.

During the consent process, when the authorize endpoint is hit and a code is delivered in the redirect to the app, your app can request an ID token together with the code. This token is a JSON web token containing the tenant Id as the **tid** claim-type, so you just need to parse this to get the ID for the tenant-specific endpoint.
### Getting an initial ID token with Consent
The following is an example of how to trigger consent using an [OpenID Connect Hybrid Flow](http://openid.net/specs/openid-connect-core-1_0.html#HybridFlowAuth) request:

    GET https://login.microsoftonline.com/common/oauth2/authorize?state=e82ea723-7112-472c-94d4-6e66c0ca52b6&response_type=code+id_token&scope=openid&nonce=c328d2df-43d1-4e4d-a884-7cfb492beadc&client_id=0308CDD9-874D-4F87-85E0-A0DA7E05F999&redirect_uri=https:%2f%2flocalhost:44304%2fHome%2f&resource=https:%2f%2fgraph.windows.net%2f&prompt=admin_consent&response_mode=form_post HTTP/1.1

This request provides your app with the consent flow and redirect back with the code and ID token in a POST request. Your app can ignore the code and get the ID token from the received form data. For more information on form post response mode, see the [OpenID spec](http://openid.net/specs/oauth-v2-form-post-response-mode-1_0-02.html#FormPostResponseExample).

In ASP.Net you can retrieve the ID token via Request.Form["id_token"] on the redirect page, finding the tenant ID in the **tid** claim within the **id_token**.

##Getting an app-only token

The following code snippet shows using the Azure AD client library to acquire an app-only token via the client credential flow:

```cs
//need to address the tenant specific authority/token issuing endpoint
//https://login.microsoftonline.com/<tenant-id>/oauth2/authorize
//retrieved tenantID from ID token for the app during consent flow (authorize flow)
string authority = appConfig.AuthorizationUri.Replace("common", tenantId);
AuthenticationContext authenticationContext = new AuthenticationContext(authority,false);
string certfile = Server.MapPath(appConfig.ClientCertificatePfx);
X509Certificate2 cert = new X509Certificate(certfile,appConfig.ClientCertificatePfxPassword, X509KeyStorageFlags.MachineKeySet);
ClientAssertionCertificate cac = new ClientAssertionCertificate(appConfig.ClientId, cert);
var authenticationResult = await authenticationContext.AcquireTokenAsync(resource, cac);
return authenticationResult.AccessToken;
```
 
The application for this example maintains the private key in a well-protected directory on the web server as a PFX file. However it is better to maintain the private key in more secure storage such as the Windows certificate storage of the computer account.
For a complete sample of a web app using the client credential flow, see the [o365api-as-apponly-webapp sample](https://github.com/mattleib/o365api-as-apponly-webapp).

##Configuring a X.509 public cert for your application

The final part is how to configure an X.509 public certificate for your app. As this is not exposed in the Azure management portal UI, you need to configure this by manually editing the app manifest. To do this, you need to:

- Create a self-issued certificate if you do not have an X.509 certificate already.

- Retrieve the base64 encoded certificate value and thumbprint from a .cer X509 public certificate file using Windows PowerShell.

- Upload the certificate through the app manifest file.
	You can use the [makecert.exe tool](https://msdn.microsoft.com/en-us/library/bfsktky3.aspx), included with the [.NET Framework tools](https://msdn.microsoft.com/en-us/library/d9kh6s92.aspx), to generate a self-issued certificate.

###To generate a self-issued certificate using the makecert.exe tool:

1. From the command line, type and run

	`makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 12/15/2014 -e 12/15/2016 -ss my -len 2048`

2. Open the **Certificates** management console snap-in and connect to your user account.

3. Find the new certificate in the **Personal** folder and export it to a base64-encoded CER file.

	**Note** Make sure the key length is at least 2048 when generating the X.509 certificate. Shorter key length are not accepted as valid keys.

###To get the base64 encoded cert value and thumbprint from a .cer X509 public certificate file

1. From the Windows PowerShell prompt, type and run the following cmdlets:

    ```
$cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$cer.Import("mycer.cer")
$bin = $cer.GetRawCertData()
$base64Value = [System.Convert]::ToBase64String($bin)
$bin = $cer.GetCertHash()
$base64Thumbprint = [System.Convert]::ToBase64String($bin)
$keyid = [System.Guid]::NewGuid().ToString()
```

	**Note** This step shows using Windows PowerShell to get the properties of a x.509 certificate. Other platforms provide similar tools to retrieve properties of certificates.

2. Store the values for **$base64Thumbprint**, **$base64Value** and **$keyid**, as you will need them when you upload the certificate in the next set of steps.

###To upload the certificate through the manifest file

1. Sign in to the [Azure management portal](https://manage.windowsazure.com/).

2. Click **Active Directory** on the left menu, and then click on the desired directory.

3. On the top menu, click **Applications**, and then click the application you want to configure. The **Quick Start** page will appear with single sign-on and other configuration information.

4. Click **Manage manifest** in the command bar, and select **Download manifest**.

5. Open the downloaded file for editing and replace the empty **KeyCredentials** property with the following JSON:

	```json
"keyCredentials": [
    {
      "customKeyIdentifier": "$base64Thumbprint_from_above",
      "keyId": "$keyid_from_above",
      "type": "AsymmetricX509Cert",
      "usage": "Verify",
      "value":  "$base64Value_from_above"
     }
   ], 
```

  for example:

  ```json
"keyCredentials": [
    {
      "customKeyIdentifier": "ieF43L8nkyw/PEHjWvj+PkWebXk=",
      "keyId": "2d6d849e-3e9e-46cd-b5ed-0f9e30d078cc",
      "type": "AsymmetricX509Cert",
      "usage": "Verify",
      "value": "MIICWjCCAgSgAwIBA***omitted for brevity***qoD4dmgJqZmXDfFyQ"
    }
  ],
```

  The [KeyCredentials](http://msdn.microsoft.com/en-us/library/azure/dn151681.aspx) property is a collection, making it possible to upload multiple X.509 certificates for rollover scenarios or delete certificates for compromise scenarios.

6.	Save your changes, and upload the updated app manifest file by clicking **Manage manifest** in the command bar, selecting **Upload manifest**, browsing to your updated manifest file and then selecting it.


  
  
  

