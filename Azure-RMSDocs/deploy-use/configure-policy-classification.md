---
title: "为 Azure 信息保护标签配置条件"
description: "在配置标签的条件时，可以自动将标签分配到文档或电子邮件。 或者，可以提示用户选择建议的标签。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: aa41d4f34f0ed43682f9ba426ec18204457980c3
ms.sourcegitcommit: 2f1936753adf8d2fbea780d0a3878afa621daab5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2017
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>如何配置 Azure 信息保护的自动和建议分类的条件

>*适用于：Azure 信息保护*

在配置标签的条件时，可以自动将标签分配到文档或电子邮件。 或者，可以提示用户选择建议的标签： 

- 自动分类适用于 Word、Excel 和 PowerPoint（如果文件已保存，并在发送电子邮件时将应用到 Outlook）。 自动分类不能用于以前手动标记的文件。
 
- 保存文件时，将建议的分类应用于 Word、Excel 和 PowerPoint。

配置条件时，可以使用预定义的模式，如“信用卡号”或“美国社会安全号码 (SSN)”。 或者，你可以定义自定义字符串或模式作为自动分类的条件。 这些条件适用于文档和电子邮件中的正文文本和页眉及页脚。 有关这些条件的详细信息，请参阅[以下过程](#to-configure-recommended-or-automatic-classification-for-a-label)中的步骤 5。

它们应用于多个标签时，将如何计算多个条件：

1. 根据在策略中指定的位置，将标签排序以供评估：排在第一的标签具有最低的位置（敏感度最低），排在最后的标签具有最高位置（敏感度最高）。

2. 应用最敏感的标签。
 
3. 应用最后一个子标签。

> [!TIP]
>若要获取最佳用户体验并确保业务连续性，我们建议你从用户建议分类开始，而不是自动操作。 此配置使你的用户能够接受标记或保护操作中，或覆盖这些建议（如果它们不适用于其文档或电子邮件）。

通过自定义策略提示配置条件以将标签应用于建议的操作的示例提示：

![Azure 信息保护检测和建议](../media/info-protect-recommend-calloutsv2.png)

在此示例中，用户可以单击“立即更改”应用建议的标签，或通过选择“消除”来替代该建议。

## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>配置标签的建议或自动分类

1. 如果尚未执行此操作，请打开新的浏览器窗口，并以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果要配置的标签将应用于所有用户，请选择“Azure 信息保护 - 全局策略”边栏选项卡。
    
    如果要配置的标签位于[作用域内策略](configure-policy-scope.md)中，仅应用于所选用户，请从“策略”菜单选项中选择“作用域内策略”。 然后从“Azure 信息保护 - 作用域内策略”边栏选项卡选择作用域内策略。

3. 从“Azure 信息保护 - 全局策略”边栏选项卡或“策略: \<名称>”边栏选项卡中，选择要配置的标签。 

4. 在“**标签**”边栏选项卡上的“**配置条件以自动应用该标签**”部分中，单击“**添加新的条件**”。

5. 在“条件”边栏选项卡上，选择“信息类型”（如果要使用预定义的条件）或“自定义”（如果要指定自己的条件）：
    - 对于“信息类型”：从可用条件列表中选择，然后选择最小出现次数以及出现计数中是否应具有唯一的值。
        
        信息类型使用 Office 365 数据丢失防护 (DLP) 敏感信息类型和模式检测。 可以从多种常见敏感信息类型中进行选择，其中某些类型特定于不同的区域。 有关详细信息，请参阅 Office 文档中的 [What the sensitive information types look for](https://support.office.com/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b)（敏感信息类型查找的内容）。 
        
        可从 Azure 门户选择的信息类型列表会定期更新，以包含任何新的 Office DLP 添加。 但是，该列表不包含作为规则包定义和上传到 Office 365 安全与合规中心的任何自定义敏感信息类型。 
        
        Azure 信息保护评估你选择的信息类型时，不使用 Office DLP 置信度设置，而是根据最低置信度进行匹配。
    
    - 对于“**自定义**”：指定匹配的名称和短语，其必须排除引号和特殊字符。 然后指定是否匹配正则表达式，区分大小写，发生的最小数目以及发生计数中是否应具有唯一的值。
        
        正则表达式使用 Office 365 正则表达式模式。 有关详细信息，请参阅 Office 文档中的[基于匹配定义正则表达式](https://technet.microsoft.com/library/jj674702(v=exchg.150).aspx#Anchor_2)。
        
6. 确定是否需要更改“最小出现次数”和“仅计算唯一值的出现次数”，然后选择“保存”。 
    
    出现次数选项示例：选择社会安全号码的信息类型并将最小出现次数设置为 2，并且文档已两次列出同一社会安全号码：如果将“仅计算唯一值的出现次数”设置为“开”，则不符合条件。 如果将此选项设置为“关闭”，则满足条件。

7. 返回到“标签”边栏选项卡上，配置以下内容，然后单击“保存”：
    
    - 选择自动或建议的分类：对于**选择如何应用该标签：自动或向用户建议**，选择“**自动**”或“**建议**”。
    
    - 指定用户提示或策略提示文本：保持默认文本或指定你自己的字符串。

8. 若要使所做的更改适用于用户，请在初始“Azure 信息保护”边栏选项卡，单击“发布”。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


