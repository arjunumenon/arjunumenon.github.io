---
layout: post
title:  "Get SharePoint Document Library Name from the File Unique ID using REST API"
author: Arjun Menon
categories: [ SharePoint Online, Document Library ]
image: assets/images/documentlibrary-name-REST.jpg
tags: [SharePoint]
---

Have you recieved a use case where you need to know the Document Library Name from the Unique Id of the File. Let us assume you have a URL with unique File id something similar to this, 

` https://contoso.sharepoint.com/:w:/r/sites/contososite/_layouts/15/Doc.aspx?sourcedoc=%7BD0E8F75B-DCD7-478E-9CAA-41944F21D722%7D&file=MySharingCentral.docx&action=default&mobileredirect=true `

You know that the File Unique ID is `D0E8F75B-DCD7-478E-9CAA-41944F21D722`
How do we get to know the Document Library Name and if needed Item id from there?
There is a REST API Method GetFileById via which you will be able to get the information about the file. But by default, you will just get the information about the file without library information.
There comes the life safer expand parameter, `ListItemAllFields/ParentList`. With the expansion for ParentList attribute, you will get the information about the List / Library where the file belongs to. How cool is that?
Now the whole API call may look something similar to this,

    https://contoso.sharepoint.com/sites/contososite/_api/web/GetFileById('d0e8f75b-dcd7-478e-9caa-41944f21d722')/?$expand=ListItemAllFields/ParentList

and Bingo, you will get the result like below.

    {
        "ListItemAllFields": {
            "ParentList": {
                "AllowContentTypes": true,
                "BaseTemplate": 101,
                "BaseType": 1,
                "ContentTypesEnabled": false,
                "CrawlNonDefaultViews": false,
                "Created": "2020-07-11T19:32:18Z",
                "CurrentChangeToken": {
                    "StringValue": "1;3;cb640971-a01a-4d1c-8995-2559ec5079a5;637408756053300000;236691478"
                },
                "DefaultContentApprovalWorkflowId": "00000000-0000-0000-0000-000000000000",
                "DefaultItemOpenUseListSetting": false,
                "Description": "",
                "Direction": "none",
                "DisableGridEditing": false,
                "DocumentTemplateUrl": "/sites/contososite/Shared Documents/Forms/template.dotx",
                "DraftVersionVisibility": 0,
                "EnableAttachments": false,
                "EnableFolderCreation": true,
                "EnableMinorVersions": false,
                "EnableModeration": false,
                "EnableRequestSignOff": true,
                "EnableVersioning": true,
                "EntityTypeName": "Shared_x0020_Documents",
                "ExemptFromBlockDownloadOfNonViewableFiles": false,
                "FileSavePostProcessingEnabled": false,
                "ForceCheckout": false,
                "HasExternalDataSource": false,
                "Hidden": false,
                "Id": "cb640971-a01a-4d1c-8995-2559ec5079a5",
                "ImagePath": {
                    "DecodedUrl": "/_layouts/15/images/itdl.png?rev=47"
                },
                "ImageUrl": "/_layouts/15/images/itdl.png?rev=47",
                "IrmEnabled": false,
                "IrmExpire": false,
                "IrmReject": false,
                "IsApplicationList": false,
                "IsCatalog": false,
                "IsPrivate": false,
                "ItemCount": 4,
                "LastItemDeletedDate": "2020-07-11T19:32:18Z",
                "LastItemModifiedDate": "2020-11-13T14:42:14Z",
                "LastItemUserModifiedDate": "2020-11-04T15:18:26Z",
                "ListExperienceOptions": 0,
                "ListItemEntityTypeFullName": "SP.Data.Shared_x0020_DocumentsItem",
                "MajorVersionLimit": 500,
                "MajorWithMinorVersionsLimit": 0,
                "MultipleDataList": false,
                "NoCrawl": false,
                "ParentWebPath": {
                    "DecodedUrl": "/sites/contososite"
                },
                "ParentWebUrl": "/sites/contososite",
                "ParserDisabled": false,
                "ServerTemplateCanCreateFolders": true,
                "TemplateFeatureId": "00bfea71-e717-4e80-aa17-d0c71b360101",
                "Title": "Documents"
            },
    }
 And you can can see that there is a property called **Title** which is basically the name of your document library.

 <span>Photo by <a href="https://unsplash.com/@mvdheuvel?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Maarten van den Heuvel</a> on Unsplash</span>
