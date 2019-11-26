---
title: Custom configurations - Azure Information Protection unified labeling client
description: Information about customizing the Azure Information Protection unified labeling client for Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v2client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1fcab238281326ff8e885f655a936392e1519eb1
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474375"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>Admin Guide: Custom configurations for the Azure Information Protection unified labeling client

>*Applies to: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions for: [Azure Information Protection unified labeling client for Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Use the following information for advanced configurations that you might need for specific scenarios or a subset of users when you manage the Azure Information Protection unified labeling client.

These settings require editing the registry or specifying advanced settings. The advanced settings use [Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps).

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>How to configure advanced settings for the client by using Office 365 Security & Compliance Center PowerShell

When you use Office 365 Security & Compliance Center PowerShell, you can configure advanced settings that support customizations for label policies and labels. 例如：

- The setting to display the Information Protection bar in Office apps is a ***label policy advanced setting***.
- The setting to specify a label color is a ***label advanced setting***.

In both cases, after you [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps), specify the *AdvancedSettings* parameter with the identity (name or GUID) of the policy or label, and specify key/value pairs in a [hash table](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables). 使用以下语法：

For a label policy setting, single string value:

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}

For label policy settings, multiple string values for the same key:

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

For a label setting, single string value:

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}

For label settings, multiple string values for the same key:

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

To remove an advanced setting, use the same syntax but specify a null string value.


#### <a name="examples-for-setting-advanced-settings"></a>Examples for setting advanced settings

Example 1: Set a label policy advanced setting for a single string value:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

Example 2: Set a label advanced setting for a single string value:

    Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}

Example 3: Set a label advanced setting for multiple string values:

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

Example 4: Remove a label policy advanced setting by specifying a null string value:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>Specifying the identity for the label policy or label

Specifying the label policy name for the PowerShell *Identity* parameter is straightforward because you see only one policy name in the admin center where you manage your label policies. However, for labels, you see both a **Name** and **Display name** in the admin centers. In some cases, the value for both will be the same but they can be different:

- **Name** is the original name of the label and it is unique across all your labels. If you change the name of your label after it is created, this value remains the same. For labels that have been migrated from Azure Information Protection, you might see the label ID of the label from the Azure portal.

- **Display name** is the name of the label that users see and it doesn't have to be unique across all your labels. For example, users see one **All Employees** sublabel for the **Confidential** label, and another **All Employees** sublabel for the **Highly Confidential** label. These sublabels both display the same name, but are not the same label and have different settings.

For configuring your label advanced settings, use the **Name** value. For example, to identify the label in the following picture, you would specify `-Identity "All Company"`:

![Use 'Name' rather than 'Display name' to identify a sensitivity label](../media/labelname_scc.png)

If you prefer to specify the label GUID, this value is not displayed in the admin center where you manage your labels. However, you can use the following Office 365 Security & Compliance Center PowerShell command to find this value:

    Get-Label | Format-Table -Property DisplayName, Name, Guid


#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>Order of precedence - how conflicting settings are resolved

Using one of the admin centers where you manage your sensitivity labels, you can configure the following label policy settings:

- **Apply this label by default to documents and emails**

- **Users must provide justification to remove a label or lower classification label**

- **Require users to apply a label to their email or document**

- **Provide users with a link to a custom help page**

