---
title: 分类和标签的常见问题解答 - AIP
description: 使用 Azure 信息保护进行分类和设置标签时遇到问题？ 请查看此处是否有答案。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/14/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 2c0d391e2d00ec7d0bc09d98de3fe6f502f999a4
ms.sourcegitcommit: 4c4af9766342272eaa18df720ba3738d44ba99c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51707736"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>有关 Azure 信息保护中的分类和标签的常见问题

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

遇到有关 Azure 信息保护的专门与分类和标签有关的问题？  请查看此处是否有答案。 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>使用 Azure 信息保护中的分类功能可以做些什么？

请尝试学习我们的[编辑策略并创建新标签](infoprotect-quick-start-tutorial.md)教程，在短短几分钟内即可正常使用。

有关其他分类特性和功能何时可用的信息，请留意[企业移动性 + 安全性博客](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity/label-name/Azure%20Information%20Protection)和 [Yammer 站点](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)上的公告。 当前版本具有一些限制，包括以下内容：

- Office Web 应用 (Office Online) 中不具有标签功能。

- 没有分类或标签与 Exchange Online 或 SharePoint Online 集成。

> [!NOTE]
> 现提供预览：
> - 分类和标签的集中式报告。 有关详细信息，请参阅 [Azure 信息保护的中心报告](reports-aip.md)。
> - 适用于移动设备（iOS 和 Android）和 Mac 计算机的 Office 应用的标签功能可供选择加入 [Office 预览体验计划](https://support.office.com/article/what-is-office-insider-f4208185-b63a-4b68-9c7a-9a32d2411c16)的客户使用。 有关详细信息，请参阅[将敏感标签应用于 Office 中的文档和电子邮件](https://aka.ms/officemipdocs)。


通过访问 Azure 信息保护的 [UserVoice 站点](https://msip.uservoice.com/)，请求新功能并对请求进行投票。

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>是否需要是全局管理员才能配置分类和标签？

通过新引入的信息保护管理员角色，此问题现已在主要常见问题解答页上进行回答：[是否必须是全局管理员才能配置 Azure 信息保护？我可以委派给其他管理员吗？](faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators)

如果在安装 [Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)时选择安装演示策略，则无需登录门户即可查看和试用标签功能。 演示策略在本地安装 Azure 信息保护的默认策略，因此可以尝试为文档和电子邮件设置标签，但是，在未登录 Azure 门户的情况下将无法更改或添加新标签。 

## <a name="can-a-file-have-more-than-one-classification"></a>文件是否可以有多个分类？

用户一次仅可为每个文档或电子邮件选择一个标签，这通常只会产生一个分类。 但如果用户选择子标签，这实际上会同时应用两个标签；主标签和次要标签。 通过使用子标签，文件可以有两个分类，表示附加控制级别的父\子关系。

例如，标签“机密”可能包含子标签，如“法律”和“财务”。 可对这些子标签应用不同的分类视觉标记和不同的权限管理模板。 用户不能自行选择“机密”标签；只能选择其中一个子标签，如“法律”。 因此，会看到设置的标签是“机密\法律”。 该文件的元数据包括“Confidential”的一个自定义文本属性和“Legal”的一个自定义文本属性，以及另一个同时包含这两个值（“Confidential Legal”）的自定义文本属性。 

使用子标签时，请不要在主标签处配置视觉标记、保护和条件。 使用子级别时，请仅在子标签上配置这些设置。 如果在主标签及其子标签上配置这些设置，那么子标签上的设置具有更高优先级。

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>如何防止他人删除或更改标签？

尽管[策略设置](configure-policy-settings.md)要求用户说明降低分类标签、删除标签或删除保护的理由，但此设置无法阻止上述操作。 要防止用户删除或更改标签，内容必须已受到保护，并且保护权限不向用户授予导出或完全控制[使用权限](configure-usage-rights.md)。 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>标记一封电子邮件时，是否有任何附件会自动获得相同的标记？

不能。 标记有附件的电子邮件时，这些附件不会继承相同的标记。 附件仍不带标签，或者保留单独应用的标签。 不过，如果电子邮件的标签应用了保护配置，此保护配置也会应用于 Office 附件。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP 解决方案和其他应用如何与 Azure 信息保护相集成？

因为 Azure 信息保护将永久性元数据用于分类（包括明文标签），所以此信息可供 DLP 解决方案和其他应用程序读取。 

若要详细了解如何将此元数据与 Exchange Online 邮件流规则配合使用和相关示例，请参阅[配置 Azure 信息保护标签的 Exchange Online 邮件流规则](configure-exo-rules.md)。

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>对于电子邮件来说，Azure 信息保护分类与 Exchange 邮件分类有什么不同？

Exchange 邮件分类是一种较旧的功能，其可对电子邮件进行分类，且独立于 Azure 信息保护分类执行。 

但是，可以将这两个解决方案进行集成，以便当用户使用 Outlook 网页版和某些移动邮件应用程序中对电子邮件进行分类时，可自动添加 Azure 信息保护分类和相应的标签标记。 

可以使用同一技术将标签用于 Outlook 网页版和这些移动邮件应用程序。

有关配置步骤，请参阅[将 Exchange 邮件分类与 Azure 信息保护集成，实现移动设备标记解决方案](./rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution)。 



