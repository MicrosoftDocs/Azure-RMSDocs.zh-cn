---
# required metadata

title: 从 AD RMS 迁移到 Azure Rights Management - 阶段 2 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# 迁移阶段 2 - 客户端配置

*适用于：Active Directory Rights Management Services、Azure Rights Management*

使用以下信息，完成从 AD RMS 迁移到 Azure Rights Management (Azure RMS) 的阶段 2。 这些过程涉及[从 AD RMS 迁移到 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 中的步骤 5.


## 步骤 5. 将客户端重新配置为使用 Azure RMS
对于 Windows 客户端：

1.  [下载迁移脚本](http://go.microsoft.com/fwlink/?LinkId=524619)：

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    这些脚本将重置 Windows 计算机上的配置，以使其将使用 Azure RMS 服务而不是 AD RMS。

2.  按照重定向脚本 (Redirect_OnPrem.cmd) 中的说明修改脚本，使其指向新的 Azure RMS 租户。

3.  在 Windows 计算机上，使用提升的特权，在用户的上下文中运行这些脚本。

对于移动设备客户端和 Mac 计算机：

-   删除在部署 [AD RMS 移动设备扩展](http://technet.microsoft.com/library/dn673574.aspx)时创建的 DNS SRV 记录.

#### 由迁移脚本进行的更改
本节介绍迁移脚本进行的更改。 你只能将此信息出于参考目的，或用于故障排除，或者用于你想要自己进行这些更改的场合。

CleanUpRMS_RUN_Elevated.cmd：

-   删除 %userprofile%\AppData\Local\Microsoft\DRM 和 %userprofile%\AppData\Local\Microsoft\MSIPC 文件夹的内容，包括任何子文件夹以及具有长文件名的任何文件。

-   删除以下注册表项的内容：

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   删除以下注册表值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd：

-   为以下每个位置下作为参数提供的每个 URL 创建以下注册表值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    每一项均具有 REG_SZ 值 **https://OldRMSserverURL/_wmcs/licensing**，其数据采用以下格式：**https://&lt;YourTenantURL&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* 采用以下格式：**{GUID}.rms.[Region].aadrm.com**.
    > 
    > 例如：5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > 在对 Azure RMS 运行 **Get-AadrmConfiguration** cmdlet 时，可以通过标识 [RightsManagementServiceId](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) 值找到此值。


## 后续步骤
要继续迁移，请转到[阶段 3 - 支持复制配置](migrate-from-ad-rms-phase3.md).

<!--HONumber=Apr16_HO4-->


