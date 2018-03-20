ms.TocTitle: Query the Office Graph
Title: Query the Office Graph using GQL and SharePoint Online Search REST APIs
Description: Use Graph Query Language (GQL) to query the Office Graph via the SharePoint Online Search REST API to get items (relationship edges) that satisfy a filter.
ms.ContentId: 1be99137-c27a-4724-a01a-722e39df329e
ms.topic: article (how-tos)
ms.date: November 19, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Query the Office Graph using GQL and SharePoint Online Search REST APIs

**Prerelease content**

_**Applies to:** Office 365 | Office 365 First Release program | SharePoint Online_

<p class="previewnote">Are you looking for the Microsoft Graph, a single endpoint that you can use to access a number of Microsoft’s cloud technologies? See [Microsoft Graph](https://graph.microsoft.io). The content below applies to the Office Graph, which is currently in [Preview](..\howto\platform-development-preview-features-overview.md).</p>

The Office Graph computes insights across Office 365 and makes these insights available through the Microsoft Graph, the single endpoint that you can use to access a number of Microsoft's cloud technologies. Currently, you can query for the following insights from the Office Graph:

- [TrendingAround](https://graph.microsoft.io/en-us/docs/api-reference/beta/api/user_list_trendingaround)
- [WorkingWith](https://graph.microsoft.io/en-us/docs/api-reference/beta/api/user_list_workingwith)

Graph Query Language (GQL) is a preliminary query language designed to query the Office Graph via the SharePoint Online Search REST API. By using GQL, you can query the Office Graph to get items for an actor that satisfies a particular filter.



**Note** The features and APIs documented in this article are in preview and are subject to change. The current additions to the Search REST API are a preliminary solution to make it possible to query the Office Graph, mainly intended for the Office Delve experience. Feel free to experiment with querying the Office Graph but do not use these features, or other features and APIs documented in this article,Â in production. Your feedback about these features and APIs is important. [Let us know](http://officespdev.uservoice.com/) what you think. 
Connect with us on [Stack Overflow](http://stackoverflow.com/questions/tagged/office365). Tag your questions with [office365].


## Office Graph represents relationships among enterprise objects as edges
<a name="sectionSection0"> </a>

The Office Graph contains information about enterprise objects, such as people and documents, as well as the relationships and interactions among these objects. 
The relationships and interactions are represented as _edges_.

Some edges represent a single interaction:
-  **Modified**  — Carl modified a document.
-  **Viewed** — Jarvis viewed a presentation.
    
Some edges are computed based on multiple interactions:
-  **WorkingWith** — People whom you frequently interact with.   
-  **TrendingAround** — Items that are popular in your circle of colleagues.
    
Some edges are relationships between enterprise objects:
-  **OrgManager**,  **OrgColleague**, and so on — Organizational structure edges.
    
See  [Available action types](..\howto\query-Office-graph-using-gql-with-search-rest-api.md#bk_actiontypes) for a list of current Office Graph edges and their descriptions.

Figure 1 shows the Search aspect of Office Graph, where information is gathered through activity across Office 365 services and processed to create edges. 
Currently, the information in the Office Graph is gathered from SharePoint Online, OneDrive for Business, Exchange Online, the Microsoft Azure Active Directory, and Delve.




**Figure 1. A simplified view of the Search aspect of Office Graph and Delve, the main experience it powers**

![The search aspect of Office Graph and Delve, the main experience it powers.](images\Office_graph_search_aspecpt.png)


## The Office Graph data model and edge properties
<a name="sectionSection1"> </a>


As with any graph, each edge in the Office Graph has a source node and a target node. The source node is called the **actor** and the target node is called the **object**.

**Figure 2. The relationship among actor, edge, and object**

![Each edge has a source node (the actor), and a target node (the object)](images\Office_graph_relationship_actor_object.png)


**Edges** have the properties listed in Table 1.


**Table 1. Edge property descriptions and their types**


|**Property**|**Type**|**Description**|
|:-----|:-----|:-----|
| **ActorId**|Integer|The ID of the actor.|
| **ObjectId**|Integer|The ID of the object.|
| **Action type**|Integer|An ID that identifies what action or relationship type the edge represents. Important action types are listed in  [Available action types](..\howto\query-Office-graph-using-gql-with-search-rest-api.md#bk_actiontypes).|
| **Time**|String|A timestamp of the edge; based on the ISO 8601 standard. The semantics of the time stamp depend on the type of the edge. See  [Available action types](..\howto\query-Office-graph-using-gql-with-search-rest-api.md#bk_actiontypes).|
| **Weight**|Integer|A number that indicates the importance of the edge. The semantics of the weight depend on the type of the edge. See  [Available action types](..\howto\query-Office-graph-using-gql-with-search-rest-api.md#bk_actiontypes). |
| **Blob**|Blob|For internal use only.|
| **BlobContent**|String|For internal use only.|
| **ObjectSource**|Integer|For internal use only.|
The nodes in the Office Graph have the same managed properties as defined in the SharePoint Online  [search schema](http://technet.microsoft.com/en-us/library/jj219630%28v=office.15%29). You can retrieve **Retrievable** properties by using the **SelectProperties** query property.


## Graph query extensions in the SharePoint Online Search REST API
<a name="sectionSection2"> </a>

You can query the Office Graph via the SharePoint Online  [SharePoint Search REST API](http://msdn.microsoft.com/library/8a4f7863-e4c1-4099-9189-a1894db36930%28Office.15%29.aspx) by putting two new properties in the query property bag: **GraphQuery** and **GraphRankingModel**. The **GraphQuery** is written in GQL.

You can combine **GraphQuery** and **GraphRankingModel** with the other query parameters that you are familiar with from Search in SharePoint Online, excluding refiners and query templates.

Typically, when you query the Office Graph, you want to find items that are related to other items, and retrieve information about these items and their relationships. For example, you want to query the graph for "everything related to Carl Steadman" or "all items modified by Jarvis Ferro".




**Figure 2. A typical graph query call via REST**

![In a graph query, you can use a content part (Querytext) and a graph part (GraphQuery). The GraphQuery property is specified as part of Properties.](images\Office_graph_graph_query_components.png)

A graph query can contain both a content part (**Querytext**) and a graph part (**GraphQuery**). 
You can use these to do a combined search on the contents of a whole item and the interactions people have had with this particular item. 
The **Querytext** property is mandatory. If you want to match all items without filtering any part of the content, you can use an asterisk (*).

GQL has one main operator: **ACTOR**. The **ACTOR** operator finds all actions of the given actor that satisfies a filter and then returns all the objects for these actions. 
For example, to return documents modified by Carl Steadman (assuming the **ActorId** = 1234 for Carl Steadman) you can split this information into:



- Carl Steadman is the **ACTOR**.
    
- Modify is the **action** with ID = 1003.
    
- Document is the **object**, which is returned in the result.
    
Then, you can write the following query.

 `ACTOR(1234, action:1003)`

The following is the syntax for the  **ACTOR** operator.

 `ACTOR(<ActorId> [, filter])`

The **ActorId** is the ID of the node you want to look up the actions for. The **filter** is a predicate applied to all outgoing edges of the actor. The **filter** is constructed using the **Action**, **Time**, and **Weight** from Table 1 in combination with Boolean operators: **AND**, **NOT**, and **OR**. The result of the query is the objects of all edges that match the **filter**.

You can combine **ACTOR** operators by using the **AND** and **OR** operators. For example, to return all items modified by both Jarvis Ferro ( **ActorId** = 1234) and Austin Ingalls ( **ActorId** = 5678), you write the following.

 `AND(ACTOR(1234, action:1003), ACTOR(5678, action:1003))`

Write the following to return all items modified by either Jarvis Ferro or Austin Ingalls.

 `OR(ACTOR(1234, action:1003), ACTOR(5678, action:1003))`

When you write graph queries that require you to use the **ActorId** of the authenticated user, you can use the **ME** macro as an equivalent substitute. For example, to return documents modified by the authenticated user, write the following.

 `ACTOR(ME, action:1003)`


## Available action types
<a name="bk_actiontypes"> </a>


**Table 2. Action types and their descriptions**

|**Action Type**|**Description**|**Visibility**|**ID**|**Weight**|**Timestamp**|
|:-----|:-----|:-----|:-----|:-----|:-----|
| **PersonalFeed**|The actor's personal feed as shown on their  **Home** view in Delve.|Private|1021|A sequence number.|When the item was added to the feed on the  **Home** view in Delve.|
| **Modified**|Items that the actor has modified in the last three months.|Public|1003|The number of modifications.|Last modified.|
| **OrgColleague**|Everyone who reports to the same manager as the actor.|Public|1015|Always 1.|-|
| **OrgDirect**|The actor's direct reports.|Public|1014|Always 1.|-|
| **OrgManager**|The person whom the actor reports to.|Public|1013|Always 1.|-|
| **OrgSkipLevelManager**|The actor's skip-level manager.|Public|1016|Always 1.|-|
| **WorkingWith**|People whom the actor communicates with or works with frequently.|Private|1019|A relevance score.|-|
| **TrendingAround**|Items popular with people whom the actor works with or communicates with frequently.|Public|1020|A relevance score.|-|
| **Viewed**|Items viewed by the actor in the last three months.|Private|1001|The number of views.|Last viewed.|
| **WorkingWithPublic**|A public version of the  **WorkingWith** edge.|Public|1033|A sequence number.|-|

## Running graph queries against SharePoint 2013
<a name="sectionSection4"> </a>

To query the Office Graph, you must add the **GraphQuery** to the property bag of the **KeywordQuery** class. The value of this property must be the graph query string in GQL format. 
To query for a person's ID (**ActorId**), such as Carl Steadman (username:carls), you can write the following REST query.

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='Username:carls'&amp;SourceId='b09a7990-05ea-4af9-81ef-edfab16c4e31'&amp;SelectProperties='UserName,DocId'
```

**Note** The result source to use to run a particular query is the **SourceId**; b09a7990-05ea-4af9-81ef-edfab16c4e31 is the ID for the People Search result source.

The resulting output contains the person's ID (DocId=21865248), as shown.




```XML
<d:element m:type="SP.KeyValue">
    <d:Key>DocId</d:Key>
    <d:Value>21865248</d:Value>
    <d:ValueType>Edm.Int64</d:ValueType>
</d:element>

```


### Examples

The following examples show how you can write single actor and multiple actor queries to query the Office Graph. 
These examples use Carl as the actor with **ActorId**: 2962.

The results returned by these queries can contain a maximum of ten items because that's the default number. 
You can increase the number of results by using the **RowLimit()** property, as shown in [this](..\howto\query-Office-graph-using-gql-with-search-rest-api.md#rowlimit_example) example.


### Single actor queries


- First ten items related to you.
    
     **Syntax**:  `ACTOR(ME)`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:ACTOR(ME)'
```

- First ten items related to Carl.
    
     **Syntax**:  `ACTOR(2962)`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:ACTOR(2962)'
```

- Your manager.
    
     **Syntax**:  `ACTOR(ME, action:1013)`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:ACTOR(ME\,action\:1013)'
```

- First ten items that you recently modified or viewed.
    
     **Syntax**:  `ACTOR(ME, OR(action:1001,action:1003))`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:ACTOR(ME\,OR(action\:1001\,action\:1003))'
```

- First ten items that you modified on August 15, 2014.
    
     **Syntax**:  `ACTOR(ME, AND(action:1003, time:datetime(2014-08-15)))`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:ACTOR(ME\,AND(action\:1003\,time\:datetime(2014-08-15)))'
```

- First ten items that you modified on June 26, 2014 or later.
    
     **Syntax**:  `ACTOR(ME, AND(action:1003, time:range(datetime(2014-06-26),max)))`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:ACTOR(ME\,AND(action\:1003\,time\:range(datetime(2014-06-26)\,max)))'
```

### Multiple actor queries


- First ten items related to you and Carl.
    
     **Syntax**:  `AND(ACTOR(ME), ACTOR(2962))`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:AND(ACTOR(ME)\,ACTOR(2962))'
```

- First ten items related to you or Carl.
    
     **Syntax**:  `OR(ACTOR(ME), ACTOR(2962))`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:OR(ACTOR(ME)\,ACTOR(2962))'
```

- First ten items you recently viewed, and Carl recently modified.
    
     **Syntax**:  `AND(ACTOR(ME, action:1001), ACTOR(2962, action:1003))`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:AND(ACTOR(ME\,action\:1001)\,ACTOR(2962\,action\:1003))'
```

### Understanding the graph query result format

The format of the result for graph queries is similar to the result for search queries, with one additional column, **Edges**, as part of the **RelevantResult** **ResultTable** returned by the [SharePoint 2013 search Query APIs](http://msdn.microsoft.com/library/ae9d73ed-1140-430b-9287-01dbbe8ae7d1%28Office.15%29.aspx). 
The format of  **Edges** is an array of edges serialized to JSON.

For example, the following query requests the list of people a particular actor (**ActorId**: 21894957) works with (**ActionId**: 1033).

```no-highlight 
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='Graphquery:ACTOR(21894957\,action\:1033)'&amp;SelectProperties='Docid,Title'
```

The output is the following XML structure, containing **Edges** and other elements. In this example, only one **Edges** element is returned.

```XML
<d:element m:type="SP.KeyValue">
    <d:Key>Edges</d:Key>
    <d:Value>[{"ActorId":21894957,"ObjectId":21900499,
        "Properties":{"Action":1033,"Blob":[],
        "ObjectSource":1,"Time":"2013-12-02T13:56:25.5979646Z",
        "Weight":61}}]
    </d:Value>
    <d:ValueType>Edm.String</d:ValueType>
</d:element>
```

### Graph query access control

Graph queries use the same access control mechanisms as search queries. A graph query returns only items the user has access to.

The Office Graph also provides an access control mechanism for all its edges. Each action type of an edge in the graph can be private or public. 
Public edges are visible to all users in the organization. Private edges are visible only to the actor. They are ignored when another user performs a graph query. 
For example, Carl Steadman can query the Office Graph for items that he viewed. If another user performs this query with Carl Steadman's **ActorId**, he or she gets an empty result. 
The Visibility column of Table 2 lists which action types are public and which are private.


### Advanced query examples

You can write graph queries in many different ways to accomplish different tasks. The following examples are intended to provide a simple guide for how you can write these advanced queries.


#### Combine the GraphQuery property with other query properties


 **Example 1**: First ten items related to you or Carl, and include the **DocId** and **Edges** properties in the results.

```no-highlight 
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:OR(ACTOR(ME)\,ACTOR(2962))'&amp;SelectProperties='DocId,Edges'
```

**Note**  You will receive more properties in the output than just **DocId** and **Edges**; for example, **RankId** and **PartitionId**. This is because these are the default properties that are returned by the Search service.


 **Example 2**: First 100 items related to you or Carl.
<a name="rowlimit_example"> </a>

```no-highlight 
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:OR(ACTOR(ME)\,ACTOR(2962))'&amp;RowLimit=100
```

The edges that you get as a result of the graph query are those that you specifically requested for in the query. 
But, in some cases you might want to retrieve additional edge types without affecting which documents are returned in the query result.


 **Example 3**: Retrieve all documents trending around you (**ActionId**: 1020), and also return information about whether you viewed and modified these documents. 
You can do this by using the Boolean construct shown below.


 **Syntax**: `AND(
           ACTOR(ME, action:1020), 
           ACTOR(ME, OR(action:1020,action:1001,action:1003)))`

```no-highlight 
https://<tenant_address>/_api/search/query?Querytext='*'&Properties='GraphQuery:AND(ACTOR(ME\,action\:1020)\,ACTOR(ME\,OR(action\:1020\,action\:1001\,action\:1003)))'&SelectProperties='Docid,Title'
```


#### Use the GraphRankingModel property to sort results

You can sort the result returned for graph queries in two ways: by the edge's **Timestamp** or the edge's **Weight**.


- To sort based on the edge timestamp, set the **GraphRankingModel** property equal to `{"features"\:[{"function"\:"EdgeTime"}]}`.
    
- To sort based on the edge weight, set the **GraphRankingModel** property equal to `{"features"\:[{"function"\:"EdgeWeight"}]}`.
    
In both cases, you must also set the  **RankingModelId** property to `'0c77ded8-c3ef-466d-929d-905670ea1d72'`. If an item in the result is the object of more than one edge matching the
graph query, the highest **Timestamp** or **Weight** is used.



 **Example 1**: Sort items that you recently modified by the time that they were last modified.

 **Syntax**:  `GraphQuery:ACTOR(ME, action:1003) GraphRankingModel:{"features"\:[{"function"\:"EdgeTime"}]} RankingModelId='0c77ded8-c3ef-466d-929d-905670ea1d72'`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:ACTOR(ME\,action\:1003),GraphRankingModel:{"features"\:[{"function"\:"EdgeTime"}]}'
&amp;RankingModelId='0c77ded8-c3ef-466d-929d-905670ea1d72'
```

 **Example 2**: Sort the people you work with (**WorkingWith**) by their closeness to you.

 **Syntax**:  `GraphQuery:ACTOR(ME, action:1019) GraphRankingModel:{"features"\:[{"function"\:"EdgeWeight"}]} RankingModelId='0c77ded8-c3ef-466d-929d-905670ea1d72'`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&amp;Properties='GraphQuery:ACTOR(ME\,action\:1019),GraphRankingModel:{"features"\:"function"\:"EdgeWeight"}]}'
&amp;RankingModelId='0c77ded8-c3ef-466d-929d-905670ea1d72'
```



For multiple actor queries, you can use a parameter called **actorCombination** in the **GraphRankingModel** to choose how to combine rank scores for the different actors.


 **Example 3**: Find documents trending around both you and Carl, and sort them by the sum of their trending weight.

 **Syntax**:  `AND(ACTOR(ME, action:1020), ACTOR(2962, action:1020))
             GraphRankingModel:{"actorCombination"\:"sum"\,"features"\:[{"function"\:"EdgeWeight"}]}
             RankingModelId='0c77ded8-c3ef-466d-929d-905670ea1d72'`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='*'&Properties='GraphQuery:AND(ACTOR(ME\, action\:1020)\,ACTOR(2962\,action\:1020)),
GraphRankingModel:{ "actorCombination"\:"sum"\,"features"\:[{"function"\:"EdgeWeight"}]}'
&RankingModelId='0c77ded8-c3ef-466d-929d-905670ea1d72'
```



The **actorCombination** parameter supports "min", "max", and "sum" values; the default value is "max". 

#### Combine the GraphQuery property with content queries or full-text queries



 **Example**: Combine **GraphQuery** with **Querytext**='Title:design' to query for all items that you have recently viewed with "design" in their title.

 **Syntax**:  `GraphQuery:ACTOR(ME, action:1001) Querytext='Title:design'`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='Title:design'&amp;Properties='GraphQuery:ACTOR(ME)\,action\:1001))
```

To modify the query, you can use any query in **Querytext**.



#### Using the GraphRestrictionMode query property to modify the result
When you run a graph query, the default set of items that you get in return is the intersection of the graph result and the content result. 
But, if you want Office Graph to return only the content result, you can set the **GraphRestrictionMode** property to false. Any edges that match the graph query are also returned as part of this result.



 **Example**: Combine **GraphQuery** with **Querytext**='Title:design' to query for all items that you recently viewed that have "design" in their title.

 **Syntax**:  `GraphQuery:ACTOR(ME, action:1001) Querytext='design'
            GraphRestrictionMode:false`

```no-highlight
https://<tenant_address>/_api/search/query?Querytext='design'&amp;Properties='GraphQuery:ACTOR(ME)\,action\:1001),GraphRestrictionMode:false'&SelectProperties='Docid,Title'
```



## Additional resources
<a name="bk_addresources"> </a>


-  [Office 365 APIs Platform Overview](..\howto\platform-development-overview.md)
    
-  [What is Delve?](http://support.office.com/article/1315665a-c6af-4409-a28d-49f8916878ca)
    
-  [Delve for Office 365 admins](http://support.office.com/article/54f87a42-15a4-44b4-9df0-d36287d9531b)
    

