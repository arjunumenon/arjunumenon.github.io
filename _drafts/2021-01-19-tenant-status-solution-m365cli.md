---
layout: post
title:  "Monitor and Notify Office 365 health status using CLI for Microsoft 365"
author: Arjun Menon
categories: [ M365Status, M365CLI, ITPro]
image: assets/images/2021-01-19-tenant-status-solution-m365cli.jpg
tags: [M365Status, M365CLI, featured]
---

Are you an IT Pro who wants to have a solution which checks the status of your Microsoft 365 Tenant. You can always get the status of Microsoft 365 status, whether everything is going smooth or are there any outages going on currently.

How about if you get notified when something goes wrong in your tenant and you gets that information before your users complain. Awesome, right?

## Solution

[CLI for Microsoft 365](https://pnp.github.io/cli-microsoft365/){:target="_blank"} provides some powerful and lightweight commands via which you can get the health status of your Office 365 Tenant. With the combination multiple commands, you can create a full fledged and powerful solution through which you can get updates, notified if some of the services are not working as expected.

Following are the actions which we are doing for completing the solution

### 1. CLI Command / Logic

1. Check the health status of your tenant using Microsoft 365
2. If the status is something other than normal,
   1. Add the details to a SharePoint List with details
      1. Bonus Solution : Create a Power Automate which will be triggered on the item creation and define any complex logic if needed
   2. Send an email notification immediately to configured users
3. No action needs to be done if the status is normal

### 2. Schedule the script

1. Create a PowerShell script with commands usin CLI for Microsoft 365
2. Using Windows Scheduler, schedule the PowerShell scripts to be run every minute

## Implementation

### Authentication and Login

Biggest advantage CLI for Microsoft 365 has is its ability to [Persist Connection Information](https://pnp.github.io/cli-microsoft365/concepts/persisting-connection/){:target="_blank"}. After logging in to Microsoft 365, the CLI for Microsoft 365 will persist the information about the connection until you explicitly log out from Microsoft 365
Once you have authenticated to the tenant, your scripts will be executed without the need for authentication everytime. Since the solution is not a confidential or Complex business Process, it is safe to go ahead with this approach. CLI for Microsoft 365 also provides [Logging in with Certificate](https://pnp.github.io/cli-microsoft365/user-guide/connecting-office-365/#log-in-using-a-certificate){:target="_blank"} if you prefer that approach.
