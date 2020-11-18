---
layout: post
title:  "Get Permission Report for a file in SharePoint Online using REST API"
author: Arjun Menon
categories: [ SharePoint Online, Document Library ]
image: assets/images/Permission-SPDocument-REST.jpg
tags: [SharePointOnline]
---

How do we get the permission report for a particular SharePoint file. Now with change in Sharing experience in Modern SharePoint, there are many aspects like **external sharing**, **direct sharing**, **sharing via link** etc for sharing unlike the conventional sharing which was there before. With easiness comes responsibility, right?
How do we get the permission report using REST API.

There is a method called `GetSharingInformation` which you is part of SharePoint List Item REST API which could be called. This will give you an output which has detailed information about Shared links, principals with whom the file has been shared with etc. etc. All you need to do is go through the result and fetch the needed information. 
So your complete URL would look something like this,

    https://contoso.sharepoint.com/sites/contososite/_api/web/lists/getbytitle('Documents')/items(2)/GetSharingInformation?$select=permissionsInformation&$Expand=permissionsInformation

I will be writing another blog which talks about the various properties which are available as an output of the REST call.

Thanks to the initial findings of this nugget by [Paul Matthews](https://twitter.com/cann0nf0dder){:target="_blank"} in his [BLOG](https://cann0nf0dder.wordpress.com/2018/04/04/externally-sharing-getsharinginformation-rest-api/){:target="_blank"} without which I would have struggled for another 2 days or more to find this.

<span>Photo by <a href="https://unsplash.com/@ubahnverleih?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">C M</a> on Unsplash</span>
