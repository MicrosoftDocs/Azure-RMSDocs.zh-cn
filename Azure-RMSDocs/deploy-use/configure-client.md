---
title: "Azure 信息保护客户端&colon;安装和配置客户端 | Azure 信息保护"
description: "面向管理员提供的有关在 Windows 计算机和移动设备上部署 Azure 信息保护客户端的信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4cdac14d3a77ea7bcce23b914bc3be0a1f46d2b5
ms.openlocfilehash: 25a018cb8a94179b5eb5748efabe18a8c26c7554


---

# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Azure 信息保护客户端：安装和配置客户端

>*适用于：Azure 信息保护、Office 365*

运行 Office 2010 的计算机需要安装 Azure 信息保护客户端（或 Rights Management 共享应用程序），对 Azure 权限管理服务和 Azure 信息保护服务进行身份验证。 同时建议将此客户端用于所有支持 Azure 权限管理服务和 Azure 信息保护的 Windows 计算机以及 iOS 和 Android 设备。 

Azure 信息保护客户端通过安装 Office 外接程序与 Office 应用程序集成，方便用户从 Office 功能区直接标记和保护文档和电子邮件。 此客户端还针对 Azure 权限管理服务无法本机支持的文件类型提供标记和保护；它还提供一个受保护文件查看器和一个文档跟踪站点，便于用户跟踪和撤销受保护的文件。

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>适用于 Windows 的 Azure 信息保护客户端：安装和配置
有关适用于 Windows 的客户端的企业安装和配置，请参阅 [Azure 信息保护管理员指南](../rms-client/client-admin-guide.md)。

> [!TIP]
> 若要为单台计算机快速安装和测试 Azure 信息保护客户端，请参阅 [Azure 信息保护客户端用户指南](../rms-client/client-user-guide.md)中的[下载和安装 Azure 信息保护客户端](../rms-client/install-client-app.md)。

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>适用于 iOS 和 Android 的 Azure 信息保护客户端：安装和管理
若要安装适用于这些常用移动平台的 Azure 信息保护客户端，可通过使用 [Microsoft Azure 信息保护页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用。 不需要配置。

> [!NOTE]
> 针对 Mac 计算机和 Windows Phone，可通过此页中的链接下载适用于移动设备的 RMS 共享应用。 这些设备当前不支持 Azure 信息保护客户端。

**如果安装了 Microsoft Intune**：由于 Azure 信息保护应用包括 Microsoft Intune 应用软件开发工具包，因此通过 Intune 注册 iOS 和 Android 设备时，可以为这些设备部署并管理 Azure 信息保护查看器。 更多详细信息，请参阅 Intune 文档中的[在 Microsoft Intune 控制台中配置和部署移动应用程序管理策略](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 对于步骤 2，使用说明来发布策略托管应用。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Feb17_HO2-->

