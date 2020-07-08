---
title: 入门 - 适用于 iOS 和 Android 的 AIP 应用
description: 使用适用于 iOS 和 Android 的 Azure 信息保护应用查看电子邮件或文件
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/07/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 4b50f89c9f8d0a965b630c82461f1190bb893938
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048691"
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用入门

适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)**

本页介绍如何测试运行适用于 iOS 或 Android 的 Azure 信息保护应用。

当用户需要打开受保护的电子邮件或文件时，大多数用户通常都会使用 Azure 信息保护应用。 但是，如果你是管理员为你的用户测试应用程序，或者你只是想要在需要时试用它，请使用下面的说明查看设备上受保护的文件。

> [!IMPORTANT]
> 在开始之前，请仔细阅读有关[适用于 iOS 或 Android 的 Azure 信息保护应用](mobile-app-faq.md)的要求和说明。
> 

## <a name="access-a-protected-file-from-your-device"></a>从设备访问受保护的文件

若要测试 AIP 移动应用，请确保可以从设备访问以下类型的受保护文件之一：

|文件类型  |说明  |
|---------|---------|
|**.Rpmsg 文件**     | 受权限保护的电子邮件消息。 如果你的移动电子邮件应用不以本机方式支持 rights management 数据保护，受保护的电子邮件将显示为电子邮件附件。 </br></br>使用其他设备（如 Windows 计算机上的 Outlook）向自己发送受权限保护的电子邮件，可以从移动设备访问该邮件。 </br></br>**注意：** 有关以本机方式支持 rights management 的电子邮件客户端的列表，请参阅[启用应用程序](../requirements-applications.md#rms-enlightened-applications)中的**电子邮件**列。 |
|**受权限保护的 PDF 文件**     | 1. 从 Windows 计算机中，使用 AIP[经典](client-classify-protect.md)或[统一标签客户](clientv2-classify-protect.md)端客户端保护 PDF 文件。 </br>2. 向自己发送受保护的 PDF，或将其上传到 SharePoint 受保护的库，并将其共享到你自己的电子邮件地址。        |
|**.Ptxt 或 .pjpg 或 .ppng**     | 1. 从 Windows 计算机上，使用 AIP[经典](client-classify-protect.md)或[统一标签客户](clientv2-classify-protect.md)端客户端保护文本或图像文件。 </br></br>2. 向自己发送受保护的文件，或将其上传到 SharePoint 受保护的库，并将其共享到你自己的电子邮件地址。 </br></br>**注意：** 有关详细信息，请参阅[分类和保护支持的文件类型](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)   |
| | |

### <a name="open-the-protected-file-on-your-mobile"></a>打开移动设备上的受保护文件

1. 点击电子邮件附件或链接以打开受保护的内容。

1. 出现提示时，选择 " **AIP 查看器**" 应用以查看受保护的内容。

1. 出现提示时，请使用你的工作或学校帐户登录，或者选择一个证书。

经过身份验证后，AIP 查看器应用会显示电子邮件或文件。

> [!NOTE]
> 始终打开受保护的内容，以打开 AIP 应用。 在出现提示时，请不要尝试登录到应用程序，或从 AIP 查看器应用程序中打开受保护的文件。
> 

## <a name="next-steps"></a>后续步骤

使用以下方法之一来提供有关 AIP 移动应用的反馈：

- 中转到 "**设置**" "  >  **发送反馈**"
- 在我们的[Yammer 网站](https://www.yammer.com/AskIPTeam)上发布你的问题