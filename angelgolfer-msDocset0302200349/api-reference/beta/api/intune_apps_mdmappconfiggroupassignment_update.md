﻿# Update mdmAppConfigGroupAssignment

> **Important:** APIs under the /beta version in Microsoft Graph are in preview and are subject to change. Use of these APIs in production applications is not supported.

> **Note:** Using the Microsoft Graph APIs to configure Intune controls and policies still requires that the Intune service is [correctly licensed](https://go.microsoft.com/fwlink/?linkid=839381) by the customer.

Update the properties of a [mdmAppConfigGroupAssignment](../resources/intune_apps_mdmappconfiggroupassignment.md) object.
## Prerequisites
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](../../../concepts/permissions_reference.md).

|Permission type|Permissions (from most to least privileged)|
|:---|:---|
|Delegated (work or school account)|DeviceManagementApps.ReadWrite.All|
|Delegated (personal Microsoft account)|Not supported.|
|Application|Not supported.|

## HTTP Request
<!-- {
  "blockType": "ignored"
}
-->
``` http
PATCH /deviceAppManagement/mobileAppConfigurations/{managedDeviceMobileAppConfigurationId}/groupAssignments/{mdmAppConfigGroupAssignmentId}
```

## Request headers
|Header|Value|
|:---|:---|
|Authorization|Bearer &lt;token&gt; Required.|
|Accept|application/json|

## Request body
In the request body, supply a JSON representation for the [mdmAppConfigGroupAssignment](../resources/intune_apps_mdmappconfiggroupassignment.md) object.

The following table shows the properties that are required when you create the [mdmAppConfigGroupAssignment](../resources/intune_apps_mdmappconfiggroupassignment.md).

|Property|Type|Description|
|:---|:---|:---|
|appConfiguration|String|The navigation link to the mdm app Configuration being targeted.|
|targetGroupId|String|The Id of the AAD group we are targeting the mdm app configuration to.|
|id|String|Key of the entity.|



## Response
If successful, this method returns a `200 OK` response code and an updated [mdmAppConfigGroupAssignment](../resources/intune_apps_mdmappconfiggroupassignment.md) object in the response body.

## Example
### Request
Here is an example of the request.
``` http
PATCH https://graph.microsoft.com/beta/deviceAppManagement/mobileAppConfigurations/{managedDeviceMobileAppConfigurationId}/groupAssignments/{mdmAppConfigGroupAssignmentId}
Content-type: application/json
Content-length: 98

{
  "appConfiguration": "App Configuration value",
  "targetGroupId": "Target Group Id value"
}
```

### Response
Here is an example of the response. Note: The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.
``` http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 213

{
  "@odata.type": "#microsoft.intune_apps_graph.mdmAppConfigGroupAssignment",
  "appConfiguration": "App Configuration value",
  "targetGroupId": "Target Group Id value",
  "id": "347b9b52-9b52-347b-529b-7b34529b7b34"
}
```



