ms.TocTitle: Office Graph
Title: Get insights from the Office Graph
Description: Learn how to use insights from the Office Graph to retrieve and present the most relevant content in different contexts.
ms.ContentId: 976e724b-25b5-4926-a0db-10910c2a10fa
ms.topic: article (how-tos)
ms.date: November 19, 2015
redirect_url: ../howto/query-Office-graph-using-gql-with-search-rest-api

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]


# Get insights from the Office Graph

_**Applies to:** Office 365_

<p class="previewnote">The Office Graph is currently in [Preview](..\howto\platform-development-preview-features-overview.md), and the features described below should **not be used in production**.</p>

The Office Graph computes insights across Office 365 and makes these insights available through the Microsoft Graph, the single endpoint that you can use to access a number of Microsoft's cloud technologies. See [Microsoft Graph](https://graph.microsoft.io/).

Currently there are two insights from the Office Graph that you can query for: **TrendingAround** and **WorkingWith**. For more information, see [TrendingAround](https://graph.microsoft.io/docs/api-reference/beta/api/user_list_trendingaround) and [WorkingWith](https://graph.microsoft.io/docs/api-reference/beta/api/user_list_workingwith).