---
title: 自定义配置-Azure 信息保护统一标记客户端
description: 有关自定义 Windows 的 Azure 信息保护统一标记客户的信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: b269b4b16507a79c0f08d6c9cc290c22dd69f769
ms.sourcegitcommit: b92f60a87f824fc2da1e599f526898e3a0c919c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2019
ms.locfileid: "67343748"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>管理员指南：Azure 信息保护统一标记客户端的自定义配置

>适用对象：  Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2
>
> 说明： *[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

管理 Azure 信息保护统一标记客户端时，可能需要用于特定方案或一部分用户的高级配置中使用以下信息。

这些设置需要编辑注册表，或指定通过使用 Office 365 安全与合规性中心 PowerShell 高级设置。

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>如何使用 Office 365 安全与合规性中心 PowerShell 配置客户端的高级的设置

当你使用[Office 365 安全与合规性中心 PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps)，可以配置高级的设置，支持自定义项的标签策略和标签。 例如：

- 若要在 Office 应用中显示信息保护栏的设置是***标记策略高级设置***。
- 若要指定标签颜色的设置是***高级设置的标签***。

在这两种情况下，您指定*AdvancedSettings*参数标识 （名称或 GUID） 的策略或标签，并指定中的键/值对[哈希表](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables)，使用以下语法：

标签策略设置的单个字符串值：

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}

对于标签策略设置，为相同的键的多个字符串值：

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

标签设置的单个字符串值：

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}

对于标签设置，为相同的键的多个字符串值：

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

若要删除一种高级的设置，请使用相同的语法，但指定一个 null 字符串值。


#### <a name="examples-for-setting-advanced-settings"></a>设置高级的设置的示例

示例 1：设置高级设置的单个字符串值的标签策略：

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

示例 2：设置高级设置的单个字符串值的标签：

    Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}

示例 3：设置高级设置多个字符串值的标签：

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

示例 4:删除标签策略指定一个 null 字符串值的高级设置：

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>指定标签策略或标签的标识

指定适用于 PowerShell 的标签策略名称*标识*参数非常简单，因为您看到在管理中心内管理标签策略的其中一个策略名称。 但是，对于标签，您看到两者**名称**并**显示名称**中管理员为中心。 在某些情况下，两个值将相同，但它们可以是不同：

- **名称**是原始标签的名称，它是唯一的所有标签。 如果在创建后更改标签名称，此值保持不变。

- **显示名称**的标签，用户将看到并无需在您的所有标签是唯一的名称。 例如，用户会看到一个**所有员工**为 sublabel**机密**标签和另一个**所有员工**sublabel 为**高度机密**标签。 这些子标签都显示相同的名称，但不是相同的标签，具有不同的设置。

配置高级设置标签，使用**名称**值。 例如，若要标识下图中的标签，将指定`-Identity "All Company"`:

![使用 Name 而不是显示名称来标识敏感度标签](../media/labelname_scc.png)

如果想要指定标签的 GUID，此值不是显示在管理中心内管理你的标签。 但是，可以使用以下 Office 365 安全与合规性中心 PowerShell 命令来查找此值：

    Get-Label | Format-Table -Property DisplayName, Name, Guid


#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>优先顺序-如何设置已解决的冲突的顺序

使用其中一个管理员中心中管理敏感度标签，可以配置以下标签策略设置：

- **默认情况下应用此标签，文档和电子邮件**

- **用户必须提供理由与删除的标签或较低分类标签**

- **要求用户将标签应用到其电子邮件或文档**

- **向用户提供指向自定义帮助页的链接**

