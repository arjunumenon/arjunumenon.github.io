---
layout: post
title:  "Query page contents with SharePoint and M365 Search"
author: Arjun Menon
categories: [ PnPPowerShell, SharePoint ]
image: assets/images/post-2.jpg
tags: [PnPPowerShell]
---

Every time I look at the search capabilities of SharePoint and Office 365, there’s no doubt they’ve come a long way since the early days. There is also an expectation that search “just works” - predominantly because of the extraordinary capability of Google’s product and the perception that it picks up all online content, with no intervention. There is an SEO industry that specialises in making publicly available content successfully searchable by Google.

SharePoint’s search capability is highly customisable. Content metadata drives a great part of the custom capabilities of SharePoint search, and from what we’ve seen so far in the integration of SharePoint search in to the Microsoft 365 search roadmap, the ability to continue using customised search based on content metadata is not going away.

## Searching page contents

Sometimes when you have a custom search experience, there is a need to be quite specific about which parts of the content is searched, and which parts are not. Take, for example, an experience where the content of a page is important, and there is metadata with similar keywords present, that shouldn’t actually be searched. Often I’ve developed search experiences where the user has a series of refiners, they may include department names like “human resources”, and “Information technology.” With these types of refiners, it makes for a poor user experience when a user is searching for the word “human” and the results include all content identified by the “Human Resources” refiner. It’s important to separate out the keyword search capability from the refiner capability.

When a SharePoint search is executed with just keywords in a search box, the search engine looks at the full-text index, and returns all content with relevant results. The full-text index includes the contents of all pages, both modern and classic, so a basic keyword search will return any page relevant to the search query.

The advanced search scenario described above calls for what’s known as a property restricted query. This style of search query allows the search words to be specified against a particular property, but to exclude other properties from the queried keywords. For example, a using a property restricted query, a search can be performed where the words “Human Resources” exist in the page contents, but not necessarily in a page’s metadata.

Page content is, by default, included in SharePoint’s search index. This is true for classic publishing sites, and is also true for modern Communications sites, even though the underlying metadata / column name is different for the two types of sites.

## Classic pages

The classic publishing site page stores its content in a field named:

PublishingPageContent
The field schema of this field is as follows:

{% highlight typescript %}
<Field ID="{F55C4D88-1F2E-4ad9-AAA8-819AF4EE7EE8}" Name="PublishingPageContent" StaticName="PublishingPageContent" SourceID="http://schemas.microsoft.com/sharepoint/v3" Group="Page Layout Columns" DisplayName="Page Content" Description="Page Content is a site column created by the Publishing feature. It is used on the Article Page Content Type as the content of the page." Type="HTML" Required="FALSE" Sealed="TRUE" RichText="TRUE" RichTextMode="FullHtml" Customization="" />
{% endhighlight %}

## Modern pages

The modern page stores its content in a field named:

CanvasContent1
The field schema of this field looks like this: