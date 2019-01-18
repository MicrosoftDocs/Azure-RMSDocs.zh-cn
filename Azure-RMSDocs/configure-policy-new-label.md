---
title: 新的 Azure 信息保护标签 - AIP
description: 尽管 Azure 信息保护附带了可以自定义的默认标签，你还可以创建用户可在信息保护栏中看到的自己的标签。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: 3bc01282e579368105687fe53157ce2a05dbe4ff
ms.sourcegitcommit: 9dc6da0fb7f96b37ed8eadd43bacd1c8a1a55af8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2019
ms.locfileid: "54393520"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>如何创建 Azure 信息保护的标签

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*

尽管 Azure 信息保护附带了可以自定义的默认标签，你还可以创建自己的标签。

可以添加新标签，或在需要更高级别的分类时将新子标签添加到现有标签。 例如，[默认策略](configure-policy-default.md)中的最后一个标签包含子标签。

创建标签的首个子标签时，用户不能再选择原始父标签。 如有必要，请新建子标签来重新创建父标签设置，让用户能够应用相同的设置。

使用以下说明添加一个新标签，随后可以将其添加到 Azure 信息保护策略。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“分类” > “标签”菜单选项中：在“Azure 信息保护 - 标签”边栏选项卡上，执行以下操作之一：
    
    - 创建新标签：单击“添加新标签”。
    
    - 创建新子标签：针对要创建子标签的标签，右键单击或选择上下文菜单（“...”），然后单击“添加子标签”。

3. 在“**标签**”或“**子标签**”边栏选项卡上，选择要应用于此新标签的选项，然后单击“**保存**”。
    
    指定显示名称时，禁止指定一些字符（如反斜杠和 & 号），因为并非所有使用 Azure 信息保护的服务和应用程序都支持这些字符。 除了禁止指定的字符外，还请不要指定 # 字符。    
    
    请注意，新标签将自动分配为黑色。 从颜色列表中选择一种可区分的颜色，或者输入颜色的红色、绿色和蓝色 (RGB) 组成的十六进制三元色代码。 例如，#DAA520。 如果需要有关这些代码的参考，可首先查看 MSDN 文档中实用的[按名称排列颜色](https://msdn.microsoft.com/library/aa358802(v=vs.85).aspx)。可在多种图片编辑程序（例如 Microsoft 画图，用户可在此程序中通过调色板选择自定义颜色，它会自动显示 RGB 值）中找到这些代码。

4. 将新的标签提供给用户：从“分类” > “策略”菜单选项中，选择要包含新标签的策略。 选择“添加或删除标签”。 从“策略:添加或删除标签”边栏选项卡中选择标签，然后依次选择“确定”和“保存”。
    
    >[!TIP]
    >对于新标签，请考虑首先将它们添加到用于测试的作用域内策略。 如果对结果满意，则从该测试范围删除标签，然后将标签添加到在生产中使用的策略。     
    
    有关添加标签的详细信息，请参阅[如何添加或删除标签](configure-policy-add-remove-label.md)。
    
    更改将会自动提供给用户和服务。 不再提供单独发布选项。

5. 如果希望此新标签名称和描述以不同的语言为用户显示：请按照[如何为不同的语言配置标签](configure-policy-languages.md)中的过程进行操作。 

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  


