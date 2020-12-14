---
title: "Getting Licensed Users vs MFA Usage"
categories:
  - Blog
tags:
  - Powershell
  - MFA
  - Office 365
slug: Licensed Users MFA Usage
---

## Comparing Licensed Users to Users with MFA Enabled

This script gets all the tenants that a partner account is managing and pulls the total licensed user accounts for each tenant and the total of licensed users that have MFA in a any state but null.

```powershell
$array = @()
Connect-MsolService
$partnerContracts = Get-MsolPartnerContract -All
foreach ($partnerContract in $partnerContracts) {
    $allusers = Get-MsolUser -TenantId $partnerContract.TenantID -All | Where-Object { $_.isLicensed -eq $true }
    $MFAUsers = Get-MsolUser -TenantId $partnerContract.TenantID -All | Where-Object { $_.isLicensed -eq $true -and $_.StrongAuthenticationMethods -ne $null -or $_.StrongAuthenticationRequirements.State -ne $null }
    $companyName = Get-MsolCompanyInformation -TenantId $partnerContract.TenantId
    $auCount = $allusers.count
    $mfauCount = $MFAUsers.count
    $results = "" | Select-Object CompanyName,Usercount,MFACount
    $results.CompanyName = $companyName.DisplayName
    $results.Usercount = $auCount
    $results.MFACount = $mfauCount
    $array += $results
}
$array
```
