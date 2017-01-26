---
title: "Rights Management 共享应用程序&colon;客户端安装和配置 | Azure 信息保护"
description: "面向管理员提供的有关在 Windows 计算机和移动设备上部署 Rights Management (RMS) 共享应用程序的信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 0d15a232bc1f0b1bce94e48c7e9c6f6b9419b5dd


---

# <a name="rights-management-sharing-application-installation-and-configuration-for-clients"></a>权限管理共享应用程序：客户端安装和配置

>*适用于：Azure 信息保护、Office 365*

客户端计算机需要使用 Rights Management (RMS) 共享应用程序，才能将 Azure Rights Management 服务用于 Office 2010，建议在支持 Azure 信息保护中的 Azure Rights Management 服务的所有计算机和移动设备上使用该应用程序。 通过安装 Office 加载项，RMS 共享应用程序可与 Office 应用程序集成在一起，使得用户能够轻松地从功能区直接保护文件和电子邮件。 RMS 共享应用程序还针对 Azure Rights Management 服务无法以本机方式支持的文件类型提供常规保护；它还提供一个文档跟踪站点，以便让用户跟踪保护的文件和撤消保护。

## <a name="the-rms-sharing-application-for-windows-installation-and-configuration"></a>适用于 Windows 的 RMS 共享应用程序：安装和配置
若要为企业部署安装和配置适用于 Windows 的 RMS 共享应用程序，请参阅 [Rights Management 共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)。

> [!TIP]
> 如果你希望为单个计算机快速安装和测试 RMS 共享应用程序，请参阅 [Rights Management 共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)中的[下载和安装 Rights Management 共享应用程序](../rms-client/install-sharing-app.md)。

## <a name="the-rms-sharing-application-for-mobile-platforms-installation-and-management"></a>适用于移动平台的 RMS 共享应用程序：安装和管理
若要安装适用于移动平台的 RMS 共享应用程序，请使用 [Microsoft Rights Management 页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用程序。 在此应用中使用 Azure Rights Management 服务不需要任何配置。

> [!NOTE]
> 适用于 iOS 和 Android 的 RMS 共享应用程序现已替换为 Azure 信息保护应用。

**如果安装了 Microsoft Intune**：由于 Azure 信息保护应用包括 Microsoft Intune 应用软件开发工具包，因此通过 Intune 注册 iOS 和 Android 设备时，可以为这些设备部署并管理 Azure 信息保护应用。 更多详细信息，请参阅 Intune 文档中的[在 Microsoft Intune 控制台中配置和部署移动应用程序管理策略](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 对于步骤 2，使用说明来发布策略托管应用。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Jan17_HO4-->


