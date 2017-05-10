---
title: "新的 Azure 信息保护标签"
description: "尽管 Azure 信息保护附带了可以自定义的默认标签，你还可以创建用户可在信息保护栏中看到的自己的标签。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: 91feb6dfd9421d7c5cccf53b45f8a0f35e74007d
ms.sourcegitcommit: e3974cc1490581414084669632cad54b12b05d5a
ms.translationtype: HT
ms.contentlocale: zh-CN
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>如何创建 Azure 信息保护的标签

>*适用于：Azure 信息保护*

尽管 Azure 信息保护附带了可以自定义的默认标签，你还可以创建用户可在信息保护栏中看到的自己的标签。

可以添加新标签，或在需要更高级别的分类时将新子标签添加到现有标签。 例如，[默认策略](configure-policy-default.md)中的最后一个标签包含子标签。

使用以下说明将一个新标签添加到 Azure 的信息保护策略。

1. 如果尚未执行此操作，请在新的浏览器窗口中以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果要添加的新标签会应用于所有用户，请在“策略: 全局”边栏选项卡中执行以下操作之一。 

    - 创建新的标签：单击“**添加新的标签**”。

    - 创建新的子标签：对于要创建子标签的标签，右键单击或选择上下文菜单 (**...**)，然后单击“**添加子标签**”。
    
     如果要添加的新标签位于[作用域内策略](configure-policy-scope.md)中，以便仅应用于所选用户，请首先从初始的“Azure 信息保护”边栏选项卡中选择作用域内策略。

3. 在“**标签**”或“**子标签**”边栏选项卡上，选择要应用于此新标签的选项，然后单击“**保存**”。
    
    请注意，新标签将自动分配为黑色。 从颜色列表中选择一种可区分的颜色，或者输入颜色的红色、绿色和蓝色 (RGB) 组成的十六进制三元色代码。 例如，#DAA520。 如果需要有关这些代码的参考，可首先查看 MSDN 文档中实用的[按名称排列颜色](https://msdn.microsoft.com/library/aa358802\(v=vs.85).aspx)。这些代码应用于许多图片编辑程序（例如Microsoft 画图，用户可在此程序中通过调色板选择自定义颜色，它会自动显示 RGB 值）。

4. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

