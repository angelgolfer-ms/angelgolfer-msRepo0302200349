---
ms.Toctitle: HTTP response status codes
title: Office 365 HTTP response status codes
description: Locate error codes and status information for Office 365 APIs.
ms.date: May 26, 2016
---

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]


# HTTP response status codes

_**Applies to:** Office 365_

Microsoft web servers use HTTP Response Status Codes to communicate responses when processing requests. 

For a complete description of HTTP Status Codes, see [List of HTTP status codes](http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml#http-status-codes-1).

The following table lists the most common status codes returned by Microsoft web servers.

|HTTP status code| HTTP status description| Description|
|:-----|:-----|:-----|
|200|	OK| No error; the request is successful|
|201|	Created|	No error; a new entity was created|
|202|	Accepted|	No error; the request was accepted for processing|
|204|	No Content|	Request succeeded, response is empty|
|400|	Bad Request|	Invalid parameter passed|
|401|	Unauthorized|	The request requires user authentication|
|403|	Forbidden|	Use has insufficient access rights for the attempted operation| 
|404|	Not Found|	Invalid URI|
|405|	MethodNotAllowed|	The method or content type requested is not supported|
|406|	NotAcceptable|	The content type requested is not supported|
|410|	Gone|	The requested entity no longer exists|
|415|	UnsupportedMediaType|	The content type requested is not supported|
|429|	Too Many Requests|	Rate limit exceeded|
|500|	Internal| Server Error	Transaction failed|
|501|	NotImplemented|	Request failed, future implementation is likely|
|503|	Service Unavailable|	System unavailable; try again later|

## JSON reponses

For the format Microsoft follows when responding via JSON, see [Error Responses in OData JSON Format Version 4.0 Plus Errata 02](http://docs.oasis-open.org/odata/odata-json-format/v4.0/errata02/os/odata-json-format-v4.0-errata02-os-complete.html#_Toc403940655).

## Response example

An error response might contain [annotations](http://docs.oasis-open.org/odata/odata-json-format/v4.0/errata02/os/odata-json-format-v4.0-errata02-os-complete.html#_Instance_Annotations) in any of its JSON objects.
```json
{
  "error": {
    "code": "501",
    "message": "Unsupported functionality",
    "target": "query",
    "details": [
      {
       "code": "301",
       "target": "$search" 
       "message": "$search query option not supported",
      }
    ],
    "innererror": {
      "trace": [...],
      "context": {...}
    }
  }
}

```

