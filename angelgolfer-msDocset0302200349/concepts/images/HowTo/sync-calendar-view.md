ms.TocTitle: Sync events in calendar view
Title: Synchronize events in an Outlook calendar view
Description: See a step-by-step example to synchronize events in a specific time range in the user's calendar.
ms.ContentId: afcf00f0-9222-470c-bb2b-a0f5e1a63a30
ms.topic: article (how-tos)
ms.date: June 29, 2016

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]

#Synchronize events in an Outlook calendar view

_**Applies to:** Exchange Online | Office 365 | Hotmail.com | Live.com | MSN.com | Outlook.com | Passport.com_

The API to synchronize events applies to calendar data secured by Azure Active Directory on 
Office 365, and to similar data in Microsoft accounts specifically in these domains: Hotmail.com, 
Live.com, MSN.com, Outlook.com, and Passport.com.


You can use the Outlook Calendar REST API to synchronize and get new, modified, or deleted events within a specific time range 
from a user's calendar. The API to [sync a calendar view](..\api\calendar-rest-operations.md#SyncCalendarView) is a GET operation 
on a calendar view which specifies:
- The specific calendar to sync in
- Start and end dates for the range of events to sync
- Special request headers that differentiate this GET operation from a [GET calendar view](..\api\calendar-rest-operations.md#GetCalendarView) 
operation:
  - "Prefer: odata.track-changes" - you must include this header in all sync requests except for those that include a 
  `skipToken` (further explained in step 2 below).  
  - "Prefer: odata.maxpagesize={x}" - you can include this header to specify the maximum number of full events that the sync
  request returns at one time.

Synchronizing a calendar view can involve one or more sync requests; each sync request is a GET call.
The number of GET calls you need to sync a calendar view depends on the "delta" (how many new, updated or deleted events) in the 
specified time range, and the `maxpagesize` you specify for each GET call. After you have synchronized a calendar
view with a round of GET calls, further attempts to sync will return no more delta's, until events in that calendar view are 
added, modified or deleted again.

<a name="SyncCalendarViewWorkflow"> </a>
## Workflow to sync a calendar view

The following describes how multiple GET calls are chained in a typical round of synchronization.

![Initial synchronization requests returns a deltalink. Use the deltaToken and any subsequent skipToken to make the next request. If a deltalink is returned again, the client is synchronized with the service.](images\O365API_SyncCalView_Process.png) 

1. [Initial sync request](#SampleInitialSyncReq): The very first sync request sets up the sync state.  
2. [Initial sync response](#SampleInitialSyncResponse): 
  - Check for "Preference-Applied: odata.track-changes" in the response header to confirm a successful sync attempt and the 
resource supports synchronization.
  - If the sync attempt was successful, the initial response always contains an `@odata.deltaLink` with a `deltaToken` value. 
  If the response contains any data, save the `deltaToken` value for the second request.
  - If the initial response wasn't successful, or doesn't return any data indicating there are no events in the specified calendar view,
    this round of sync ends.  
3. Subsequent sync request: Use the `deltaToken` or `skipToken` value from the previous request to issue the next request. See 
the [second](#SampleSecondSyncReq) and [third](#SampleThirdSyncReq) sync requests as examples.
4. [Subsequent sync response](#SampleSecondSyncResponse):
  - If the response returns any data, and, there is more data to sync in that time range, the response would 
include an `@odata.nextLink` and a `skipToken` value. Save the `skipToken` for the next sync request.
  - Go back to step 3, follow the `nextLink`, if any, apply the corresponding `skipToken` value in the next sync request, 
  and follow any subsequent `nextLink`, until you have synchronized all the data in the time range for that calendar.
5. [Final sync response](#SampleThirdSyncResponse): When all events in the calendar view are synchronized, the final response in this round would include 
an `@odata.deltaLink` and a `deltaToken` again. Save the `deltaToken` value for the next round of synchronization.

The very first round of sync requests gets all the events within the specified time range and calendar. 
Using the `deltaToken` value from the previous round, the next round of sync will return only the differences 
(newly added, modified or deleted events) since the last round. 
 

<a name="SyncCalendarViewRecurrence"> </a>
## Recurring events and synchronization

Here's the information you need to know about how recurring events are handled for calendar view synchronization.

- The service performs meeting expansion and sends the series master event and all of the event instances within the time window.
- The series master event contains the recurrence pattern and the time window for the series. 
- The event instances contain their start and end time information as well as information about event occurrence exception. 


<a name="SyncCalendarViewDeletions"> </a>
## Deleted events and synchronization
Deleted events will contain a reason property with the value of "deleted" to indicate a deleted entity. 
If the event is  a recurring master event, you should delete all of the occurrences and exceptions. 



<a name="NextSteps"> </a>
## Next steps

Whether you're ready to start building an app or just want to learn more, we've got you covered.


- Ready to get started? Start by [setting up your environment](..\howto\setup-development-environment.md), then check out our [first app walkthrough](..\howto\getting-started-Office-365-APIs.md).
    
- Explore the Office 365 APIs using the interactive [API Sandbox](http://apisandbox.msdn.microsoft.com/).

- Want samples? [We've got them](..\howto\starter-projects-and-code-samples.md).
    

Or, learn more about using the Office 365 platform:

- [Overview of developing on the Office 365 platform](..\howto\platform-development-overview.md)
    
- [Office 365 app authentication and resource authorization](..\howto\common-app-authentication-tasks.md)
    
- [Manually register your app with Azure AD so it can access Office 365 APIs](..\howto\add-common-consent-manually.md)
  
- [Calendar REST APIs operations reference](..\api\calendar-rest-operations.md)

- [Discovery Service REST API operations reference](..\api\discovery-service-rest-operations.md)

- [Resource reference for the Mail, Calendar, and Contacts REST APIs](..\api\complex-types-for-mail-contacts-calendar.md)

<a name="SyncCalendarViewSamples"> </a>

## Appendix: Sample sync requests and responses

This section contains a round of 3 sync requests and responses for a time range in the user's default calendar.

<a name="SampleInitialSyncReq"> </a>

### Initial sync request

```
GET https://outlook.office.com/api/v2.0/me/calendarview?startDateTime=2015-04-25T00:00:00Z&endDateTime=2015-05-30T00:00:00Z HTTP/1.1
```

The request header includes the following 2 lines, requesting up to 3 full events for the sync response.
```
Prefer: odata.track-changes
Prefer: odata.maxpagesize=3
```

<a name="SampleInitialSyncResponse"> </a>

### Initial sync response

The response header includes these lines, indicating the sync attempt was successful:
```
HTTP/1.1 200 OK
Preference-Applied: odata.track-changes
```

The response body contains 3 single events without recurrences, and includes an `@odata.deltaLink` with a `deltaToken` value. 
```
{
    "@odata.context": "https://outlook.office.com/api/v2.0/$metadata#Me/CalendarView",
    "value": [
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE1M2==_bs88AAAFKPQUAAA=')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAABSlf9A==\"",
            "Id": "AAMkAGE1M2==_bs88AAAFKPQUAAA=",
            "ChangeKey": "mODEKWhc/Um6lA3uPm7PPAAABSlf9A==",
            "Categories": [
            ],
            "DateTimeCreated": "2015-04-24T23:18:44.1912484Z",
            "DateTimeLastModified": "2015-04-24T23:18:44.8932487Z",
            "Subject": "Bug bash",
            "BodyPreview": "Let's get this right!",
            "Body": {
                "ContentType": "HTML",
                "Content": "<html>\r\n<head>\r\n<meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\">\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n"
            },
            "Importance": "Normal",
            "HasAttachments": false,
            "Start": "2015-04-24T23:30:00Z",
            "StartTimeZone": "Pacific Standard Time",
            "End": "2015-04-25T00:00:00Z",
            "EndTimeZone": "Pacific Standard Time",
            "Reminder": 15,
            "Location": {
                "DisplayName": "My house",
                "Address": {
                    "Street": "",
                    "City": "",
                    "State": "",
                    "CountryOrRegion": "",
                    "PostalCode": ""
                },
                "Coordinates": {
                    "Accuracy": "NaN",
                    "Altitude": "NaN",
                    "AltitudeAccuracy": "NaN",
                    "Latitude": "NaN",
                    "Longitude": "NaN"
                }
            },
            "ResponseStatus": {
                "Response": "Organizer",
                "Time": "0001-01-01T00:00:00Z"
            },
            "ShowAs": "Busy",
            "IsAllDay": false,
            "IsCancelled": false,
            "IsOrganizer": true,
            "ResponseRequested": true,
            "Type": "SingleInstance",
            "SeriesMasterId": null,
            "Attendees": [
                {
                    "EmailAddress": {
                        "Address": "may@contoso.com",
                        "Name": "May Walton"
                    },
                    "Status": {
                        "Response": "None",
                        "Time": "0001-01-01T00:00:00Z"
                    },
                    "Type": "Required"
                }
            ],
            "Recurrence": null,
            "Organizer": {
                "EmailAddress": {
                    "Address": "chasity@contoso.com",
                    "Name": "Chasity Bonner"
                }
            },
            "iCalUId": "040000008200==F283EB",
            "WebLink": "https://contoso.com/owa/?ItemID=AAMkAGE1M2%3D%3D%2Bbs88AAAAAAENAACY4MQpaFz9SbqUDe4%2Bbs88AAAFKPQUAAA%3D&exvsurl=1&viewmodel=ICalendarItemDetailsViewModelFactory"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE1M2==_bs88AAAFKPQXAAA=')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAABSlf+A==\"",
            "Id": "AAMkAGE1M2==_bs88AAAFKPQXAAA=",
            "ChangeKey": "mODEKWhc/Um6lA3uPm7PPAAABSlf+A==",
            "Categories": [
            ],
            "DateTimeCreated": "2015-04-25T03:23:32.2628681Z",
            "DateTimeLastModified": "2015-04-25T03:23:32.2784683Z",
            "Subject": "Dinner!",
            "BodyPreview": "",
            "Body": {
                "ContentType": "HTML",
                "Content": "<html>\r\n<head>\r\n<meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\">\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n"
            },
            "Importance": "Normal",
            "HasAttachments": false,
            "Start": "2015-04-25T01:00:00Z",
            "StartTimeZone": "Eastern Standard Time",
            "End": "2015-04-25T01:30:00Z",
            "EndTimeZone": "Eastern Standard Time",
            "Reminder": 15,
            "Location": {
                "DisplayName": "Kitchen",
                "Address": {
                    "Street": "",
                    "City": "",
                    "State": "",
                    "CountryOrRegion": "",
                    "PostalCode": ""
                },
                "Coordinates": {
                    "Accuracy": "NaN",
                    "Altitude": "NaN",
                    "AltitudeAccuracy": "NaN",
                    "Latitude": "NaN",
                    "Longitude": "NaN"
                }
            },
            "ResponseStatus": {
                "Response": "Organizer",
                "Time": "0001-01-01T00:00:00Z"
            },
            "ShowAs": "Busy",
            "IsAllDay": false,
            "IsCancelled": false,
            "IsOrganizer": true,
            "ResponseRequested": true,
            "Type": "SingleInstance",
            "SeriesMasterId": null,
            "Attendees": [
            ],
            "Recurrence": null,
            "Organizer": {
                "EmailAddress": {
                    "Address": "chasity@contoso.com",
                    "Name": "Chasity Bonner"
                }
            },
            "iCalUId": "040000008200==4F6A35",
            "WebLink": "https://contoso.com/owa/?ItemID=AAMkAGE1M2%3D%3D%2Bbs88AAAFKPQXAAA%3D&exvsurl=1&viewmodel=ICalendarItemDetailsViewModelFactory"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE1M2==_bs88AAAFKPQcAAA=')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAABSlgBw==\"",
            "Id": "AAMkAGE1M2==_bs88AAAFKPQcAAA=",
            "ChangeKey": "mODEKWhc/Um6lA3uPm7PPAAABSlgBw==",
            "Categories": [
            ],
            "DateTimeCreated": "2015-04-26T02:54:03.4260923Z",
            "DateTimeLastModified": "2015-04-26T02:54:03.6132924Z",
            "Subject": "Discuss all the REST API",
            "BodyPreview": "I think it will meet our requirements!",
            "Body": {
                "ContentType": "HTML",
                "Content": "<html>\r\n<head>\r\n<meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\">\r\n</head>\r\n<body>\r\nI think it will meet our requirements!\r\n</body>\r\n</html>\r\n"
            },
            "Importance": "Normal",
            "HasAttachments": false,
            "Start": "2015-04-26T02:00:00Z",
            "StartTimeZone": "Pacific Standard Time",
            "End": "2015-04-26T03:00:00Z",
            "EndTimeZone": "Pacific Standard Time",
            "Reminder": 15,
            "Location": {
                "DisplayName": "",
                "Address": null,
                "Coordinates": null
            },
            "ResponseStatus": {
                "Response": "Organizer",
                "Time": "0001-01-01T00:00:00Z"
            },
            "ShowAs": "Busy",
            "IsAllDay": false,
            "IsCancelled": false,
            "IsOrganizer": true,
            "ResponseRequested": true,
            "Type": "SingleInstance",
            "SeriesMasterId": null,
            "Attendees": [
                {
                    "EmailAddress": {
                        "Address": "kristopher@contoso.com",
                        "Name": "Kristopher Nemeth"
                    },
                    "Status": {
                        "Response": "None",
                        "Time": "0001-01-01T00:00:00Z"
                    },
                    "Type": "Required"
                }
            ],
            "Recurrence": null,
            "Organizer": {
                "EmailAddress": {
                    "Address": "chasity@contoso.com",
                    "Name": "Chasity Bonner"
                }
            },
            "iCalUId": "040000008200==D1D0BF",
            "WebLink": "https://contoso.com/owa/?ItemID=AAMkAGE1M2%3D%3D%2Bbs88AAAAAAENAACY4MQpaFz9SbqUDe4%2Bbs88AAAFKPQcAAA%3D&exvsurl=1&viewmodel=ICalendarItemDetailsViewModelFactory"
        }
    ],
    "@odata.deltaLink": "https://outlook.office.com/api/v2.0/me/calendarview/?startDateTime=2015-04-25T00%3a00%3a00Z&endDateTime=2015-05-30T00%3a00%3a00Z&%24deltatoken=d17ffb043b724d3c9521e8464ed318d6"
}
```

<a name="SampleSecondSyncReq"> </a>

### Second sync request

The second sync request uses the `deltaToken` value from the first response.

```
GET https://outlook.office.com/api/v2.0/me/calendarview?startDateTime=2015-04-25T00:00:00Z&endDateTime=2015-05-30T00:00:00Z&$deltatoken=d17ffb043b724d3c9521e8464ed318d6 HTTP/1.1
```

The request header includes the following 2 lines:
```
Prefer: odata.track-changes
Prefer: odata.maxpagesize=3
```


<a name="SampleSecondSyncResponse"> </a>

### Second sync response

The second response header includes this line, indicating the sync attempt was successful:
```
HTTP/1.1 200 OK
```

The second response body contains a series master event, 2 single instances, and 5 occurrences associated with the series master event. 
The response body also includes an `@odata.nextLink` with a `skipToken` value.
```
{
    "@odata.context": "https://outlook.office.com/api/v2.0/$metadata#Me/CalendarView/$delta",
    "value": [
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE==_bs88AAAFKPQVAAA=')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAAB7h3QQ==\"",
            "Id": "AAMkAGE==_bs88AAAFKPQVAAA=",
            "ChangeKey": "mODEKWhc/Um6lA3uPm7PPAAAB7h3QQ==",
            "Categories": [
            ],
            "DateTimeCreated": "2015-04-25T00:18:24.7188484Z",
            "DateTimeLastModified": "2015-04-29T01:27:42.8480225Z",
            "Subject": "Little nap",
            "BodyPreview": "",
            "Body": {
                "ContentType": "HTML",
                "Content": "<html>\r\n<head>\r\n<meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\">\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n"
            },
            "Importance": "Normal",
            "HasAttachments": false,
            "Start": "2015-04-25T00:30:00Z",
            "StartTimeZone": "Pacific Standard Time",
            "End": "2015-04-25T01:00:00Z",
            "EndTimeZone": "Pacific Standard Time",
            "Reminder": 15,
            "Location": {
                "DisplayName": "In the sun",
                "Address": {
                    "Street": "",
                    "City": "",
                    "State": "",
                    "CountryOrRegion": "",
                    "PostalCode": ""
                },
                "Coordinates": {
                    "Accuracy": "NaN",
                    "Altitude": "NaN",
                    "AltitudeAccuracy": "NaN",
                    "Latitude": "NaN",
                    "Longitude": "NaN"
                }
            },
            "ResponseStatus": {
                "Response": "Organizer",
                "Time": "0001-01-01T00:00:00Z"
            },
            "ShowAs": "Busy",
            "IsAllDay": false,
            "IsCancelled": false,
            "IsOrganizer": true,
            "ResponseRequested": true,
            "Type": "SeriesMaster",
            "SeriesMasterId": null,
            "Attendees": [
            ],
            "Recurrence": {
                "Pattern": {
                    "Type": "Daily",
                    "Interval": 1,
                    "Month": 0,
                    "Index": "First",
                    "FirstDayOfWeek": "Sunday",
                    "DayOfMonth": 0
                },
                "Range": {
                    "Type": "EndDate",
                    "StartDate": "2015-04-24T00:00:00-07:00",
                    "EndDate": "2015-04-28T00:00:00-07:00",
                    "NumberOfOccurrences": 0
                }
            },
            "Organizer": {
                "EmailAddress": {
                    "Address": "chasity@contoso.com",
                    "Name": "Chasity Bonner"
                }
            },
            "iCalUId": "040000008200==C98B54",
            "WebLink": "https://contoso.com/owa/?ItemID=AAMkAGE%3D%3D%2Bbs88AAAFKPQVAAA%3D&exvsurl=1&viewmodel=ICalendarItemDetailsViewModelFactory"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE==_bs88AAAFKPQdAAA=')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAABSlgCg==\"",
            "Id": "AAMkAGE==_bs88AAAFKPQdAAA=",
            "ChangeKey": "mODEKWhc/Um6lA3uPm7PPAAABSlgCg==",
            "Categories": [
            ],
            "DateTimeCreated": "2015-04-26T02:54:17.4192923Z",
            "DateTimeLastModified": "2015-04-26T02:54:17.6064929Z",
            "Subject": "Discuss all the REST API",
            "BodyPreview": "I think it will meet our requirements!",
            "Body": {
                "ContentType": "HTML",
                "Content": "<html>\r\n<head>\r\n<meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\">\r\n</head>\r\n<body>\r\nI think it will meet our requirements!\r\n</body>\r\n</html>\r

\n"
            },
            "Importance": "Normal",
            "HasAttachments": false,
            "Start": "2015-04-26T02:00:00Z",
            "StartTimeZone": "Pacific Standard Time",
            "End": "2015-04-26T03:00:00Z",
            "EndTimeZone": "Pacific Standard Time",
            "Reminder": 15,
            "Location": {
                "DisplayName": "",
                "Address": null,
                "Coordinates": null
            },
            "ResponseStatus": {
                "Response": "Organizer",
                "Time": "0001-01-01T00:00:00Z"
            },
            "ShowAs": "Busy",
            "IsAllDay": false,
            "IsCancelled": false,
            "IsOrganizer": true,
            "ResponseRequested": true,
            "Type": "SingleInstance",
            "SeriesMasterId": null,
            "Attendees": [
                {
                    "EmailAddress": {
                        "Address": "diana@contoso.com",
                        "Name": "Diana Michael"
                    },
                    "Status": {
                        "Response": "None",
                        "Time": "0001-01-01T00:00:00Z"
                    },
                    "Type": "Required"
                }
            ],
            "Recurrence": null,
            "Organizer": {
                "EmailAddress": {
                    "Address": "chasity@contoso.com",
                    "Name": "Chasity Bonner"
                }
            },
            "iCalUId": "040000008200==CDA6AD",
            "WebLink": "https://contoso.com/owa/?ItemID=AAMkAGE%3D%3D%2Bbs88AAAFKPQdAAA%3D&exvsurl=1&viewmodel=ICalendarItemDetailsViewModelFactory"
        },

        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE==_bs88AAAKB6KtAAA=')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAACgkNZA==\"",
            "Id": "AAMkAGE==_bs88AAAKB6KtAAA=",
            "ChangeKey": "mODEKWhc/Um6lA3uPm7PPAAACgkNZA==",
            "Categories": [
            ],
            "DateTimeCreated": "2015-05-05T11:15:43.0696852Z",
            "DateTimeLastModified": "2015-05-05T11:15:43.1944851Z",
            "Subject": "Outlook APIs talk",
            "BodyPreview": "",
            "Body": {
                "ContentType": "HTML",
                "Content": "<html>\r\n<head>\r\n<meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\">\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n"
            },
            "Importance": "Normal",
            "HasAttachments": false,
            "Start": "2015-05-06T17:30:00Z",
            "StartTimeZone": "Pacific Standard Time",
            "End": "2015-05-06T18:30:00Z",
            "EndTimeZone": "Pacific Standard Time",
            "Reminder": 15,
            "Location": {
                "DisplayName": "Downtown park",
                "Address": {
                    "Street": "",
                    "City": "",
                    "State": "",
                    "CountryOrRegion": "",
                    "PostalCode": ""
                },
                "Coordinates": {
                    "Accuracy": "NaN",
                    "Altitude": "NaN",
                    "AltitudeAccuracy": "NaN",
                    "Latitude": "NaN",
                    "Longitude": "NaN"
                }
            },
            "ResponseStatus": {
                "Response": "NotResponded",
                "Time": "0001-01-01T00:00:00Z"
            },
            "ShowAs": "Tentative",
            "IsAllDay": false,
            "IsCancelled": false,
            "IsOrganizer": false,
            "ResponseRequested": true,
            "Type": "SingleInstance",
            "SeriesMasterId": null,
            "Attendees": [
                {
                    "EmailAddress": {
                        "Address": "Donovan@contoso.com",
                        "Name": "Donovan Sandberg"
                    },
                    "Status": null,
                    "Type": "Required"
                },
                {
                    "EmailAddress": {
                        "Address": "may@contoso.com",
                        "Name": "May Walton"
                    },
                    "Status": null,
                    "Type": "Required"
                },
                {
                    "EmailAddress": {
                        "Address": "Kristopher@contoso.com",
                        "Name": "Kristopher Nemeth"
                    },
                    "Status": null,
                    "Type": "Required"
                }
            ],
            "Recurrence": null,
            "Organizer": {
                "EmailAddress": {
                    "Address": "Donovan@contoso.com",
                    "Name": "Donovan Sandberg"
                }
            },
            "iCalUId": "040000008200==C81231",
            "WebLink": "https://contoso.com/owa/?ItemID=AAMkAGE%3D%3d%2Bbs88AAAKB6KtAAA%3D&exvsurl=1&viewmodel=ICalendarItemDetailsViewModelFactory"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAAB7h3QQ==\"",
            "Id": "AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==",
            "SeriesMasterId": "AAMkAGE_bs88AAAFKPQVAAA=",
            "Start": "2015-04-25T00:30:00Z",
            "End": "2015-04-25T01:00:00Z",
            "Type": "Occurrence"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAAB7h3QQ==\"",
            "Id": "AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==",
            "SeriesMasterId": "AAMkAGE_bs88AAAFKPQVAAA=",
            "Start": "2015-04-26T00:30:00Z",
            "End": "2015-04-26T01:00:00Z",
            "Type": "Occurrence"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAAB7h3QQ==\"",
            "Id": "AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==",
            "SeriesMasterId": "AAMkAGE_bs88AAAFKPQVAAA=",
            "Start": "2015-04-27T00:30:00Z",
            "End": "2015-04-27T01:00:00Z",
            "Type": "Occurrence"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAAB7h3QQ==\"",
            "Id": "AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==",
            "SeriesMasterId": "AAMkAGE_bs88AAAFKPQVAAA=",
            "Start": "2015-04-28T00:30:00Z",
            "End": "2015-04-28T01:00:00Z",
            "Type": "Occurrence"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAAB7h3QQ==\"",
            "Id": "AAMkAGE-Um6lA3uPm7PPAAABSj0FQAAEA==",
            "SeriesMasterId": "AAMkAGE_bs88AAAFKPQVAAA=",
            "Start": "2015-04-29T00:30:00Z",
            "End": "2015-04-29T01:00:00Z",
            "Type": "Occurrence"
        }
    ],
    "@odata.nextLink": "https://outlook.office.com/api/v2.0/me/calendarview/?startDateTime=2015-04-25T00%3a00%3a00Z&endDateTime=2015-05-30T00%3a00%3a00Z&%24skipToken=a1e5b10261804221aceb856143b8af19"
}
```

<a name="SampleThirdSyncReq"> </a>

### Third sync request

The third sync request uses the `skipToken` value from the second response.

```
GET https://outlook.office.com/api/v2.0/me/calendarview?startDateTime=2015-04-25T00:00:00Z&endDateTime=2015-05-30T00:00:00Z&$skiptoken=a1e5b10261804221aceb856143b8af19 HTTP/1.1
```

The request header includes the following 2 lines:
```
Prefer: odata.track-changes
Prefer: odata.maxpagesize=3
```

<a name="SampleThirdSyncResponse"> </a>

### Final sync response

The final response header includes this line, indicating the sync attempt was successful:
```
HTTP/1.1 200 OK
```

The final response body contains one master series event and 4 occurrences associated with the series master event. 
The response body also includes an `@odata.deltaLink` with a `deltaToken` value, indicating that sync is complete for that calendar view.

```

{
    "@odata.context": "https://outlook.office.com/api/v2.0/$metadata#Me/CalendarView/$delta",
    "value": [
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE==_bs88AAAKB6KrAAA=')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAACgkNYA==\"",
            "Id": "AAMkAGE==_bs88AAAKB6KrAAA=",
            "ChangeKey": "mODEKWhc/Um6lA3uPm7PPAAACgkNYA==",
            "Categories": [
            ],
            "DateTimeCreated": "2015-03-05T11:14:13.7752849Z",
            "DateTimeLastModified": "2015-03-05T11:14:13.8220851Z",
            "Subject": "Breakfast at Cafe",
            "BodyPreview": "",
            "Body": {
                "ContentType": "HTML",
                "Content": ""<html>\r\n<head>\r\n<meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\">\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n"
            },
            "Importance": "Normal",
            "HasAttachments": false,
            "Start": "2015-04-27T15:00:00Z",
            "StartTimeZone": "Pacific Standard Time",
            "End": "2015-04-27T16:00:00Z",
            "EndTimeZone": "Pacific Standard Time",
            "Reminder": 15,
            "Location": {
                "DisplayName": "City Hall",
                "Address": {
                    "Street": "",
                    "City": "",
                    "State": "",
                    "CountryOrRegion": "",
                    "PostalCode": ""
                },
                "Coordinates": {
                    "Accuracy": "NaN",
                    "Altitude": "NaN",
                    "AltitudeAccuracy": "NaN",
                    "Latitude": "NaN",
                    "Longitude": "NaN"
                }
            },
            "ResponseStatus": {
                "Response": "NotResponded",
                "Time": "0001-01-01T00:00:00Z"
            },
            "ShowAs": "Tentative",
            "IsAllDay": false,
            "IsCancelled": false,
            "IsOrganizer": false,
            "ResponseRequested": true,
            "Type": "SeriesMaster",
            "SeriesMasterId": null,
            "Attendees": [
                {
                    "EmailAddress": {
                        "Address": "Donovan@contoso.com",
                        "Name": "Donovan Sandberg"
                    },
                    "Status": null,
                    "Type": "Required"
                },
                {
                    "EmailAddress": {
                        "Address": "May@contoso.com",
                        "Name": "May Walton"
                    },
                    "Status": null,
                    "Type": "Required"
                },
                {
                    "EmailAddress": {
                        "Address": "Kristopher@contoso.com",
                        "Name": "Kristopher Nemeth"
                    },
                    "Status": null,
                    "Type": "Required"
                }
            ],
            "Recurrence": {
                "Pattern": {
                    "Type": "Daily",
                    "Interval": 1,
                    "Month": 0,
                    "Index": "First",
                    "FirstDayOfWeek": "Sunday",
                    "DayOfMonth": 0
                },
                "Range": {
                    "Type": "EndDate",
                    "StartDate": "2015-04-27T00:00:00-07:00",
                    "EndDate": "2015-04-30T00:00:00-07:00",
                    "NumberOfOccurrences": 0
                }
            },
            "Organizer": {
                "EmailAddress": {
                    "Address": "Donovan@contoso.com",
                    "Name": "Donovan Sandberg"
                }
            },
            "iCalUId": "040000008200==D272AE",
            "WebLink": "https://contoso.com/owa/?ItemID=AAMkAGE%3D%3D2Bbs88AAAKB6KrAAA3D&exvsurl=1&viewmodel=ICalendarItemDetailsViewModelFactory"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE==7PPAAACgeiqwAAEA==')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAACgkNYA==\"",
            "Id": "AAMkAGE==7PPAAACgeiqwAAEA==",
            "SeriesMasterId": "AAMkAGE==_bs88AAAKB6KrAAA=",
            "Start": "2015-04-27T15:00:00Z",
            "End": "2015-04-27T16:00:00Z",
            "Type": "Occurrence"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE==7PPAAACgeiqwAAEA==')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAACgkNYA==\"",
            "Id": "AAMkAGE==7PPAAACgeiqwAAEA==",
            "SeriesMasterId": "AAMkAGE==_bs88AAAKB6KrAAA=",
            "Start": "2015-04-28T15:00:00Z",
            "End": "2015-04-28T16:00:00Z",
            "Type": "Occurrence"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE==7PPAAACgeiqwAAEA==')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAACgkNYA==\"",
            "Id": "AAMkAGE==7PPAAACgeiqwAAEA==",
            "SeriesMasterId": "AAMkAGE==_bs88AAAKB6KrAAA=",
            "Start": "2015-04-29T15:00:00Z",
            "End": "2015-04-29T16:00:00Z",
            "Type": "Occurrence"
        },
        {
            "@odata.id": "https://outlook.office.com/api/v2.0/Users('chasity@contoso.com')/Events('AAMkAGE==7PPAAACgeiqwAAEA==')",
            "@odata.etag": "W/\"mODEKWhc/Um6lA3uPm7PPAAACgkNYA==\"",
            "Id": "AAMkAGE==7PPAAACgeiqwAAEA==",
            "SeriesMasterId": "AAMkAGE==_bs88AAAKB6KrAAA=",
            "Start": "2015-04-30T15:00:00Z",
            "End": "2015-04-30T16:00:00Z",
            "Type": "Occurrence"
        },

    ],
    "@odata.deltaLink": "https://outlook.office.com/api/v2.0/me/calendarview/?startDateTime=2015-04-25T00%3a00%3a00Z&endDateTime=2015-05-30T00%3a00%3a00Z&%24deltaToken=294a8f04cc0345c5ae093d484629e186"
}
```
