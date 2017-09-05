---
title: "更改 Azure 信息保护标签"
description: "可以更改或优化用户可以在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对其进行配置。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: 343b38caa14d3f67a932eedae37ed10c55f371ff
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2017
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>如何更改或自定义 Azure 信息保护的现有标签

>*适用于：Azure 信息保护*

可以更改或优化用户可以在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对其进行配置。

例如，你可以更改标签或子标签名称、工具提示、颜色、顺序、是否应用页脚或水印等可视标记、是否应用 Azure 权限管理保护以及建议或自动分类。

若要更改标签，请按照以下说明操作。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 要更改全局策略中的标签，使其适用于所有用户，请从“Azure 信息保护 - 全局策略”边栏选项卡中选择要更改的标签，之后根据需要选择任何边栏选项卡进行更改。 要更改[作用域内策略](configure-policy-scope.md)中的标签，使其仅应用于所选用户，请先从“策略”菜单选项中选择“作用域内策略”。 然后从“Azure 信息保护 - 作用域内策略”边栏选项卡选择作用域内策略。

    例外情况是，如果想要重排标签，可在全局策略或选定作用域内策略的策略边栏选项卡上执行操作：右键单击标签或选择标签的上下文菜单，然后选择“上移”或“下移”选项。

3. 无论何时在边栏选项卡上进行更改，如果想要保留所做的更改，请在该边栏选项卡上单击“**保存**”。

4. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

5. 如果更改了标签名称或说明，并针对其他语言进行了配置，则必须再次导出“Azure信息保护”策略，提供新的翻译并导入更改。 有关详细信息，请参阅[如何为不同的语言配置标签](configure-policy-languages.md)。

> [!TIP]
>如果你想要将其中一个默认标签返回到默认值，请使用 [默认信息保护策略](configure-policy-default.md)(#默认信息保护策略) 中的信息。

## <a name="next-steps"></a>后续步骤

若要详细了解可针对标签配置的选项以及可针对 Azure 信息保护策略配置的其他设置，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


