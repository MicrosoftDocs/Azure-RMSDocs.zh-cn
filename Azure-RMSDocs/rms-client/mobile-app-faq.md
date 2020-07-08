---
title: 适用于 iOS & Android 的 Azure 信息保护应用
description: 了解适用于 iOS 和 Android 设备的 Azure 信息保护（AIP）应用程序的基础知识
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/07/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 0f849dfefa6af9ffd95dcca0c731ed216f465b11
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86046396"
---
# <a name="what-is-the-azure-information-protection-app-for-ios-or-android"></a>什么是适用于 iOS 或 Android 的 Azure 信息保护应用？

适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)**

使用适用于 iOS 和 Android 的 Azure 信息保护（AIP）应用，你可以在你的电子邮件应用不支持 rights management 数据保护的情况中查看受权限保护的电子邮件（**.rpmsg**文件）。  

使用 AIP 应用，还可以查看受权限保护的 PDF 文档（受保护的 PDF 和**ppdf**文件）、图像和文本文件。

> [!NOTE]
> AIP 应用仅是查看器，并且不允许你创建新的或回复受保护的电子邮件，或者创建或编辑受保护的文件。 应用程序也无法打开所查看文件的附件，如受保护的 PDF 文档或电子邮件的附件。
>

## <a name="aip-mobile-app-requirements"></a>AIP 移动应用要求

适用于 iOS 和 Android 的 AIP 移动应用可用于以下系统：

- [支持的移动操作系统版本](#supported-mobile-os-versions)
- [支持的登录凭据](#supported-sign-in-credentials)
- [支持的文件扩展名](#supported-file-extensions)

### <a name="supported-mobile-os-versions"></a>支持的移动操作系统版本

AIP 移动应用需要以下最小移动操作系统之一： 

- iOS 11 
- Android 6。0 

> [!NOTE]
> Intel Cpu 不支持 AIP 移动应用。
> 

### <a name="supported-sign-in-credentials"></a>支持的登录凭据

使用以下操作之一登录到 AIP： 

- **工作或学校凭据。** 如果你的组织已使用移动设备扩展在本地 AD RMS，或者使用 Azure 信息保护，则使用。
 
- **一个 Microsoft 帐户**。 如果使用个人电子邮件地址来保护文件，请使用[Microsoft 帐户](https://signup.live.com)登录。 

    - 你可以使用自己的 Hotmail、Gmail 或适用于 Microsoft 帐户的任何其他电子邮件地址。
    
> [!NOTE]
> 当使用 Microsoft 帐户时，并非所有应用程序都可以打开受保护的内容。 有关详细信息，请参阅[打开受保护文档的支持方案](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)。
> 

### <a name="supported-file-extensions"></a>支持的文件扩展名

可以打开 .rpmsg、.pdf、.ppdf、.pjpg、.pjpeg、.ptiff、.ppng、.ptxt、.pxml 以及几个其他的文本和图像文件格式。

有关文本和图像文件扩展名的完整列表，请参阅管理员指南中[分类和保护的支持文件类型](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)部分中的第一个表格。

## <a name="installing-your-aip-mobile-apps-and-viewing-files"></a>安装 AIP 移动应用和查看文件

如果你的移动设备由 Microsoft Intune 管理，则你可以从公司门户下载应用。

否则，从以下内容访问应用：

- [ITunes](https://apps.apple.com/app/microsoft-rights-management/id689516635)或[Google Play](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)商店
- [Azure 信息保护下载页](https://portal.azurerms.com/#/download)。 选择 "**移动设备**" 部分中的[iOS](https://apps.apple.com/app/microsoft-rights-management/id689516635)或[Android](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)图标。

安装完成后，请等待，直到收到受保护的电子邮件或文件，并在打开时选择**AIP 查看器**。

系统将提示你使用工作或学校帐户登录，或者系统会提示你选择一个证书。 经过身份验证后，你的电子邮件或文件将会打开，你将能够读取其内容。

> [!TIP]
> 若要立即试用，请向自己发送受保护的电子邮件或文件以进行查看。 
>
> 有关详细信息，请参阅[适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用入门](mobile-app-get-started.md)。
> 

## <a name="next-steps"></a>后续步骤

使用以下方法之一来提供有关 AIP 移动应用的反馈：

- 中转到 "**设置**" "  >  **发送反馈**"
- 在我们的[Yammer 网站](https://www.yammer.com/AskIPTeam)上发布你的问题
