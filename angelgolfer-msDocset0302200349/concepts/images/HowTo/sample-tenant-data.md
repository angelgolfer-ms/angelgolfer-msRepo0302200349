ms.TocTitle: Office 365 sample tenant data
Title: Office 365 sample tenant data
Description: Find the sample user mail, contacts, calendar, and documents data associated with the interactive REST API reference and the API Sandbox for Office 365 APIs.
ms.ContentId: f14745a4-1763-43a4-bcc4-ffd9b2df92f6
ms.topic: article (how-tos)
ms.date: April 29, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Office 365 sample tenant data

_**Applies to:** Office 365_

When you use an interactive "Try" button for the REST operations in the [Mail, Calendar, Contacts, or Files API references](..\howto\rest-api-overview.md), we are sending the request to a live tenant populated with sample data.


![The interactive "Try" button in the REST API reference.](images/SampleTenantDataTryButton.png)

The [API Sandbox for Office 365 APIs](https://apisandbox.msdn.microsoft.com/) connects to the same tenant as well. Here's a list showing you the data that is associated with the sample user in the sample tenant:

##Mail

|**Folder**|**Email Subject**|
|:-----|:-----|
|Sent Mail|Meeting Notes <br/> Contract Signing <br/> Rob:Alex 1:1 <br/> Daily Team Meeting|
|Inbox|Meeting Notes (with attachment; also a reply to an earlier email sent by Alex D) <br/> Event tomorrow - atrium closed|

##Contacts

|**Name**|**Alias**|
|:-----|:-----|
|Garth Fort|garthf|
|Janet Schorr|janets|
|Katie Jordan (also duplicated in the "Finance" Contacts folder)|katiej|
|Pavel Bansky|pavelb|
|Rob Young|roby|

##Calendar
- Time zone: Pacific Standard Time

|**Meeting Title**|**Recurrence or Date/Time**|
|:-----|:-----|
|Daily Team Meeting|Every week day, 11:00-11:30 AM|
|Weekly Meeting on Contoso Project|Every Monday, 2:00 PM|
|Rob:Alex 1:1|Every third Wednesday of the month, 9:30 AM|
|Thanksgiving Holiday|Nov 27, 2014, all day|
|Christmas Holiday|Dec 25, 2014, all day|
|New Year's Day Holiday|Jan 1, 2015, all day|
|Thanksgiving Holiday|Nov 26, 2015, all day|


##Documents

|**Folder**|**File**|
|:-----|:-----|
|Root Folder|Ad Goals Presentation.pptx <br/> Ad Goals.docx <br/> Annual Party Planning.docx <br/> Ideas for XT1000 Series.docx <br/> Marketing.pptx <br/> Meeting Notes.docx <br/> Proposal for Ad Campaign.docx <br/> Quick notes.txt <br/> Shopping List.xlsx <br/> Slogan Suggestions.docx <br/> Timesheet_Alexd.xlsx <br/> XT1000 Series.pptx |
|Shared with Everyone|Denver Data.xlsx|


##Users and groups


There are fifty users defined in the sample Office 365 tenant. Each user belongs to two of the four groups defined in the sample data: Employees or Managers, and Marketing or Sales. Each employee except Josephine McNeil (demo1) has a manager.

| **givenName** | **surname** | **UPN** | **Gender** | **telephoneNumber** | **Manager** | **Group**  | **Group** | **Group** |
|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|:-----|
| Josephine | McNeil | demo1 | Female | 4255550100 |  | Managers |  |  |
| Kelli | Leach | demo2 | Female | 4255550100 | Autumn Webster | Employees | Marketing |  |
| Tamika | Carroll | demo3 | Female | 4255550100 | Callie Dillard | Employees | Marketing |  |
| Gilbert | Shelly | demo4 | Male | 4255550100 | Zelma Huff | Employees | Sales |  |
| Elisabeth | Dunn | demo5 | Female | 4255550100 | Diana Hewitt | Employees | Sales |  |
| Penelope | Logan | demo6 | Female | 4255550100 | Greg Toscano | Employees | Sales |  |
| Donovan | Carbajal | demo7 | Male | 4255550100 | Greg Toscano | Employees | Sales |  |
| Sallie | Payne | demo8 | Female | 4255550100 | Donna Sweet | Employees | Sales |  |
| Evangelina | Higgins | demo9 | Female | 4255550100 | Donna Sweet | Employees | Sales |  |
| Chasity | Mullins | demo10 | Female | 4255550100 | Laura Brennan | Employees | Marketing |  |
| Carlton | Fiore | demo11 | Male | 4255550100 | Laura Brennan |  | Marketing |  |
| Autumn | Webster | demo12 | Female | 4255550100 | Laura Brennan | Managers | Marketing |  |
| Emmanuel | Wolcott | demo13 | Male | 4255550100 | Laura Brennan | Employees | Marketing |  |
| Callie | Dillard | demo14 | Female | 4255550100 | Laura Brennan | Managers | Marketing |  |
| Darlene | Hale | demo15 | Female | 4255550100 | Betty Carroll | Employees | Marketing |  |
| Evelyn | Watts | demo16 | Female | 4255550100 | Betty Carroll | Managers | Marketing |  |
| Gail | Steele | demo17 | Female | 4255550100 | Betty Carroll | Employees | Marketing |  |
| Theodore | Coppola | demo18 | Male | 4255550100 | Betty Carroll | Employees | Marketing |  |
| Bennie | Coggins | demo19 | Male | 4255550100 | Betty Carroll | Employees | Marketing |  |
| Laura | Bishop | demo20 | Female | 4255550100 | Autumn Webster | Employees | Marketing |  |
| Alexander | Yoo | demo21 | Male | 4255550100 | Autumn Webster | Managers | Marketing |  |
| Chasity | Salinas | demo22 | Female | 4255550100 | Autumn Webster | Employees | Marketing |  |
| Al | Mota | demo23 | Male | 4255550100 | Autumn Webster | Employees | Marketing |  |
| Zelma | Huff | demo24 | Female | 4255550100 | Autumn Webster | Managers | Marketing |  |
| Dane | Clemente | demo25 | Male | 4255550100 | Autumn Webster | Employees | Marketing |  |
| Donna | Sweet | demo26 | Female | 4255550100 | Autumn Webster | Managers | Marketing |  |
| Sheila | Griffin | demo27 | Female | 4255550100 | Callie Dillard | Managers | Marketing |  |
| Beth | Hardy | demo28 | Female | 4255550100 | Callie Dillard | Employees | Marketing |  |
| Elsa | Hansen | demo29 | Female | 4255550100 | Callie Dillard | Employees | Marketing |  |
| Laura | Brennan | demo30 | Female | 4255550100 | Josephine McNeil | Managers | Marketing | Employees |
| Betty | Carroll | demo31 | Female | 4255550100 | Josephine McNeil | Managers | Marketing | Employees |
| Jan | Madden | demo32 | Female | 4255550100 | Evelyn Watts | Employees | Marketing |  |
| Lorena | Bird | demo33 | Female | 4255550100 | Evelyn Watts | Employees | Sales |  |
| Ada | Lang | demo34 | Female | 4255550100 | Evelyn Watts | Employees | Sales |  |
| Katelyn | Nielsen | demo35 | Female | 4255550100 | Alexander Yoo | Employees | Sales |  |
| Jillian | Gonzalez | demo36 | Female | 4255550100 | Alexander Yoo | Employees | Sales |  |
| Joe | Swearingen | demo37 | Male | 4255550100 | Alexander Yoo | Employees | Sales |  |
| Mitchell | Rodman | demo38 | Male | 4255550100 | Zelma Huff | Employees | Sales |  |
| Ester | O'Neil | demo39 | Female | 4255550100 | Zelma Huff | Employees | Sales |  |
| Vicky | Booth | demo40 | Female | 4255550100 | Zelma Huff | Managers | Sales |  |
| Diana | Hewitt | demo41 | Female | 4255550100 | Sheila Griffin | Managers | Sales |  |
| Eileen | Klein | demo42 | Female | 4255550100 | Sheila Griffin | Employees | Sales |  |
| Greg | Toscano | demo43 | Male | 4255550100 | Sheila Griffin | Managers | Sales |  |
| Keisha | Stout | demo44 | Female | 4255550100 | Vicky Booth | Employees | Sales |  |
| Bettie | Santana | demo45 | Female | 4255550100 | Vicky Booth | Employees | Sales |  |
| Evelyn | Rodgers | demo46 | Female | 4255550100 | Vicky Booth | Employees | Sales |  |
| Imelda | Miranda | demo47 | Female | 4255550100 | Vicky Booth | Employees | Sales |  |
| Cathleen | Silva | demo48 | Female | 4255550100 | Diana Hewitt | Employees | Sales |  |
| Tami | Glover | demo49 | Female | 4255550100 | Diana Hewitt | Employees | Sales |  |
| Lynne  | Deleon | demo50 | Female | 4255550100 | Greg Toscano | Employees | Sales |  | |



### Employees by manager

| **Manager** | **ManagerUPN** | **Name** | **UPN** |
|:-----|:-----|:-----|:-----|
|  |  | Josephine McNeil | demo01 |
| Josephine McNeil | demo1 | Laura Brennan | demo30 |
|  |  | Betty Carroll | demo31 |
| Autumn Webster | demo12 | Kelli Leach | demo02 |
|  |  | Laura Bishop | demo20 |
|  |  | Alexander Yoo | demo21 |
|  |  | Chasity Salinas | demo22 |
|  |  | Al Mota | demo23 |
|  |  | Zelma Huff | demo24 |
|  |  | Dane Clemente | demo25 |
|  |  | Donna Sweet | demo26 |
| Callie Dillard | demo14 | Tamika Carroll | demo03 |
|  |  | Sheila Griffin | demo27 |
|  |  | Beth Hardy | demo28 |
|  |  | Elsa Hansen | demo29 |
| Evelyn Watts | demo16 | Jan Madden | demo32 |
|  |  | Lorena Bird | demo33 |
|  |  | Ada Lang | demo34 |
| Alexander Yoo | demo21 | Katelyn Nielsen | demo35 |
|  |  | Jillian Gonzalez | demo36 |
|  |  | Joe Swearingen | demo37 |
| Zelma Huff | demo24 | Gilbert Shelly | demo04 |
|  |  | Mitchell Rodman | demo38 |
|  |  | Ester O'Neil | demo39 |
|  |  | Vicky Booth | demo40 |
| Donna Sweet | demo26 | Sallie Payne | demo08 |
|  |  | Evangelina Higgins | demo09 |
| Sheila Griffin | demo27 | Diana Hewitt | demo41 |
|  |  | Eileen Klein | demo42 |
|  |  | Greg Toscano | demo43 |
| Laura Brennan | demo30 | Chasity Mullins | demo10 |
|  |  | Carlton Fiore | demo11 |
|  |  | Autumn Webster | demo12 |
|  |  | Emmanuel Wolcott | demo13 |
|  |  | Callie Dillard | demo14 |
| Betty Carroll | demo31 | Darlene Hale | demo15 |
|  |  | Evelyn Watts | demo16 |
|  |  | Gail Steele | demo17 |
|  |  | Theodore Coppola | demo18 |
|   |  | Bennie Coggins | demo19 |
| Vicky Booth | demo40 | Keisha Stout | demo44 |
|   |  | Bettie Santana | demo45 |
|   |  | Evelyn Rodgers | demo46 |
|   |  | Imelda Miranda | demo47 |
| Diana Hewitt | demo41 | Elisabeth Dunn | demo05 |
|   |  | Cathleen Silva | demo48 |
|   |  | Tami Glover | demo49 |
| Greg Toscano | demo43 | Penelope Logan | demo06 |
|   |  | Donovan Carbajal | demo07 |
|   |  | Lynne  Deleon | demo50 |


### Employees by group

| **Group**  | **Description** | **givenName** | **surname** | **UPN** |
|:-----|:-----|:-----|:-----|:-----|
| Employees | All users who are not managers | Kelli | Leach | demo2 |
|  |  | Tamika | Carroll | demo3 |
|  |  | Gilbert | Shelly | demo4 |
|  |  | Elisabeth | Dunn | demo5 | 
|  |  | Penelope | Logan | demo6 |
|  |  | Donovan | Carbajal | demo7 |
|  |  | Sallie | Payne | demo8 |
|  |  | Evangelina | Higgins | demo9 |
|  |  | Chasity | Mullins | demo10 |
|  |  | Emmanuel | Wolcott | demo13 |
|  |  | Darlene | Hale | demo15 | 
|  |  | Gail | Steele | demo17 |
|  |  | Theodore | Coppola | demo18 |
|  |  | Bennie | Coggins | demo19 |
|  |  | Laura | Bishop | demo20 |
|  |  | Chasity | Salinas | demo22 |
|  |  | Al | Mota | demo23 |
|  |  | Dane | Clemente | demo25 |
|  |  | Beth | Hardy | demo28 |
|  |  | Elsa | Hansen | demo29 |
|  |  | Laura | Brennan | demo30 |
|  |  | Betty | Carroll | demo31 |
|  |  | Jan | Madden | demo32 |
|  |  | Lorena | Bird | demo33 |
|  |  | Ada | Lang | demo34 |
|  |  | Katelyn | Nielsen | demo35 |
|  |  | Jillian | Gonzalez | demo36 |
|  |  | Joe | Swearingen | demo37 |
|  |  | Mitchell | Rodman | demo38 |
|  |  | Ester | O'Neil | demo39 |
|  |  | Eileen | Klein | demo42 |
|  |  | Keisha | Stout | demo44 |
|  |  | Bettie | Santana | demo45 |
|  |  | Evelyn | Rodgers | demo46 |
|  |  | Imelda | Miranda | demo47 |
|  |  | Cathleen | Silva | demo48 |
|  |  | Tami | Glover | demo49 |
|  |  | Lynne  | Deleon | demo50 |
| Managers | All users who are managers | Josephine | McNeil | demo1 |
|  |  | Autumn | Webster | demo12 |
|  |  | Callie | Dillard | demo14 |
|  |  | Evelyn | Watts | demo16 |
|  |  | Alexander | Yoo | demo21 |
|  |  | Zelma | Huff | demo24 |
|  |  | Donna | Sweet | demo26 |
|  |  | Sheila | Griffin | demo27 |
|  |  | Laura | Brennan | demo30 |
|  |  | Betty | Carroll | demo31 |
|  |  | Vicky | Booth | demo40 |
|  |  | Diana | Hewitt | demo41 |
|  |  | Greg | Toscano | demo43 |
| Marketing | Marketing department | Kelli | Leach | demo2 |
|  |  | Tamika | Carroll | demo3 |
|  |  | Chasity | Mullins | demo10 |
|  |  | Carlton | Fiore | demo11 |
|  |  | Autumn | Webster | demo12 |
|  |  | Emmanuel | Wolcott | demo13 |
|  |  | Callie | Dillard | demo14 |
|  |  | Darlene | Hale | demo15 |
|  |  | Evelyn | Watts | demo16
|  |  | Gail | Steele | demo17 |
|  |  | Theodore | Coppola | demo18 |
|  |  | Bennie | Coggins | demo19 |
|  |  | Laura | Bishop | demo20 |
|  |  | Alexander | Yoo | demo21 |
|  |  | Chasity | Salinas | demo22 |
|  |  | Al | Mota | demo23 |
|  |  | Zelma | Huff | demo24 |
|  |  | Dane | Clemente | demo25 |
|  |  | Donna | Sweet | demo26 |
|  |  | Sheila | Griffin | demo27 |
|  |  | Beth | Hardy | demo28 |
|  |  | Elsa | Hansen | demo29 |
|  |  | Laura | Brennan | demo30 |
|  |  | Betty | Carroll | demo31 |
|  |  | Jan | Madden | demo32 |
| Sales | Sales department | Gilbert | Shelly | demo4 |
|  |  | Elisabeth | Dunn | demo5 |
|  |  | Penelope | Logan | demo6 |
|  |  | Donovan | Carbajal | demo7 |
|  |  | Sallie | Payne | demo8 |
|  |  | Evangelina | Higgins | demo9 |
|  |  | Lorena | Bird | demo33 | 
|  |  | Ada | Lang | demo34 |
|  |  | Katelyn | Nielsen | demo35 |
|  |  | Jillian | Gonzalez | demo36 |
|  |  | Joe | Swearingen | demo37 |
|  |  | Mitchell | Rodman | demo38 |
|  |  | Ester | O'Neil | demo39 |
|  |  | Vicky | Booth | demo40 |
|  |  | Diana | Hewitt | demo41 |
|  |  | Eileen | Klein | demo42 |
|  |  | Greg | Toscano | demo43 |
|  |  | Keisha | Stout | demo44 |
|  |  | Bettie | Santana | demo45 |
|  |  | Evelyn | Rodgers | demo46 |
|  |  | Imelda | Miranda | demo47 |
|  |  | Cathleen | Silva | demo48 |
|  |  | Tami | Glover | demo49 | 
|  |  | Lynne  | Deleon | demo50 |
| All Users | All users at the company | Managers | Employees | demo51 | 



