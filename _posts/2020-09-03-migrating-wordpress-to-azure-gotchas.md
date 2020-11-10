---
layout: post
title:  "Query page contents with SharePoint and M365 Search"
author: Arjun Menon
categories: [ PnPPowerShell, SharePoint ]
image: assets/images/post-3.jpg
tags: [PnPPowerShell]
---

I’m in the process of migrating a WordPress site to be hosted in Azure, primarily to make it easier to manage and configure than its current host in DreamHost.

Source:

- PHP 5.x
- MySQL

Destinations:

Azure WordPress Docker image (with MySQL in App enabled)
Azure Linux WordPress Docker image (with a separate Azure MySQL service)
This post is a work-in-progress. I’m writing this post to keep track of the issues faced with different hosting options available in Azure.

## Azure Linux WordPress Docker image

MySQL in App doesn’t seem to be supported on a Linux image - however this post suggests otherwise
The MySQL image for Azure doesn’t support MyISAM as a data engine due to lack of transaction support; if your original WordPress database uses
