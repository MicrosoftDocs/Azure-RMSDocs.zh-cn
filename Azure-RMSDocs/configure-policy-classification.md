---
title: 为 Azure 信息保护标签配置条件 - AIP
description: 可以自动将标签分配到文档或电子邮件的条件。 或者，可以提示用户选择建议的标签。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: fe80fdc803d15ba450cb333da15e82b19a76441e
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60179929"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>如何配置 Azure 信息保护的自动和建议分类的条件

>适用对象：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> *说明：[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

在配置标签的条件时，可以自动将标签分配到文档或电子邮件。 或者，可以提示用户选择建议的标签。 

配置这些条件时，可使用预定义的模式，如“信用卡号”或“美国社会安全号码 (SSN)”。 或者，你可以定义自定义字符串或模式作为自动分类的条件。 这些条件适用于文档和电子邮件中的正文文本和页眉及页脚。 有关这些条件的详细信息，请参阅[以下过程](#to-configure-recommended-or-automatic-classification-for-a-label)中的步骤 5。

若要获取最佳用户体验并确保业务连续性，我们建议你从用户建议分类开始，而不是自动操作。 此配置使你的用户能够接受分类和任何关联保护，或覆盖这些建议（如果它们不适用于其文档或电子邮件）。

通过自定义策略提示配置条件以将标签应用于建议的操作的示例提示：

![Azure 信息保护检测和建议](./media/info-protect-recommend-calloutsv2.png)

在此示例中，用户可以单击“立即更改”应用建议的标签，或通过选择“消除”来替代该建议。 如果用户选择消除建议并且在下一次打开文档时该条件仍然适用，会再次显示标签建议。

如果配置自动分类（而不是建议分类），系统自动应用标签，并且用户仍会在自己的 Word、Excel 和 PowerPoint 中看到通知。 不过，“立即更改”和“关闭”按钮都替换为“确定”。 在 Outlook 中，自动分类无通知，且发送电子邮件时将应用标签。

> [!IMPORTANT]
>请勿为自动分类和用户定义的权限配置标签。 “用户定义的权限”选项是一个[保护设置](configure-policy-protection.md)，允许用户指定应向其授予权限的人员。
>
>如果为自动分类和用户定义的权限配置标签，则会检查内容是否符合条件，并且不会应用用户定义的权限设置。 可使用建议的分类和用户定义的权限。

## <a name="how-automatic-or-recommended-labels-are-applied"></a>如何应用自动标签或建议的标签

- 自动分类会在保存文档时应用到 Word、Excel 和 PowerPoint，并在发送电子邮件时应用到 Outlook。 
    
    如果文档和电子邮件之前已手动添加标签（或之前已使用更高级别的分类添加标签），则不能使用自动分类。 

- 建议的分类会在保存文档时应用到 Word、Excel 和 PowerPoint。 除非配置当前处于预览阶段的[高级客户端设置](./rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)，否则无法使用建议的 Outlook 分类。
    
    对于之前已设置标签（更高级别的分类标签）的文档，无法使用建议的分类。 

可以更改此行为，以便 Azure 信息保护客户端定期检查文档是否符合指定的条件规则。 此配置需要当前为预览效果的[高级客户端设置](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)。

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>多条件应用到多个标签时的评估方式

1. 根据在策略中指定的位置，对标签进行排序以进行评估：首先放置的标签具有最低位置（最不敏感），最后放置的标签具有最高位置（最敏感）。

2. 应用最敏感的标签。
 
3. 将应用最后一个子标签。


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>配置标签的建议或自动分类

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“分类” > “标签”菜单选项中：在“Azure 信息保护 - 标签”边栏选项卡上，选择要配置的标签。

3. 在“**标签**”边栏选项卡上的“**配置条件以自动应用该标签**”部分中，单击“**添加新的条件**”。

4. 在“条件”边栏选项卡上，选择“信息类型”（如果要使用预定义的条件）或“自定义”（如果要指定自己的条件）：
    - 对于“信息类型”：从可用条件列表中选择，然后选择最小出现次数以及出现计数中是否应具有唯一的值。
        
        信息类型使用 Office 365 数据丢失防护 (DLP) 敏感信息类型和模式检测。 可以从多种常见敏感信息类型中进行选择，其中某些类型特定于不同的区域。 有关详细信息，请参阅 Office 365 文档中的[敏感信息类型查找的内容](/office365/securitycompliance/what-the-sensitive-information-types-look-for)。
        
        可从 Azure 门户选择的信息类型列表会定期更新，以包含任何新的 Office DLP 添加。 但是，该列表不包含作为规则包定义和上传到 Office 365 安全与合规中心的任何自定义敏感信息类型。
        
        > [!IMPORTANT]
        > 某些信息类型需要最低版本的客户端。 [详细信息](#sensitive-information-types-that-require-a-minimum-version-of-the-client) 
        
        Azure 信息保护评估你选择的信息类型时，不使用 Office DLP 置信度设置，而是根据最低置信度进行匹配。
    
    - 对于“自定义”：指定要匹配的名称和短语，其必须排除引号和特殊字符。 然后指定是否匹配正则表达式，区分大小写，发生的最小数目以及发生计数中是否应具有唯一的值。
        
        正则表达式使用 Office 365 正则表达式模式。 为帮助你指定自定义条件的正则表达式，请参阅 Boost 的以下特定版本的 [Perl 正则表达式语法](https://www.boost.org/doc/libs/1_37_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html)。
        
5. 确定是否需要更改“最小出现次数”和“仅计算唯一值的出现次数”，然后选择“保存”。 
    
    出现次数选项示例：选择社会安全号码的信息类型，将最小出现次数设置为 2，文档中两次列出相同的社会安全号码：如果将“仅用唯一值计算出现次数”设置为“开”，则不满足此条件。 如果将此选项设置为“关闭”，则满足条件。

6. 返回到“标签”边栏选项卡上，配置以下内容，然后单击“保存”：
    
    - 选择自动分类或建议分类：对于“选择如何应用该标签：自动或向用户建议”，选择“自动”或“建议”。
    
    - 指定用于用户提示或策略提示的文本：保留默认文本或指定你自己的字符串。

单击“保存”时，更改将会自动提供给用户和服务。 不再提供单独发布选项。

### <a name="sensitive-information-types-that-require-a-minimum-version-of-the-client"></a>需要最低版本客户端的敏感信息类型

以下的敏感信息类型需要[当前通用版本](./rms-client/client-version-release-history.md#version-1482040)Azure 信息保护客户端：

- **Azure 服务总线连接字符串**
- **Azure IoT 连接字符串**
- **Azure 存储帐户**
- **Azure IAAS 数据库连接字符串和 Azure SQL 连接字符串**
- **Azure Redis 缓存连接字符串**
- **Azure SAS**
- **SQL Server 连接字符串**
- **Azure DocumentDB 身份验证密钥**
- **Azure 发布设置密码**
- **Azure 存储帐户密钥（通用）**

有关这些敏感信息类型的详细信息，请参阅以下博客文章：[Azure 信息保护可帮助你可以通过自动发现凭据更安全](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-helps-you-to-be-more-secure-by/ba-p/360181)

此外，有关 Azure 信息保护客户端和不再在 Azure 门户中的显示的最新正式发布版本不支持以下的敏感信息类型：

- **欧盟电话号码**
- **欧盟 GPS 坐标**

## <a name="next-steps"></a>后续步骤

请考虑部署 [Azure 信息保护扫描程序](deploy-aip-scanner.md)，它可使用自动分类规则发现和保护网络共享和本地文件存储中的文件并对其进行分类。  

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。
