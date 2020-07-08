---
title: 自定义配置-Azure 信息保护统一标签客户端
description: 有关自定义适用于 Windows 的 Azure 信息保护统一标签客户端的信息。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v2client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 390f89d124d68591e8eaade67f6666d3f7c32ed4
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048861"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>管理员指南： Azure 信息保护统一标签客户端的自定义配置

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012*
>
> **对于 Windows 7 和 Office 2010，具有扩展 Microsoft 支持的客户也可以获得这些版本的 Azure 信息保护支持。请咨询你的支持联系人了解完整的详细信息。*
>
> *适用于以下内容的说明： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

在管理 Azure 信息保护统一标签客户端时，请使用以下信息来了解特定方案或用户子集可能需要的高级配置。

这些设置需要编辑注册表或指定高级设置。 高级设置使用[Office 365 Security & 相容性中心 PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps)。

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>如何使用 Office 365 Security & 相容性中心 PowerShell 配置客户端的高级设置

使用 Office 365 Security & 相容性中心 PowerShell 时，可以配置支持标签策略和标签自定义的高级设置。 例如：

- 在 Office 应用中显示信息保护栏的设置是 "***标签策略" 高级设置***。
- 用于指定标签颜色的设置是 "***标签高级" 设置***。

在这两种情况下，在[连接到 Office 365 Security & 相容性中心 PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps)后，请使用策略或标签的标识（名称或 GUID）指定*AdvancedSettings*参数，并在[哈希表](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables)中指定键/值对。 使用以下语法：

对于 "标签" 策略设置，单个字符串值：

```ps
Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}
```

对于 "标签" 策略设置，相同键的多个字符串值：

```ps
Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}
```

对于标签设置，则为单个字符串值：

```ps
Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}
```

对于标签设置，相同键的多个字符串值：

```ps
Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}
```

若要删除高级设置，请使用相同的语法，但指定空字符串值。

> [!IMPORTANT]
> 使用字符串中的空格将阻止应用标签。 

#### <a name="examples-for-setting-advanced-settings"></a>设置高级设置的示例

示例1：为单个字符串值设置标签策略高级设置：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}
```

示例2：为单个字符串值设置标签高级设置：

```ps
Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}
```

示例3：为多个字符串值设置标签高级设置：

```ps
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}
```

示例4：通过指定空字符串值删除标签策略高级设置：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}
```

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>为标签策略或标签指定标识

指定 PowerShell*标识*参数的标签策略名称很简单，因为在管理标签策略的管理中心，你只会看到一个策略名称。 但对于标签，你会在 "管理中心" 中看到 "**名称**" 和 "**显示名称**"。 在某些情况下，两者的值都是相同的，但它们可能不同：

- **Name**是标签的原始名称，在所有标签中都是唯一的。 如果在创建标签之后更改其名称，此值保持不变。 对于从 Azure 信息保护迁移的标签，你可能会看到 "Azure 门户中的标签的标签 ID。

- **显示名称**是用户看到的标签名称，并且在所有标签中不必唯一。 例如，用户会看到一个**员工**子标签了 "**机密**" 标签，而另一个**员工子标签 "** **高度机密**" 标签。 这些子标签都显示相同的名称，但不是相同的标签，并且具有不同的设置。

若要配置标签高级设置，请使用 "**名称**" 值。 例如，若要标识下图中的标签，请指定 `-Identity "All Company"` ：

![使用 "Name" 而不是 "Display Name" 标识敏感度标签](../media/labelname_scc.png)

如果希望指定标签 GUID，此值不会显示在管理标签的管理中心。 不过，你可以使用以下 Office 365 Security & 相容性中心 PowerShell 命令来查找此值：

```ps
Get-Label | Format-Table -Property DisplayName, Name, Guid
```

#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>优先顺序-如何解决冲突的设置

使用管理你的敏感度标签的管理中心之一，你可以配置以下标签策略设置：

- **默认情况下将此标签应用于文档和电子邮件**

- **用户必须提供理由以删除标签或较低分类标签**

- **要求用户将标签应用于其电子邮件或文档**

- **为用户提供自定义帮助页的链接**

