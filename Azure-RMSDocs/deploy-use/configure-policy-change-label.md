---
title: "更改 Azure 信息保护标签"
description: "可以更改或细化用户在“信息保护”栏上看到的标签，方法是在 Azure 信息保护策略中对其进行配置。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: f1ffd4c459f2fa194372450f5713c920422f744d
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>如何更改或自定义 Azure 信息保护的现有标签

>*适用于：Azure 信息保护*

可以更改或细化用户在“信息保护”栏上看到的标签，方法是在 Azure 信息保护策略中对其进行配置。

例如，可以更改标签或子标签名称、工具提示、颜色和顺序。 可以更改标签是否适用于页脚或水印等视觉标记。 还可以更改标签是否适用于保护、建议的分类或自动分类。

若要更改标签，请按照以下说明进行操作：

1. 如果尚未执行此操作，请打开新的浏览器窗口，并以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 若要通过全局策略更改标签使其适用于所有用户，请从“Azure 信息保护 - 全局策略”边栏选项卡中选择要更改的标签，并根据需要转到任何后续边栏选项卡。 若要通过[作用域内策略](configure-policy-scope.md)更改标签使其仅适用于选定的用户，请先从“策略”菜单选项选择“作用域内策略”。 然后从“Azure 信息保护 - 作用域内策略”边栏选项卡选择作用域内策略。

    例外情况是要重排标签顺序。 在全局策略或所选作用域内策略的策略边栏选项卡上：右键单击标签或选择标签的上下文菜单。 然后，选择“上移”或“下移”选项。

3. 每当在边栏选项卡上进行更改后，单击该边栏选项卡上的“保存”（如果要保留所做的更改）。

4. 要使所做的更改适用于用户，请在“Azure 信息保护”边栏选项卡上，单击“发布”。

5. 如果已更改标签显示名称或说明并已为其他语言配置了这些项：请重新导出 Azure 信息保护策略，提供新的翻译，然后导入所做的更改。 有关详细信息，请参阅[如何为不同语言配置标签](configure-policy-languages.md)。

> [!TIP]
>如果要将某个默认标签恢复为默认值，请使用[默认信息保护策略](configure-policy-default.md)中的信息。

## <a name="next-steps"></a>后续步骤

有关配置可以为标签生成的选项以及 Azure 信息保护策略的其他设置的详细信息，请使用[配置组织的策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


