---
# required metadata

title: Rights Management 共享应用程序 &colon; 客户端安装和配置 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 权限管理共享应用程序：客户端安装和配置

*适用于：Azure Rights Management、Office 365*

客户端计算机需要权限管理 (RMS) 共享应用程序，才能将 Azure RMS 用于 Office 2010，建议在支持 Azure RMS 的所有计算机和移动设备上使用该应用程序。 通过安装 Office 加载项，RMS 共享应用程序可与 Office 应用程序集成在一起，使得用户能够轻松地从功能区直接保护文件和电子邮件。 RMS 共享应用程序还针对 Azure RMS 无法以本机方式支持的文件类型提供常规保护，以保护所有文件类型；此外，它提供一个文档跟踪站点，让用户跟踪他们保护的文件和撤消保护。

## 适用于 Windows 的 RMS 共享应用程序：安装和配置
若要为企业部署安装和配置适用于 Windows 的 RMS 共享应用程序，请参阅 [Rights Management 共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md).

> [!TIP]
> 如果你希望为单个计算机快速安装和测试 RMS 共享应用程序，请参阅 [Rights Management 共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)中的[下载和安装 Rights Management 共享应用程序](../rms-client/install-sharing-app.md).

## 适用于移动平台的 RMS 共享应用程序：安装和管理
若要安装适用于移动平台的 RMS 共享应用程序，请使用 [Microsoft Rights Management 页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用程序。 无需任何配置即可将 Azure RMS 用于此应用。

**如果你有 Microsoft Intune**：因为 RMS 共享应用包括了 Microsoft Intune 应用软件开发工具包，所以你拥有以下选项：

-   对于通过 Intune 注册的设备，可以为运行 iOS 和 Android 的设备部署和管理 RMS 共享应用。 更多详细信息，请参阅 Intune 文档中的[在 Microsoft Intune 控制台中配置和部署移动应用程序管理策略](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 对于步骤 2，使用说明来发布策略托管应用。

-   对于不是通过 Intune 注册的设备，可以为运行 Android 的设备管理 RMS 共享应用。 有关详细信息，请参阅[使用 Microsoft Intune 创建和部署移动应用管理策略](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune).



<!--HONumber=Apr16_HO4-->