如果为用户配置了多个标签策略，每个都有可能不同的策略设置，则将根据管理中心中策略的顺序应用最后一个策略设置。 有关详细信息，请参阅[标签策略优先级（顺序问题）](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#label-policy-priority-order-matters)

标签高级设置遵循相同的优先级逻辑：当标签位于多个标签策略中并且标签具有高级设置时，将根据管理中心中策略的顺序应用上一个高级设置。

标签策略高级设置按相反顺序应用：除了一个例外，还会根据 "管理中心" 中策略的顺序，应用第一个策略的高级设置。 例外情况是高级设置*OutlookDefaultLabel*，它为 Outlook 设置不同的默认标签。 对于此标签策略的高级设置，将根据管理中心中策略的顺序应用最后一个设置。


#### <a name="available-advanced-settings-for-label-policies"></a>标签策略的可用高级设置

将*AdvancedSettings*参数与[LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-labelpolicy?view=exchange-ps)和[LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-labelpolicy?view=exchange-ps)一起使用。

|设置|应用场景和说明|
|----------------|---------------|
|AdditionalPPrefixExtensions|[支持更改 \<EXT> 。\<EXT>使用此高级属性 .pfile 到 P](#additionalpprefixextensions)
|AttachmentAction|[对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|DisableMandatoryInOutlook|[使 Outlook 邮件免于强制标记](#exempt-outlook-messages-from-mandatory-labeling)
|EnableAudit|[禁止向 Azure 信息保护分析发送审核数据](#disable-sending-audit-data-to-azure-information-protection-analytics)|
|EnableContainerSupport|[允许从 PST、rar、7zip 和 MSG 文件中删除保护](#enable-removal-of-protection-from-compressed-files)
|EnableCustomPermissions|[在文件资源管理器中禁用自定义权限](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|EnableLabelBySharePointProperties|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)
|HideBarByDefault|[在 Office 应用中显示“信息保护”栏](#display-the-information-protection-bar-in-office-apps)|
|LogMatchedContent|[向 Azure 信息保护分析发送信息类型匹配项](#send-information-type-matches-to-azure-information-protection-analytics)|
|OutlookBlockTrustedDomains|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[为 Outlook 设置不同的默认标签](#set-a-different-default-label-for-outlook)|
|OutlookJustifyTrustedDomains|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[在 Outlook 中启用建议的分类](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PFileSupportedExtensions|[更改要保护的文件类型](#change-which-file-types-to-protect)|
|PostponeMandatoryBeforeSave|[使用强制标签时，删除文档的“以后再说”](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[删除其他标记解决方案中的页眉和页脚](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[为用户添加“报告问题”](#add-report-an-issue-for-users)|
|RunAuditInformationTypesDiscovery|[禁止将文档中发现的敏感信息发送到 Azure 信息保护分析](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
|RunPolicyInBackground|[开启在后台持续运行的分类](#turn-on-classification-to-run-continuously-in-the-background)
|ScannerConcurrencyLevel|[限制扫描程序使用的线程数](#limit-the-number-of-threads-used-by-the-scanner)|
|ScannerFSAttributesToSkip | [在扫描期间跳过或忽略文件，具体取决于文件属性](#skip-or-ignore-files-during-scans-depending-on-file-attributes)
|UseCopyAndPreserveNTFSOwner | [在标记期间保留 NTFS 所有者](#preserve-ntfs-owners-during-labeling-public-preview)

用于检查标签策略设置对名为 "Global" 的标签策略有效的示例 PowerShell 命令：

```ps
(Get-LabelPolicy -Identity Global).settings
```

#### <a name="available-advanced-settings-for-labels"></a>标签的可用高级设置

使用带有[新标签](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps)和[设置标签](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)的*AdvancedSettings*参数。

|设置|应用场景和说明|
|----------------|---------------|
|color|[指定标签的颜色](#specify-a-color-for-the-label)|
|customPropertiesByLabel|[应用标签时应用自定义属性](#apply-a-custom-property-when-a-label-is-applied)|
|DefaultSubLabelId|[为父标签指定默认子标签](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|SMimeEncrypt|[将标签配置为在 Outlook 中应用 S/MIME 保护](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[将标签配置为在 Outlook 中应用 S/MIME 保护](#configure-a-label-to-apply-smime-protection-in-outlook)|

用于检查标签设置对名为 "Public" 的标签有效的示例 PowerShell 命令：

```ps
(Get-Label -Identity Public).settings
```

## <a name="display-the-information-protection-bar-in-office-apps"></a>在 Office 应用中显示“信息保护”栏

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

默认情况下，用户必须选择 "**敏感度**" 按钮中的 "**显示栏**" 选项，以在 Office 应用中显示信息保护栏。 使用**HideBarByDefault**键，并将值设置为**False** ，以便为用户自动显示此栏，以便他们可以从栏或按钮中选择标签。 

对于所选的标签策略，请指定以下字符串：

- 密钥： **HideBarByDefault**

- 值：False****

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}
```

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>使 Outlook 邮件免于强制标记

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

默认情况下，当你启用 "**所有文档和电子邮件**的标签策略" 设置时，必须具有标签，所有已保存的文档和已发送的电子邮件都必须应用标签。 配置以下高级设置时，策略设置仅适用于 Office 文档，而不适用于 Outlook 邮件。

对于所选的标签策略，请指定以下字符串：

- 密钥： **DisableMandatoryInOutlook**

- 值： **True**

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{DisableMandatoryInOutlook="True"}
```

## <a name="enable-recommended-classification-in-outlook"></a>在 Outlook 中启用建议的分类

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

为建议的分类配置标签时，系统将提示用户接受或关闭 Word、Excel 和 PowerPoint 中建议的标签。 此设置将此标签建议扩展到也在 Outlook 中显示。

对于所选的标签策略，请指定以下字符串：

- 键：OutlookRecommendationEnabled****

- 值： **True**

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}
```

## <a name="enable-removal-of-protection-from-compressed-files"></a>启用从压缩文件中删除保护

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

配置此设置时，将启用[PowerShell](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-powershell) cmdlet **set-aipfilelabel** ，以允许从 PST、RAR、7zip 和 MSG 文件中删除保护。

- 密钥： **EnableContainerSupport**

- 值： **True**

启用策略的示例 PowerShell 命令：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableContainerSupport="True"}
```

## <a name="set-a-different-default-label-for-outlook"></a>为 Outlook 设置不同的默认标签

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

当你配置此设置时，Outlook 不会应用默认标签，该标签配置为 "**默认情况下将此标签应用于文档和电子邮件**" 选项。 相反，Outlook 可应用不同的默认标签，也可不应用标签。

对于所选的标签策略，请指定以下字符串：

- 键：OutlookDefaultLabel****

- 值： \<**label GUID**> 或**None**

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}
```

## <a name="change-which-file-types-to-protect"></a>更改要保护的文件类型

这些配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

默认情况下，Azure 信息保护的统一标签客户端将保护所有文件类型，并且来自客户端的扫描程序仅保护 Office 文件类型和 PDF 文件。

您可以通过指定下列选项之一来更改所选标签策略的此默认行为：

### <a name="pfilesupportedextension"></a>PFileSupportedExtension

- 密钥： **PFileSupportedExtensions**

- 负值**\<string value>** 

使用下表来确定要指定的字符串值：

| 字符串值| 客户端| 扫描仪|
|-------------|-------|--------|
|\*|默认值：将保护应用于所有文件类型|将保护应用于所有文件类型|
|\<null value>| 将保护应用于 Office 文件类型和 PDF 文件| 默认值：将保护应用于 Office 文件类型和 PDF 文件|
|Convertto-html-Json （".jpg"，".png"）|除了 Office 文件类型和 PDF 文件，还会将保护应用到指定的文件扩展名 | 除了 Office 文件类型和 PDF 文件，还会将保护应用到指定的文件扩展名

示例1：用于统一客户端的 PowerShell 命令仅保护 Office 文件类型和 PDF 文件，其中标签策略命名为 "客户端"：

```ps
Set-LabelPolicy -Identity Client -AdvancedSettings @{PFileSupportedExtensions=""}
```

示例2：用于扫描程序的 PowerShell 命令，用于保护所有文件类型，其中标签策略命名为 "Scanner"：

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

示例3：用于扫描程序的 PowerShell 命令，用于保护 .txt 文件和 .csv 文件以及 Office 文件和 PDF 文件，其中标签策略命名为 "Scanner"：

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".txt", ".csv")}
```

利用此设置，你可以更改受保护的文件类型，但不能将默认保护级别从本机更改为通用。 例如，对于运行统一标签客户端的用户，你可以更改默认设置，以便仅保护 Office 文件和 PDF 文件而不是所有文件类型。 但不能将这些文件类型更改为使用 .pfile 文件扩展名进行常规保护。

### <a name="additionalpprefixextensions"></a>AdditionalPPrefixExtensions

统一标签客户端支持更改 \<EXT> 。\<EXT>使用高级属性**AdditionalPPrefixExtensions**.pfile 到 P。 右键单击、PowerShell 和扫描程序支持此高级属性。 所有应用都有类似的行为。   

- 密钥： **AdditionalPPrefixExtensions**

- 负值**\<string value>** 

使用下表来确定要指定的字符串值：

| 字符串值| 客户端和扫描程序|
|-------------|---------------|
|\*|所有 .Pfile 扩展变为 P\<EXT>|
|\<null value>| 默认值的行为类似于默认的保护值。|
|Convertto-html-Json （"dwg"，".zip"）|除了前面的列表，"dwg" 和 ".zip" 变为 P\<EXT>| 

示例1： PowerShell 命令的行为类似于默认行为，即保护 "dwg" 变为 ".pfile"：

```ps
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions =""}
```

示例2： PowerShell 命令：在文件受到保护时，将通用保护（.pfile）中的所有 .Pfile 扩展更改为本机保护（. pdwg）：

```ps
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions ="*"}
```

示例3：使用此服务时将 "dwg" 更改为 "pdwg" 的 PowerShell 命令将保护此文件：

```ps
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions =ConvertTo-Json(".dwg")}
```

对于此设置，以下扩展（". txt"，".xml"，".bmp"，". jt"，".jpg"，"jpeg"，". jpe"，". jif"，"jfif"，". *"，".png"，".tif"，". tiff"，".gif"）始终变为 P \<EXT> 。值得注意的是，".ptxt" 不是 ".pfile"。 
仅当启用了高级属性- [**PFileSupportedExtension**](#pfilesupportedextension)的 pfile 保护时， **AdditionalPPrefixExtensions**才有效。 

例如，在使用以下命令时：

```ps
Set-LabelPolicy -AdvancedSettings @{PFileSupportedExtensions=""}
```

不能 .Pfile 保护，而**AdditionalPPrefixExtensions**中的值将被忽略。 

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>使用强制标签时，删除文档的“以后再说”

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

使用 "**所有文档和电子邮件**的标签策略" 设置必须具有标签时，用户首次保存 Office 文档和发送电子邮件时，系统将提示用户选择标签。 对于文档，用户可以选择“以后再说”**** 暂时关闭提示以选择标签，并返回到文档。 但是不能在未选择标签的情况下关闭已保存的文档。 

在配置此设置时，将删除“以后再说”**** 选项，以便首次保存文档时用户必须选择一个标签。

对于所选的标签策略，请指定以下字符串：

- 键：PostponeMandatoryBeforeSave****

- 值：False****

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}
```

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>删除其他标记解决方案中的页眉和页脚

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

可以通过两种方法从其他标记解决方案中删除分类。 第一种方法从 Word 文档中删除任何形状，其中的形状名称与 advanced 属性**WordShapeNameToRemove**中定义的名称相匹配，第二种方法允许您从 Word、Excel 和 PowerPoint 文档中删除或替换**RemoveExternalContentMarkingInApp**高级属性中定义的基于文本的标头或表尾。 

### <a name="use-the-wordshapenametoremove-advanced-property"></a>使用 WordShapeNameToRemove 高级属性

*版本2.6.101.0 和更高版本支持**WordShapeNameToRemove**高级属性*

此设置使您可以在其他标签解决方案应用这些视觉标记后，删除或替换 Word 文档中基于形状的标签。 例如，该形状包含旧标签的名称，你现在已将该标签迁移到 "敏感度" 标签，以使用新标签名称及其自己的形状。

若要使用此高级属性，需要在 Word 文档中查找该形状的名称，然后在 " **WordShapeNameToRemove** " 属性的 "形状" 高级属性列表中定义这些名称。 服务将删除 Word 中以此高级属性的形状列表中定义的名称开头的任何形状。

通过定义要删除的所有形状的名称并避免在所有形状中检查文本（这是一种消耗大量资源的过程），避免删除包含要忽略的文本的形状。

如果未在此附加高级属性设置中指定 Word 形状，并且 Word 包含在**RemoveExternalContentMarkingInApp**项值中，则将检查在**ExternalContentMarkingToRemove**值中指定的文本的所有形状。 

查找要使用的形状的名称并希望排除：

1. 在 Word 中，显示 "**选择**" 窗格： "**主页**" 选项卡 >**编辑**组 >**选择**"选项" >**选择 "窗格**。

2. 选择要标记为删除的页面上的形状。 标记的形状的名称现在会在**选择**窗格中突出显示。

使用形状的名称为 * * * * * * * * * * * * * * * * * * * * * * * WordShapeNameToRemove。 

示例：形状名称为**dc**。 若要删除具有此名称的形状，则指定值：`dc`。

- 密钥： **WordShapeNameToRemove**

- 值：\<**Word shape name**> 

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{WordShapeNameToRemove="dc"}
```

如果有多个 Word 形状要删除，请指定任意数量的值，以便删除形状。

### <a name="use-the-removeexternalcontentmarkinginapp-advanced-property"></a>使用 RemoveExternalContentMarkingInApp 高级属性

此设置使你可以从文档中删除或替换由其他标签解决方案应用的基于文本的页眉或页脚。 例如，旧的页脚包含已迁移到敏感度标签的旧标签的名称，以使用新标签名称及其自己的页脚。

当统一标签客户端在其策略中获取此配置时，在 Office 应用中打开文档并将任何敏感度标签应用于该文档时，将删除或替换旧的页眉和页脚。

Outlook 不支持此配置，并且请注意，在 Word、Excel 和 PowerPoint 中使用它时，会对这些应用的性能产生负面影响。 该配置允许你根据应用程序来定义设置，例如，搜索 Word 文档页眉和页脚中的文本，而不是 Excel 电子表格或 PowerPoint 演示文稿中的。

因为模式匹配会影响用户的性能，所以建议你将 Office 应用程序类型（**W**Ord、E**X**项、 **P**owerPoint）限制为只需搜索的类型。
对于所选的标签策略，请指定以下字符串：
- 键：RemoveExternalContentMarkingInApp****

- 值：\<**Office application types WXP**> 

示例：

- 若要仅搜索 Word 文档，请指定 W****。

- 若要搜索 Word 文档和 PowerPoint 演示文稿，请指定 WP****。

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}
```

然后需要至少一个高级客户端设置 ExternalContentMarkingToRemove，**** 指定页眉或页脚的内容以及如何删除或替换它们。

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>如何配置 ExternalContentMarkingToRemove

指定 ExternalContentMarkingToRemove 键的字符串值时，拥有三个使用正则表达式的选项****：

- 用以删除页眉或页脚中所有内容的部分匹配。

    示例：页眉或页脚包含字符串 TEXT TO REMOVE****。 想要完全删除这些页面或页脚。 可指定值：`*TEXT*`。

- 用以删除页眉或页脚中特定字词的完全匹配。

    示例：页眉或页脚包含字符串 TEXT TO REMOVE****。 只想删除单词 TEXT，结果使页眉或页脚字符串变为 TO REMOVE********。 可指定值：`TEXT `。

- 用以删除页眉或页脚中所有内容的完全匹配。

    示例：页眉或页脚包含字符串 TEXT TO REMOVE****。 想要删除其字符串为 TEXT TO REMOVE 的页眉或页脚。 可指定值：`^TEXT TO REMOVE$`。


指定的字符串的匹配模式不区分大小写。 最大字符串长度为255个字符，且不能包含空格。 

因为某些文档可能包括不可见字符或者不同类型的空格或制表符，可能检测不到指定的短语或句子的字符串。 只要有可能，指定单个易区分的单词作为值，并确保在生产环境中部署之前测试结果。

对于同一标签策略，请指定以下字符串：

- 键：ExternalContentMarkingToRemove****

- 值：\<**string to match, defined as regular expression**> 

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}
```

#### <a name="multiline-headers-or-footers"></a>多行页眉或页脚

如果页眉或页脚文本不只一行，则为每行创建一个键和值。 例如，下面是具有两行文本的页脚：

The file is classified as Confidential****

Label applied manually****

若要删除此多行页脚，请为同一标签策略创建以下两个条目：

- 键：ExternalContentMarkingToRemove****

- 密钥值1： ** \* 机密***

- 键值2： ** \* 应用标签*** 

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}
```

#### <a name="optimization-for-powerpoint"></a>针对 PowerPoint 的优化

PowerPoint 中的页脚以形状的形式实现。 若要避免删除那些你指定的但不属于页面或页脚的形状，可使用以下附加高级客户端设置：PowerPointShapeNameToRemove****。 我们还建议使用此设置来避免检查所有形状中的文本，因为这将占用大量资源。

如果未指定这项附加的高级客户端设置，并且 PowerPoint 包括在 RemoveExternalContentMarkingInApp **** 键值中，将对所有形状检查你在 ExternalContentMarkingToRemove 值中指定的文本****。 

查找用作页眉或页脚的形状的名称：

1. 在 PowerPoint 中，显示“选择”窗格：“格式”选项卡 >“排列”组 >“选择”窗格****************。

2. 选择幻灯片上包含页眉或页脚的形状。 所选形状的名称现在突出显示在“选择”**** 窗格中。

使用形状的名称为 PowerPointShapeNameToRemove**** 键指定一个字符串字。 

示例：形状名称是 fc****。 若要删除具有此名称的形状，则指定值：`fc`。

- 键：PowerPointShapeNameToRemove****

- 值：\<**PowerPoint shape name**> 

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}
```

如果要删除多个 PowerPoint 形状，请指定任意数量的值，以便删除形状。

默认情况下，只检查主幻灯片的页眉和页脚。 若要将检查范围扩展到所有幻灯片，将占用大量资源，则可以使用 RemoveExternalContentMarkingInAllSlides**** 附加高级客户端设置：

- 键：RemoveExternalContentMarkingInAllSlides****

- 值： **True**

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}
```

## <a name="disable-custom-permissions-in-file-explorer"></a>在文件资源管理器中禁用自定义权限

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

默认情况下，当用户在文件资源管理器中右键单击并选择 "**分类和保护**" 时，会看到名为 "**使用自定义权限保护**" 的选项。 使用此选项可以设置自己的保护设置，这些设置可以替代标签配置中可能包含的任何保护设置。 用户还能看到一个用于删除保护的选项。 当你配置此设置时，用户看不到这些选项。

若要配置此高级设置，请为所选标签策略输入以下字符串：

- 键：EnableCustomPermissions****

- 值：False****

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}
```

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

当你将高级客户端设置配置为[在文件资源管理器中禁用自定义权限](#disable-custom-permissions-in-file-explorer)时，默认情况下，用户将无法查看或更改已在受保护文档中设置的自定义权限。

但是，还可以指定另一个高级客户端设置，以便在此方案中，用户可以在使用文件资源管理器并右键单击文件时，查看并更改受保护文档的自定义权限。

若要配置此高级设置，请为所选标签策略输入以下字符串：

- 密钥： **EnableCustomPermissionsForCustomProtectedFiles**

- 值： **True**

示例 PowerShell 命令：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}
```

## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

此设置适用于用户将带标签的文档附加到电子邮件，且未标记电子邮件本身。 在这种情况下，将根据应用于附件的分类标签为其自动选择标签。 最大分类标签处于选中状态。

附件必须是物理文件，并且不能是指向文件的链接（例如，指向 Microsoft SharePoint 或 OneDrive 上的文件的链接）。

你可以将此设置配置为 "**建议**"，以使用户可以使用可自定义的工具提示将所选标签应用到其电子邮件。 用户可接受或忽略该建议。 或者，你可以将此设置配置为**自动**，其中所选标签会自动应用，但用户可以在发送电子邮件之前删除标签或选择其他标签。

> [!NOTE]
> 如果将具有最高分类标签的附件配置为通过用户定义权限的设置进行保护：
> 
> - 如果标签的用户定义权限包括 Outlook （不要转发），则选择该标签，并且不会向电子邮件应用 "转发保护"。
> - 如果标签的用户定义权限仅用于 Word、Excel、PowerPoint 和文件资源管理器，则该标签不会应用于电子邮件，也不会受到保护。
> 

若要配置此高级设置，请为所选标签策略输入以下字符串：

- 键1： **AttachmentAction**

- 项值1：**建议**或**自动**

- 密钥2： **AttachmentActionTip**

- 键值2： " \<customized tooltip> "

自定义工具提示仅支持一种语言。

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}
```

## <a name="add-report-an-issue-for-users"></a>为用户添加“报告问题”

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

当指定以下高级客户端设置时，用户将看到一个“报告问题”选项，他们可以从“帮助和反馈”客户端对话框中选择该选项********。 为链接指定 HTTP 字符串。 例如，为用户报告问题设置的自定义 Web 页面，或者发送给支持人员的电子邮件地址。 

若要配置此高级设置，请为所选标签策略输入以下字符串：

- 密钥：ReportAnIssueLink****

- 负值**\<HTTP string>**

网站示例值：`https://support.contoso.com`

电子邮件地址示例值：`mailto:helpdesk@contoso.com`

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}
```

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>在 Outlook 中实施弹出消息，警告、证明或阻止发送电子邮件

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

当创建并配置以下高级客户端设置时，用户可以在 Outlook 中看到弹出消息，这些消息可以在发送电子邮件之前警告他们，或者要求他们提供发送电子邮件的理由，或者在存在以下任何一种情况时阻止他们发送电子邮件：

- **其电子邮件或电子邮件附件有一个特定的标签**：
    - 附件可以是任何文件类型

- **其电子邮件或电子邮件的附件没有标签**：
    - 附件可以是 Office 文档或 PDF 文档

满足这些条件时，用户将看到一个弹出消息，其中包含以下操作之一：

- **警告**：用户可以确认并发送或取消。

- **两端对齐**：系统会提示用户提供理由（预定义的选项或自由格式）。  然后，用户可以发送或取消电子邮件。 说明理由的文本被写入电子邮件 x - 标头，以便其他系统可以读取。 例如，数据丢失防护 (DLP) 服务。

- **阻止**：阻止用户发送电子邮件，但条件仍然存在。 该消息包括阻止电子邮件的原因，以便用户可以解决问题。 例如，删除特定收件人或标记电子邮件。 

当弹出消息用于特定标签时，可以按域名为收件人配置例外。

> [!TIP]
> 有关如何配置这些设置的演练示例，请参阅视频[Azure 信息保护 Outlook 弹出窗口配置](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/)。

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>若要针对特定标签实现用于警告、验证或阻止的弹出消息：

对于所选策略，请创建以下一个或多个具有以下键的高级设置。 对于值，按其 Guid 指定一个或多个标签，每个标签用逗号分隔。

以逗号分隔的字符串形式提供的多个标签 Guid 的示例值： 

```sh
dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f
```

- 警告消息：
    
    - 密钥： **OutlookWarnUntrustedCollaborationLabel**
    
    - 值：\<**label GUIDs, comma-separated**>

- 对齐消息：
    
    - 密钥： **OutlookJustifyUntrustedCollaborationLabel**
    
    - 值：\<**label GUIDs, comma-separated**>

- 阻止邮件：
    
    - 密钥： **OutlookBlockUntrustedCollaborationLabel**
    
    - 值：\<**label GUIDs, comma-separated**>


示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}
```

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>为特定标签配置的弹出消息免除域名

对于在这些弹出消息中指定的标签，可以免除特定域名，使用户不会看到其电子邮件地址中包含该域名的收件人的邮件。 在这种情况下，发送电子邮件时不会受消息干扰。 若要指定多个域，将其添加为单个字符串，以逗号分隔。

典型配置是仅针对组织外部的收件人或并非组织授权合作伙伴的收件人显示弹出消息。 在这种情况下，可以指定组织和合作伙伴使用的所有电子邮件域。

对于相同的标签策略，创建以下高级客户端设置，为该值指定一个或多个域，每个域都由逗号分隔。

多个域的示例值，以逗号分隔的字符串表示：`contoso.com,fabrikam.com,litware.com`

- 警告消息：
    
    - 密钥： **OutlookWarnTrustedDomains**
    
    - 负值**\<**domain names, comma separated**>**

- 对齐消息：
    
    - 密钥： **OutlookJustifyTrustedDomains**
    
    - 负值**\<**domain names, comma separated**>**

- 阻止邮件：
    
    - 密钥： **OutlookBlockTrustedDomains**
    
    - 负值**\<**domain names, comma separated**>**

例如，你为 "**机密 \ 所有员工**" 标签指定了**OutlookBlockUntrustedCollaborationLabel** advanced client 设置。 你现在可以指定**OutlookJustifyTrustedDomains**和**contoso.com**的其他高级客户端设置。 因此，用户可以 john@sales.contoso.com 在将其标记为 "**机密 \ 所有员工**" 时向其发送电子邮件，但会阻止向 Gmail 帐户发送具有相同标签的电子邮件。

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}
```

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>若要针对没有标签的电子邮件或附件实现用于警告、验证或阻止的弹出消息：

对于同一标签策略，请创建具有以下值之一的以下高级客户端设置：

- 警告消息：
    
    - 密钥： **OutlookUnlabeledCollaborationAction**
    
    - 值：**警告**

- 对齐消息：
    
    - 密钥： **OutlookUnlabeledCollaborationAction**
    
    - 值：**两端对齐**

- 阻止邮件：
    
    - 密钥： **OutlookUnlabeledCollaborationAction**
    
    - 值： **Block**

- 关闭这些消息：
    
    - 密钥： **OutlookUnlabeledCollaborationAction**
    
    - 值： **Off**


示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}
```

#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>为不带标签的电子邮件附件定义 "警告"、"对齐" 或 "阻止" 弹出消息的特定文件扩展名

默认情况下，"警告"、"对齐" 或 "阻止" 弹出消息适用于所有 Office 文档和 PDF 文档。 可以通过以下方式优化此列表：指定哪些文件扩展名应显示警告、调整或阻止具有其他高级设置的消息，以及以逗号分隔的文件扩展名列表。

要定义为逗号分隔字符串的多个文件扩展名的示例值：`.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

在此示例中，未标记的 PDF 文档不会导致警告、对齐或阻止弹出消息。

对于同一标签策略，请输入以下字符串： 


- 密钥： **OutlookOverrideUnlabeledCollaborationExtensions**

- 负值**\<**file name extensions to display messages, comma separated**>**


示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}
```

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>为不带附件的电子邮件指定其他操作

默认情况下，你为 OutlookUnlabeledCollaborationAction 指定的值将应用于不带标签的电子邮件或附件。 可以通过为不带附件的电子邮件指定另一高级设置来优化此配置。

使用以下值之一创建高级客户端设置：

- 警告消息：
    
    - 密钥： **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 值：**警告**

- 对齐消息：
    
    - 密钥： **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 值：**两端对齐**

- 阻止邮件：
    
    - 密钥： **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 值： **Block**

- 关闭这些消息：
    
    - 密钥： **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 值： **Off**

如果未指定此客户端设置，则为 OutlookUnlabeledCollaborationAction 指定的值将用于没有附件的未标记电子邮件以及带有附件的未标记电子邮件。

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior="Warn"}
```

## <a name="disable-sending-audit-data-to-azure-information-protection-analytics"></a>禁止向 Azure 信息保护分析发送审核数据

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

Azure 信息保护统一标签客户端支持中心报表，并在默认情况下将其审核数据发送到[Azure 信息保护分析](../reports-aip.md)。 有关所发送和存储的信息的详细信息，请参阅中央报表文档中的[收集和发送到 Microsoft](../reports-aip.md#information-collected-and-sent-to-microsoft)部分的信息。

若要更改此行为，以便统一标签客户端不发送此信息，请为所选标签策略输入以下字符串：

- 密钥： **EnableAudit**

- 值：False****

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableAudit="False"}
```

## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>禁止将文档中发现的敏感信息发送到 Azure 信息保护分析

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

在 Office 应用中使用 Azure 信息保护统一标签客户端时，它会在首次保存文档时查找文档中的敏感信息。 **如果**提供[EnableAudit](#disable-sending-audit-data-to-azure-information-protection-analytics) advanced 设置，则不会将任何预定义和自定义的敏感信息类型都发送到[Azure 信息保护分析](../reports-aip.md)。

若要更改此行为，以便不发送统一标签客户端找到的敏感信息类型，请为所选标签策略输入以下字符串：

- 密钥： **RunAuditInformationTypesDiscovery**

- 值：False****

如果设置了此 "高级客户端" 设置，则仍然可以从客户端发送审核信息，但当用户访问标记内容时，该信息将被限制为报表。

例如：

- 使用此设置，可以看到用户访问了标记为 "**机密 \ 销售**" Financial.docx。

- 如果没有此设置，可以看到 Financial.docx 包含6个信用卡号。
    
    - 如果同时还启用[用于更深入分析的内容匹配](../reports-aip.md#content-matches-for-deeper-analysis)，那么，还能够查看具体的信用卡卡号。

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{RunAuditInformationTypesDiscovery="False"}
```

## <a name="send-information-type-matches-to-azure-information-protection-analytics"></a>向 Azure 信息保护分析发送信息类型匹配项
 
此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

默认情况下，统一标签客户端不会将敏感信息类型的内容匹配发送到[Azure 信息保护分析](../reports-aip.md)。 有关可以发送的其他信息的详细信息，请参阅中央报表文档中的 "[深入分析的内容匹配](../reports-aip.md#content-matches-for-deeper-analysis)" 部分。

若要在发送敏感信息类型时发送内容匹配项，请在标签策略中创建以下高级客户端设置： 

- 密钥： **LogMatchedContent**

- 值： **True**

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="True"}
```

## <a name="limit-cpu-consumption"></a>限制 CPU 消耗

从扫描程序版本 2.7. x 开始，我们建议使用以下**ScannerMaxCPU**和**ScannerMinCPU**高级设置方法限制 CPU 消耗。 

> [!IMPORTANT]
> 当使用以下线程限制策略时，将忽略**ScannerMaxCPU**和**ScannerMinCPU**高级设置。 若要使用**ScannerMaxCPU**和**ScannerMinCPU**高级设置限制 CPU 消耗，请取消使用限制线程数的策略。 

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

若要限制扫描仪计算机上的 CPU 使用率，可通过创建两个高级设置来管理： **ScannerMaxCPU**和**ScannerMinCPU**。 

默认情况下， **ScannerMaxCPU**设置为100，这意味着不存在最大 CPU 使用量的限制。 在这种情况下，扫描程序进程将尝试使用所有可用的 CPU 时间，以最大程度地提高扫描速率。

如果将**ScannerMaxCPU**设置为小于100，则 scanner 将在过去30分钟内监视 cpu 消耗，并且如果最大 cpu 超过你设置的限制，则将开始减少为新文件分配的线程数。 只要 CPU 消耗高于为**ScannerMaxCPU**设置的限制，线程数的限制就会继续。

**ScannerMinCPU**，仅当**ScannerMaxCPU**不等于100时才会检查。 不能将**ScannerMinCPU**设置为大于**ScannerMaxCPU**数字的数字。 建议将**ScannerMinCPU**设置为至少15个点低于**ScannerMaxCPU**的值。   

此设置的默认值为50，这意味着，如果在过去30分钟内 CPU 消耗低于此值，则 scanner 将开始添加新线程以并行扫描更多文件，直到 CPU 使用率达到为**ScannerMaxCPU**设置的级别。 

## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>限制扫描程序使用的线程数

> [!IMPORTANT]
> 当使用以下线程限制策略时，将忽略**ScannerMaxCPU**和**ScannerMinCPU**高级设置。 若要使用**ScannerMaxCPU**和**ScannerMinCPU**高级设置限制 CPU 消耗，请取消使用限制线程数的策略。 

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

默认情况下，扫描程序使用运行扫描程序服务的计算机上的所有可用处理器资源。 如果需要限制此服务扫描时的 CPU 消耗，请在标签策略中创建以下高级设置。 

对于该值，请指定扫描程序可以并行运行的并发线程数。 扫描程序为其扫描的每个文件使用单独的线程，因此此限制配置还定义了可以并行扫描的文件数。 

首次配置测试值时，建议为每个核心指定 2 个，然后监视结果。 例如，如果在具有 4 个核心的计算机上运行扫描程序，请先将值设置为 8。 如有必要，请根据扫描程序计算机所需的最终性能和扫描速率相应增减该数量。 

- 密钥： **ScannerConcurrencyLevel**

- 负值**\<number of concurrent threads>**

示例 PowerShell 命令，其中标签策略命名为 "Scanner"：

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{ScannerConcurrencyLevel="8"}
```

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>从 Secure Islands 和其他标记解决方案迁移标签

此配置使用 "标签[高级" 设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

此配置与文件扩展名为 ppdf 的受保护 PDF 文件不兼容。 不能使用文件资源管理器或 PowerShell 通过客户端打开这些文件。

对于标记为 "安全岛" 的 Office 文档，你可以使用你定义的映射通过敏感度标签重新标记这些文档。 此外，这种方法还可用于重用其他解决方案对 Office 文档标记的标签。 

此配置选项的结果是，Azure 信息保护统一标签客户端会应用新的敏感度标签，如下所示：

- 对于 Office 文档：在桌面应用中打开文档时，新的敏感度标签将显示为 "已设置"，并在保存文档时应用。

- 对于 PowerShell： [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)和[AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification)可以应用新的敏感度标签。

- 对于文件资源管理器：在 "Azure 信息保护" 对话框中，将显示新的敏感度标签，但并不设置。

此配置要求你为要映射到旧标签的每个敏感度标签指定一个名为**labelByCustomProperties**的高级设置。 然后，使用以下语法设置每个条目的值：

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

指定所选的迁移规则名称。 使用描述性名称可帮助您确定如何将以前标记的解决方案中的一个或多个标签映射到敏感度标签。

请注意，此设置不会从文档中删除原始标签，也不会删除可能已应用原始标签的文档中的任何视觉标记。 若要删除页眉和页脚，请参阅前面的部分[标记解决方案，删除页眉和页脚](#remove-headers-and-footers-from-other-labeling-solutions)。

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>示例 1：相同标签名称的一对一映射

要求：安全孤岛标签为 "机密" 的文档应由 Azure 信息保护重新标记为 "机密"。

在本示例中：

- Secure Islands 标签名为“Confidential”，存储在名为“Classification”的自定义属性中********。

高级设置：

- 密钥： **labelByCustomProperties**

- 值：**安全孤岛标签为机密、分类、机密**

示例 PowerShell 命令，其中的标签命名为 "机密"：

```ps
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}
```

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>示例 2：不同标签名称的一对一映射

要求：通过安全孤岛标记为 "敏感" 的文档应由 Azure 信息保护重新标记为 "高度机密"。

在本示例中：

- Secure Islands 标签名为“Sensitive”，存储在名为“Classification”的自定义属性中********。

高级设置：

- 密钥： **labelByCustomProperties**

- 值：**安全孤岛标签敏感、分类、敏感**

示例 PowerShell 命令，其中标签命名为 "高度机密"：

```ps
Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}
```

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>示例 3：标签名称的多对一映射

要求：你有两个安全孤岛标签，其中包含 "内部" 一词，并且你希望 Azure 信息保护统一标签客户端将具有这些安全孤岛标签的文档重新标记为 "常规"。

在本示例中：

- Secure Islands 标签包含单词“Internal”，存储在名为“Classification”的自定义属性中********。

高级客户端设置：

- 密钥： **labelByCustomProperties**

- 值：**安全孤岛标签包含内部、分类、。 \*内部。 \* **

示例 PowerShell 命令，其中标签命名为 "General"：

```ps
Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}
```

#### <a name="example-4-multiple-rules-for-the-same-label"></a>示例4：针对相同标签的多个规则

如果需要相同标签的多个规则，则为同一键定义多个字符串值。 

在此示例中，名为 "机密" 和 "机密" 的安全群岛标签存储在名为**分类**的自定义属性中，你希望 Azure 信息保护统一标签客户端应用名为 "机密" 的敏感度标签：

```ps
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}
```

### <a name="extend-your-label-migration-rules-to-emails"></a>将标签迁移规则扩展到电子邮件

除了通过指定其他标签策略高级设置以外，还可以将 labelByCustomProperties 高级设置与 Outlook 电子邮件一起使用。 但是，此设置对 Outlook 的性能有一个已知的负面影响，因此，仅当你对其具有强大的业务要求时才配置此附加设置，并记得在你完成从其他标记解决方案的迁移后将其设置为空字符串值。

若要配置此高级设置，请为所选标签策略输入以下字符串：

- 密钥： **EnableLabelByMailHeader**

- 值： **True**

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}
```

### <a name="extend-your-label-migration-rules-to-sharepoint-properties"></a>将标签迁移规则扩展到 SharePoint 属性

可以将 labelByCustomProperties 高级设置用于 SharePoint 属性，这些属性可能会作为列公开给用户。

使用 Word、Excel 和 PowerPoint 时，支持此设置。

若要配置此高级设置，请为所选标签策略输入以下字符串：

- 密钥： **EnableLabelBySharePointProperties**

- 值： **True**

示例 PowerShell 命令，其中标签策略命名为 "Global"：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelBySharePointProperties="True"}
```

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>应用标签时应用自定义属性

此配置使用 "标签[高级" 设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

在某些情况下，你可能需要将一个或多个自定义属性应用于文档或电子邮件消息，以及敏感标签应用的元数据。

例如：

- 正在[从另一个标记解决方案](#migrate-labels-from-secure-islands-and-other-labeling-solutions)（例如 Secure Islands）进行迁移。 为了在迁移过程中实现互操作性，您希望使用敏感性标签同时应用其他标签解决方案使用的自定义属性。

- 对于内容管理系统（例如 SharePoint 或其他供应商提供的文档管理解决方案），您希望对标签使用具有不同值的一致的自定义属性名称，并使用用户友好名称，而不是标记 GUID。

对于用户使用 Azure 信息保护统一标签客户端标记的 Office 文档和 Outlook 电子邮件，你可以添加一个或多个定义的自定义属性。 你还可以将此方法用于统一标签客户端，以便将自定义属性显示为来自其他解决方案的标签，这些解决方案尚未由统一的标签客户端标记。

由于此配置选项，Azure 信息保护统一标签客户端将应用任何其他自定义属性，如下所示：

- 对于 Office 文档：在桌面应用中标记文档时，在保存文档时应用附加的自定义属性。

- 对于 Outlook 电子邮件：当电子邮件标记为 Outlook 时，在发送电子邮件时，其他属性将应用于 x 标头。

- 对于 PowerShell： [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)和[AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification)在文档标记并保存时应用其他自定义属性。 如果未应用敏感性标签，则[get-aipfilestatus](/powershell/module/azureinformationprotection/get-aipfilestatus)会将自定义属性显示为映射的标签。

- 对于文件资源管理器：当用户右键单击文件并应用标签时，将应用自定义属性。

此配置要求你为要应用其他自定义属性的每个敏感度标签指定一个名为**customPropertiesByLabel**的高级设置。 然后，使用以下语法设置每个条目的值：

```sh
[custom property name],[custom property value]
```

> [!IMPORTANT]
> 使用字符串中的空格将阻止应用标签。

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>示例1：为标签添加单个自定义属性

要求： Azure 信息保护统一标签客户端标记为 "机密" 的文档应具有名为 "分类" 的附加自定义属性，其值为 "Secret"。

在本示例中：

- 敏感度标签命名为 "**机密**"，并创建名为 "Secret" 的自定义**属性，其**值为 "**机密**"。

高级设置：

- 密钥： **customPropertiesByLabel**

- 值：**分类、机密**

示例 PowerShell 命令，其中的标签命名为 "机密"：

```ps
    Set-Label -Identity Confidential -AdvancedSettings @{customPropertiesByLabel="Classification,Secret"}
```

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>示例2：为标签添加多个自定义属性

若要为同一个标签添加多个自定义属性，需要为同一键定义多个字符串值。

示例 PowerShell 命令：标签命名为 "常规"，并且你想要添加一个名为**分类**的自定义属性，其值为 "**常规**"，另一个名为 "**敏感度**" 的自定义属性的值为 "**内部**"：

```ps
Set-Label -Identity General -AdvancedSettings @{customPropertiesByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}
```

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>将标签配置为在 Outlook 中应用 S/MIME 保护

此配置使用必须使用 Office 365 Security & 相容性中心 PowerShell 配置的标签[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)。

仅当使用的是[S/MIME 部署](https://docs.microsoft.com/microsoft-365/security/office-365-security/s-mime-for-message-signing-and-encryption)并且需要标签以自动将此保护方法应用于电子邮件，而不是从 Azure 信息保护 Rights Management 保护时，才使用这些设置。 应用的保护与用户通过在 Outlook 中手动选择 S/MIME 选项应用的保护一样。

若要为 S/MIME 数字签名配置高级设置，请为所选标签输入以下字符串：

- 密钥： **SMimeSign**

- 值： **True**

若要配置 S/MIME 加密的高级设置，请为所选标签输入以下字符串：

- 密钥： **SMimeEncrypt**

- 值： **True**

如果你指定的标签配置为加密，则对于 Azure 信息保护统一标签客户端，S/MIME 保护仅替换 Outlook 中的 Rights Management 保护。 统一标签客户端的正式发行版将继续使用为管理中心的标签指定的加密设置。 对于带有内置标签的 Office 应用，这些功能不应用 S/MIME 保护，而是应用 "不转发" 保护。

如果希望标签仅在 Outlook 中可见，请将标签配置为仅将加密应用到**outlook 中的电子邮件**。

示例 PowerShell 命令，其中标签命名为 "仅收件人"：

```ps
Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}
```

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>为父标签指定默认子标签

此配置使用 "标签[高级" 设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

将子标签添加到标签时，用户将无法再对文档或电子邮件应用父标签。 默认情况下，用户选择父标签以查看他们可以应用的子标签，然后选择其中一个子标签。 如果配置此高级设置，当用户选择父标签时，系统会自动为其选择和应用子标签： 

- 密钥： **DefaultSubLabelId**

- 值：\<sublabel GUID>

示例 PowerShell 命令，其中的父标签命名为 "机密"，而 "所有 Employees" 子标签具有8faca7b8-8d20-48a3-8ea2-0f96310a848e 的 GUID：

```ps
Set-Label -Identity "Confidential" -AdvancedSettings @{DefaultSubLabelId="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}
```

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>开启在后台持续运行的分类

此配置使用 "标签[高级" 设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。 此设置处于预览状态，并且可能会更改。

当你配置此设置时，它会更改 Azure 信息保护统一标签客户端如何向文档应用自动和建议标签的默认行为：

对于 Word、Excel 和 PowerPoint，自动分类在后台持续运行。

此行为不会对 Outlook 变化。
当 Azure 信息保护统一标签客户端定期检查文档中指定的条件规则时，此行为将为存储在 SharePoint 中的文档启用自动和建议的分类和保护。 由于已运行条件规则，因此大型文件可实现更快保存。

条件规则不会作为用户类型实时运行。 而会在文档发生修改时作为后台任务定期运行。

若要配置此高级设置，请输入以下字符串：

- 键：RunPolicyInBackground****
- 值： **True**



示例 PowerShell 命令： 

```ps
Set-LabelPolicy -Identity PolicyName -AdvancedSettings @{RunPolicyInBackground = "true"}
```

## <a name="specify-a-color-for-the-label"></a>指定标签的颜色

此配置使用必须使用 Office 365 Security & 相容性中心 PowerShell 配置的标签[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)。

使用此高级设置设置标签的颜色。 若要指定颜色，请输入颜色的红色、绿色和蓝色（RGB）分量的十六进制三方代码。 例如，#40e0d0 为青绿色的 RGB 十六进制值。

如果需要这些代码的参考，可从 MSDN web 文档的页面找到一个有用的表格 [\<color>](https://developer.mozilla.org/docs/Web/CSS/color_value) 。你还可以在许多应用程序中找到这些代码，以便你编辑图片。 例如，通过 Microsoft 画图，从调色板中选择自定义颜色，系统将自动显示 RGB 值，该值可供复制。

若要配置标签颜色的高级设置，请为所选标签输入以下字符串：

- 键：**颜色**

- 值：\<RGB hex value>

示例 PowerShell 命令，其中标签命名为 "Public"：

```ps
Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}
```

## <a name="sign-in-as-a-different-user"></a>以其他用户身份登录

在生产环境中，当用户使用 Azure 信息保护统一标签客户端时，通常不需要以其他用户身份登录。 不过，作为管理员，你在测试阶段可能需要以其他用户身份登录。 

你可以使用 " **Microsoft Azure 信息保护**" 对话框来验证你当前登录的帐户：打开 Office 应用程序，然后在 "**主页**" 选项卡上，选择 "**敏感度**" 按钮，然后选择 "**帮助和反馈**"。 帐户名称会显示在“客户端状态”**** 部分中。

请确保还要检查所显示的登录帐户的域名。 很容易忽视的一点是，使用正确的帐户名登录，但域不正确。 使用错误帐户的症状包括未能下载标签，或者看不到所需的标签或行为。

以其他用户身份登录：

1. 导航到 %localappdata%\Microsoft\MSIP 并删除 TokenCache 文件********。

2. 重新启动任何打开的 Office 应用程序，并使用其他用户帐户登录。 如果在 Office 应用程序中看不到用于登录到 Azure 信息保护服务的提示，请返回**Microsoft Azure 信息保护**对话框，并从 "更新的**客户端状态**" 部分中选择 "**登录**"。

此外：

- 完成这些步骤后，如果 Azure 信息保护的统一标签客户端仍以旧帐户登录，请从 Internet Explorer 中删除所有 cookie，然后重复步骤1和2。

- 如果使用的是单一登录，必须在删除令牌文件后注销 Windows，再使用其他用户帐户登录。 然后，Azure 信息保护的统一标签客户端会使用当前登录的用户帐户自动进行身份验证。

- 此解决方案支持以同一租户中的其他用户身份登录。 不支持以不同租户中的其他用户身份登录。 若要使用多个租户测试 Azure 信息保护，请使用不同的计算机。

- 你可以使用 "**帮助和反馈**" 中的 "**重置设置**" 选项注销并删除 Office 365 Security & 相容性中心、Microsoft 365 安全中心或 Microsoft 365 相容性中心的当前已下载标签和策略设置。


## <a name="support-for-disconnected-computers"></a>对断开连接的计算机的支持

> [!IMPORTANT]
> 以下标签方案支持断开连接的计算机：文件资源管理器、PowerShell、Office 应用和扫描仪。

默认情况下，Azure 信息保护的统一标签客户端会自动尝试连接到 internet，以便从标记管理中心下载标签和标签策略设置： Office 365 Security & 相容中心、Microsoft 365 安全中心或 Microsoft 365 符合性中心。 如果计算机在一段时间内无法连接到 internet，则可以导出和复制为统一标签客户端手动管理策略的文件。

说明：

1. 在 Azure AD 中选择或创建一个用户帐户，你将使用该帐户下载要在断开连接的计算机上使用的标签和策略设置。

2. 作为此帐户的附加标签策略设置，禁用使用**EnableAudit**高级设置将[审核数据发送到 Azure 信息保护分析](#disable-sending-audit-data-to-azure-information-protection-analytics)。
    
    建议执行此步骤，因为如果断开连接的计算机进行了定期 internet 连接，则会将日志记录信息发送到包含步骤1中的用户名的 Azure 信息保护分析。 该用户帐户可能不同于在断开连接的计算机上使用的本地帐户。

3. 在具有 internet 连接的计算机上安装了具有统一标签的客户端并使用步骤1中的用户帐户登录后，下载标签和策略设置。

4. 在此计算机上，导出日志文件。
    
    例如，运行[AIPLogs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs) cmdlet，或使用客户端的 "[帮助和反馈](clientv2-admin-guide.md#installing-and-supporting-the-azure-information-protection-unified-labeling-client)" 对话框中的 "**导出日志**" 选项。 
    
    日志文件将作为单个压缩文件导出。

5.  打开压缩文件，然后从 POLICY.MSIP 文件夹中复制任何具有 .xml 文件扩展名的文件。

6. 将这些文件粘贴到断开连接的计算机上的 **%localappdata%\Microsoft\MSIP**文件夹中。

7. 如果你选择的用户帐户通常连接到 internet，请通过将**EnableAudit**值设置为**True**，再次启用发送审核数据。

请注意，如果此计算机上的用户从 "[帮助和反馈](clientv2-admin-guide.md#help-and-feedback-section)" 中选择 "**重置设置**" 选项，则此操作将删除策略文件并使客户端无法运行，直到您手动替换文件或客户端连接到 internet 并下载这些文件。

如果断开连接的计算机正在运行 Azure 信息保护扫描程序，则必须执行其他配置步骤。 有关详细信息，请参阅[限制：扫描仪服务器无法](../deploy-aip-scanner-prereqs.md#restriction-the-scanner-server-cannot-have-internet-connectivity)从扫描程序部署说明获得 internet 连接。

## <a name="change-the-local-logging-level"></a>更改本地日志记录级别

默认情况下，Azure 信息保护统一标签客户端会将客户端日志文件写入到 **%localappdata%\Microsoft\MSIP**文件夹。 这些文件供 Microsoft 支持部门用来排除故障。
 
若要更改这些文件的日志记录级别，请在注册表中找到以下值名称并将值数据设置为所需的日志记录级别：

**HKEY_CURRENT_USER \SOFTWARE\Microsoft\MSIP\LogLevel**

将日志记录级别设置为以下值之一：

- **关闭**：没有本地日志记录。

- **错误**：仅限错误。

- **警告**：错误和警告。

- **Info**：最小日志记录，不包括任何事件 id （扫描仪的默认设置）。

- **调试**：完整信息。

- **跟踪**：详细日志记录（客户端的默认设置）。

此注册表设置不会更改为[集中报告](../reports-aip.md)发送到 Azure 信息保护的信息。

## <a name="skip-or-ignore-files-during-scans-depending-on-file-attributes"></a>在扫描期间跳过或忽略文件，具体取决于文件属性

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

默认情况下，Azure 信息保护统一标签扫描程序会扫描所有相关文件。 但是，你可能想要定义要跳过的特定文件，例如用于已移动的存档文件或文件。 

使用**ScannerFSAttributesToSkip**高级设置，使扫描程序可以根据文件属性跳过特定文件。 在 "设置" 值中，列出将使文件在全部设置为**true**时要跳过的文件属性。 此文件属性列表使用和逻辑。

下面的示例 PowerShell 命令演示了如何将此高级设置用于名为 "Global" 的标签。

**跳过只读和存档的文件**

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_READONLY, FILE_ATTRIBUTE_ARCHIVE"}
```

**跳过只读或存档的文件**

若要使用或逻辑，请多次运行同一属性。 例如：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_READONLY"}
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_ARCHIVE"}
```

> [!TIP]
> 建议你考虑启用扫描程序以跳过具有以下属性的文件：
> * FILE_ATTRIBUTE_SYSTEM
> * FILE_ATTRIBUTE_HIDDEN
> * FILE_ATTRIBUTE_DEVICE
> * FILE_ATTRIBUTE_OFFLINE
> * FILE_ATTRIBUTE_RECALL_ON_DATA_ACCESS
> * FILE_ATTRIBUTE_RECALL_ON_OPEN
> * FILE_ATTRIBUTE_TEMPORARY

有关可在**ScannerFSAttributesToSkip**高级设置中定义的所有文件属性的列表，请参阅[Win32 file Attribute 常量](https://docs.microsoft.com/windows/win32/fileio/file-attribute-constants)

## <a name="preserve-ntfs-owners-during-labeling-public-preview"></a>在标记期间保留 NTFS 所有者（公共预览版）

此配置使用策略[高级设置](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，你必须使用 Office 365 Security & 相容性中心 PowerShell 进行配置。

默认情况下，"扫描仪"、"PowerShell" 和 "文件资源管理器扩展" 标签不会保留在标记之前定义的 NTFS 所有者。 

若要确保保留 NTFS 所有者值，请将所选标签策略的 " **UseCopyAndPreserveNTFSOwner**高级" 设置设置为 " **true** "。

> [!CAUTION]
> 仅当可以确保扫描程序与扫描存储库之间的低延迟、可靠网络连接时，才定义此高级设置。 自动标记过程中的网络故障可能会导致文件丢失。

示例 PowerShell 命令（如果标签策略命名为 "Global"）：

```ps
Set-LabelPolicy -Identity Global -AdvancedSettings @{ UseCopyAndPreserveNTFSOwner ="true"}
```

## <a name="next-steps"></a>后续步骤

自定义 Azure 信息保护统一标签客户端后，请参阅以下资源，了解支持此客户端所需的其他信息：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)
