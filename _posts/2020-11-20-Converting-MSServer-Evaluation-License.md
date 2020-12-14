---
title: "Convert Microsoft Server Evaluation Version to Full Version"
date: 2020-11-20 14:00:00 +0000
categories: [Microsoft, Server]
tags:
  - Microsoft
  - Server
  - License
  - Convert
slug: MS Server Evaluation to Full
---

Before you upgrade the license on a evaluation installation of Microsoft Server, you will need to install the KMS client key for the installed version the OS you are using.

## Finding the KMS Client Key

Microsoft list all available KMS keys [here](https://docs.microsoft.com/en-us/windows-server/get-started/kmsclientkeys)

### Installing the KMS Client Key

Now that you have the KMS Client Key that matches the version of Microsoft Server you are running you will need to install it using the DISM tool.

```bat
DISM /Online /Set-Edition:ServerStandard /ProductKey:N69G4-B89J2-4G8F4-WWYCC-J464C /AcceptEula
```

*In the above example it is using the KMS Client Key for Microsoft Server Standard 2019. You will need to change Set-Edition to match the version you're using.*

Once the above command has completed you will be prompted to reboot the server. You will need to go ahead and restart the server.
You will now see that the evaluation details in the bottom right of the desktop has now been removed.

## Installing the MAK license Key

You will find your MAK license key/product key in your VLSC portal.

To install your license key you will need to use the slmgr tool.

```bat
slmgr /ipk <INSERT YOUR KEY>
```

You will now need to activate this, again using the slmgr tool.

```bat
slmgr /ato
```

To confirm that the activation has worked, you should see window confirming that the activation was successful.
