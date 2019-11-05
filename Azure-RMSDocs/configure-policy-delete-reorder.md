---
title: 删除或重排 Azure 信息保护标签 - AIP
description: 可以删除或重排用户可见的 Azure 信息保护标签。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: ddbe7273bb6bfc931ef9bcbe73a847156c5f4183
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559626"
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>如何删除或重排 Azure 信息保护的标签

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> *适用于[Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*

可以删除或重排用户在 Office 应用程序中看到的 Azure 信息保护标签，方法是为标签选择这些操作。

![在 Azure 信息保护策略中删除或重排标签](./media/info-protect-contextmenu.png)

在删除已应用到文档和电子邮件的标签时，当 Azure 信息保护客户端在下一次打开这些文档和客户端，用户将看到标签的“未设置”状态。 但是，标签信息仍然保留在元数据中，并且仍可以通过查找此标签信息的服务进行读取。

此外，如果删除的标签已应用保护，该保护就不会被删除。 标签中的保护设置将保留并显示在“保护模板”部分。 现在可以将此模板转换为新的标签。 此模板存在时，无法创建与已删除标签的名称相同的新标签。 如果想那么做，有如下选项可供选择：

- 将模板转换为标签。 
    
    建议采用此操作，因为随后可以按需更改此模板的名称并修改保护设置。

- 使用 PowerShell 重命名模板或将它删除。
    
    在执行这些操作前，请考虑其他管理员或服务是否正在使用此模板或者曾经使用过此模板。 可以通过不会更改的模板 ID 或模板名称（可以更改）来标识模板。 最佳做法是仅在确信用户无需打开受模板保护的文档或电子邮件时，才可删除模板。

有关管理保护模板的详细信息，请参阅[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)。

相反，删除标签之前，请考虑禁用它，或从策略中将其删除：
    
- 在禁用已应用到文档和电子邮件的标签时，不会从这些文档和电子邮件中删除应用的标签。 标签保留在策略中，但不再显示为用户可在信息保护栏上选择的标签。 通过禁用此标签，可保持原始配置，以供希望相同策略中的用户以后选择此标签时使用，在此情况下，只需重新启用此标签即可。

- 从策略中删除标签时，也不会从这些文档和电子邮件中删除应用的标签。 但当你从策略中删除标签，你将可以将此标签添加到另一个策略。 有关详细信息，请参阅[向 Azure 信息保护策略添加标签或从中删除标签](configure-policy-add-remove-label.md)。

对标签进行排序，以便用户在信息保护栏中的逻辑进度中就可以看到它们。 例如，以敏感度递增的方式排列标签，以便用户先看到最不敏感的标签，最后看到最敏感的标签。 [默认策略](configure-policy-default.md)使用此配置，并在标签名中反映出逐渐递增的敏感级别。

> [!IMPORTANT]
>如果为标签配置的 [条件](configure-policy-classification.md)(#条件) 可能会应用于多个标签，必须从最不敏感到最敏感排列标签。 这一顺序可确保当并评估条件时，应用最敏感的标签。


按照以下说明进行这些更改。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到 " **Azure 信息保护**" 窗格。 
    
    例如，在 "资源"、"服务" 和 "文档" 的 "搜索" 框中，开始键入**信息**并选择 " **Azure 信息保护**"。

2. 从 "**分类** > **标签**" 菜单选项：在 " **Azure 信息保护-标签**" 窗格中，执行以下一项或多项操作： 

    - 删除标签：对于你想要删除的标签，右键单击或选择上下文菜单 (...)，单击“删除此标签”，然后单击“确定”以确认。 

    - 禁用标签：选择你想要禁用的标签。 在 "**标签**" 窗格中 **，选择**"**关闭**"，然后单击 "**保存**"。

    - 重排标签：针对想要重排的标签，右键单击或选择上下文菜单 ( **...** )，然后单击“**上移**”或“**下移**”直到标签位于所需的顺序。  

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  