用户配置多个标签策略后，每个都有可能不同的策略设置的最后一个策略设置应用根据在管理中心内的策略的顺序。 有关详细信息，请参阅[标记策略优先级 （顺序很重要）](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels#label-policy-priority-order-matters)

高级设置的标签遵循优先级相同的逻辑：时标签在标签的多个策略，而该标签具有高级设置，将根据在管理中心内的策略的顺序应用最后一个高级的设置。

按相反的顺序应用标签策略高级设置：有一个例外，将根据在管理中心内的策略的顺序应用中的第一个策略的高级的设置。 例外情况是高级的设置*OutlookDefaultLabel*，用于为 Outlook 设置不同的默认标签。 为此标签策略高级的设置仅，最后一个设置被应用根据在管理中心内的策略的顺序。

#### <a name="available-advanced-settings-for-label-policies"></a>可用的标签策略高级设置

|设置|应用场景和说明|
|----------------|---------------|
|AttachmentAction|[对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|EnableCustomPermissions|[禁用在文件资源管理器中的自定义权限](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|labelByCustomProperties|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|LogMatchedContent|[禁止为一部分用户发送信息类型匹配项](#disable-sending-information-type-matches-for-a-subset-of-users)|
|OutlookBlockTrustedDomains|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[为 Outlook 设置不同的默认标签](#set-a-different-default-label-for-outlook)|
|OutlookJustifyTrustedDomains|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[在 Outlook 中启用建议的分类](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PostponeMandatoryBeforeSave|[使用强制标签时，删除文档的“以后再说”](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[删除其他标记解决方案中的页眉和页脚](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[为用户添加“报告问题”](#add-report-an-issue-for-users)|
|RunAuditInformationTypeDiscovery|[禁用将在文档中发现的敏感信息发送到 Azure 信息保护 analytics](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|

示例 PowerShell 命令来检查有效的标签策略在标签策略设置名为"Global":

    (Get-LabelPolicy -Identity Global).settings

#### <a name="available-advanced-settings-for-labels"></a>可用的高级的设置的标签

|设置|应用场景和说明|
|----------------|---------------|
|颜色|[指定标签的颜色](#specify-a-color-for-the-label)|
|customPropertyByLabel|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|DefaultSubLabelId|[指定父标签的默认子标签](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[应用标签时应用的自定义属性](#apply-a-custom-property-when-a-label-is-applied)|
|SMimeEncrypt|[将标签配置为在 Outlook 中应用 S/MIME 保护](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[将标签配置为在 Outlook 中应用 S/MIME 保护](#configure-a-label-to-apply-smime-protection-in-outlook)|

示例 PowerShell 命令来检查有效的标签应用标签设置名为"Public":

    (Get-Label -Identity Public).settings

## <a name="display-the-information-protection-bar-in-office-apps"></a>在 Office 应用中显示“信息保护”栏

此配置使用的策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

默认情况下，用户必须选择**显示数据条**选项从**敏感度**按钮以在 Office 应用中显示信息保护栏。 使用**HideBarByDefault**密钥，然后将值设置为**False**可自动显示此栏以便用户，以便他们可以从栏或按钮选择标签。 

对于所选的标签策略中，指定以下字符串：

- 密钥：**HideBarByDefault**

- Value：**False**

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}

## <a name="enable-recommended-classification-in-outlook"></a>在 Outlook 中启用建议的分类

此配置使用的策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

为建议的分类配置标签时，系统将提示用户接受或关闭 Word、Excel 和 PowerPoint 中建议的标签。 此设置将此标签建议扩展到也在 Outlook 中显示。

对于所选的标签策略中，指定以下字符串：

- 密钥：**OutlookRecommendationEnabled**

- Value：**True**

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}

## <a name="set-a-different-default-label-for-outlook"></a>为 Outlook 设置不同的默认标签

此配置使用的策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

在配置此设置时，Outlook 不会应用配置策略设置的选项为默认标签**默认情况下应用此标签，文档和电子邮件到**。 相反，Outlook 可应用不同的默认标签，也可不应用标签。

对于所选的标签策略中，指定以下字符串：

- 密钥：**OutlookDefaultLabel**

- 值： \<**标签 GUID**> 或**None**

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}


## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>使用强制标签时，删除文档的“以后再说”

此配置使用的策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

当你使用的标签策略设置**所有文档和电子邮件必须都有标签**，系统会提示用户选择一个标签，首次保存 Office 文档和当他们发送一封电子邮件。 对于文档，用户可以选择“以后再说”  暂时关闭提示以选择标签，并返回到文档。 但是不能在未选择标签的情况下关闭已保存的文档。 

在配置此设置时，将删除“以后再说”  选项，以便首次保存文档时用户必须选择一个标签。

对于所选的标签策略中，指定以下字符串：

- 密钥：**PostponeMandatoryBeforeSave**

- Value：**False**

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>删除其他标记解决方案中的页眉和页脚

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

借助这些设置，可以在其他标记解决方案已应用这些视觉标记的情况下，从文档中删除或替换基于文本的页眉或页脚。 例如，旧的页脚包含旧标签的名称，你现在已迁移到敏感度标签以使用新的标签名称和其自己的页脚。

时统一标记客户端在其策略中获取此配置，会移除或更换时在 Office 应用中打开该文档和任何敏感度标签应用于文档的旧标头和表尾。

Outlook 不支持此配置，并且请注意，在 Word、Excel 和 PowerPoint 中使用它时，会对这些应用的性能产生负面影响。 该配置允许你根据应用程序来定义设置，例如，搜索 Word 文档页眉和页脚中的文本，而不是 Excel 电子表格或 PowerPoint 演示文稿中的。

由于模式匹配会影响用户的性能，我们建议您限制的 Office 应用程序类型 (**W**ord， **E**xcel， **P**owerPoint) 仅限需要在其中搜索。

对于所选的标签策略中，指定以下字符串：

- 密钥：**RemoveExternalContentMarkingInApp**

- Value：\<Office 应用程序类型 WXP>  

例如：

- 若要仅搜索 Word 文档，请指定 W  。

- 若要搜索 Word 文档和 PowerPoint 演示文稿，请指定 WP  。

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}

然后需要至少一个高级客户端设置 ExternalContentMarkingToRemove，  指定页眉或页脚的内容以及如何删除或替换它们。

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>如何配置 ExternalContentMarkingToRemove

指定 ExternalContentMarkingToRemove 键的字符串值时，拥有三个使用正则表达式的选项  ：

- 用以删除页眉或页脚中所有内容的部分匹配。
    
    例如：页眉或页脚包含字符串 TEXT TO REMOVE  。 想要完全删除这些页面或页脚。 可指定值：`*TEXT*`。

- 用以删除页眉或页脚中特定字词的完全匹配。
    
    例如：页眉或页脚包含字符串 TEXT TO REMOVE  。 只想删除单词 TEXT，结果使页眉或页脚字符串变为 TO REMOVE   。 可指定值：`TEXT `。

- 用以删除页眉或页脚中所有内容的完全匹配。
    
    例如：页眉或页脚具有字符串 TEXT TO REMOVE  。 想要删除其字符串为 TEXT TO REMOVE 的页眉或页脚。 可指定值：`^TEXT TO REMOVE$`。
    

指定的字符串的匹配模式不区分大小写。 最大字符串长度为 255 个字符。

因为某些文档可能包括不可见字符或者不同类型的空格或制表符，可能检测不到指定的短语或句子的字符串。 只要有可能，指定单个易区分的单词作为值，并确保在生产环境中部署之前测试结果。

对于相同的标签策略，指定以下字符串：

- 密钥：**ExternalContentMarkingToRemove**

- 值：\<要匹配的字符串，定义为正则表达式>  

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}

#### <a name="multiline-headers-or-footers"></a>多行页眉或页脚

如果页眉或页脚文本不只一行，则为每行创建一个键和值。 例如，下面是具有两行文本的页脚：

The file is classified as Confidential 

Label applied manually 

若要删除此多行尾，应创建相同的标签策略的以下两个条目：

- 密钥：**ExternalContentMarkingToRemove**

- 键值 1： **\*Confidential***

- 键值 2： **\*Label applied*** 

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}


#### <a name="optimization-for-powerpoint"></a>针对 PowerPoint 的优化

PowerPoint 中的页脚以形状的形式实现。 若要避免删除那些你指定的但不属于页面或页脚的形状，可使用以下附加高级客户端设置：PowerPointShapeNameToRemove  。 我们还建议使用此设置来避免检查所有形状中的文本，因为这将占用大量资源。

如果未指定这项附加的高级客户端设置，并且 PowerPoint 包括在 RemoveExternalContentMarkingInApp  键值中，将对所有形状检查你在 ExternalContentMarkingToRemove 值中指定的文本  。 

查找用作页眉或页脚的形状的名称：

1. 在 PowerPoint 中，显示“选择”窗格  ：“格式”选项卡 >“排列”组 >“选择”窗格    。

2. 选择幻灯片上包含页眉或页脚的形状。 所选形状的名称现在突出显示在“选择”  窗格中。

使用形状的名称为 PowerPointShapeNameToRemove  键指定一个字符串字。 

例如：形状名称是 fc  。 若要删除具有此名称的形状，则指定值：`fc`。

- 密钥：**PowerPointShapeNameToRemove**

- Value：\<PowerPoint 形状名称>  

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}

如果有多个要删除的 PowerPoint 形状，指定具有形状以删除任意数量的值。

默认情况下，只检查主幻灯片的页眉和页脚。 若要将检查范围扩展到所有幻灯片，将占用大量资源，则可以使用 RemoveExternalContentMarkingInAllSlides  附加高级客户端设置：

- 密钥：**RemoveExternalContentMarkingInAllSlides**

- Value：**True**

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}


## <a name="disable-custom-permissions-in-file-explorer"></a>禁用在文件资源管理器中的自定义权限

此配置使用的策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

默认情况下，用户将看到一个名为的选项**使用自定义权限保护**它们在文件资源管理器中右键单击并选择**分类和保护**。 此选项，这些设置可以覆盖你可能已包含具有标签配置任何保护设置其自己的保护设置。 用户还能看到一个用于删除保护的选项。 在配置此设置时，用户看不见这些选项。

若要配置此高级的设置，请为所选的标签策略输入以下字符串：

- 密钥：**EnableCustomPermissions**

- Value：**False**

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限

此配置使用的策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

当配置高级客户端设置设[禁用在文件资源管理器中的自定义权限](#disable-custom-permissions-in-file-explorer)，默认情况下，用户不能查看或更改已设置在受保护的文档中的自定义权限。

但是，没有设置，以便用户可以在此方案中，请参阅并更改受保护的文档的自定义权限，在使用文件资源管理器和右键单击该文件时可以指定另一个高级客户端。

若要配置此高级的设置，请为所选的标签策略输入以下字符串：

- 密钥：**EnableCustomPermissionsForCustomProtectedFiles**

- Value：**True**

示例 PowerShell 命令：

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}


## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

此设置是为当用户将标记的文档附加到电子邮件，并不标记电子邮件本身。 在此方案中，标签会自动选择为其基于适用于附件的分类标签。 选择最高的分类标签。

附件必须是物理文件，并且不能是指向文件的链接（例如，指向 SharePoint 或 OneDrive for Business 文件的链接）。

可以配置此设置设置为**推荐**，因此系统会提示用户将所选的标签应用到其电子邮件，与可自定义工具提示。 用户可接受或忽略该建议。 或者，可以配置此设置设置为**自动**，其中所选的标签自动应用，但用户可以删除标签或发送电子邮件之前，选择一个不同的标签。

注意：对于使用设置的用户定义的权限的保护配置时使用最高的分类标签附件：

- 当标签的用户定义权限包括 Outlook （不要转发），选择标签，并且不转发保护应用到的电子邮件。 
- 只需为 Word、 Excel、 PowerPoint 和文件资源管理器将标签的用户定义权限时，该标签不应用于电子邮件，并都不是保护。

若要配置此高级的设置，请为所选的标签策略输入以下字符串：

- 键 1：**AttachmentAction**

- 键值 1：**建议**或**自动**

- 键 2：**AttachmentActionTip**

- 密钥值 2:"\<自定义工具提示 >"


示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}

## <a name="add-report-an-issue-for-users"></a>为用户添加“报告问题”

此配置使用的策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

当指定以下高级客户端设置时，用户将看到一个“报告问题”选项，他们可以从“帮助和反馈”客户端对话框中选择该选项   。 为链接指定 HTTP 字符串。 例如，为用户报告问题设置的自定义 Web 页面，或者发送给支持人员的电子邮件地址。 

若要配置此高级的设置，请为所选的标签策略输入以下字符串：

- 密钥：**ReportAnIssueLink**

- Value： **\<HTTP string>**

网站示例值：`https://support.contoso.com`

电子邮件地址示例值：`mailto:helpdesk@contoso.com`

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>在 Outlook 中实施弹出消息，警告、证明或阻止发送电子邮件

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

当创建并配置以下高级客户端设置时，用户可以在 Outlook 中看到弹出消息，这些消息可以在发送电子邮件之前警告他们，或者要求他们提供发送电子邮件的理由，或者在存在以下任何一种情况时阻止他们发送电子邮件：

- **其电子邮件或电子邮件附件有一个特定的标签**：
    - 附件可以是任何文件类型

- **其电子邮件或电子邮件的附件没有标签**：
    - 附件可以是 Office 文档或 PDF 文档

如果满足这些条件，收件人的电子邮件地址不包含在允许的域具有指定的名称的列表，用户将看到一个弹出消息，使用以下操作之一：

- **警告**：用户可以确认、发送或取消。

- **验证**：提示用户说明理由（预定义选项或自由格式）。  然后，用户可以发送或取消电子邮件。 说明理由的文本被写入电子邮件 x - 标头，以便其他系统可以读取。 例如，数据丢失防护 (DLP) 服务。

- **阻止**：如果上述情况持续，将阻止用户发送电子邮件。 该消息包括阻止电子邮件的原因，以便用户可以解决问题。 例如，删除特定收件人或标记电子邮件。 


> [!TIP]
> 虽然本教程适用于 Azure 信息保护客户端而不是统一标记客户端，您可以看到这些高级设置中为自己使用的操作[教程：配置 Azure 信息保护来控制的信息使用 Outlook oversharing](../infoprotect-oversharing-tutorial.md)。

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>若要针对特定标签实现用于警告、验证或阻止的弹出消息：

对于所选的策略，使用以下项中创建一个或多个以下的高级设置。 值，指定由其 Guid，每个由逗号分隔的一个或多个标签。

多个标签的 Guid 作为以逗号分隔字符串的示例值： `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- 警告消息：
    
    - 密钥：**OutlookWarnUntrustedCollaborationLabel**
    
    - 值： \<**标签以逗号分隔的 Guid**>

- 对齐消息：
    
    - 密钥：**OutlookJustifyUntrustedCollaborationLabel**
    
    - 值： \<**标签以逗号分隔的 Guid**>

- 阻止邮件：
    
    - 密钥：**OutlookBlockUntrustedCollaborationLabel**
    
    - 值： \<**标签以逗号分隔的 Guid**>


示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}


### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>若要针对没有标签的电子邮件或附件实现用于警告、验证或阻止的弹出消息：

对于相同的标签策略，创建以下高级客户端设置以下值之一：

- 警告消息：
    
    - 密钥：**OutlookUnlabeledCollaborationAction**
    
    - Value：**警告**

- 对齐消息：
    
    - 密钥：**OutlookUnlabeledCollaborationAction**
    
    - Value：**两端对齐**

- 阻止邮件：
    
    - 密钥：**OutlookUnlabeledCollaborationAction**
    
    - Value：**阻止**

- 关闭这些消息：
    
    - 密钥：**OutlookUnlabeledCollaborationAction**
    
    - Value：**Off**


示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}


#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>若要定义特定文件扩展名为，则发出警告，对齐，或阻止不具有标签的电子邮件附件的弹出消息

默认情况下，则发出警告，两端对齐，或阻止弹出消息适用于所有 Office 文档和 PDF 文档。 文件扩展名应显示，则发出警告，证明，可以通过指定优化此列表或阻止的邮件的其他高级设置和一列以逗号分隔的文件扩展名。

多个文件扩展名将定义为一个以逗号分隔字符串的示例值： `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

在此示例中，不会导致未标记的 PDF 文档中，则发出警告，对齐，或阻止弹出消息。

对于相同的标签策略中，输入以下字符串： 


- 密钥：**OutlookOverrideUnlabeledCollaborationExtensions**

- 值： **\<** 文件扩展名以显示消息，以逗号分隔 **>**


示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}

### <a name="to-specify-the-allowed-domain-names-for-recipients-exempt-from-the-pop-up-messages"></a>为收件人指定允许的域名，免除弹出消息

当其他高级客户端设置中指定的域名时，用户看不弹出消息用于设置其电子邮件地址中包含该域名的收件人。 在这种情况下，发送电子邮件时不会受消息干扰。 若要指定多个域，将其添加为单个字符串，以逗号分隔。

典型配置是仅针对组织外部的收件人或并非组织授权合作伙伴的收件人显示弹出消息。 在这种情况下，可以指定组织和合作伙伴使用的所有电子邮件域。

对于相同的标签策略，创建以下高级客户端设置和值，指定一个或多个域，每个由逗号分隔。

多个域的示例值，以逗号分隔的字符串表示：`contoso.com,fabrikam.com,litware.com`

- 警告消息：
    
    - 密钥：**OutlookWarnTrustedDomains**
    
    - 值：\<域名，以逗号分隔>  

- 对齐消息：
    
    - 密钥：**OutlookJustifyTrustedDomains**
    
    - 值：\<域名，以逗号分隔>  

- 阻止邮件：
    
    - 密钥：**OutlookBlockTrustedDomains**
    
    - 值：\<域名，以逗号分隔>  

例如，永远不会阻止发送到具有 contoso.com 电子邮件地址的用户的电子邮件，可以指定高级客户端设置**OutlookBlockTrustedDomains**并**contoso.com**。 因此，用户看不在 Outlook 中的警告弹出消息在发送电子邮件至john@sales.contoso.com。

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}

## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>禁用将在文档中发现的敏感信息发送到 Azure 信息保护 analytics

此配置使用的策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

[Azure 信息保护分析](../reports-aip.md)可以发现并报告该内容包含敏感信息时保存 Azure 信息保护客户端的文档。 默认情况下，此信息发送由 Azure 信息保护统一到 Azure 信息保护 analytics 标记。

若要更改此行为，以便统一标记客户端不发送此信息，请为所选的标签策略输入以下字符串：

- 密钥：RunAuditInformationTypeDiscovery 

- Value：**False**

如果设置此高级客户端设置、 审核结果仍将从统一标记客户端发送，但信息仅限于 reporting 时用户已访问标记为内容。

例如：

- 如果不进行此设置，可以看到用户访问的 Financial.docx 已被设置 Confidential \ Sales 标签  。

- 如果进行此设置，可以看到该 Financial.docx 包含 6 位数信用卡卡号。
    
    - 如果同时还启用[用于更深入分析的内容匹配](../reports-aip.md#content-matches-for-deeper-analysis)，那么，还能够查看具体的信用卡卡号。

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RunAuditInformationTypeDiscovery="False"}

## <a name="disable-sending-information-type-matches-for-a-subset-of-users"></a>禁止为一部分用户发送信息类型匹配项

此配置使用的策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

当你选中用于收集敏感信息类型或自定义条件的内容匹配项的[Azure 信息保护分析](../reports-aip.md)对应的复选框时，默认由所有用户发送此信息。 如果您有一些不应发送此数据的用户，创建以下高级客户端设置中为这些用户的标签策略： 

- 密钥：**LogMatchedContent**

- Value：**False**

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="Disable"}

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>从 Secure Islands 和其他标记解决方案迁移标签

此配置使用标签[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

此配置不符合具有文件扩展名为.ppdf 的受保护 PDF 文件。 这些文件无法打开文件资源管理器、 PowerShell 或扫描程序。

对于 Secure Islands 标记的 Office 文档，可以通过使用你定义的映射重新标记敏感度标签与这些文档。 此外，这种方法还可用于重用其他解决方案对 Office 文档标记的标签。 

由于此配置选项，而新的敏感度标签应用 Azure 信息保护统一标记客户端，如下所示：

- 对于 Office 文档：当在桌面应用中打开文档时，新的敏感度标签显示为已设置并保存文档时应用。

- 对于 PowerShell：[Set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)并[集 AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification)可以将应用新的敏感度标签。

- 对于文件资源管理器：在 Azure 信息保护对话框中，新的敏感度标签显示，但未设置。

此配置需要你指定一个命名的高级设置**labelByCustomProperties**为每个你想要将映射到旧标签的敏感度标签。 然后，使用以下语法设置每个条目的值：

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

指定所选的迁移规则名称。 请使用描述性名称，可帮助你确定从将旧标记解决方案的方式的一个或多个标签应映射到敏感度标签。 此名称显示在扫描程序报告和事件查看器中。

请注意，此设置不会从文档中删除原始标签，也不会删除可能已应用原始标签的文档中的任何视觉标记。 若要删除页眉和页脚，请参阅前面部分[从其他标记解决方案中删除页眉和页脚](#remove-headers-and-footers-from-other-labeling-solutions)。

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>示例 1：相同标签名称的一对一映射

要求：对于 Secure Islands 标记为“机密”的文档，应由 Azure 信息保护重新标记为“机密”。

在此示例中：

- Secure Islands 标签名为“Confidential”，存储在名为“Classification”的自定义属性中   。

高级设置：

- 密钥： **labelByCustomProperties**

- Value：**安全标记为机密、 分类、 机密**

示例 PowerShell 命令，其中标签名为"机密":

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>示例 2：不同标签名称的一对一映射

要求：对于 Secure Islands 标记为“敏感”的文档，应由 Azure 信息保护重新标记为“高度机密”。

在此示例中：

- Secure Islands 标签名为“Sensitive”，存储在名为“Classification”的自定义属性中   。

高级设置：

- 密钥： **labelByCustomProperties**

- Value：**安全标记是区分，分类，不区分**

示例 PowerShell 命令，其中标签名为"高度机密":

    Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>示例 3：标签名称的多对一映射

要求：具有两个 Secure Islands 标签包含单词"内部"，并且您希望由 Azure 信息保护统一标记客户端的文档之一的这些 Secure Islands 标签重新标记为"常规"。

在此示例中：

- Secure Islands 标签包含单词“Internal”，存储在名为“Classification”的自定义属性中   。

高级客户端设置：

- 密钥： **labelByCustomProperties**

- Value：**安全标记包含内部，分类。\*内部。\***

示例 PowerShell 命令，其中标签名为"常规":

    Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}

#### <a name="example-4-multiple-rules-for-the-same-label"></a>示例 4:相同标签的的多个规则

当需要相同的标签用于多个规则时，定义为相同的键的多个字符串值。 

在此示例中：

- Secure Islands 标签名为"机密"和"机密"存储在名为的自定义属性 * * 分类，并且想要应用的敏感度标签名为"机密"的 Azure 信息保护统一标记客户：

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

### <a name="extend-your-label-migration-rules-to-emails"></a>将标签扩展到电子邮件迁移规则

可以使用通过指定其他标签策略高级设置高级设置除了 Office 文档的 Outlook 电子邮件与你 labelByCustomProperties。 但是，此设置具有已知负对 Outlook 的性能的影响，因此配置此附加设置，只有一个强大业务需求为其，并记得将其设置为 null 的字符串值，完成后从迁移其他标记解决方案。

若要配置此高级的设置，请为所选的标签策略输入以下字符串：

- 密钥：**EnableLabelByMailHeader**

- Value：**Tue**

示例 PowerShell 命令，其中标签策略名为"Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>应用标签时应用的自定义属性

此配置使用标签[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

当你想要将一个或多个自定义属性应用到除应用的敏感度标签的元数据的文档或电子邮件时，则可能存在一些方案。

例如：

- 过程中都[另一个标记解决方案迁移](#migrate-labels-from-secure-islands-and-other-labeling-solutions)，例如 Secure Islands。 在迁移期间的互操作性，您希望同时应用由其他标记解决方案的自定义属性的敏感度标签。

- 有关内容管理系统 （如 SharePoint 或从另一个供应商的文档管理解决方案），你想要使用不同的值的标签，而不是标签 GUID 的用户友好名称且使用一致的自定义属性名称。

对于 Office 文档和 Outlook 电子邮件通过使用 Azure 信息保护统一标记客户端，该用户标签可以添加一个或多个定义的自定义属性。 此方法对于统一标记客户端还可用于将自定义属性显示来自其他解决方案的内容不由统一标记客户端尚未标记的标签。

由于此配置选项，而自定义的任何其他属性所应用的 Azure 信息保护统一标记客户端，如下所示：

- 对于 Office 文档：当文档被标记为桌面应用程序中时，保存该文档时应用的其他自定义属性。

- 为 Outlook 电子邮件：当在 Outlook 中标记电子邮件时，其他属性应用于 x 标头时发送电子邮件。

- 对于 PowerShell：[Set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)并[集 AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification)标记和保存文档时应用的其他自定义属性。 [Get-aipfilestatus](/powershell/module/azureinformationprotection/get-aipfilestatus)作为映射标签显示自定义属性，如果不应用的敏感度标签。

- 对于文件资源管理器：用户右键单击该文件，并应用标签，将应用的自定义属性。

此配置需要你指定一个命名的高级设置**customPropertyByLabel**为每个你想要应用的其他自定义属性的敏感度标签。 然后，使用以下语法设置每个条目的值：

`[custom property name],[custom property value]`

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>示例 1：添加一个标签的单个自定义属性

要求：Azure 信息保护统一标记客户端标记为"机密"的文档应具有名为"机密"值"分类"的其他自定义属性。

在此示例中：

- 名为的敏感度标签**Confidential** ，并创建一个名为的自定义属性**分类**值为**机密**。

高级设置：

- 密钥： **customPropertyByLabel**

- Value：**Classification,Secret**

示例 PowerShell 命令，其中标签名为"机密":

    Set-Label -Identity Confidential -AdvancedSettings @{customPropertyByLabel="Classification,Secret"}

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>示例 2：添加一个标签的多个自定义属性

若要添加多个相同的标签的自定义属性，您需要定义一个键的多个字符串值。

示例 PowerShell 命令，其中标签名为"常规"和你想要添加一个名为的自定义属性**分类**值为**常规**和第二个自定义属性名为**敏感度**值为**内部**:

    Set-Label -Identity General -AdvancedSettings @{customPropertyByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>将标签配置为在 Outlook 中应用 S/MIME 保护

此配置使用标签[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

使用这些设置，仅当你有正在运行时[S/MIME 部署](https://docs.microsoft.com/office365/SecurityCompliance/s-mime-for-message-signing-and-encryption)并且想要自动应用此保护方法应用于电子邮件而不是 Azure 信息保护中的 Rights Management 保护的标签。 应用的保护与用户通过在 Outlook 中手动选择 S/MIME 选项应用的保护一样。

若要配置的 S/MIME 数字签名的高级的设置，请为所选标签输入以下字符串：

- 密钥：**SMimeSign**

- Value：**True**

若要配置 S/MIME 加密的高级的设置，请为所选标签输入以下字符串：

- 密钥：**SMimeEncrypt**

- Value：**True**

如果您指定的标签配置的预览版 Azure 信息保护统一标记客户端，加密的 S/MIME 保护将替换仅在 Outlook 中的 Rights Management 保护。 统一标记客户端的正式发布版本继续使用在管理中心中的标签为指定的加密设置。 对于 Office 应用程序与内置标记，这些不适用于 S/MIME 保护但相反，应用不转发保护。

如果你想要仅可以在 Outlook 中看到的标签，配置标签以应用到加密**仅在电子邮件在 Outlook 中的**。

示例 PowerShell 命令，其中标签名为"仅收件人":

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>指定父标签的默认子标签

此配置使用标签[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。 它被受统一标记仅限客户端的预览版本。

当将子标签添加到标签时，用户可以不再到文档或电子邮件应用父标签。 默认情况下，用户选择要查看子标签，它们可以应用，并选择这些子标签之一的父标签。 如果配置此高级设置，当用户选择父标签时，子标签被自动选择并应用于它们： 

- 密钥：**DefaultSubLabelId**

- 值： \<sublabel GUID >

示例 PowerShell 命令，其中父标签名为"机密"和"所有员工"子标签都有 8faca7b8-8 d 20-48a3-8ea2-0f96310a848e 一个 GUID:

    Set-Label -Identity "Confidential" -AdvancedSettings @{defaultsublabels="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}

## <a name="specify-a-color-for-the-label"></a>指定标签的颜色

此配置使用标签[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)必须通过使用 Office 365 安全与合规性中心 PowerShell 配置。

使用此高级设置来设置标签的颜色。 若要指定的颜色，颜色的红色、 绿色和蓝色 (RGB) 组件的输入十六进制三元色代码。 例如，#40e0d0 是青绿色的 RGB 十六进制值。

如果您需要引用这些代码，您会发现从一个帮助表[\<颜色 >](https://developer.mozilla.org/docs/Web/CSS/color_value)从 MSDN web 文档的页。也可在许多可编辑图片的应用程序中找到这些代码。 例如，通过 Microsoft 画图，从调色板中选择自定义颜色，系统将自动显示 RGB 值，该值可供复制。

若要配置标签的颜色的高级的设置，请为所选标签中输入以下字符串：

- 密钥：**颜色**

- Value：\<RGB 十六进制值 >

示例 PowerShell 命令，其中标签名为"Public":

    Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}

## <a name="sign-in-as-a-different-user"></a>以其他用户身份登录

在生产环境中，用户通常不需要其他用户在使用 Azure 信息保护时统一标记的客户端的身份登录。 不过，作为管理员，你在测试阶段可能需要以其他用户身份登录。 

可以使用“MicrosoftAzure 信息保护”对话框验证当前登录的帐户  ：打开 Office 应用程序并在**主页**选项卡上，选择**敏感度**按钮，并选择**帮助和反馈**。 帐户名称会显示在“客户端状态”  部分中。

请确保还要检查所显示的登录帐户的域名。 很容易忽视的一点是，使用正确的帐户名登录，但域不正确。 使用错误帐户的症状包括无法下载标签，或看不到标签或预期的行为。

以其他用户身份登录：

1. 导航到 %localappdata%\Microsoft\MSIP 并删除 TokenCache 文件   。

2. 重新启动任何打开的 Office 应用程序，并使用其他用户帐户登录。 如果您没有在 Office 应用程序中登录到 Azure 信息保护服务中看到在提示符下，返回到**Microsoft Azure 信息保护**对话框并选择**登录**从更新**客户端状态**部分。

此外：

- 完成这些步骤后，仍使用旧帐户 Azure 信息保护统一标记客户端已签名，如果从 Internet Explorer 中，删除所有 cookie，然后重复步骤 1 和 2。

- 如果使用的是单一登录，必须在删除令牌文件后注销 Windows，再使用其他用户帐户登录。 Azure 信息保护统一标记客户端然后自动进行身份验证使用当前登录的用户帐户中。

- 此解决方案支持以同一租户中的其他用户身份登录。 不支持以不同租户中的其他用户身份登录。 若要使用多个租户测试 Azure 信息保护，请使用不同的计算机。

- 可以使用**将设置重置**选项从**帮助和反馈**注销并从 Office 365 安全与合规中心中删除当前下载的标签和策略设置Microsoft 365 安全中心或 Microsoft 365 合规中心。


## <a name="change-the-local-logging-level"></a>更改本地日志记录级别

默认情况下，Azure 信息保护统一到的标记客户端写入客户端日志文件 **%localappdata%\Microsoft\MSIP**文件夹。 这些文件供 Microsoft 支持部门用来排除故障。
 
若要更改这些文件的日志记录级别，请在注册表中找到以下值名称，并将值数据设置为所需的日志记录级别：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

将日志记录级别设置为以下值之一：

- **关闭**：没有本地日志记录。

- **错误**：只有错误。

- **Info**：最低级别日志记录，其中不含事件 ID。

- **Debug**：完整信息。

- **Trace**：详细日志记录（客户端默认设置）。

此注册表设置不会更改发送到适用于 Azure 信息保护的信息[中央报告](../reports-aip.md)。


## <a name="next-steps"></a>后续步骤
现在，你已自定义 Azure 信息保护统一标记客户端，请参阅以下资源，可能需要支持此客户端的其他信息：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)
