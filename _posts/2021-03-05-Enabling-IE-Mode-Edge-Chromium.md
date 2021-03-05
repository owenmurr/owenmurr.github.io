---
title: "Enabling IE Mode in Edge Chromium"
description: "A quick script to enable IE mode in Edge Chromium Version. This will allow for sites that require ActiveX, for example, to work correctly in Edge."
categories: [Edge]
tags:
  - Microsoft
  - Edge
  - IE
  - Internet Explorer
slug: Edge IE Mode
---

1. Download the ADMX files from Microsoft for Edge to the root of the user folder.
2. Unzip the file.
3. Copy the ADMX files to the local PolicyDefinitions folder.  
4. Create the registry keys that would normally be created when enabling the settings in Group Policy.
5. Check that IE is installed/enabled on the machine.

```powershell
#Requires -RunAsAdministrator

$source = "https://msedge.sf.dl.delivery.mp.microsoft.com/filestreamingservice/files/814d7696-a129-49c5-9060-1345a83c4a66/MicrosoftEdgePolicyTemplates.zip"

$zipFile = "C:\Users\$env:USERNAME\edgeadmx.zip"
$unzipFile = "C:\Users\$env:USERNAME\edgeadmx"

Write-host "Downloading Microsoft Edge Policy Templates" -ForegroundColor Black -BackgroundColor Magenta
Invoke-WebRequest -Uri $source -OutFile $zipFile

Write-Host "Expanding Zip file" -ForegroundColor Black -BackgroundColor Magenta
Expand-Archive -Path $zipfile -DestinationPath $unzipFile -Force

Write-Host "Copying ADMX file to C:\Windows\PolicyDefinitions" -ForegroundColor Black -BackgroundColor Magenta
Copy-Item -Path $unzipFile\windows\admx\msedge.admx -Destination "C:\Windows\PolicyDefinitions"

Write-Host "Copying ADML file to C:\Windows\PolicyDefinitions\en-US" -ForegroundColor Black -BackgroundColor Magenta
Copy-Item -Path $unzipFile\windows\admx\en-US\msedge.adml -Destination "C:\Windows\PolicyDefinitions\en-US"

Write-Host "Creating new registry key - Edge" -ForegroundColor Black -BackgroundColor Magenta
New-Item -Path HKLM:\SOFTWARE\Policies\Microsoft\ -Name Edge

Write-Host "Creating new DWORD value - InternetExplorerIntegrationLevel" -ForegroundColor Black -BackgroundColor Magenta
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Edge -Name "InternetExplorerIntegrationLevel" -Value "1" -PropertyType DWord

Write-Host "Creating new STRING value - InternetExplorerIntegrationSiteList" -ForegroundColor Black -BackgroundColor Magenta
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Edge -Name "InternetExplorerIntegrationSiteList" -Value "file:///C:\Users\$env:USERNAME\edgeIE11SiteList.xml" -PropertyType String

Write-host "Checking that Internet Explorer is enabled" -ForegroundColor Black -BackgroundColor Magenta
$IE = Get-WindowsOptionalFeature -Online | Where-Object { $_.FeatureName -eq "Internet-Explorer-Optional-amd64" }

If ($IE.state -Match "Enabled") {
    Write-Host "Internet Explorer already enabled" -ForegroundColor Black -BackgroundColor Magenta
} else {
    Write-Host "Enabling Internet Explorer" -ForegroundColor Black -BackgroundColor Magenta
    Enable-WindowsOptionalFeature -FeatureName Internet-Explorer-Optional-amd64 -All -Online
    Write-Host "If this errors in anyway, please install via Settings and install from the optional features menu. Powershell and Settings dont seem to play well" -ForegroundColor Black -BackgroundColor Red
}
```

An XML file is also required, an example of this below. The XML file can contain multiple sites.

```xml
<site-list version="1">
    <created-by>
        <tool>EMIESiteListManager</tool>
        <version>10.0.14357.1004</version>
        <date-created>04/01/2020 12:28:42</date-created>
    </created-by>
    <site url="www.google.com">
        <compat-mode>Default</compat-mode>
        <open-in>IE11</open-in>
    </site>
</site-list>
```
You may need to reboot the machine for the new changes to be detected. 

To confirm everything above is working correctly you will see the IE icon next to the URL bar in Edge.

![Edge IE Mode"](/assets/img/Posts/Edge/EdgeIEMode.png)