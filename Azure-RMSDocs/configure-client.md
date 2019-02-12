---
title: Azure 信息保护客户端 - 安装和配置
description: 面向管理员提供的有关在 Windows 计算机和移动设备上部署 Azure 信息保护客户端的信息。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/05/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8b6735715bbd7ac86e75838683e14efb8864ffc3
ms.sourcegitcommit: e8b4a09db9aad7f6540b4c2fd92b1e8008c999b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737233"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Azure 信息保护客户端：客户端安装和配置

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

运行 Office 2010 的计算机需要 Azure 信息保护客户端来对 Azure 权限管理服务和 Azure 信息保护服务进行身份验证。 同时建议将此客户端用于所有支持 Azure 权限管理服务和 Azure 信息保护的 Windows 计算机以及 iOS 和 Android 设备。 

Azure 信息保护客户端通过安装 Office 外接程序与 Office 应用程序集成，方便用户从 Office 功能区直接标记和保护文档和电子邮件。 此客户端还针对 Azure Rights Management 服务无法本机支持的文件类型提供标记和保护；它还提供一个受保护文件查看器和一个文档跟踪站点，便于用户跟踪和撤销受保护的文件。

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>适用于 Windows 的 Azure 信息保护客户端：安装和配置

有关适用于 Windows 的客户端的企业安装和配置，请参阅 [Azure 信息保护管理员指南](./rms-client/client-admin-guide.md)。

> [!TIP]
> 若要为单台计算机快速安装和测试 Azure 信息保护客户端，请参阅 [Azure 信息保护客户端用户指南](./rms-client/client-user-guide.md)中的[下载和安装 Azure 信息保护客户端](./rms-client/install-client-app.md)。

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>适用于 iOS 和 Android 的 Azure 信息保护客户端：安装和管理

若要安装适用于这些常用移动平台的 Azure 信息保护客户端，可通过使用 [Microsoft Azure 信息保护页](https://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用。 不需要配置。

> [!NOTE]
> 对于 Mac 计算机，该页的链接将下载 RMS 共享应用。 这些计算机不支持 Azure 信息保护客户端。

### <a name="integration-with-intune"></a>与 Intune 集成

由于 Azure 信息保护应用使用 Microsoft Intune 应用软件开发工具包，因此通过 Intune 注册 iOS 和 Android 设备时，可以为这些设备部署并管理 Azure 信息保护应用：

1. [将 Azure 信息保护添加到 Intune](/intune/apps-add) 

2. 执行以下任一项或两项操作：
    
    - 通过[将应用分配给用户](/intune/apps-deploy)来部署应用
    
    - 使用[应用保护策略](/intune/app-protection-policies)管理应用

将 Azure 信息保护应用添加到 Intune 时的其他信息：

- 对于 iOS：从 Intune 搜索并添加应用。

- 对于 Android：添加应用时，请使用以下“应用商店 URL”：
        
        https://play.google.com/store/apps/details?id=com.microsoft.ipviewer

当 Azure 信息保护应用配置为 Android 设备的应用保护策略时，除了打开受保护的文本、图像和 PDF 文档之外，此应用还可以打开音频和视频文件。 有关详细信息，请参阅[使用 Azure 信息保护应用查看媒体文件](/intune/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app)。

## <a name="next-steps"></a>后续步骤

在安装和配置 Azure 信息保护客户端后，可能需要详细了解客户端如何解释可用于保护文档和电子邮件的不同使用权限。 有关详细信息，请参阅 [Configuring usage rights for Azure Rights Management](configure-usage-rights.md)（为 Azure Rights Management 配置使用权限）。
