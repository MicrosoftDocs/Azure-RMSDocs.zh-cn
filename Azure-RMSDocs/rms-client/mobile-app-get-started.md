---
title: 入门 - 适用于 iOS 和 Android 的 AIP 应用
description: 使用适用于 iOS 和 Android 的 Azure 信息保护应用查看电子邮件或文件
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: deca101aacd4d3026b0783581ccfe57be5a5dc7a
ms.sourcegitcommit: 28c1de5f9d1426f160f0e0bafcf9f76769e662b6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2019
ms.locfileid: "71679041"
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用入门

适用范围：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*

在使用本页上的说明之前，请务必阅读[有关 iOS 版和 Android 版 Azure 信息保护应用的常见问题解答](mobile-app-faq.md)。 此页面说明了应用的作用、支持的设备，以及有关应用使用方法的基本信息。

当用户需要打开受保护的电子邮件或文件时，大多数用户通常都会使用 Azure 信息保护应用。 但如果你是管理员，并且想要为你的用户测试该应用，或者你只是想在使用它之前先试用一下，则可以使用以下说明。

> [!NOTE]
> 不用先打开应用，再选择要查看的文档和电子邮件。 相反，可先打开文档或电子邮件，然后选择此应用以查看文档或电子邮件。
>
> 同样，除非系统提示你，否则不用尝试登录应用。

要使用以下说明，需通过移动设备访问该应用支持的其中一个文件。 例如：

- **.rpmsg 文件**：这是受权限保护的电子邮件消息，当移动设备上的电子邮件应用本机不支持权限数据保护时，会在电子邮件中以附件形式存在。 
    
    使用另一台设备可向自己发送权限保护的电子邮件消息，用户可从自己的移动设备访问。 例如，在 Windows 计算机使用 Outlook。 有关以本机方式支持 rights management 的电子邮件客户端的列表, 请参阅[支持 Azure Rights Management 数据保护的应用程序](../requirements-applications.md)中第一个表中的 "**电子邮件**" 列。

- **受权限保护的 PDF 文件**：在 Windows 计算机中, 使用 Azure 信息保护客户端 ([经典](client-classify-protect.md)或[统一标签客户端](clientv2-classify-protect.md)) 来保护 PDF 文件, 然后将此受权限保护的 PDF 文件作为电子邮件中的附件发送。 或者，使用电子邮件地址将 PDF 文件上传到 SharePoint 保护的库，然后共享。

- **.ptxt、.pjpg 或 .ppng**：在 Windows 计算机中, 使用 Azure 信息保护客户端保护某个文本或图像文件, 然后将此受保护的文件作为电子邮件附件发送。 有关可用于测试的文件类型的完整列表，请参阅 Azure 信息保护客户端管理指南中的[支持分类和保护的文件类型](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)部分的第一个表格。 

若要在 Azure 信息保护查看器应用中查看这些文件，请点击此电子邮件附件或链接。 系统提示选择一个应用来打开文件时，请选择“AIP 查看器”应用。 然后系统会提示使用工作或学校帐户登录，或提示选择一个证书。 对这些凭据进行身份验证后，Azure 信息保护应用会显示电子邮件或文件以供阅读。

## <a name="next-steps"></a>后续步骤

若有本[常见问题解答](mobile-app-faq.md)未解决的此应用相关问题或反馈，请访问我们的 [Yammer 站点](https://www.yammer.com/AskIPTeam)。
