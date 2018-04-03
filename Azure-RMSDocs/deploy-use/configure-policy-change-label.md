---
title: 更改 Azure 信息保护标签
description: 可以更改或优化用户可以在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对其进行配置。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: aac1d87fb76848e31a21a046f14442293d29aa9f
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>如何更改或自定义 Azure 信息保护的现有标签

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

可以更改或优化用户可以在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对其进行配置。

例如，可以更改标签或子标签名称、工具提示、颜色和顺序。 可以更改标签是否应用视觉标记，例如页脚或水印。 还可以更改标签是否应用保护，是否建议该标签或自动分类。

若要更改标签，请按照以下说明操作：

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 要更改全局策略中的标签，使其适用于所有用户，请从“Azure 信息保护 - 全局策略”边栏选项卡中选择要更改的标签，之后根据需要选择任何边栏选项卡进行更改。 要更改[作用域内策略](configure-policy-scope.md)中的标签，使其仅应用于所选用户，请先从“策略”菜单选项中选择“作用域内策略”。 然后从“Azure 信息保护 - 作用域内策略”边栏选项卡选择作用域内策略。

    例外情况是如果你想要重排标签。 在全局策略或所选作用域策略的策略边栏选项卡上：右键单击标签，或选择该标签的上下文菜单。 然后，选择“上移”或“下移”选项。

3. 无论何时在边栏选项卡上进行更改，如果想要保留所做的更改，请在该边栏选项卡上单击“**保存**”。

4. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

5. 如果更改了标签显示名称或说明，并针对其他语言进行了配置：再次导出 Azure信息保护策略，提供新的翻译并导入更改。 有关详细信息，请参阅[如何为不同的语言配置标签](configure-policy-languages.md)。

> [!TIP]
>如果你想要将其中一个默认标签返回到默认值，请使用 [默认信息保护策略](configure-policy-default.md)(#默认信息保护策略) 中的信息。

## <a name="next-steps"></a>后续步骤

若要详细了解可针对标签配置的选项以及可针对 Azure 信息保护策略配置的其他设置，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


