---
title: "Moving Virtual Machine Storage - Error 0x80070005"
categories:
  - Blog
tags:
  - Virtual Machine
  - VM
  - Hyper-V
  - Virtual Machine Storage
  - Moving VM Storage
  - Error Code 0x80070005
Slug: Virtual Machine Storage 0x80070005
---

## Moving Virtual Machine Storage - Error 0x80070005

Recently I have needed to move Hyper-V VMs storage to another CSV for a customer. When moving the VM through the GUI, I have selected the VHD and moved this over to the root of the storage folder.

This then has given me the following error:

![Error code 0x80070005 Virtual Machine Storage](/assets/img/Posts/VMStorageMove.jpg)

To get around this error, I created a new folder in the storage location matching the name of the server. Once created I was able to select this as the new location for the VM data and move the data successfully without any further issues.
