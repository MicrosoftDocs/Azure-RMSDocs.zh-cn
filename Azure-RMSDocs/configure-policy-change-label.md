---
title: 更改 Azure 信息保护标签 - AIP
description: 可以更改或优化用户可以在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对其进行配置。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 4530f365f63756c61a7ad97936cffb64cc22d1b8
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2020
ms.locfileid: "75742868"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>如何更改或自定义 Azure 信息保护的现有标签

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> *适用于[Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*


通过在 Azure 门户中配置标签，可以更改或优化用户在“信息保护”栏或从 Office 功能区的“保护”按钮看到的任何标签。

例如，可以更改标签或子标签名称、工具提示、颜色和顺序。 可以更改标签是否应用视觉标记，例如页脚或水印。 还可以更改标签是否应用保护，是否建议该标签或自动分类。

若要更改标签，请按照以下说明操作：

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”窗格。 
    
    例如，在 "资源"、"服务" 和 "文档" 的 "搜索" 框中，开始键入**信息**并选择 " **Azure 信息保护**"。

2. 从 "**分类** > **标签**" 菜单选项：在 " **Azure 信息保护-标签**" 窗格中，选择要更改的标签。

    除非你想要对标签进行重新排序：右键单击标签或选择标签的上下文菜单（而不是选择标签）。 然后，选择“上移”或“下移”选项。

3. 无论何时在新窗格中进行更改，如果想要保留所做的更改，请单击该窗格上的 "**保存**"。
    
    单击“保存”时，更改将会自动提供给用户和服务。 不再提供单独发布选项。

4. 如果更改了标签显示名称或说明，并针对其他语言进行了配置：再次导出 Azure信息保护策略，提供新的翻译并导入更改。 有关详细信息，请参阅[如何为不同的语言配置标签](configure-policy-languages.md)。

> [!TIP]
>如果你想要将其中一个默认标签返回到默认值，请使用 [默认信息保护策略](configure-policy-default.md)(#默认信息保护策略) 中的信息。

## <a name="next-steps"></a>后续步骤

若要详细了解可针对标签配置的选项以及可针对 Azure 信息保护策略配置的其他设置，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。



