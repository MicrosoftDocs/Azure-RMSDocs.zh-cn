---
title: 分类和标签的常见问题解答 - AIP
description: 使用 Azure 信息保护进行分类和设置标签时遇到问题？ 请查看此处是否有答案。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 681d40f86598aaa328c41df9ec76b27c1c24d0c1
ms.sourcegitcommit: 465709879998fcb78cd2a4efda559c43ed661dda
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59233779"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>有关 Azure 信息保护中的分类和标签的常见问题

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

遇到有关 Azure 信息保护的专门与分类和标签有关的问题？  请查看此处是否有答案。 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>使用 Azure 信息保护中的分类功能可以做些什么？

请尝试学习我们的[编辑策略并创建新标签](infoprotect-quick-start-tutorial.md)教程，在短短几分钟内即可正常使用。

有关其他分类特性和功能何时可用的信息，请留意[企业移动性 + 安全性博客](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity/label-name/Azure%20Information%20Protection)和 [Yammer 站点](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)上的公告。 当前版本具有一些限制，包括以下内容：

- Office Web 应用 (Office Online) 中不具有标签功能。

- 没有分类或标签与 Exchange Online 或 SharePoint Online 集成。

> [!NOTE]
> 现提供预览：
> - 分类和标签的集中式报告。 有关详细信息，请参阅 [Azure 信息保护的中心报告](reports-aip.md)。
>
>**最近发布了**：
> - 移动设备（iOS 和 Android）和 Mac 计算机的 Office 应用具有内置标记功能。 有关详细信息，请参阅[将敏感标签应用于 Office 中的文档和电子邮件](https://aka.ms/officemipdocs)。

通过访问 Azure 信息保护的 [UserVoice 站点](https://msip.uservoice.com/)，请求新功能并对请求进行投票。

## <a name="which-preview-client-do-i-install-for-testing-new-functionality"></a>安装哪个预览客户端来测试新功能？

目前有两个 Windows 预览版客户端： 

- 从 Azure 门户下载标签和策略设置的 Azure 信息保护客户端。 此客户端在正式发布版客户端的基础上生成。

- 从以下其中一个管理中心下载标签和策略设置的 Azure 信息保护统一标签客户端：Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 365 合规中心。 此客户端现在提供第二个预览版。

如果 Azure 信息保护统一标记客户端目前的功能集和功能可满足你的业务需求，建议使用它进行测试。 如果无法满足你的业务需求，或者如果你已在 Azure 门户中配置了标签，而这些标签尚未[迁移到统一标记存储](configure-policy-migrate-labels.md)，请使用 Azure 信息保护客户端。

有关详细信息，包括特性和功能的比较表，请参阅[选择使用哪个 Azure 信息保护客户端](./rms-client/use-client.md#choose-which-azure-information-protection-client-to-use)。

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

有关此元数据的详细信息，请参阅[电子邮件和文档中存储的标签信息](configure-policy.md#label-information-stored-in-emails-and-documents)。

有关将此元数据与 Exchange Online 邮件流规则配合使用的示例，请参阅[配置 Azure 信息保护标签的 Exchange Online 邮件流规则](configure-exo-rules.md)。

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>我能否创建自动包含分类的文档模板？

是。 可以将标签配置为，[应用包含标签名称的页眉或页脚](configure-policy-markings.md)。 不过，如果这无法满足你的要求，可以创建包含所需格式设置的文档模板，并将分类添加为域代码。 

例如，文档的页眉中可能有一个显示分类的表。 或者，对引用文档分类的简介使用具体的字词。

若要在文档中添加此域代码，请执行以下操作：

1. 标记并保存文档。 此操作新建可立即用于域代码的元数据字段。

2. 在文档中，将光标置于要添加标签分类的位置，再在“插入”选项卡中依次选择“文本” > “文档部件” > “字段”。

3. 在“字段”对话框中，选择“类别”下拉列表中的“文档信息”。 然后，选择“字段名称”下拉列表中的“DocProperty”。

4. 在“属性”下拉列表中，依次选择“敏感度”和“确定”。

此时，当前标签的分类显示在文档中，并且这个值会在你每次打开文档或使用模板时自动刷新。 因此，如果标签发生更改，那么对此域代码显示的分类也会在文档中自动更新。

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>对于电子邮件来说，Azure 信息保护分类与 Exchange 邮件分类有什么不同？

Exchange 邮件分类是一种较旧的功能，其可对电子邮件进行分类，且独立于 Azure 信息保护分类执行。 

但是，可以将这两个解决方案进行集成，以便当用户使用 Outlook 网页版和某些移动邮件应用程序中对电子邮件进行分类时，可自动添加 Azure 信息保护分类和相应的标签标记。 

可以使用同一技术将标签用于 Outlook 网页版和这些移动邮件应用程序。

有关配置步骤，请参阅[将 Exchange 邮件分类与 Azure 信息保护集成，实现移动设备标记解决方案](./rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution)。 



