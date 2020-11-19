---
layout: post
title:  "Authenticating SharePoint with Multi Factor Authentication using PnP PowerShell"
author: Arjun Menon
categories: [ PnPPowerShell, SharePoint ]
image: assets/images/NewApplication.jpg
tags: [PnPPowerShell]
---
SharePoint PnP PowerShell is super helpful when you have a schedule jobs running. You just need to create a package and schedule it in your jobs.

But the issue comes when you have Multi-factor authentication. With Multi-factor authentication, you would need an attended access which is impossible for scheduled PowerShell execution.

We do have details in the PnP PowerShell App Permission article. But since it did not cover the complete approach, I though I would jot it down.

With that in place the solution would be to authenticate using Azure AD App authentication mechanism. We had initiate an issue in GitHub and got response from PnP Legend Erwin Van Huen that Add-In method is recommended. I had to spent some time myself for that to completed. So I thought I would jot the steps which I had followed.

Please keep in mind the pre-requisites for the below approach

PnP PowerShell in your machine
SharePoint Online
Azure AD Management Permission
Since you are going to create an Application in Azure AD, you would need the permission

 Steps are as below.

## Generate Certificate

```powershell
$CommonName = "SP Online PowerShell Authentication"
$OrganizationName = "AUM INC."
$CertificatePath = "C:\PowerShellScript\Certifate\\PnPPSSPACerti.PFX"

$AuthenticatorCertificate = New-PnPAzureCertificate -CommonName $CommonName -Organization $OrganizationName  -out $CertificatePath

Write-Host $AuthenticatorCertificate.KeyCredentials
```

The above script will generate the PFX file in the location. It will show something like the below.

Random update for testing the Pages..
