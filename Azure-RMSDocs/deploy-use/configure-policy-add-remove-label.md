---
title: 向 Azure 信息保护策略添加标签或从中删除标签
description: 向所有用户的全局策略或子集用户的作用域内策略添加 Azure 信息保护标签，或从中删除标签。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/22/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.openlocfilehash: 73152d2202096775d315f874b30269c89213f8e1
ms.sourcegitcommit: 94d1c7c795e305444e9fde17ad73e46f242bcfa9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2018
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>向 Azure 信息保护策略添加标签或从中删除标签

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

>[!NOTE]
> 本文反映了 Azure 门户的最新更新，它允许你独立于全局策略或作用域内策略来创建标签。 还将删除发布策略的选项。 如果租户尚未更新这些更改，例如，你仍看到 Azure 信息保护的“发布”选项，而没有看到“分类”菜单选项，请等待几天，然后再返回查看这些说明。  

创建 Azure 信息保护标签后，可以将其添加到策略，以便它可供用户使用。 如果标签面向所有用户，则将标签添加到全局策略。 如果标签面向所有子集用户，则将标签添加到作用域内策略。 目前，只能将标签添加到一个策略。 若要添加子标签，其父标签必须位于同一策略中，或位于全局策略中。

对于已存在于一个策略中的标签，可以从策略中将其删除。 此操作不会删除标签。 仍可以在另一个策略中使用。

如果尚未创建标签，请参阅[如何为 Azure 信息保护创建新标签](configure-policy-new-label.md)。

如果需要创建作用域内策略，以便将标签应用到子集用户，请参阅[如何使用作用域内策略为特定用户配置 Azure 信息保护策略](configure-policy-scope.md)。

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>若要向策略添加标签或从中删除标签

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“分类” > “策略”菜单选项：在“Azure 信息保护” - “策略”边栏选项卡上，如果要添加或删除的标签应用于所有用户，请选择“全局”。

    如果要添加或删除的标签适用于子集用户，请改为选择作用域内策略。

3. 在“策略”边栏选项卡上，选择“添加或删除标签”。

4. 在“策略: 添加或删除标签”边栏选项卡上，如果所有标签都已在策略中，将看到这些带复选框的标签均已选中，并会在”策略“列中看到相应的策略名称。
     
    子标签显示为缩进。 在作用域内策略中，从全局策略继承的标签显示为不可用。
    
    执行下列一项或多项操作，然后单击“确定”：
    
    - 若要添加标签，请选中，将添加所选的复选框。
    
    - 若要删除标签，请清除其复选框。
  
5. 单击“**保存**”以保存更改。
   
    更改将会自动提供给用户和服务。 不再提供单独发布选项。


## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
