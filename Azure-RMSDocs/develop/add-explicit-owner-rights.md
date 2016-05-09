---
# required metadata

title: 添加显式所有者权限 | Azure RMS
description: 应用程序在从头开始创建许可证时应显式添加“所有者”权限。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b2cd9dd4-6590-488e-9efb-27bdab41eff6

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 添加显式所有者权限

应用程序在从头开始创建许可证 ([**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)) 时应显式添加“所有者”权限。

## 先决条件

应用程序在使用 [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch) 创建许可证句柄时，还必须显式授予所有者完全权限（权限）。

**注意**  使用 [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty) 以及 **IPC\_LI\_OWNER** 属性将用户设置为“所有者”不会授予所有者完全权限。

 
## 方案 - 将权限分配给许可证

在此 C++ 示例中，所需权限会添加到使用 [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch) 创建的许可证。 该示例演示如何通过权限列表创建权限并分配给许可证。

会向这些用户添加以下两种权限：

-   分配给 joe@contoso.com 的 *读取* 权限
-   分配给 mary\_kay@contoso.com 的 *完全* 权限

**注意** - 此代码示例仅演示在创建特定权限并添加到给定许可证时所涉及的步骤。

    // Create User Rights structure
    IPC_USER_RIGHTS ownerRightForOwner = {0};

    // Create rights
    LPCWSTR rgwszOwnerRights[1] = {IPC_GENERIC_ALL};

    // Assign values to members of Rights structure
    ownerRightForOwner.User.dwType = IPC_USER_TYPE_IPC;
    ownerRightForOwner.User.wszID = IPC_USER_ID_OWNER;
    ownerRightForOwner.rgwszRights = rgwszOwnerRights;
    ownerRightForOwner.cRights = 1;

    // Create User Rights structure for Joe with Read permissions
    IPC_USER_RIGHTS joeReadRight = {0};
    LPCWSTR rgwszReadRights[1] = {IPC_GENERIC_READ};

    // Assign values to members of Rights structure for Joe
    joeReadRight.User.dwType = IPC_USER_TYPE_EMAIL;
    joeReadRight.User.wszID = "joe@contoso.com";
    joeReadRight.rgwszRights = rgwszReadRights;
    joeReadRight.cRights = 1;

    // Create User Rights structure for Mary Kay with Full permissions
    IPC_USER_RIGHTS mary_kayFullRight = {0};
    LPCWSTR rgwszFullRights[1] = {IPC_GENERIC_ALL};

    // Assign values to members of Rights structure for Mary Kay
    mary_kayFullRight.User.dwType = IPC_USER_TYPE_EMAIL;
    mary_kayFullRight.User.wszID = L"mary_kay@contoso.com";
    mary_kayFullRight.rgwszRights = rgwszFullRights;
    mary_kayFullRight.cRights = 1;

    // Create User Rights List and assign the above rights
    size_t uNoOfUserRights = 3;
    PIPC_USER_RIGHTS_LIST pUserRightsList = NULL;
    pUserRightsList = reinterpret_cast<PIPC_USER_RIGHTS_LIST>
    (new BYTE[ sizeof(IPC_USER_RIGHTS_LIST) + uNoOfUserRights * sizeof(IPC_USER_RIGHTS)]);

    if(pUserRightsList == NULL)
    {
      // Handle error
    }

    // Assign values to members of Rights List structure for Joe and Mary Kay
    (*pUserRightsList).cbSize = sizeof(IPC_USER_RIGHTS_LIST);
    (*pUserRightsList).cUserRights = uNoOfUserRights;
    (*pUserRightsList).rgUserRights[0] = ownerRightForOwner;
    (*pUserRightsList).rgUserRights[1] = joeReadRight;
    (*pUserRightsList).rgUserRights[2] = mary_kayFullRight;

    // Set the Rights List property on the license via its handle
    // hLicense is a license handle created with IpcCreateLicenseFromScratch
    hr = IpcSetLicenseProperty(hLicense, FALSE, IPC_LI_USER_RIGHTS_LIST, pUserRightsList);

    if(FAILED(hr))
    {
      // Handle the error
    }



## 相关主题

* [开发人员说明](developer-notes.md)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)
 

 


<!--HONumber=Apr16_HO3-->


