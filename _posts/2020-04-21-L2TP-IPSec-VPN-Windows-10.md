---
title: "L2TP/IPSec VPN in Windows 10"
categories:
  - Blog
tags:
  - VPN
  - L2TP
  - IPSec
  - Registy
  - Windows 10
slug: 
---

Add the registry key needed to allow L2TP/IPSec VPNs to connect correctly in Windows 10.

```bat
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PolicyAgent /v AssumeUDPEncapsulationContextOnSendRule /d 2 /t REG_DWORD
```
