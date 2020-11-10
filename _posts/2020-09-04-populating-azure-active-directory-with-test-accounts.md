---
layout: post
title:  "Populating Azure Active Directory with test accounts"
author: Arjun Menon
categories: [ PnPPowerShell, SharePoint ]
image: assets/images/post-4.jpg
tags: [PnPPowerShell, featured]
---

I often need to set up new Office 365 tenants for development and testing, and it’s always handy to have a series of accounts in those tenants, to represent real-life scenarios. A long time ago, when we were working on-premises, and everything was in our own test Active Directories, I called upon a [trusty PowerShell script (with associated CSV and photos) put together by Mark Rhodes,<https://mrhodes.net/2011/10/25/adding-285-contoso-users-with-pictures-to-your-development-environment-active-directory/>], to populate my Active Directory. While the original public DropBox location has since disappeared, I managed to find a copy of it on one of my old VMs.

This week I felt it was about time the script got a bit of an update. My plan is to leverage an Azure AD script by GitHub user CharbelNemnom, I added Mark’s CSV and photo images to it, with a couple of tweaks to bring it all together, and presto! 272 users in Azure Active Directory, with manager relationships, phone number, locations, and photos!

You can find the script in my fork of CharbelNemnom’s repo here:

<https://github.com/mpowney/Power-MVP-Elite/tree/master/Invoke-AzureADBulkUserCreation>
After grabbing the script, ADUsers.csv file, and contents of UserImages folder (either cloning it with Git or downloading), run the following PowerShell, connecting with an account that is an Azure Active Directory admin:

$credential = Get-Credential
.\Invoke-AzureADBulkUserCreation -FilePath $pwd\ADUsers.csv -Credential $credential -Verbose
You will need to update all @contoso.com domain references in ADUsers.csv, to instead refer to the name of your Azure AD tenant. For example, if you log in to your Azure AD as an account user@fabrikam.onmicrosoft.com you should update ADUsers.csv to replace all instances of @contoso.com with @fabrikam.onmicrosoft.com

You may also have a Custom Domain in already configured your Azure Active Directory, for example, yourdomain.com. If so, replace @contoso.com with @yourdomain.com in ADUsers.csv

Note: if the PowerShell AzureAD module isn’t already installed, the above command will require you to open PowerShell as an administrator, to install the module.
