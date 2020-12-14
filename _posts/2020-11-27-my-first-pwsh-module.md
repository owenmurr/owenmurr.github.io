---
title: "My First Published Powershell Module"
description: 
date: 2020-11-27 08:00:00 +0000
categories: [Powershell, Modules]
image: /assets/img/Posts/powershell.png
tags:
  - Powershell
  - PWSH
  - Module
  - api
  - IP Geo Location
  - IP Address
slug: my first pwsh module
---

## My First Published Powershell Module

### Get-IPGeolocation.psm1

I have published my first Powershell module to PSGallery.

Sometimes in my day to day job I need a quick way of looking up IP information and wanting a quicker method that doesn't mean I have to open up a web browser and visit a website, I wrote a small Powershell module to allow me to get the information.

The module pulls information on entered IP addresses using the [ipapi](https://ipapi.co/) api, which allows for upto 30000 free calls per month and upto 1000 a day.

### Usage

At the moment it is relatively simple module with one function:

```powershell
Get-IPGeolocation -IPAddress <IP> -AllInfo
```

The above command will return all available information available from [ipapi](https://ipapi.co/).

Without the -AllInfo switch it only returns a minimal information:

```powershell
C:\Users\Owen Murr> Get-IPGeolocation -IPAddress 1.1.1.1

IP      Country   City   Org
--      -------   ----   ---
1.1.1.1 Australia Sydney CLOUDFLARENET
```

### Installation

It can be installed from [PSGallery](https://www.powershellgallery.com/):

```powershell
Install-Module -Name IPGeolocation
```
