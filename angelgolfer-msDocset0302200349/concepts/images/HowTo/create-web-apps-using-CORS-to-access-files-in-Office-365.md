ms.TocTitle: Create JavaScript web apps using CORS to access files
Title: Create JavaScript web apps using CORS to access Office 365 APIs 
Description: Configure a JavaScript web app to make cross-origin resource sharing (CORS) requests to the Office 365 APIs; get the entire source code of this example.
ms.ContentId: e3c6a490-be58-4967-8be6-29e8b4f4bf8c
ms.topic: article (how-tos)
ms.date: August 13, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]

# Create JavaScript web apps using CORS to access Office 365 APIs

_**Applies to:** Office 365_

The Office 365 APIs provide access to mail, calendars, and contacts from Exchange Online; files and folders from SharePoint Online and OneDrive for Business; users and groups from Azure AD.

It's possible to access all of this data from a JavaScript client application with little to no server code using cross-origin resource sharing (CORS). Developers now have the option to use CORS to send requests to the Office 365 APIs to access, modify, and create data reliably. 

Before you begin using CORS requests to access the Office 365 APIs, you need to [set up your Office 365 development environment](https://msdn.microsoft.com/en-us/office/office365/howto/setup-development-environment). After that, we'll walk you through enabling your JavaScript application to make CORS requests to the Office 365 APIs by: registering your app with Azure Active Directory, determining the resource endpoint, getting an access token, and making an authenticated request to an Office 365 API. 

**Note** Internet Explorer must use Internet Explorer 11 with [MS15-032: Cumulative security update for Internet Explorer (KB3038314)](https://www.microsoft.com/en-us/download/details.aspx?id=46655) installed for this sample to work. 

## Register your app with Azure AD

The first thing you need to do is register your application with Azure AD. Sign in to the [Azure Management Portal](https://manage.windowsazure.com) to get started. Once signed in, follow these instructions: 

1. Click the **Active Directory** node in the left column and select the directory linked to your Office 365 subscription. 

2. Select the **Applications** tab and then **Add** at the bottom of the screen. 

3. On the pop-up, select **Add an application my organization is developing**. 

4. Choose a name for your app, such as *o365-cors-sample*, and select **Web application and/or web API** as its Type. Then click the arrow to continue. 

5. The value of **Sign-on URL** is the URL where your application will be hosted. 

6. The value of **App ID URI** is a unique identifier for Azure AD to identify your app. You can use *http://{your_subdomain}/o365-cors-sample*, where *{your_subdomain}* is the subdomain of **.onmicrosoft** you specified while signing up for your Office 365 Developer Site. Then click the check mark to provision your application. 

7. Now that your app has been provisioned, select the **Configure** tab. 

8. Scroll down to the **permissions to other applications** section and click the **Add application** button. 

9. In this sample, we'll demonstrate how to get a user's files so add the **Office 365 SharePoint Online** application. Click the plus sign in the application's row and then click the check mark at the top right to add it. Then click the check mark at the bottom right to continue.

10. In the **Office 365 SharePoint Online** row, select **Delegated Permissions**, and in the selection list, choose **Read users' files**. 

11. Click **Save** to save the app's configuration. 

### Configure your app to allow the OAuth 2.0 implicit grant flow

In order to get an access token for Office 365 API requests, your application will use the OAuth implicit grant flow. You need to update the application's manifest to allow the OAuth implicit grant flow because it is not allowed by default. 

1. Select the **Configure** tab of your application's entry in the Azure Management Portal. 

2. Using the **Manage Manifest** button in the drawer, download the manifest file for the application and save it to your computer.

3. Open the manifest file with a text editor. Search for the *oauth2AllowImplicitFlow* property. By default it is set to *false*; change it to *true* and save the file.

4. Using the **Manage Manifest** button, upload the updated manifest file.

You've now successfully registered your application with Azure AD. 

## Determine the resource endpoint

In order to make any API requests, you'll need to determine the correct endpoint of the resource you want to use. The endpoint you'll use is determined by what information you want from Office 365. Refer to the API reference documentation to get the endpoint you want. 

* [Mail API reference](https://msdn.microsoft.com/office/office365/APi/mail-rest-operations)

* [Contacts API reference](https://msdn.microsoft.com/office/office365/APi/contacts-rest-operations)

* [Calendar API reference](https://msdn.microsoft.com/office/office365/APi/calendar-rest-operations)

* [Files API reference](https://msdn.microsoft.com/office/office365/APi/files-rest-operations)

Alternatively, you can take advantage of the [Office 365 unified API (preview)](.\office-365-unified-api-overview.md) to access all of the APIs from a single endpoint, ```https://graph.microsoft.com```. Refer to the [Office 365 unified API reference](.\office-365-unified-api-reference.md) to browse all of the supported endpoints. 

For this sample, we will use the Files API to get a user's files. The endpoint for this operation is ```https://{your_subdomain}-my.sharepoint.com/_api/v1.0/me/files```, where ```{your_subdomain}``` is the subdomain of **.onmicrosoft** you specified while signing up for your Office 365 Developer Site. 

**Note** If you are developing a multi-tenant application, you can use the [Discovery Service](https://msdn.microsoft.com/en-us/office/office365/howto/discover-service-endpoints) to determine the endpoints you'll need. However, this is not possible to do in client-side JavaScript applications and will require sever-side code. 

## Get an access token from Azure

Office 365 uses OAuth 2.0 tokens issued by Azure AD to authenticate JavaScript clients. Tokens are obtained using the OAuth 2.0 implicit grant flow. Using implicit grant, your application requests an access token from Azure AD for the currently signed-in user by sending the user to an authorization URL where the user signs in with their Office 365 credentials and then is redirected back to the app with the access token in the URL. 

The following function builds the authorization URL and navigates to it to begin the authentication process.

```javascript
function requestToken() { 
  // Change clientId and replyUrl to reflect your app's values 
  // found on the Configure tab in the Azure Management Portal. 
  // Also change {your_subdomain} to your subdomain for both endpointUrl and resource. 
  var clientId    = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX';
  var replyUrl    = 'http://replyUrl/'; 
  var endpointUrl = 'https://{your_subdomain}-my.sharepoint.com/_api/v1.0/me/files';
  var resource = "https://{your_subdomain}-my.sharepoint.com"; 

  var authServer  = 'https://login.windows.net/common/oauth2/authorize?';  
  var responseType = 'token'; 

  var url = authServer + 
            "response_type=" + encodeURI(responseType) + "&" + 
            "client_id=" + encodeURI(clientId) + "&" + 
            "resource=" + encodeURI(resource) + "&" + 
            "redirect_uri=" + encodeURI(replyUrl); 

  window.location = url; 
}
```

If the user chooses to grant your app access to their Office 365 data, they will be redirected back to your app with the access token in the URL. The function below gets called whenever the page loads and checks for the access token in the URL and extracts it if it's present. 

```javascript
var urlParameterExtraction = new (function () { 
  function splitQueryString(queryStringFormattedString) { 
    var split = queryStringFormattedString.split('&'); 

    // If there are no parameters in URL, do nothing.
    if (split == "") {
      return {};
    } 

    var results = {}; 

    // If there are parameters in URL, extract key/value pairs. 
    for (var i = 0; i < split.length; ++i) { 
      var p = split[i].split('=', 2); 
      if (p.length == 1) 
        results[p[0]] = ""; 
      else 
        results[p[0]] = decodeURIComponent(p[1].replace(/\+/g, " ")); 
    } 

    return results; 
  } 
  
  // Split the query string (after removing preceding '#'). 
  this.queryStringParameters = splitQueryString(window.location.hash.substr(1)); 
})(); 

// Extract token from urlParameterExtraction object.
var token = urlParameterExtraction.queryStringParameters['access_token']; 
```

Now you have an access token to authenticate your CORS requests to the Office 365 APIs. 

## Make an authenticated request to an Office 365 API

At this point, you've registered your app with Azure AD, determined the correct endpoint for the resource you want access to, and have been granted an access token from Azure AD. All that's left to do is to use these pieces to make an HTTP request to the API. You'll do this by sending off an ```XMLHttpRequest``` to the Files API endpoint with the OAuth access token attached to the Authorization header of the request. 

The function below makes the request and puts the content of the response on a DOM element with an ID equal to *results*. 

```javascript
function getFilesFromO365() { 
  try 
  { 
    var endpointUrl = 'https://{your_subdomain}-my.sharepoint.com/_api/v1.0/me/files'; 
    var xhr = new XMLHttpRequest(); 
    xhr.open("GET", endpointUrl); 

    // The APIs require an OAuth access token in the Authorization header, formatted like this: 'Authorization: Bearer <token>'. 
    xhr.setRequestHeader("Authorization", "Bearer " + token); 

    // Process the response from the API.  
    xhr.onload = function () { 
      if (xhr.status == 200) { 
        var formattedResponse = JSON.stringify(JSON.parse(xhr.response), undefined, 2);
        document.getElementById("results").textContent = formattedResponse; 
      } else { 
        document.getElementById("results").textContent = "HTTP " + xhr.status + "<br>" + xhr.response; 
      } 
    } 

    // Make request.
    xhr.send(); 
  } 
  catch (err) 
  {  
    document.getElementById("results").textContent = "Exception: " + err.message; 
  } 
}  
```

The response object of the ```XMLHttpRequest``` contains the Office 365 data. In this example it's the files of the signed-in user or an error explaining why the request could not be completed. 

## Next steps

You've now walked through how to enable your JavaScript client application to make requests to the Office 365 APIs using CORS. Note that this is a simple example on how you can use CORS in client-side JavaScript applications and that you should look into [ADAL JS](https://github.com/AzureAD/azure-activedirectory-library-for-js), the Azure Active Directory Library for JavaScript, and [Create an Angular app with Office 365 APIs](..\howto\getting-started-Office-365-APIs.md?javascript) if you want to build larger scale, production applications. This library will handle the Azure AD authentication in your single-page applications for you.  

Below is the source code of this example in its entirety so you can get a clearer idea on how the pieces work together. 

**Note** If you want to host this example code somewhere, don't forget to configure the ```clientId``` and ```replyUrl``` values in the **getToken** function to your application's values found in the Azure Management Portal, as well as change the ```{your-subdomain}``` part of the ```resource``` variable to your subdomain. 

```javascript
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"> 
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <title>O365 CORS Sample</title>
    <style> 
      body { 
        font-family:'Segoe UI'; 
      } 

      .paddedElement {
        margin-top: 5px; 
      }

      .hidden {
        visibility: hidden; 
      }
    </style>
  </head>
  <body>
    <h2>O365 CORS Sample</h2>
    <label for="TxtOauthToken">OAuth Token: </label><input type="text" id="TxtOauthToken" size="80"/>
    <br />
    <label for="endpointUrl">Endpoint URL: </label><input type="text" id="endpoint" size="80" /> 
    <br />
    <input type="button" class="paddedElement" id="getToken" value="Get Token"> 
    <input type="button" class="paddedElement" id="doCors" value="Make CORS Request" visibility="hidden" />
    <br /> 
    <br />
    <label for="results" class="hidden paddedElement" id="resultHeading">Results: </label>
    <br />
    <label id="debugMessage"></label>
    <pre id="results"></pre>
    <script type="text/javascript"> 
      (function (window) { 
        var isCorsCompatible = function() {
          try
          {
              var xhr = new XMLHttpRequest();
              xhr.open("GET", getEndpointUrl());
              xhr.setRequestHeader("authorization", "Bearer " + token);
              xhr.setRequestHeader("accept", "application/json");
              xhr.onload = function () {
                 // CORS is working.
                 console.log("Browser is CORS compatible."); 
              }
              xhr.send();
          }
          catch (e)
          {
              if (e.number == -2147024891)
              {
                  console.log("Internet Explorer users must use Internet Explorer 11 with MS15-032: Cumulative security update for Internet Explorer (KB3038314) installed for this sample to work.");
              }
              else
              {
                  console.log("An unexpected error occurred. Please refresh the page."); 
              }

          }
        };

        var urlParameterExtraction = new (function () { 
          function splitQueryString(queryStringFormattedString) { 
            var split = queryStringFormattedString.split('&'); 

            // If there are no parameters in URL, do nothing.
            if (split == "") {
              return {};
            } 

            var results = {}; 

            // If there are parameters in URL, extract key/value pairs. 
            for (var i = 0; i < split.length; ++i) { 
              var p = split[i].split('=', 2); 
              if (p.length == 1) 
                results[p[0]] = ""; 
              else 
                results[p[0]] = decodeURIComponent(p[1].replace(/\+/g, " ")); 
            } 

            return results; 
          } 

          // Split the query string (after removing preceding '#'). 
          this.queryStringParameters = splitQueryString(window.location.hash.substr(1)); 
        })(); 

        var token = urlParameterExtraction.queryStringParameters['access_token']; 

        if (token == undefined) {
          document.getElementById("TxtOauthToken").value = "Click \"Get Token\" to trigger sign-in after entering the endpoint you want to use."; 

          document.getElementById("doCors").style.visibility = "hidden"; 
        }
        else {
          document.getElementById("TxtOauthToken").value = token;
          document.getElementById("doCors").style.visibility = "visible"; 
          document.getElementById("getToken").style.display = "none"; 
        }

        // Constructs the authentication URL and directs the user to it. 
        function requestToken() { 
          // Change clientId and replyUrl to reflect your app's values 
          // found on the Configure tab in the Azure Management Portal.
          var clientId    = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX';
          var replyUrl    = 'http://replyUrl/';
          var resource    = "https://{your_domain}-my.sharepoint.com";

          var authServer  = 'https://login.windows.net/common/oauth2/authorize?'; 
          var endpointUrl = getEndpointUrl();

          var responseType = 'token'; 

          var url = authServer + 
                    "response_type=" + encodeURI(responseType) + "&" + 
                    "client_id=" + encodeURI(clientId) + "&" + 
                    "resource=" + encodeURI(resource) + "&" + 
                    "redirect_uri=" + encodeURI(replyUrl); 
 
          window.location = url; 
        } 

        document.getElementById("getToken").onclick = requestToken; 

        function getEndpointUrl() { 
          return document.getElementById("endpoint").value; 
        } 

        function getFilesFromO365() { 
          document.getElementById("results").textContent = ""; 

          // Check browser compatbility. Check console output for details.
          isCorsCompatible(); 

          try 
          { 
            var xhr = new XMLHttpRequest(); 
            xhr.open("GET", getEndpointUrl()); 

            // The APIs require an OAuth access token in the Authorization header, formatted like this: 'Authorization: Bearer <token>'. 
            xhr.setRequestHeader("Authorization", "Bearer " + token); 

            // Process the response from the API.  
            xhr.onload = function () { 
              document.getElementById("resultHeading").style.visibility = "visible"; 

              if (xhr.status == 200) { 
                var formattedResponse = JSON.stringify(JSON.parse(xhr.response), undefined, 2);
                document.getElementById("results").textContent = formattedResponse; 
              } else { 
                document.getElementById("results").textContent = "HTTP " + xhr.status + "<br>" + xhr.response; 
              } 
            } 

            // Make request.
            xhr.send(); 
          } 
          catch (err) 
          { 
            document.getElementById("resultHeading").style.visibility = "visible"; 
            document.getElementById("results").textContent = "Exception: " + err.message; 
          } 
        } 

        document.getElementById("doCors").onclick = getFilesFromO365; 

      })(window); 
    </script> 
  </body>
</html>
```

## Additional resources

**Code Samples**

-  [Office 365 APIs starter projects and code samples](..\howto\Starter-projects-and-code-samples.md) 
-  [Office Developer on GitHub](https://github.com/OfficeDev)

**Reference**

-  [Create an Angular app with Office 365 APIs](..\howto\getting-started-Office-365-APIs.md?javascript)
-  [Office 365 REST APIs reference](..\api\API-Catalog.md)
-  [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js)