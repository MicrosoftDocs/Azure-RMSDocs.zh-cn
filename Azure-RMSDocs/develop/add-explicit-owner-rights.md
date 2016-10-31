---
title: "如何添加显式所有者权限 | Azure RMS"
description: Your application should explicitly add "Owner" rights when creating a license from scratch.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EF43FAC4-ABB4-459D-B173-972B5716F816
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8be965d76578c28457eee207b56e5da83f7eb468
ms.openlocfilehash: 36c0bece4fb99e4d92fcda0c57da1b3cee11e37a


---

# 操作说明：添加显式所有者权限

应用程序使用 [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx) 从头开始创建许可证时应显式添加“所有者”权限。

## 先决条件

应用程序在使用 [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx) 创建许可证句柄时，还必须显式授予所有者完全权力（权限）。

>[!NOTE] 
> 使用 [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx) 以及 **IPC\_LI\_OWNER** 属性将用户设置为“所有者”不会授予所有者完全权限。

下列示例代码仅演示创建特定权限并添加到给定许可证时所涉及的步骤。

## 说明
 
## 步骤 1：示例方案

在此示例中，所需权限会添加到使用 [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx) 创建的许可证。 该示例演示如何通过权限列表创建权限并分配给许可证。

会向这些用户添加以下两种权限：

-   分配给 joe@contoso.com 的 *读取* 权限
-   分配给 mary\_kay@contoso.com 的 *完全* 权限

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

- [开发人员说明](developer-notes.md)
- [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx)
- [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)
 

 



<!--HONumber=Oct16_HO3-->


