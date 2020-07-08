---
title: 为 Azure 信息保护标签配置条件 - AIP
description: 可以自动将标签分配到文档或电子邮件的条件。 或者，可以提示用户选择建议的标签。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: e760ae71b07c72dc761e51c9ebc07bb52c5b006c
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047790"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>如何配置 Azure 信息保护的自动和建议分类的条件

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)


>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

> [!NOTE]
> 这些说明适用于 Azure 信息保护客户端（经典版），而不是 Azure 信息保护统一标记客户端。 不确定这些客户端之间有何区别？ 请参见[常见问题解答](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。
> 
> 如果你正在寻找有关为统一标签客户端配置自动和建议分类的信息，请参阅 Microsoft 365 符合性文档。 例如，[自动对内容应用敏感标签](/microsoft-365/compliance/apply-sensitivity-label-automatically)。

在配置标签的条件时，可以自动将标签分配到文档或电子邮件。 或者，可以提示用户选择建议的标签。 

配置这些条件时，可使用预定义的模式，如“信用卡号”或“美国社会安全号码 (SSN)”********。 或者，你可以定义自定义字符串或模式作为自动分类的条件。 这些条件适用于文档和电子邮件中的正文文本和页眉及页脚。 有关这些条件的详细信息，请参阅[以下过程](#to-configure-recommended-or-automatic-classification-for-a-label)中的步骤 5。

若要获取最佳用户体验并确保业务连续性，我们建议你从用户建议分类开始，而不是自动操作。 此配置使你的用户能够接受分类和任何关联保护，或覆盖这些建议（如果它们不适用于其文档或电子邮件）。

通过自定义策略提示配置条件以将标签应用于建议的操作的示例提示：

![Azure 信息保护检测和建议](./media/info-protect-recommend-calloutsv2.png)

在此示例中，用户可以单击“立即更改”**** 应用建议的标签，或通过选择“消除”**** 来替代该建议。 如果用户选择消除建议并且在下一次打开文档时该条件仍然适用，会再次显示标签建议。

如果配置自动分类（而不是建议分类），系统自动应用标签，并且用户仍会在自己的 Word、Excel 和 PowerPoint 中看到通知。 但是，"**立即更改**" 和 "**取消**" 按钮将替换为 **"确定"**。 在 Outlook 中，自动分类无通知，且发送电子邮件时将应用标签。

> [!IMPORTANT]
>请勿为自动分类和用户定义的权限配置标签。 “用户定义的权限”选项是一个[保护设置](configure-policy-protection.md)，允许用户指定应向其授予权限的人员。
>
>如果为自动分类和用户定义的权限配置标签，则会检查内容是否符合条件，并且不会应用用户定义的权限设置。 可使用建议的分类和用户定义的权限。

## <a name="how-automatic-or-recommended-labels-are-applied"></a>如何应用自动标签或建议的标签

- 自动分类在保存文档时应用到 Word、Excel 和 PowerPoint，并在发送电子邮件时应用到 Outlook。 
    
    不能将自动分类用于以前已手动标记的或者以前已使用更高分类自动标记的文档和电子邮件。 

- 保存文档时，建议的分类适用于 Word、Excel 和 PowerPoint。 除非配置当前处于预览阶段的[高级客户端设置](./rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)，否则无法使用建议的 Outlook 分类。
    
    对于之前已设置标签（更高级别的分类标签）的文档，无法使用建议的分类。 

可以更改此行为，以便 Azure 信息保护客户端定期检查文档是否符合指定的条件规则。 例如，如果你对自动保存在 Microsoft SharePoint、OneDrive for work 或 school 或 OneDrive for home 中的 Office 应用[程序使用自动保存，](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5)则这种做法非常合适。 若要支持此方案，可以配置当前处于预览阶段的[高级客户端设置](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)。 此设置会启用分类，使其在后台连续运行。

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>多条件应用到多个标签时的评估方式

1. 根据在策略中指定的位置，将标签排序以供评估：排在第一的标签具有最低的位置（敏感度最低），排在最后的标签具有最高位置（敏感度最高）。

2. 应用最敏感的标签。
 
3. 将应用最后一个子标签。


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>配置标签的建议或自动分类

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到“Azure 信息保护”**** 窗格。 
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”**** 并选择“Azure 信息保护”****。

2. 从 "**分类**  >  **标签**" 菜单选项：在 " **Azure 信息保护-标签**" 窗格中，选择要配置的标签。

3. 在 "**标签**" 窗格的 "**配置自动应用此标签的条件**" 部分中，单击 "**添加新条件**"。

4. 如果要使用预定义条件，请在 "**条件**" 窗格中选择 "**信息类型**"，如果要指定自己的条件，请选择 "**自定义**"：
    - 对于“信息类型”：从可用条件列表中选择，然后选择最小出现次数以及出现计数中是否应具有唯一的值****。
        
        信息类型使用 Office 365 数据丢失防护 (DLP) 敏感信息类型和模式检测。 可以从多种常见敏感信息类型中进行选择，其中某些类型特定于不同的区域。 有关详细信息，请参阅 Office 365 文档中的[敏感信息类型查找的内容](/microsoft-365/compliance/what-the-sensitive-information-types-look-for)。
        
        可从 Azure 门户选择的信息类型列表会定期更新，以包含任何新的 Office DLP 添加。 但是，该列表不包含作为规则包定义和上传到 Office 365 安全与合规中心的任何自定义敏感信息类型。
        
        > [!IMPORTANT]
        > 某些信息类型需要最低版本的客户端。 [详细信息](#sensitive-information-types-that-require-a-minimum-version-of-the-client) 
        
        Azure 信息保护评估你选择的信息类型时，不使用 Office DLP 置信度设置，而是根据最低置信度进行匹配。
    
    - 对于“**自定义**”：指定匹配的名称和短语，其必须排除引号和特殊字符。 然后指定是否匹配正则表达式，区分大小写，发生的最小数目以及发生计数中是否应具有唯一的值。
        
        正则表达式使用 Office 365 正则表达式模式。 为帮助你指定自定义条件的正则表达式，请参阅 Boost 的以下特定版本的 [Perl 正则表达式语法](https://www.boost.org/doc/libs/1_37_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html)。
        
5. 确定是否需要更改“最小出现次数”和“仅计算唯一值的出现次数”，然后选择“保存”************。 
    
    出现次数选项示例：选择社会安全号码的信息类型并将最小出现次数设置为 2，并且文档已两次列出同一社会安全号码：如果将“仅计算唯一值的出现次数”设置为“开”，则不符合条件********。 如果将此选项设置为“关闭”，则满足条件****。

6. 返回到 "**标签**" 窗格，配置以下各项，然后单击 "**保存**"：
    
    - 选择自动或建议的分类：对于**选择如何应用该标签：自动或向用户建议**，选择“**自动**”或“**建议**”。
    
    - 指定用户提示或策略提示文本：保持默认文本或指定你自己的字符串。

单击“保存”**** 时，更改将会自动提供给用户和服务。 不再提供单独发布选项。

### <a name="sensitive-information-types-that-require-a-minimum-version-of-the-client"></a>需要最低版本客户端的敏感信息类型

以下敏感信息类型需要 Azure 信息保护客户端的1.48.204.0 的最低版本：

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

有关这些敏感信息类型的详细信息，请参阅以下博客文章： [Azure 信息保护通过自动发现凭据帮助提高安全性](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-helps-you-to-be-more-secure-by/ba-p/360181)

此外，从 Azure 信息保护客户端的1.48.204.0 开始，以下敏感信息类型不受支持，并且不再显示在 Azure 门户中。 如果你有使用这些敏感信息类型的标签，则建议你删除它们，因为我们无法确保对它们进行正确的检测，并且应忽略对扫描程序报告中的任何引用：

- **欧盟电话号码**
- **欧盟 GPS 坐标**

## <a name="next-steps"></a>后续步骤

请考虑部署 [Azure 信息保护扫描程序](deploy-aip-scanner.md)，它可使用自动分类规则发现和保护网络共享和本地文件存储中的文件并对其进行分类。  

有关配置 Azure 信息保护策略的详细信息，请使用[配置组织的策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。
