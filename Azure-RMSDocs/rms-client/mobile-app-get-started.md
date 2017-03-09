---
title: "入门 - 适用于 iOS 和 Android 的 AIP 应用"
description: 
keywords: "如何使用适用于 iOS 和 Android 的 Azure 信息保护应用查看电子邮件或文件"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 14f0d3ba1c01f0fd1b68d2b793e2bb5c8ee9906e
ms.lasthandoff: 02/24/2017


---

# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用入门

适用于：Active Directory Rights Management Services、Azure 信息保护

当用户需要打开受保护的电子邮件或文件时，大多数用户通常都会自动使用 Azure 信息保护应用。 但如果你是管理员，并且想要为你的用户测试该应用，或者你只是想在使用它之前先试用一下，则可以使用以下说明。

在移动设备上，需访问该应用支持的其中一个文件来查看操作中的查看器。 例如：

- **.rpmsg 文件**：此为权限保护的电子邮件消息，当移动设备上的电子邮件应用本机不支持权限数据保护时，会在电子邮件中以附件形式存在。 
    
    使用另一台设备可向自己发送权限保护的电子邮件消息，用户可从自己的移动设备访问。 例如，在 Windows 计算机使用 Outlook。 有关本机支持权限管理的电子邮件客户端列表，请参阅[支持 Azure Rights Management 数据保护的应用程序](../get-started/requirements-applications.md)中的“电子邮件”列。

- **受权限保护的 PDF 文件**：在 Windows 计算机中，使用 Azure 信息保护客户端[保护 PDF 文件](client-classify-protect.md)，然后通过电子邮件以附件的形式向自己发送此受权限保护的 PDF 文件。 或者，使用电子邮件地址将 PDF 文件上传到 SharePoint 保护的库，然后共享。

- **.ptxt、.pjpg 或 .ppng**：在 Windows 计算机中，使用 Azure 信息保护客户端保护文本或图像文件，然后以电子邮件附件的形式向自己发送此受保护的文件。 有关可用于测试的文件类型的完整列表，请参阅 Azure 信息保护客户端管理员指南中的[保护支持的文件类型及其文件扩展名](client-admin-guide-file-types.md#supported-file-types-for-protection-and-their-file-name-extensions)部分。 

若要在 Azure 信息保护查看器应用中查看这些文件，请点击此电子邮件附件或链接。 系统提示选择一个应用来打开文件时，请选择“AIP 查看器”应用。 然后系统会提示登录到工作或学校帐户。 身份验证成功后，Azure 信息保护应用会显示电子邮件或文件以供阅读。

## <a name="next-steps"></a>后续步骤

如果你有关于此应用的其他问题，请检查这些问题是否在[适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题解答](mobile-app-faq.md)中得到处理。 

对于其他问题，请访问我们的 [Yammer 站点](https://www.yammer.com/AskIPTeam)或[发送电子邮件到信息保护团队](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
