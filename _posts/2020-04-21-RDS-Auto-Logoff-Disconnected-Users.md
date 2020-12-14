---
title: "RDS - Auto Logoff Disconnected Users"
categories: [Microsoft, RDS]
tags:
  - RDS
  - GPO
  - Remote Desktop
  - Group Policy
  - Disconnect
---

## Limit RDS disconnected times

Sometimes you its neccessary to limit the amount of time that users stay connected to your RDS environment, this could be either to save resources that are not being used or it could help in resolving issues with users and temporary profiles.

This can be done through group policy:

### GPO Configuration -

The setting which you need to change can be found here -

![Group Policy Setting RDS Session Time Limits](/assets/img/Posts/GPO/GroupPolicyRDSSessionTimeLimits.png)

User Configuration -> Administrative Templates -> Windows Components -> Remote Desktop Services -> Remote Desktop Session Host -> Session Time Limits -> Set time limit for disconnected session

![RDS Session Time Limits](/assets/img/Posts/GPO/GroupPolicyRDSSessionTimeLimits1.png)

Set to 'Enabled' and choose the time limit for user accounts in a disconnected state to be logged off.

Add the RDS server(s) to GPO Scope.

This will now automatically disconnect users after the set period has passed.
