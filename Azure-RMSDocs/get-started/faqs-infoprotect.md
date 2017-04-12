---
title: "分类和标签的常见问题解答 - AIP"
description: "使用 Azure 信息保护进行分类和设置标签时遇到问题？ 请查看此处是否有答案。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: b6980bdcecb02471159f7873e80a05d234726d0e
ms.sourcegitcommit: 85aaded97659bbc0a3932569aab29b1bf472fea4
translationtype: HT
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>有关 Azure 信息保护中的分类和标签的常见问题

>*适用于：Azure 信息保护、Office 365*

遇到有关 Azure 信息保护的专门与分类和标签有关的问题？  请查看此处是否有答案。 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>使用 Azure 信息保护中的分类功能可以做些什么？

请尝试学习我们的快速入门教程，以便在数分钟内了解相关功能：[《Quick start tutorial for Azure Information Protection》](infoprotect-quick-start-tutorial.md)（Azure 信息保护快速入门教程）。

有关其他分类特性和功能何时可用的信息，请留意[企业移动性和安全性博客](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection)和 [Yammer 站点](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)上的公告。 当前版本具有一些限制，包括以下内容：

- 标签名称和工具提示仅支持一种语言。

- 对于分类和标签没有任何集中式日志记录。

- 自动分类的条件必须是短语或模式。

- 适用于移动设备（iOS 和 Android）和 Mac 计算机的 Office 应用或 Office Web 应用（Office Online）不具有标签功能。

- 没有分类或标签与 Exchange Online 或 SharePoint Online 集成。

- 用于合作伙伴和开发人员的 SDK 尚不包括分类和标签。

2 月发布的版本将删除很多之前的限制。 有关详细信息，请参阅[博客文章通告](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/)。

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>是否需要是全局管理员才能配置分类和标签？

若要配置 Azure 信息保护策略，必须以 Azure Active Directory 全局管理员的身份登录到 Azure 门户。

如果在安装 [Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)时选择安装演示策略，则无需登录门户即可查看和试用标签功能。 演示策略在本地安装 Azure 信息保护的默认策略，因此可以尝试为文档和电子邮件设置标签，但是，在未登录 Azure 门户的情况下将无法更改或添加新标签。 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>Azure 门户中的哪些选项是 P1 或 P2？

若要查看 **Azure 信息保护高级版 1** (P1) 订阅与 **Azure 信息保护高级版 2** (P2) 订阅中包含的功能，请参阅 Azure 信息保护站点中的[功能列表](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)。 但是一般原则为，高级功能（如自动分类和保留自己的密钥 (HYOK)）特定于 Azure 信息保护高级版 2 订阅。

## <a name="can-a-file-have-more-than-one-classification"></a>文件是否可以有多个分类？

用户一次仅可为每个文档或电子邮件选择一个标签，这通常只会产生一个分类。 但如果用户选择子标签，这实际上会同时应用两个标签；主标签和次要标签。 通过使用子标签，文件可以有两个分类，表示附加控制级别的父\子关系。

例如，标签“机密”可能包含子标签，如“法律”和“财务”。 可对这些子标签应用不同的分类可视化标记和不同的权限管理模板。 用户不能单独选择“机密”标签；必须选择其中一个子标签，如“法律”。 因此，会看到设置的标签是“机密\法律”。 该文件的元数据包括“机密”的一个自定义文本属性和“法律”的一个自定义文本属性，以及另一个同时包含两个值（“机密 法律”）的自定义文本属性。 

使用子标签时，请不要在主标签处配置可视标记、保护和条件。 使用子级别时，请仅在子级别配置这些设置。 如果在主标签及其子标签上配置这些设置，那么子标签上的设置具有更高优先级。

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>标记一封电子邮件时，是否有任何附件会自动获得相同的标记？

不能。 标记有附件的电子邮件时，这些附件不会继承相同的标记。 附件将保持不带标签，或者保留单独应用的标签。 但是，如果电子邮件的标签应用了保护，则该保护也适用于附件。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP 解决方案和其他应用如何与 Azure 信息保护相集成？

因为 Azure 信息保护将永久性元数据用于分类，其中包括明文标签，所以该信息可以被 DLP 解决方案和其他应用读取。 对于文件，该元数据存储在自定义属性中；对于电子邮件，该信息存储在电子邮件标头中。

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>对于电子邮件来说，Azure 信息保护分类与 Exchange 邮件分类有什么不同？

Exchange 邮件分类是一种较旧的功能，其可对电子邮件进行分类，且独立于 Azure 信息保护分类执行。 但是，你可以将这两个解决方案进行集成，以便当用户使用 Outlook Web 应用和在某些移动邮件应用程序中对电子邮件进行分类时，自动添加 Azure 信息保护分类和相应的标签标记。 Exchange 添加分类，Azure 信息保护客户端应用该分类的相应标签设置。

虽然 Outlook Web 应用尚不本地支持 Azure 信息保护分类和保护，但可通过同样的方法将标签用于除桌面 Outlook 客户端之外的电子邮件客户端。

要实现此解决方案： 

1. 使用 [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell cmdlet 创建邮件分类，其 Name 属性映射到 Azure 信息保护策略中的标签名称。 

2. 为每个标签创建 Exchange 传输规则：邮件属性包括配置的分类时应用规则，并修改邮件属性以设置邮件头。 

    对于邮件头，可通过检查所发送的的电子邮件的 Internet 邮件头来查找要指定的信息，这些邮件头是使用 Azure 信息保护标签进行分类的。 查找邮件头 **msip_labels**，以及紧随其后的字符串，直至分号（包括分号）。 以上述示例为例：
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    然后，对于此规则中的邮件头，将 **msip_labels** 指定为邮件头，此字符串的其余部分指定为邮件头的值。 例如：
    
    ![示例 Exchange Online 传输规则，用于为特定 Azure 信息保护标签设置邮件头](../media/exchange-rule-for-message-header.png)

测试此规则前，请记住，创建或编辑传输规则时通常会存在延迟（例如，等待一个小时）。 但当规则生效后，用户使用 Outlook Web 访问应用或支持权限管理保护的移动设备客户端时，会发生以下情况： 

- 用户选择 Exchange 邮件分类，并发送电子邮件。

- Exchange 规则检测 Exchange 分类，并对应修改邮件头以添加 Azure 信息保护分类。

- 运行 Azure 信息保护客户端的收件人在 Outlook 中查看电子邮件时，他们将看到分配的 Azure 信息保护标签以及所有对应的电子邮件标头、页脚或水印。 

如果 Azure 信息保护标签应用权限管理保护，请将其添加到规则配置，方法是选择修改邮件安全性的选项，应用权限保护，然后选择 RMS 模板或“不要转发”选项。

你还可以配置传输规则来执行反向映射：检测到 Azure 信息保护标签时，请设置相应的 Exchange 邮件分类。 为此，请执行以下操作：

- 对于每个 Azure 信息保护标签，请创建在 **msip_labels** 标头包含标签名称（例如 **General**）时应用的传输规则，并应用映射到此标签的邮件分类。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]