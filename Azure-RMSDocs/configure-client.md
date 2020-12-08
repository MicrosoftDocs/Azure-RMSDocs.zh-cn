---
title: Azure 信息保护客户端 - 安装和配置
description: 有关在 Windows 计算机和移动设备上部署 Azure 信息保护客户端的管理员信息。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e19400a0901c62bd00f7cd965e23ea01c36be395
ms.sourcegitcommit: 13dac930fabafeb05d71d7ae8acf5c0a78c12397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96849736"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Azure 信息保护客户端：安装和配置客户端

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

>[!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

运行 Office 2010 的计算机需要 Azure 信息保护客户端 (经典) 或 Azure 信息保护统一标签客户端向 Azure 信息保护服务进行身份验证。

不确定这两个客户端之间有何区别？  请参阅 [Azure 信息保护客户端和 Azure 信息保护统一标签客户端之间有何区别？](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)

对于所有 Windows 计算机，也建议使用这些客户端，因为它们安装 Office 加载项，以便用户可以直接从 Office 功能区轻松地标签和保护文档和电子邮件。 这些客户端还为受保护服务 (Azure Rights Management) 提供的文件类型提供标记和保护，并提供 Office 应用无法打开的受保护文件的查看器。 IOS 和 Android 有一个类似的查看器。

经典客户端还支持文档跟踪站点，使用户可以跟踪和撤销受保护的文件。

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>适用于 Windows 的 Azure 信息保护客户端：安装和配置

有关适用于 Windows 的客户端的企业安装和配置，请参阅以下管理指南：

- 统一标签客户端： [Azure 信息保护统一标签客户端管理员指南](./rms-client/clientv2-admin-guide.md)

- 经典客户端： [Azure 信息保护客户端管理员指南](./rms-client/client-admin-guide.md)

但是，如果要为一台计算机快速安装和测试这些客户端，请参阅用户指南中的以下说明：

- 统一标签客户端： [下载并安装 Azure 信息保护统一标签客户端](./rms-client/install-unifiedlabelingclient-app.md)

- 经典客户端：从[Azure 信息保护客户端用户指南](./rms-client/client-user-guide.md)[下载并安装 azure 信息保护客户端](./rms-client/install-client-app.md)。

## <a name="the-azure-information-protection-app-for-ios-and-android-installation-and-management"></a>适用于 iOS 和 Android 的 Azure 信息保护应用：安装和管理

若要安装适用于 iOS 和 Android 的 Azure 信息保护应用查看器，请使用 [Microsoft Azure 信息保护页](https://go.microsoft.com/fwlink/?LinkId=303970)上的链接。 不需要任何配置。

> [!NOTE]
> 对于 Mac 计算机，该页的链接将下载 RMS 共享应用。 这些计算机不支持 Azure 信息保护客户端。

### <a name="integration-with-intune"></a>与 Intune 集成

由于 Azure 信息保护查看器应用使用 Microsoft Intune 应用软件开发工具包，因此在 Intune 注册 iOS 和 Android 设备时，可以为这些设备部署并管理 Azure 信息保护查看器应用：

1. [将 Azure 信息保护添加到 Intune](/intune/apps/apps-add)

2. 执行以下任一项或两项操作：

    - 通过[将应用分配给用户](/intune/apps/apps-deploy)来部署应用

    - 使用[应用保护策略](/intune/apps/app-protection-policies)管理应用

将 Azure 信息保护应用添加到 Intune 时的其他信息：

- 对于 iOS：从 Intune 搜索并添加应用。

- 对于 Android：添加应用时，请使用以下 **APPSTORE URL**：

    ```md
    https://play.google.com/store/apps/details?id=com.microsoft.ipviewer
    ```

当 Azure 信息保护应用配置为 Android 设备的应用保护策略时，除了打开受保护的文本、图像和 PDF 文档之外，此应用还可以打开音频和视频文件。 有关详细信息，请参阅[使用 Azure 信息保护应用查看媒体文件](/intune/fundamentals/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app)。

## <a name="next-steps"></a>后续步骤

安装并配置 Azure 信息保护客户端后，你可能需要了解有关客户端如何解释可用于保护文档和电子邮件的不同使用权限的详细信息。 有关详细信息，请参阅 [配置 Azure 信息管理的使用权限](configure-usage-rights.md)。
