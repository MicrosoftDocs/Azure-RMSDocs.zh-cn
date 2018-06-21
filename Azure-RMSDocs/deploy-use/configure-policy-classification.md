---
title: 为 Azure 信息保护标签配置条件
description: 在配置标签的条件时，可以自动将标签分配到文档或电子邮件。 或者，可以提示用户选择建议的标签。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: 053d8dfd51d8c79cdc733f4395226c12ab6e2102
ms.sourcegitcommit: 87d73477b7ae9134b5956d648c390d2027a82010
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32326746"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>如何配置 Azure 信息保护的自动和建议分类的条件

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

在配置标签的条件时，可以自动将标签分配到文档或电子邮件。 或者，可以提示用户选择建议的标签。 

配置这些条件时，可使用预定义的模式，如“信用卡号”或“美国社会安全号码 (SSN)”。 或者，你可以定义自定义字符串或模式作为自动分类的条件。 这些条件适用于文档和电子邮件中的正文文本和页眉及页脚。 有关这些条件的详细信息，请参阅[以下过程](#to-configure-recommended-or-automatic-classification-for-a-label)中的步骤 5。

若要获取最佳用户体验并确保业务连续性，我们建议你从用户建议分类开始，而不是自动操作。 此配置使你的用户能够接受分类和任何关联保护，或覆盖这些建议（如果它们不适用于其文档或电子邮件）。

通过自定义策略提示配置条件以将标签应用于建议的操作的示例提示：

![Azure 信息保护检测和建议](../media/info-protect-recommend-calloutsv2.png)

在此示例中，用户可以单击“立即更改”应用建议的标签，或通过选择“消除”来替代该建议。 如果用户选择消除建议并且在下一次打开文档时该条件仍然适用，会再次显示标签建议。 

> [!IMPORTANT]
>请勿为自动分类和用户定义的权限配置标签。 “用户定义的权限”选项是一个[保护设置](configure-policy-protection.md)，允许用户指定应向其授予权限的人员。
>
>如果为自动分类和用户定义的权限配置标签，则会检查内容是否符合条件，并且不会应用用户定义的权限设置。 可使用建议的分类和用户定义的权限。

## <a name="how-automatic-or-recommended-labels-are-applied"></a>如何应用自动标签或建议的标签

- 自动分类会在保存文档时应用到 Word、Excel 和 PowerPoint，并在发送电子邮件时应用到 Outlook。 
    
    如果文档和电子邮件之前已手动添加标签（或之前已使用更高级别的分类添加标签），则不能使用自动分类。 

- 建议的分类会在保存文档时应用到 Word、Excel 和 PowerPoint。 不能将建议的分类用于 Outlook。
    
    对于之前已设置标签（更高级别的分类标签）的文档，无法使用建议的分类。 

可以更改此行为，以便 Azure 信息保护客户端定期检查文档是否符合指定的条件规则。 此配置需要当前为预览效果的[高级客户端设置](../rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)。

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>多条件应用到多个标签时的评估方式

1. 根据在策略中指定的位置，将标签排序以供评估：排在第一的标签具有最低的位置（敏感度最低），排在最后的标签具有最高位置（敏感度最高）。

2. 应用最敏感的标签。
 
3. 将应用最后一个子标签。


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>配置标签的建议或自动分类

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“分类” > “标签”菜单选项：在“Azure 信息保护 - 标签”边栏选项卡上，选择要配置的标签。

3. 在“**标签**”边栏选项卡上的“**配置条件以自动应用该标签**”部分中，单击“**添加新的条件**”。

4. 在“条件”边栏选项卡上，选择“信息类型”（如果要使用预定义的条件）或“自定义”（如果要指定自己的条件）：
    - 对于“信息类型”：从可用条件列表中选择，然后选择最小出现次数以及出现计数中是否应具有唯一的值。
        
        信息类型使用 Office 365 数据丢失防护 (DLP) 敏感信息类型和模式检测。 可以从多种常见敏感信息类型中进行选择，其中某些类型特定于不同的区域。 有关详细信息，请参阅 Office 文档中的 [What the sensitive information types look for](https://support.office.com/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b)（敏感信息类型查找的内容）。
        
        可从 Azure 门户选择的信息类型列表会定期更新，以包含任何新的 Office DLP 添加。 但是，该列表不包含作为规则包定义和上传到 Office 365 安全与合规中心的任何自定义敏感信息类型。 
        
        Azure 信息保护评估你选择的信息类型时，不使用 Office DLP 置信度设置，而是根据最低置信度进行匹配。
    
    - 对于“**自定义**”：指定匹配的名称和短语，其必须排除引号和特殊字符。 然后指定是否匹配正则表达式，区分大小写，发生的最小数目以及发生计数中是否应具有唯一的值。
        
        正则表达式使用 Office 365 正则表达式模式。 有关详细信息，请参阅 Office 文档中的[基于匹配定义正则表达式](https://technet.microsoft.com/library/jj674702(v=exchg.150).aspx#Anchor_2)。 此外，你可能会发现参考 Boost 中的 [Perl Regular Expression Syntax](http://www.boost.org/doc/libs/1_66_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html)（Perl 正则表达式语法）将有所帮助。
        
5. 确定是否需要更改“最小出现次数”和“仅计算唯一值的出现次数”，然后选择“保存”。 
    
    出现次数选项示例：选择社会安全号码的信息类型并将最小出现次数设置为 2，并且文档已两次列出同一社会安全号码：如果将“仅计算唯一值的出现次数”设置为“开”，则不符合条件。 如果将此选项设置为“关闭”，则满足条件。

6. 返回到“标签”边栏选项卡上，配置以下内容，然后单击“保存”：
    
    - 选择自动或建议的分类：对于**选择如何应用该标签：自动或向用户建议**，选择“**自动**”或“**建议**”。
    
    - 指定用户提示或策略提示文本：保持默认文本或指定你自己的字符串。

单击“保存”时，更改将会自动提供给用户和服务。 不再提供单独发布选项。

## <a name="next-steps"></a>后续步骤

请考虑部署 [Azure 信息保护扫描程序](deploy-aip-scanner.md)，它可使用自动分类规则发现和保护网络共享和本地文件存储中的文件并对其进行分类。  

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