When more than one label policy is configured for a user, each with potentially different policy settings, the last policy setting is applied according to the order of the policies in the admin center. For more information, see [Label policy priority (order matters)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#label-policy-priority-order-matters)

Label advanced settings follow the same logic for precedence: When a label is in multiple label policies and that label has advanced settings, the last advanced setting is applied according to the order of the policies in the admin center.

Label policy advanced settings are applied in the reverse order: With one exception, the advanced settings from the first policy are applied, according to the order of the policies in the admin center. The exception is the advanced setting *OutlookDefaultLabel*, which sets a different default label for Outlook. For this label policy advanced setting only, the last setting is applied according to the order of the policies in the admin center.

#### <a name="available-advanced-settings-for-label-policies"></a>Available advanced settings for label policies

Use the *AdvancedSettings* parameter with [New-LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-labelpolicy?view=exchange-ps) and [Set-LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-labelpolicy?view=exchange-ps).

|Setting|应用场景和说明|
|----------------|---------------|
|AttachmentAction|[对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|DisableMandatoryInOutlook|[Exempt Outlook messages from mandatory labeling](#exempt-outlook-messages-from-mandatory-labeling)
|EnableAudit|[Disable sending audit data to Azure Information Protection analytics](#disable-sending-audit-data-to-azure-information-protection-analytics)|
|EnableCustomPermissions|[Disable custom permissions in File Explorer](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|EnableLabelBySharePointProperties|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)
|HideBarByDefault|[在 Office 应用程序中显示“信息保护”栏](##display-the-information-protection-bar-in-office-apps)|
|LogMatchedContent|[Send information type matches to Azure Information Protection analytics](#send-information-type-matches-to-azure-information-protection-analytics)|
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
|PFileSupportedExtensions|[Change which file types to protect](#change-which-file-types-to-protect)|
|PostponeMandatoryBeforeSave|[使用强制标签时，删除文档的“以后再说”](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[删除其他标记解决方案中的页眉和页脚](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[为用户添加“报告问题”](#add-report-an-issue-for-users)|
|RunAuditInformationTypesDiscovery|[Disable sending discovered sensitive information in documents to Azure Information Protection analytics](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
|ScannerConcurrencyLevel|[限制扫描程序使用的线程数](#limit-the-number-of-threads-used-by-the-scanner)|

Example PowerShell command to check your label policy settings in effect for a label policy named "Global":

    (Get-LabelPolicy -Identity Global).settings

#### <a name="available-advanced-settings-for-labels"></a>Available advanced settings for labels

Use the *AdvancedSettings* parameter with [New-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps) and [Set-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

|Setting|应用场景和说明|
|----------------|---------------|
|color|[Specify a color for the label](#specify-a-color-for-the-label)|
|customPropertiesByLabel|[Apply a custom property when a label is applied](#apply-a-custom-property-when-a-label-is-applied)|
|DefaultSubLabelId|[Specify a default sublabel for a parent label](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|SMimeEncrypt|[将标签配置为在 Outlook 中应用 S/MIME 保护](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[将标签配置为在 Outlook 中应用 S/MIME 保护](#configure-a-label-to-apply-smime-protection-in-outlook)|

Example PowerShell command to check your label settings in effect for a label named "Public":

    (Get-Label -Identity Public).settings

## <a name="display-the-information-protection-bar-in-office-apps"></a>在 Office 应用中显示“信息保护”栏

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

By default, users must select the **Show Bar** option from the **Sensitivity** button to display the Information Protection bar in Office apps. Use the **HideBarByDefault** key and set the value to **False** to automatically display this bar for users so that they can select labels from either the bar or the button. 

For the selected label policy, specify the following strings:

- Key: **HideBarByDefault**

- 值：False

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>Exempt Outlook messages from mandatory labeling

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

By default, when you enable the label policy setting of **All documents and emails must have a label**, all saved documents and sent emails must have a label applied. When you configure the following advanced setting, the policy setting applies only to Office documents and not to Outlook messages.

For the selected label policy, specify the following strings:

- Key: **DisableMandatoryInOutlook**

- 值：True

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{DisableMandatoryInOutlook="True"}

## <a name="enable-recommended-classification-in-outlook"></a>在 Outlook 中启用建议的分类

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

为建议的分类配置标签时，系统将提示用户接受或关闭 Word、Excel 和 PowerPoint 中建议的标签。 此设置将此标签建议扩展到也在 Outlook 中显示。

For the selected label policy, specify the following strings:

- 键：OutlookRecommendationEnabled

- 值：True

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}

## <a name="set-a-different-default-label-for-outlook"></a>为 Outlook 设置不同的默认标签

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

When you configure this setting, Outlook doesn't apply the default label that is configured as a policy setting for the option **Apply this label by default to documents and emails**. 相反，Outlook 可应用不同的默认标签，也可不应用标签。

For the selected label policy, specify the following strings:

- 键：OutlookDefaultLabel

- Value: \<**label GUID**> or **None**

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}

## <a name="change-which-file-types-to-protect"></a>Change which file types to protect

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

By default, the Azure Information Protection unified labeling client protects all file types, and the scanner from the client protects only Office file types and PDF files.

You can change this default behavior for a selected label policy, by specifying the following:

- Key: **PFileSupportedExtensions**

- Value: **<string value>** 

Use the following table to identify the string value to specify:

| “字符串值”| 客户端| 扫描仪|
|-------------|-------|--------|
|\*|Default value: Apply protection to all file types|Apply protection to all file types|
|\<null value>| Apply protection to Office file types and PDF files| Default value: Apply protection to Office file types and PDF files|
|ConvertTo-Json(".jpg", ".png")|In addition to Office file types and PDF files, apply protection to the specified file name extensions | In addition to Office file types and PDF files, apply protection to the specified file name extensions

Example 1: PowerShell command for the unified client to protect only Office file types and PDF files, where your label policy is named "Client":

    Set-LabelPolicy -Identity Client -AdvancedSettings @{PFileSupportedExtensions=""}

Example 2:  PowerShell command for the scanner to protect all file types, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

Example 3: PowerShell command for the scanner to protect .txt files and .csv files in addition to Office files and PDF files, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".txt", ".csv")}

With this setting, you can change which file types are protected but you cannot change the default protection level from native to generic. For example, for users running the unified labeling client, you can change the default setting so that only Office files and PDF files are protected instead of all file types. But you cannot change these file types to be generically protected with a .pfile file name extension.

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>使用强制标签时，删除文档的“以后再说”

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

When you use the label policy setting of **All documents and emails must have a label**, users are prompted to select a label when they first save an Office document and when they send an email. 对于文档，用户可以选择“以后再说”暂时关闭提示以选择标签，并返回到文档。 但是不能在未选择标签的情况下关闭已保存的文档。 

在配置此设置时，将删除“以后再说”选项，以便首次保存文档时用户必须选择一个标签。

For the selected label policy, specify the following strings:

- 键：PostponeMandatoryBeforeSave

- 值：False

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>删除其他标记解决方案中的页眉和页脚

This configuration uses policy [advanced settings](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

借助这些设置，可以在其他标记解决方案已应用这些视觉标记的情况下，从文档中删除或替换基于文本的页眉或页脚。 For example, the old footer contains the name of an old label that you have now migrated to sensitivity labels to use a new label name and its own footer.

When the unified labeling client gets this configuration in its policy, the old headers and footers are removed or replaced when the document is opened in the Office app and any sensitivity label is applied to the document.

Outlook 不支持此配置，并且请注意，在 Word、Excel 和 PowerPoint 中使用它时，会对这些应用的性能产生负面影响。 该配置允许你根据应用程序来定义设置，例如，搜索 Word 文档页眉和页脚中的文本，而不是 Excel 电子表格或 PowerPoint 演示文稿中的。

Because the pattern matching affects the performance for users, we recommend that you limit the Office application types (**W**ord, E**X**cel, **P**owerPoint) to just those that need to be searched.

For the selected label policy, specify the following strings:

- 键：RemoveExternalContentMarkingInApp

- 值：\<Office 应用程序类型 WXP> 

例如：

- 若要仅搜索 Word 文档，请指定 W。

- 若要搜索 Word 文档和 PowerPoint 演示文稿，请指定 WP。

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}

然后需要至少一个高级客户端设置 ExternalContentMarkingToRemove，指定页眉或页脚的内容以及如何删除或替换它们。

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>如何配置 ExternalContentMarkingToRemove

指定 ExternalContentMarkingToRemove 键的字符串值时，拥有三个使用正则表达式的选项：

- 用以删除页眉或页脚中所有内容的部分匹配。
    
    示例：页眉或页脚包含字符串 TEXT TO REMOVE。 想要完全删除这些页面或页脚。 可指定值：`*TEXT*`。

- 用以删除页眉或页脚中特定字词的完全匹配。
    
    示例：页眉或页脚包含字符串 TEXT TO REMOVE。 只想删除单词 TEXT，结果使页眉或页脚字符串变为 TO REMOVE。 可指定值：`TEXT `。

- 用以删除页眉或页脚中所有内容的完全匹配。
    
    示例：页眉或页脚包含字符串 TEXT TO REMOVE。 想要删除其字符串为 TEXT TO REMOVE 的页眉或页脚。 可指定值：`^TEXT TO REMOVE$`。
    

指定的字符串的匹配模式不区分大小写。 最大字符串长度为 255 个字符。

因为某些文档可能包括不可见字符或者不同类型的空格或制表符，可能检测不到指定的短语或句子的字符串。 只要有可能，指定单个易区分的单词作为值，并确保在生产环境中部署之前测试结果。

For the same label policy, specify the following strings:

- 键：ExternalContentMarkingToRemove

- 值：\<要匹配的字符串，定义为正则表达式> 

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}

#### <a name="multiline-headers-or-footers"></a>多行页眉或页脚

如果页眉或页脚文本不只一行，则为每行创建一个键和值。 例如，下面是具有两行文本的页脚：

The file is classified as Confidential

Label applied manually

To remove this multiline footer, you create the following two entries for the same label policy:

- 键：ExternalContentMarkingToRemove

- 键值 1：\*Confidential*

- 键值 2： **\*Label applied*** 

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}


#### <a name="optimization-for-powerpoint"></a>针对 PowerPoint 的优化

PowerPoint 中的页脚以形状的形式实现。 若要避免删除那些你指定的但不属于页面或页脚的形状，可使用以下附加高级客户端设置：PowerPointShapeNameToRemove。 我们还建议使用此设置来避免检查所有形状中的文本，因为这将占用大量资源。

如果未指定这项附加的高级客户端设置，并且 PowerPoint 包括在 RemoveExternalContentMarkingInApp键值中，将对所有形状检查你在 ExternalContentMarkingToRemove 值中指定的文本。 

查找用作页眉或页脚的形状的名称：

1. 在 PowerPoint 中，显示“选择”窗格：“格式”选项卡 >“排列”组 >“选择”窗格。

2. 选择幻灯片上包含页眉或页脚的形状。 所选形状的名称现在突出显示在“选择”窗格中。

使用形状的名称为 PowerPointShapeNameToRemove 键指定一个字符串字。 

示例：形状名称是 fc。 若要删除具有此名称的形状，则指定值：`fc`。

- 键：PowerPointShapeNameToRemove

- 值：\<PowerPoint 形状名称> 

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}

When you have more than one PowerPoint shape to remove, specify as many values as you have shapes to remove.

默认情况下，只检查主幻灯片的页眉和页脚。 若要将检查范围扩展到所有幻灯片，将占用大量资源，则可以使用 RemoveExternalContentMarkingInAllSlides 附加高级客户端设置：

- 键：RemoveExternalContentMarkingInAllSlides

- 值：True

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}


## <a name="disable-custom-permissions-in-file-explorer"></a>Disable custom permissions in File Explorer

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

By default, users see an option named **Protect with custom permissions** when they right-click in File Explorer and choose **Classify and protect**. This option lets them set their own protection settings that can override any protection settings that you might have included with a label configuration. 用户还能看到一个用于删除保护的选项。 When you configure this setting, users do not see these options.

To configure this advanced setting, enter the following strings for the selected label policy:

- 键：EnableCustomPermissions

- 值：False

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

When you configure the advanced client setting to [disable custom permissions in File Explorer](#disable-custom-permissions-in-file-explorer), by default, users are not able to see or change custom permissions that are already set in a protected document.

However, there's another advanced client setting that you can specify so that in this scenario, users can see and change custom permissions for a protected document when they use File Explorer and right-click the file.

To configure this advanced setting, enter the following strings for the selected label policy:

- Key: **EnableCustomPermissionsForCustomProtectedFiles**

- 值：True

Example PowerShell command:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}


## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签

This configuration uses policy [advanced settings](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

This setting is for when users attach labeled documents to an email, and do not label the email message itself. In this scenario, a label is automatically selected for them, based on the classification labels that are applied to the attachments. The highest classification label is selected.

附件必须是物理文件，并且不能是指向文件的链接（例如，指向 SharePoint 或 OneDrive for Business 文件的链接）。

You can configure this setting to **Recommended**, so that users are prompted to apply the selected label to their email message, with a customizable tooltip. 用户可接受或忽略该建议。 Or, you can configure this setting to **Automatic**, where the selected label is automatically applied but users can remove the label or select a different label before sending the email.

Note: When the attachment with the highest classification label is configured for protection with the setting of user-defined permissions:

- When the label's user-defined permissions include Outlook (Do Not Forward), that label is selected and Do Not Forward protection is applied to the email.
- When the label's user-defined permissions are just for Word, Excel, PowerPoint, and File Explorer, that label is not applied to the email message, and neither is protection.

To configure this advanced setting, enter the following strings for the selected label policy:

- Key 1: **AttachmentAction**

- Key Value 1: **Recommended** or **Automatic**

- Key 2: **AttachmentActionTip**

- Key Value 2: "\<customized tooltip>"

The customized tooltip supports a single language only.

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}

## <a name="add-report-an-issue-for-users"></a>为用户添加“报告问题”

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

当指定以下高级客户端设置时，用户将看到一个“报告问题”选项，他们可以从“帮助和反馈”客户端对话框中选择该选项。 为链接指定 HTTP 字符串。 例如，为用户报告问题设置的自定义 Web 页面，或者发送给支持人员的电子邮件地址。 

To configure this advanced setting, enter the following strings for the selected label policy:

- 密钥：ReportAnIssueLink

- 值：\<HTTP string>

网站示例值：`https://support.contoso.com`

电子邮件地址示例值：`mailto:helpdesk@contoso.com`

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>在 Outlook 中实施弹出消息，警告、证明或阻止发送电子邮件

This configuration uses policy [advanced settings](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

当创建并配置以下高级客户端设置时，用户可以在 Outlook 中看到弹出消息，这些消息可以在发送电子邮件之前警告他们，或者要求他们提供发送电子邮件的理由，或者在存在以下任何一种情况时阻止他们发送电子邮件：

- **其电子邮件或电子邮件附件有一个特定的标签**：
    - 附件可以是任何文件类型

- **其电子邮件或电子邮件的附件没有标签**：
    - 附件可以是 Office 文档或 PDF 文档

When these conditions are met, the user sees a pop-up message with one of the following actions:

- **Warn**: The user can confirm and send, or cancel.

- **Justify**: The user is prompted for justification (predefined options or free-form).  然后，用户可以发送或取消电子邮件。 说明理由的文本被写入电子邮件 x - 标头，以便其他系统可以读取。 例如，数据丢失防护 (DLP) 服务。

- **Block**: The user is prevented from sending the email while the condition remains. 该消息包括阻止电子邮件的原因，以便用户可以解决问题。 例如，删除特定收件人或标记电子邮件。 

When the popup-messages are for a specific label, you can configure exceptions for recipients by domain name.

> [!TIP]
> See the video [Azure Information Protection Outlook Popup Configuration](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/) for a walkthrough example of how to configure these settings.

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>若要针对特定标签实现用于警告、验证或阻止的弹出消息：

For the selected policy, create one or more of the following advanced settings with the following keys. For the values, specify one or more labels by their GUIDs, each one separated by a comma.

Example value for multiple label GUIDs as a comma-separated string: `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- 警告消息：
    
    - Key: **OutlookWarnUntrustedCollaborationLabel**
    
    - Value: \<**label GUIDs, comma-separated**>

- 对齐消息：
    
    - Key: **OutlookJustifyUntrustedCollaborationLabel**
    
    - Value: \<**label GUIDs, comma-separated**>

- 阻止邮件：
    
    - Key: **OutlookBlockUntrustedCollaborationLabel**
    
    - Value: \<**label GUIDs, comma-separated**>


Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>To exempt domain names for pop-up messages configured for specific labels

For the labels that you've specified with these pop-up messages, you can exempt specific domain names so that users do not see the messages for recipients who have that domain name included in their email address. 在这种情况下，发送电子邮件时不会受消息干扰。 若要指定多个域，将其添加为单个字符串，以逗号分隔。

典型配置是仅针对组织外部的收件人或并非组织授权合作伙伴的收件人显示弹出消息。 在这种情况下，可以指定组织和合作伙伴使用的所有电子邮件域。

For the same label policy, create the following advanced client settings and for the value, specify one or more domains, each one separated by a comma.

多个域的示例值，以逗号分隔的字符串表示：`contoso.com,fabrikam.com,litware.com`

- 警告消息：
    
    - Key: **OutlookWarnTrustedDomains**
    
    - 值：\<域名，以逗号分隔>

- 对齐消息：
    
    - Key: **OutlookJustifyTrustedDomains**
    
    - 值：\<域名，以逗号分隔>

- 阻止邮件：
    
    - Key: **OutlookBlockTrustedDomains**
    
    - 值：\<域名，以逗号分隔>

For example, you have specified the **OutlookBlockUntrustedCollaborationLabel** advanced client setting for the **Confidential \ All Employees** label. You now specify the additional advanced client setting of **OutlookJustifyTrustedDomains** and **contoso.com**. As a result, a user can send an email to john@sales.contoso.com when it is labeled **Confidential \ All Employees** but will be blocked from sending an email with the same label to a Gmail account.

Example PowerShell commands, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>若要针对没有标签的电子邮件或附件实现用于警告、验证或阻止的弹出消息：

For the same label policy, create the following advanced client setting with one of the following values:

- 警告消息：
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Value: **Warn**

- 对齐消息：
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Value: **Justify**

- 阻止邮件：
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Value: **Block**

- 关闭这些消息：
    
    - Key: **OutlookUnlabeledCollaborationAction**
    
    - Value: **Off**


Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}


#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>To define specific file name extensions for the warn, justify, or block pop-up messages for email attachments that don't have a label

By default, the warn, justify, or block pop-up messages apply to all Office documents and PDF documents. You can refine this list by specifying which file name extensions should display the warn, justify, or block messages with an additional advanced setting and a comma-separated list of file name extensions.

Example value for multiple file name extensions to define as a comma-separated string: `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

In this example, an unlabeled PDF document will not result in warn, justify, or block pop-up messages.

For the same label policy, enter the following strings: 


- Key: **OutlookOverrideUnlabeledCollaborationExtensions**

- Value: **\<** file name extensions to display messages, comma separated **>**


Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>To specify a different action for email messages without attachments

By default, the value that you specify for OutlookUnlabeledCollaborationAction to warn, justify, or block pop-up messages applies to emails or attachments that don't have a label. You can refine this configuration by specifying another advanced setting for email messages that don't have attachments.

使用以下值之一创建高级客户端设置：

- 警告消息：
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Value: **Warn**

- 对齐消息：
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Value: **Justify**

- 阻止邮件：
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Value: **Block**

- 关闭这些消息：
    
    - Key: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Value: **Off**

If you don't specify this client setting, the value that you specify for OutlookUnlabeledCollaborationAction is used for unlabeled email messages without attachments as well as unlabeled email messages with attachments.

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior="Warn"}

## <a name="disable-sending-audit-data-to-azure-information-protection-analytics"></a>Disable sending audit data to Azure Information Protection analytics

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

The Azure Information Protection unified labeling client supports central reporting and by default, sends its audit data to [Azure Information Protection analytics](../reports-aip.md). For more information about what information is sent and stored, see the [Information collected and sent to Microsoft](../reports-aip.md#information-collected-and-sent-to-microsoft) section from the central reporting documentation.

To change this behavior so that this information is not sent by the unified labeling client, enter the following strings for the selected label policy:

- Key: **EnableAudit**

- 值：False

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableAudit="False"}


## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>Disable sending discovered sensitive information in documents to Azure Information Protection analytics

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

When the Azure Information Protection unified labeling client is used in Office apps, it looks for sensitive information in documents when they are first saved. Providing the [EnableAudit](#disable-sending-audit-data-to-azure-information-protection-analytics) advanced setting is not set to **False**, any predefined and custom sensitive information types found are then sent to [Azure Information Protection analytics](../reports-aip.md).

To change this behavior so that sensitive information types found by the unified labeling client are not sent, enter the following strings for the selected label policy:

- Key: **RunAuditInformationTypesDiscovery**

- 值：False

If you set this advanced client setting, auditing information can still be sent from the client, but the information is limited to reporting when a user has accessed labeled content.

例如：

- With this setting, you can see that a user accessed Financial.docx that is labeled **Confidential \ Sales**.

- Without this setting, you can see that Financial.docx contains 6 credit card numbers.
    
    - 如果同时还启用[用于更深入分析的内容匹配](../reports-aip.md#content-matches-for-deeper-analysis)，那么，还能够查看具体的信用卡卡号。

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RunAuditInformationTypesDiscovery="False"}

## <a name="send-information-type-matches-to-azure-information-protection-analytics"></a>Send information type matches to Azure Information Protection analytics
 
This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

By default, the unified labeling client does not send content matches for sensitive info types to [Azure Information Protection analytics](../reports-aip.md). For more information about this additional information that can be sent, see the [Content matches for deeper analysis](../reports-aip.md#content-matches-for-deeper-analysis) section from the central reporting documentation.

To send content matches when sensitive information types are sent, create the following advanced client setting in a label policy: 

- Key: **LogMatchedContent**

- 值：True

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="True"}

## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>限制扫描程序使用的线程数

This configuration uses a policy [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

默认情况下，扫描程序使用运行扫描程序服务的计算机上的所有可用处理器资源。 If you need to limit the CPU consumption while this service is scanning, create the following advanced setting in a label policy. 

对于该值，请指定扫描程序可以并行运行的并发线程数。 扫描程序为其扫描的每个文件使用单独的线程，因此此限制配置还定义了可以并行扫描的文件数。 

首次配置测试值时，建议为每个核心指定 2 个，然后监视结果。 例如，如果在具有 4 个核心的计算机上运行扫描程序，请先将值设置为 8。 如有必要，请根据扫描程序计算机所需的最终性能和扫描速率相应增减该数量。 

- Key: **ScannerConcurrencyLevel**

- 值： **\<并发线程数>**

Example PowerShell command, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{ScannerConcurrencyLevel="8"}


## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>从 Secure Islands 和其他标记解决方案迁移标签

This configuration uses a label [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

This configuration is not compatible with protected PDF files that have a .ppdf file name extension. These files cannot be opened by the client using File Explorer or PowerShell.

For Office documents that are labeled by Secure Islands, you can relabel these documents with a sensitivity label by using a mapping that you define. 此外，这种方法还可用于重用其他解决方案对 Office 文档标记的标签。 

As a result of this configuration option, the new sensitivity label is applied by the Azure Information Protection unified labeling client as follows:

- For Office documents: When the document is opened in the desktop app, the new sensitivity label is shown as set and is applied when the document is saved.

- For PowerShell: [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) and [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) can apply the new sensitivity label.

- For File Explorer: In the Azure Information Protection dialog box, the new sensitivity label is shown but isn't set.

This configuration requires you to specify an advanced setting named **labelByCustomProperties** for each sensitivity label that you want to map to the old label. 然后，使用以下语法设置每个条目的值：

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

指定所选的迁移规则名称。 Use a descriptive name that helps you to identify how one or more labels from your previous labeling solution should be mapped to sensitivity label.

请注意，此设置不会从文档中删除原始标签，也不会删除可能已应用原始标签的文档中的任何视觉标记。 To remove headers and footers, see the earlier section, [Remove headers and footers from other labeling solutions](#remove-headers-and-footers-from-other-labeling-solutions).

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>示例 1：相同标签名称的一对一映射

Requirement: Documents that have a Secure Islands label of "Confidential" should be relabeled as "Confidential" by Azure Information Protection.

在此示例中：

- Secure Islands 标签名为“Confidential”，存储在名为“Classification”的自定义属性中。

The advanced setting:

- Key: **labelByCustomProperties**

- Value: **Secure Islands label is Confidential,Classification,Confidential**

Example PowerShell command, where your label is named "Confidential":

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>示例 2：不同标签名称的一对一映射

Requirement: Documents labeled as "Sensitive" by Secure Islands should be relabeled as "Highly Confidential" by Azure Information Protection.

在此示例中：

- Secure Islands 标签名为“Sensitive”，存储在名为“Classification”的自定义属性中。

The advanced setting:

- Key: **labelByCustomProperties**

- Value: **Secure Islands label is Sensitive,Classification,Sensitive**

Example PowerShell command, where your label is named "Highly Confidential":

    Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>示例 3：标签名称的多对一映射

Requirement: You have two Secure Islands labels that include the word "Internal" and you want documents that have either of these Secure Islands labels to be relabeled as "General" by the Azure Information Protection unified labeling client.

在此示例中：

- Secure Islands 标签包含单词“Internal”，存储在名为“Classification”的自定义属性中。

高级客户端设置：

- Key: **labelByCustomProperties**

- Value: **Secure Islands label contains Internal,Classification,.\*Internal.\***

Example PowerShell command, where your label is named "General":

    Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}

#### <a name="example-4-multiple-rules-for-the-same-label"></a>Example 4: Multiple rules for the same label

When you need multiple rules for the same label, define multiple string values for the same key. 

In this example, the Secure Islands labels named "Confidential" and "Secret" are stored in the custom property named **Classification**, and you want the Azure Information Protection unified labeling client to apply the sensitivity label named "Confidential":

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

### <a name="extend-your-label-migration-rules-to-emails"></a>Extend your label migration rules to emails

You can use your labelByCustomProperties advanced settings with Outlook emails in addition to Office documents by specifying an additional label policy advanced setting. However, this setting has a known negative impact on the performance of Outlook, so configure this additional setting only when you have a strong business requirement for it and remember to set it to a null string value when you have completed the migration from the other labeling solution.

To configure this advanced setting, enter the following strings for the selected label policy:

- Key: **EnableLabelByMailHeader**

- 值：True

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}

### <a name="extend-your-label-migration-rules-to-sharepoint-properties"></a>Extend your label migration rules to SharePoint properties

You can use your labelByCustomProperties advanced settings with SharePoint properties that you might expose as columns to users.

This setting is supported when you use Word, Excel, and PowerPoint.

To configure this advanced setting, enter the following strings for the selected label policy:

- Key: **EnableLabelBySharePointProperties**

- 值：True

Example PowerShell command, where your label policy is named "Global":

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelBySharePointProperties="True"}

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>Apply a custom property when a label is applied

This configuration uses a label [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

There might be some scenarios when you want to apply one or more custom properties to a document or email message in addition to the metadata that's applied by a sensitivity label.

例如：

- You are in the process of [migrating from another labeling solution](#migrate-labels-from-secure-islands-and-other-labeling-solutions), such as Secure Islands. For interoperability during the migration, you want sensitivity labels to also apply a custom property that is used by the other labeling solution.

- For your content management system (such as SharePoint or a document management solution from another vendor) you want to use a consistent custom property name with different values for the labels, and with user-friendly names instead of the label GUID.

For Office documents and Outlook emails that users label by using the Azure Information Protection unified labeling client, you can add one or more custom properties that you define. You can also use this method for the unified labeling client to display a custom property as a label from other solutions for content that isn't yet labeled by the unified labeling client.

As a result of this configuration option, any additional custom properties are applied by the Azure Information Protection unified labeling client as follows:

- For Office documents: When the document is labeled in the desktop app, the additional custom properties are applied when the document is saved.

- For Outlook emails: When the email message is labeled in Outlook, the additional properties are applied to the x-header when the email is sent.

- For PowerShell: [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) and [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) applies the additional custom properties when the document is labeled and saved. [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) displays custom properties as the mapped label if a sensitivity label isn't applied.

- For File Explorer: When the user right-clicks the file and applies the label, the custom properties are applied.

This configuration requires you to specify an advanced setting named **customPropertiesByLabel** for each sensitivity label that you want to apply the additional custom properties. 然后，使用以下语法设置每个条目的值：

`[custom property name],[custom property value]`

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>Example 1: Add a single custom property for a label

Requirement: Documents that are labeled as "Confidential" by the Azure Information Protection unified labeling client should have the additional custom property named "Classification" with the value of "Secret".

在此示例中：

- The sensitivity label is named **Confidential** and creates a custom property named **Classification** with the value of **Secret**.

The advanced setting:

- Key: **customPropertiesByLabel**

- Value: **Classification,Secret**

Example PowerShell command, where your label is named "Confidential":

    Set-Label -Identity Confidential -AdvancedSettings @{customPropertiesByLabel="Classification,Secret"}

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>Example 2: Add multiple custom properties for a label

To add more than one custom property for the same label, you need to define multiple string values for the same key.

Example PowerShell command, where your label is named "General" and you want to add one custom property named **Classification** with the value of **General** and a second custom property named **Sensitivity** with the value of **Internal**:

    Set-Label -Identity General -AdvancedSettings @{customPropertiesByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>将标签配置为在 Outlook 中应用 S/MIME 保护

This configuration uses label [advanced settings](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

Use these settings only when you have a working [S/MIME deployment](https://docs.microsoft.com/microsoft-365/security/office-365-security/s-mime-for-message-signing-and-encryption) and want a label to automatically apply this protection method for emails rather than Rights Management protection from Azure Information Protection. 应用的保护与用户通过在 Outlook 中手动选择 S/MIME 选项应用的保护一样。

To configure an advanced setting for an S/MIME digital signature, enter the following strings for the selected label:

- Key: **SMimeSign**

- 值：True

To configure an advanced setting for  S/MIME encryption, enter the following strings for the selected label:

- Key: **SMimeEncrypt**

- 值：True

If the label you specify is configured for encryption, for the Azure Information Protection unified labeling client, S/MIME protection replaces the Rights Management protection only in Outlook. The general availability version of the unified labeling client continues to use the encryption settings specified for the label in the admin center. For Office apps with built-in labeling, these do not apply the S/MIME protection but instead, apply Do Not Forward protection.

If you want the label to be visible in Outlook only, configure the label to apply encryption to **Only email messages in Outlook**.

Example PowerShell commands, where your label is named "Recipients Only":

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>Specify a default sublabel for a parent label

This configuration uses a label [advanced setting](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

When you add a sublabel to a label, users can no longer apply the parent label to a document or email. By default, users select the parent label to see the sublabels that they can apply, and then select one of those sublabels. If you configure this advanced setting, when users select the parent label, a sublabel is automatically selected and applied for them: 

- Key: **DefaultSubLabelId**

- Value: \<sublabel GUID>

Example PowerShell command, where your parent label is named "Confidential" and the "All Employees" sublabel has a GUID of 8faca7b8-8d20-48a3-8ea2-0f96310a848e:

    Set-Label -Identity "Confidential" -AdvancedSettings @{DefaultSubLabelId="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}


## <a name="specify-a-color-for-the-label"></a>Specify a color for the label

This configuration uses label [advanced settings](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) that you must configure by using Office 365 Security & Compliance Center PowerShell.

Use this advanced setting to set a color for a label. To specify the color, enter a hex triplet code for the red, green, and blue (RGB) components of the color. For example, #40e0d0 is the RGB hex value for turquoise.

If you need a reference for these codes, you'll find a helpful table from the [\<color>](https://developer.mozilla.org/docs/Web/CSS/color_value) page from the MSDN web docs. You also find these codes in many applications that let you edit pictures. 例如，通过 Microsoft 画图，从调色板中选择自定义颜色，系统将自动显示 RGB 值，该值可供复制。

To configure the advanced setting for a label's color, enter the following strings for the selected label:

- Key: **color**

- Value: \<RGB hex value>

Example PowerShell command, where your label is named "Public":

    Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}

## <a name="sign-in-as-a-different-user"></a>以其他用户身份登录

In a production environment, users wouldn't usually need to sign in as a different user when they are using the Azure Information Protection unified labeling client. 不过，作为管理员，你在测试阶段可能需要以其他用户身份登录。 

You can verify which account you're currently signed in as by using the **Microsoft Azure Information Protection** dialog box: Open an Office application and on the **Home** tab, select the **Sensitivity** button, and then select **Help and feedback**. 帐户名称会显示在“客户端状态”部分中。

请确保还要检查所显示的登录帐户的域名。 很容易忽视的一点是，使用正确的帐户名登录，但域不正确。 A symptom of using the wrong account includes failing to download the labels, or not seeing the labels or behavior that you expect.

以其他用户身份登录：

1. 导航到 %localappdata%\Microsoft\MSIP 并删除 TokenCache 文件。

2. 重新启动任何打开的 Office 应用程序，并使用其他用户帐户登录。 If you do not see a prompt in your Office application to sign in to the Azure Information Protection service, return to the **Microsoft Azure Information Protection** dialog box and select **Sign in** from the updated **Client status** section.

另外：

- If the Azure Information Protection unified labeling client is still signed in with the old account after completing these steps, delete all cookies from Internet Explorer, and then repeat steps 1 and 2.

- 如果使用的是单一登录，必须在删除令牌文件后注销 Windows，再使用其他用户帐户登录。 The Azure Information Protection unified labeling client then automatically authenticates by using your currently signed in user account.

- 此解决方案支持以同一租户中的其他用户身份登录。 不支持以不同租户中的其他用户身份登录。 若要使用多个租户测试 Azure 信息保护，请使用不同的计算机。

- You can use the **Reset settings** option from **Help and Feedback** to sign out and delete the currently downloaded labels and policy settings from the Office 365 Security & Compliance Center, the Microsoft 365 Security center, or the Microsoft 365 Compliance center.


## <a name="support-for-disconnected-computers"></a>对断开连接的计算机的支持

> [!IMPORTANT]
> Disconnected computers are supported for the following labeling scenarios only: File Explorer, PowerShell, and the scanner. To label documents in your Office apps, you must have connectivity to the internet.

By default, the Azure Information Protection unified labeling client automatically tries to connect to the internet to download the labels and label policy settings from your labeling management center: The Office 365 Security & Compliance Center, the Microsoft 365 security center, or the Microsoft 365 compliance center. If you have computers that cannot connect to the internet for a period of time, you can export and copy files that manually manages the policy for the unified labeling client.

Instructions:

1. Choose or create a user account in Azure AD that you will use to download labels and policy settings that you want to use on your disconnected computer.

2. As an additional label policy setting for this account, [disable sending audit data to Azure Information Protection analytics](#disable-sending-audit-data-to-azure-information-protection-analytics) by using the **EnableAudit** advanced setting.
    
    We recommend this step because if the disconnected computer does have periodic internet connectivity, it will send logging information to Azure Information Protection analytics that includes the user name from step 1. That user account might be different from the local account you're using on the disconnected computer.

3. From a computer with internet connectivity that has the unified labeling client installed and signed in with the user account from step 1, download the labels and policy settings.

4. From this computer, export the log files.
    
    For example, run the [Export-AIPLogs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs) cmdlet, or use the **Export Logs** option from the client's [Help and Feedback](clientv2-admin-guide.md#installing-and-supporting-the-azure-information-protection-unified-labeling-client) dialog box. 
    
    The log files are exported as a single compressed file.

5.  Open the compressed file, and from the MSIP folder, copy any files that have a .xml file name extension.

6. Paste these files into the **%localappdata%\Microsoft\MSIP** folder on the disconnected computer.

7. If your chosen user account is one that usually connects to the internet, enable sending audit data again, by setting the **EnableAudit** value to **True**.

8. For the disconnected computer to protect files, reprotect files, remove protection from files, or to inspect protected files: On the disconnected computer, run the [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) cmdlet with the *DelegatedUser* parameter and specify the user account from step 1 to set the user context. 例如：
    
        Set-AIPAuthentication -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser offlineuser@contoso.com

Be aware that if a user on this computer selects the **Reset Settings** option from [Help and feedback](clientv2-admin-guide.md#help-and-feedback-section), this action deletes the policy files and renders the client inoperable until you manually replace the files or the client connects to the internet and downloads the files.

If your disconnected computer is running the Azure Information Protection scanner, there are additional configuration steps you must take. For more information, see [Restriction: The scanner server cannot have internet connectivity](../deploy-aip-scanner.md#restriction-the-scanner-server-cannot-have-internet-connectivity) from the scanner deployment instructions.

## <a name="change-the-local-logging-level"></a>更改本地日志记录级别

By default, the Azure Information Protection unified labeling client writes client log files to the **%localappdata%\Microsoft\MSIP** folder. 这些文件供 Microsoft 支持部门用来排除故障。
 
To change the logging level for these files, locate the following value name in the registry and set the value data to the required logging level:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

将日志记录级别设置为以下值之一：

- **Off**: No local logging.

- **Error**: Errors only.

- **Warn**: Errors and warnings.

- **Info**: Minimum logging, which includes no event IDs (the default setting for the scanner).

- **Debug**: Full information.

- **Trace**: Detailed logging (the default setting for clients).

This registry setting does not change the information that's sent to Azure Information Protection for [central reporting](../reports-aip.md).

## <a name="next-steps"></a>后续步骤
Now that you've customized the Azure Information Protection unified labeling client, see the following resources for additional information that you might need to support this client:

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)
