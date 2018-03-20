ms.TocTitle: CRC Model Page
Title: CRC Model Page
Description: This page illustrates the markdown for on-page filtering by platform.
ms.ContentId: 72d424bc-ad83-4f91-90ba-66f2cb775f33
ms.topic: article (how-tos)

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]

![You are currently viewing the sandbox branch of the O365 API repo.](..\includes\sandbox_label.png)

[!INCLUDE [Add the platforms filter bar](../includes/controls/addplatformsfilter.xml)]

<a name="pagetitle"> </a>
# On-page filtering (CRC) model page  

The markdown in this file illustrates how to set up on-page filtering by platform **in the O365API repo**. A description of [how to enable filtering](#filtering_howto) and codes lines follow the platform content sections.

[!INCLUDE [BEGIN iOS section](../includes/controls/iossection.xml)]

## iOS section

Lorem way ipsum dolor sit amet, consectetur adipiscing elit. Integer nec odio. Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet. Duis sagittis ipsum. Praesent mauris. Fusce nec tellus sed augue semper porta. Mauris massa. Vestibulum lacinia arcu eget nulla. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. 

Curabitur sodales ligula in libero. Sed dignissim lacinia nunc. Curabitur tortor. Pellentesque nibh. Aenean quam. In scelerisque sem at dolor. Maecenas mattis. Sed convallis tristique sem. Proin ut ligula vel nunc egestas porttitor. Morbi lectus risus, iaculis vel, suscipit quis, luctus non, massa. Fusce ac turpis quis ligula lacinia aliquet. Mauris ipsum. 

[!INCLUDE [END iOS section](../includes/controls/iossection.xml)]

[!INCLUDE [BEGIN Android section](../includes/controls/androidsection.xml)]

## Android section

Nulla metus metus, ullamcorper vel, tincidunt sed, euismod in, nibh. Quisque volutpat condimentum velit. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Nam nec ante. Sed lacinia, urna non tincidunt mattis, tortor neque adipiscing diam, a cursus ipsum ante quis turpis. Nulla facilisi. Ut fringilla. Suspendisse potenti. Nunc feugiat mi a tellus consequat imperdiet. Vestibulum sapien. Proin quam. Etiam ultrices. Suspendisse in justo eu magna luctus suscipit. Sed lectus. 

Integer euismod lacus luctus magna. Quisque cursus, metus vitae pharetra auctor, sem massa mattis sem, at interdum magna augue eget diam. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Morbi lacinia molestie dui. Praesent blandit dolor. Sed non quam. In vel mi sit amet augue congue elementum. Morbi in ipsum sit amet pede facilisis laoreet. Donec lacus nunc, viverra nec, blandit vel, egestas et, augue. Vestibulum tincidunt malesuada tellus. Ut ultrices ultrices enim. Curabitur sit amet mauris. Morbi in dui quis est pulvinar ullamcorper. Nulla facilisi. Integer lacinia sollicitudin massa. 

[!INCLUDE [END Android section](../includes/controls/androidsection.xml)]

[!INCLUDE [BEGIN JavaScript section](../includes/controls/javascriptsection.xml)]

## JavaScript section

Cras metus. Sed aliquet risus a tortor. Integer id quam. Morbi mi. Quisque nisl felis, venenatis tristique, dignissim in, ultrices sit amet, augue. Proin sodales libero eget ante. Nulla quam. Aenean laoreet. Vestibulum nisi lectus, commodo ac, facilisis ac, ultricies eu, pede. Ut orci risus, accumsan porttitor, cursus quis, aliquet eget, justo. Sed pretium blandit orci. 

Ut eu diam at pede suscipit sodales. Aenean lectus elit, fermentum non, convallis id, sagittis at, neque. Nullam mauris orci, aliquet et, iaculis et, viverra vitae, ligula. Nulla ut felis in purus aliquam imperdiet. Maecenas aliquet mollis lectus. Vivamus consectetuer risus et tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer nec odio. Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet. Duis sagittis ipsum. Praesent mauris. 

[!INCLUDE [END JavaScript section](../includes/controls/javascriptsection.xml)]

[!INCLUDE [BEGIN ASP.NET MVC section](../includes/controls/aspnetmvcsection.xml)]

## ASP.NET MVC section

Fusce nec tellus sed augue semper porta. Mauris massa. Vestibulum lacinia arcu eget nulla. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Curabitur sodales ligula in libero. Sed dignissim lacinia nunc. Curabitur tortor. Pellentesque nibh. Aenean quam. In scelerisque sem at dolor. Maecenas mattis. 

Sed convallis tristique sem. Proin ut ligula vel nunc egestas porttitor. Morbi lectus risus, iaculis vel, suscipit quis, luctus non, massa. Fusce ac turpis quis ligula lacinia aliquet. Mauris ipsum. Nulla metus metus, ullamcorper vel, tincidunt sed, euismod in, nibh. Quisque volutpat condimentum velit. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Nam nec ante. Sed lacinia, urna non tincidunt mattis, tortor neque adipiscing diam, a cursus ipsum ante quis turpis. Nulla facilisi. Ut fringilla. 

[!INCLUDE [END ASP.NET MVC section](../includes/controls/aspnetmvcsection.xml)]


<a name="filtering_howto"> </a>
## How to enable on-page filtering
You enable on-page filtering by adding three types of Markdown-styled content includes:

-  A single **filter bar include** above the H1 line (i.e., in the position where the buttons will be rendered). To render the platforms filtering bar, you use the platforms filter bar include.
-  A pair of platform **section boundary include pairs** surrounding each section of platform-specific content.
-  A single **filter functionality enabler** include at the end of the file.

<p style="font-size:85%;margin:0 0 2em 2em;border:1px solid deeppink;border-left-width:8px;background-color:mistyrose;padding:.5em 1em;"><b>IMPORTANT: </b>All content include markdown lines must be immediately preceded and immediately followed by at least one empty line (except for the filter functionality enabler, which can be followed by EOF).</p>

Following are the content include code lines:

**Platforms filter bar include**
![Image of platforms filter bar include snippet](../includes/controls/Platforms_filter_bar.png)

**Platform section boundary include pairs**
![Image of platform section boundary include snippet pairs](../includes/controls/Platform_section_boundary_pairs.png)

<p style="font-size:85%;margin:0 0 2em 2em;border:1px solid rgb(104,189,69);border-left-width:8px;background-color:rgb(236,247,232);padding:.5em 1em;">Note that the XML _file names_ for the platform section boundary markers (enclosed in parentheses) are identical for the BEGIN and END sections; only the labels (enclosed in square brackets) differ. The labels are added for clarity; you may use any labels you wish (e.g., "BEGIN iOS section 1", "END iOS section 1", "BEGIN iOS section 2"...).</p>

**Filter functionality enabler**
![Image of filter functionality enabler include snippet](../includes/controls/Filter_functionality_enabler.png)


## Link tests section

* [bk #pagetitle](#pagetitle)
* [cross-dir ..\api\mail-rest-operations.md](..\api\mail-rest-operations.md)
* [cross-dir-with-bk ../API/files-rest-operations#DeleteFilesClient](../API/files-rest-operations.md#FileoperationsDeleteafile)
* [external-target http://msdn.microsoft.com/en-us/library/azure/dn499820.aspx](http://msdn.microsoft.com/en-us/library/azure/dn499820.aspx)
* [external-target-with-bk http://msdn.microsoft.com/en-US/library/azure/dn499820.aspx#BKMK_Web (http://msdn.microsoft.com/en-US/library/azure/dn499820.aspx#BKMK_Web)
* [out-n-back ..\howto\Starter-projects-and-code-samples.md](..\howto\Starter-projects-and-code-samples.md)
* [out-n-back-with-bk ..\howto\setup-development-environment.md#bk_VisualStudio](..\howto\setup-development-environment.md#bk_VisualStudio)
* [relative starter-projects-and-code-samples.md](starter-projects-and-code-samples.md)
* [root-relative .\starter-projects-and-code-samples.md](.\starter-projects-and-code-samples.md)

### Filter-selecting links

* <a href="setup-development-environment?ios">Open the set up topic showing the iOS filtered view</a>
* <a href="setup-development-environment?android">Open the set up topic showing the Android filtered view</a>
* <a href="setup-development-environment?javascript">Open the set up topic showing the JavaScript filtered view</a>
* <a href="setup-development-environment?aspnet">Open the set up topic showing the ASP.NET filtered view</a>

### Filter+bookmark-selecting links

* <a href="setup-development-environment?android#bk_useEclipse">Android Developer Tools and Eclipse</a>


[!INCLUDE [Enable filtering functionality ](../includes/controls/enablefiltering.xml)]