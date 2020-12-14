---
title: "Installing Exchange Management Module - Nuget Error"
categories:
  - Blog
tags:
  - Powershell
  - Exchange
  - Office 365
  - Module
  - Nuget
  - Package Management
  - ExchangeOnlineManagement
slug: EXO Powershell Nuget Error
---

## Installing Exchange Online Management Module in Powershell- Nuget Error

You may find that you get an error when installing Exchange Management Module in Powershell.

The error you may see is something along the lines of:

```powershell
  PackageManagement\Install-PackageProvider : No match was found for the specified search criteria for the provider
  'NuGet'. The package provider requires 'PackageManagement' and 'Provider' tags. Please check if the specified package
  has the tags
 ```

 To get around this error message, you will need to run the following:

 ```powershell
  [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```

I then installed the Nuget package provider, to do this enter the following:

```powershell
  Install-PackageProvider -Name NuGet
```

Once both of the above commands have been run you will then be able to install the Exchange Online Management module as normal by running:

```powershell
  Install-Module -Name ExchangeOnlineManagement
```
