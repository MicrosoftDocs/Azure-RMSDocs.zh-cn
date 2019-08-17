---
title: 自定义配置-Azure 信息保护客户端
description: 有关自定义适用于 Windows 的 Azure 信息保护客户端的信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v1client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e2cce9e76ae1b583aacc30df7d2abe5940106455
ms.sourcegitcommit: bdfade60c1939f5c540bbf82859af060eb629f68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546069"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>管理员指南：Azure 信息保护客户端的自定义配置

>适用对象：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

请参阅以下高级配置相关信息，在管理 Azure 信息保护客户端时，可能需要用于特定方案或一部分用户。

其中一些设置需要编辑注册表，一些使用的是高级设置，必须先在 Azure 门户中进行配置，再发布以供客户端下载。  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>在门户中配置高级客户端配置设置的具体步骤

1. 如果尚未这样做，请在新的浏览器窗口中[登录到 Azure 门户](../configure-policy.md#signing-in-to-the-azure-portal)，然后导航到“Azure 信息保护”边栏选项卡。

2. 从“分类” > “标签”菜单选项中：选择“策略”。

3. 在“Azure 信息保护 - 策略”边栏选项卡中，选择此策略旁边的上下文菜单 (...)，以添加高级设置。 再选择“高级设置”。
    
    可以为全局策略和作用域内策略配置高级设置。

4. 在“高级设置”边栏选项卡中，键入高级设置名称和值，再选择“保存并关闭”。

5. 确保此策略的用户重启打开过的任何 Office 应用程序。

6. 如果不再需要此设置，并希望还原为默认行为：在“高级设置”边栏选项卡中，选择不再需要的设置旁边的上下文菜单 (...)，再选择“删除”。 然后单击“保存并关闭”。

#### <a name="available-advanced-client-settings"></a>可用高级客户端设置

|Setting|应用场景和说明|
|----------------|---------------|
|DisableDNF|[在 Outlook 中隐藏或显示“不转发”按钮](#hide-or-show-the-do-not-forward-button-in-outlook)|
|DisableMandatoryInOutlook|[使 Outlook 邮件免于强制标记](#exempt-outlook-messages-from-mandatory-labeling)|
|CompareSubLabelsInAttachmentAction|[启用子标签的排序支持](#enable-order-support-for-sublabels-on-attachments) 
|ContentExtractionTimeout|[更改扫描程序的超时设置](#change-the-timeout-settings-for-the-scanner)
|EnableBarHiding|[永久隐藏 Azure 信息保护栏](#permanently-hide-the-azure-information-protection-bar)|
|EnableCustomPermissions|[设置用户是否能够使用自定义权限选项](#make-the-custom-permissions-options-available-or-unavailable-to-users)|
|EnableCustomPermissionsForCustomProtectedFiles|[对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnablePDFv2Protection|[不使用 PDF 加密 ISO 标准来保护 PDF 文件](#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)|
|FileProcessingTimeout|[更改扫描程序的超时设置](#change-the-timeout-settings-for-the-scanner)
|LabelbyCustomProperty|[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|LabelToSMIME|[将标签配置为在 Outlook 中应用 S/MIME 保护](#configure-a-label-to-apply-smime-protection-in-outlook)|
|LogLevel|[更改本地日志记录级别](#change-the-local-logging-level)
|LogMatchedContent|[禁止为一部分用户发送信息类型匹配项](#disable-sending-information-type-matches-for-a-subset-of-users)|
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
|PostponeMandatoryBeforeSave|[使用强制标签时，删除文档的“以后再说”](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|ProcessUsingLowIntegrity|[禁用扫描程序的低完整性级别](#disable-the-low-integrity-level-for-the-scanner)|
|PullPolicy|[对已断开连接计算机的支持](#support-for-disconnected-computers)
|RemoveExternalContentMarkingInApp|[删除其他标记解决方案中的页眉和页脚](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[为用户添加“报告问题”](#add-report-an-issue-for-users)|
|RunAuditInformationTypesDiscovery|[禁止将文档中发现的敏感信息发送到 Azure 信息保护分析](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
|RunPolicyInBackground|[开启在后台持续运行的分类](#turn-on-classification-to-run-continuously-in-the-background)|
|ScannerConcurrencyLevel|[限制扫描程序使用的线程数](#limit-the-number-of-threads-used-by-the-scanner)|
|SyncPropertyName|[使用现有自定义属性标记 Office 文档](#label-an-office-document-by-using-an-existing-custom-property)|
|SyncPropertyState|[使用现有自定义属性标记 Office 文档](#label-an-office-document-by-using-an-existing-custom-property)|

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>阻止针对仅 AD RMS 计算机出现的登录提示

默认情况下，Azure 信息保护客户端会自动尝试连接到 Azure 信息保护服务。 对于只与 AD RMS 通信的计算机，此配置可能导致不必要的用户登录提示。 可以通过编辑注册表来阻止此登录提示。

 - 找到以下值名称，然后将值数据设置为“0”：
    
    **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

无论此设置如何，Azure 信息保护客户端仍遵循标准的 [RMS 服务发现流程](client-deployment-notes.md#rms-service-discovery)来查找它的 AD RMS 群集。

## <a name="sign-in-as-a-different-user"></a>以其他用户身份登录

在生产环境中，如果用户使用的是 Azure 信息保护客户端，则通常不需要以其他用户身份登录。 不过，作为管理员，你在测试阶段可能需要以其他用户身份登录。 

可以使用“MicrosoftAzure 信息保护”对话框验证当前登录的帐户：打开 Office 应用程序，在“**主页**”选项卡的“**保护**”组中单击“**保护**”，然后单击“**帮助和反馈**”。 帐户名称会显示在“客户端状态”部分中。

请确保还要检查所显示的登录帐户的域名。 很容易忽视的一点是，使用正确的帐户名登录，但域不正确。 使用错误帐户的症状是，无法下载 Azure 信息保护策略，或看不到预期的标签或行为。

以其他用户身份登录：

1. 导航到 %localappdata%\Microsoft\MSIP 并删除 TokenCache 文件。

2. 重新启动任何打开的 Office 应用程序，并使用其他用户帐户登录。 如果在 Office 应用程序中没有看到登录到 Azure 信息保护服务的提示，请返回“Microsoft Azure信息保护”对话框，然后从更新的“客户端状态”部分中单击“登录”。

此外：

- 完成这些步骤后，若 Azure 信息保护客户端仍使用旧帐户登录，则从 Internet Explorer 删除所有 cookie，然后重复步骤 1 和步骤 2。

- 如果使用的是单一登录，必须在删除令牌文件后注销 Windows，再使用其他用户帐户登录。 然后，Azure 信息保护客户端会使用当前登录的用户帐户，自动进行身份验证。

- 此解决方案支持以同一租户中的其他用户身份登录。 不支持以不同租户中的其他用户身份登录。 若要使用多个租户测试 Azure 信息保护，请使用不同的计算机。

- 可以使用“帮助和反馈”中的“重置设置”选项注销并删除当前已下载的 Azure 信息保护策略。


## <a name="enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses"></a>如果组织拥有组合许可证，则强制执行仅保护模式

如果组织不具有任何 Azure 信息保护许可证，但有包含用于数据保护的 Azure Rights Management 服务的 Office 365 许可证，则用于 Windows 的 Azure 信息保护客户端会自动在[仅保护模式](client-protection-only-mode.md)下运行。

但是，如果贵组织已订阅 Azure 信息保护，默认情况下所有 Windows 计算机都可以下载 Azure 信息保护策略。 Azure 信息保护客户端不会进行许可证检查以及强制执行。 

如果某些用户没有 Azure 信息保护许可证，但拥有包含 Azure 权限管理服务的 Office 365 许可证，请在这些用户的计算机上编辑注册表，以防止用户在 Azure 信息保护中运行未经授权的分类和标签功能。

找到以下值名称并将值数据设置为 **0**：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

此外，请确保这些计算机的 %LocalAppData%\Microsoft\MSIP 文件夹中不具有名为 Policy.msip 的文件。 如果此文件存在，请将其删除。 此文件包含 Azure 信息保护策略，并且可能在编辑注册表之前已下载，如果使用演示选项安装了 Azure 信息保护客户端，那么也可能已下载此文件。

## <a name="add-report-an-issue-for-users"></a>为用户添加“报告问题”

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

当指定以下高级客户端设置时，用户将看到一个“报告问题”选项，他们可以从“帮助和反馈”客户端对话框中选择该选项。 为链接指定 HTTP 字符串。 例如，为用户报告问题设置的自定义 Web 页面，或者发送给支持人员的电子邮件地址。 

若要配置此高级设置，请输入以下字符串：

- 键:**ReportAnIssueLink**

- 值： **\<HTTP string>**

网站示例值：`https://support.contoso.com`

电子邮件地址示例值：`mailto:helpdesk@contoso.com`

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>隐藏 Windows 文件资源管理器中的“分类和保护”菜单选项

创建以下 DWORD 值名称（以及任何数值数据）：

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>对断开连接的计算机的支持

默认情况下，Azure 信息保护客户端会自动尝试连接到 Azure 信息保护服务，以下载最新的 Azure 信息保护策略。 如果知道有计算机在一段时间内无法连接到 Internet，可以编辑注册表，以阻止客户端尝试连接到服务。 

请注意，在没有 Internet 连接的情况下，客户端无法使用组织的基于云的密钥来应用保护（或删除保护）。 相反，客户端只能使用应用分类或 [HYOK](../configure-adrms-restrictions.md) 保护的标签。

若要阻止 Azure 信息保护服务登录提示，可使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)，然后为计算机下载策略。 或者，也可以通过编辑注册表来阻止此登录提示。

- 若要配置高级客户端设置，请执行以下操作：
    
    1. 输入以下字符串：
    
        - 键:**PullPolicy**
        
        - 值：**False**
    
    2. 下载包含此设置的策略，并按照随附的说明操作，将它安装在计算机上。

- 或者，若要编辑注册表，请执行以下操作：
    
    - 找到以下值名称，然后将值数据设置为“0”：
    
        **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 


客户端必须在 %LocalAppData%\Microsoft\MSIP 文件夹中有名为 Policy.msip 的有效策略文件。

可以从 Azure 门户中导出全局策略或范围内策略，并将导出的文件复制到客户端计算机。 此外，还可以使用此方法，将已过时的策略文件替换为最新策略。 不过，如果用户属于多个范围内策略，就不支持导出策略。 另请注意，如果用户选择[“帮助和反馈”](client-admin-guide.md#help-and-feedback-section)中的“重置设置”选项，此操作会删除策略文件，并导致客户端无法正常运行，直到你手动替换策略文件或客户端连接到服务并下载策略为止。

从 Azure 门户导出策略时，下载的压缩文件包含多个版本的策略。 这些策略版本对应于 Azure 信息保护客户端的不同版本：

1. 解压缩文件，然后使用下表来确定所需要的策略文件。 
    
    |文件名|相应的客户端版本|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |版本 1.2|
    |Policy1.2.msip |版本 1.3 - 1.7|
    |Policy1.3.msip |版本 1.8 - 1.29|
    |Policy1.4.msip |版本 1.32 及更高版本|
    
2. 将已标识的文件重命名为 Policy.msip，再将它复制到已安装 Azure 信息保护客户端的计算机上的 %LocalAppData%\Microsoft\MSIP 文件夹。 

如果断开连接的计算机运行的是当前的 Azure 信息保护扫描程序 GA 版本, 则需要执行其他配置步骤。 有关详细信息，请参阅扫描程序部署说明中的[限制：扫描程序服务器不能连接到 Internet](../deploy-aip-scanner.md#restriction-the-scanner-server-cannot-have-internet-connectivity)。

## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>在 Outlook 中隐藏或显示“不转发”按钮

建议使用“向 Outlook 功能区添加‘不转发’按钮”这一[策略设置](../configure-policy-settings.md)来配置此选项。 但是，也可以使用在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)来配置此选项。

配置此设置后，将在 Outlook 功能区中隐藏或显示“不转发”按钮。 此设置对 Office 菜单中的“不转发”选项没有影响。

若要配置此高级设置，请输入以下字符串：

- 键:**DisableDNF**

- 值：如果为 True 将隐藏按钮，如果为 False 将显示按钮

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>设置用户是否能够使用自定义权限选项

建议使用“设置用户是否能够使用自定义权限选项”这一[策略设置](../configure-policy-settings.md)来配置此选项。 但是，也可以使用在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)来配置此选项。 

配置此设置并为用户发布策略后，用户可看到自定义权限选项，它们可用于自行选择保护设置；这些选项也可能隐藏，使得用户无法自行选择保护设置（除非系统出现提示）。

若要配置此高级设置，请输入以下字符串：

- 键:**EnableCustomPermissions**

- 值：结果为 True 将使自定义权限选项可用，结果为 False 将隐藏此选项

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 此设置处于预览状态，并且可能会更改。

配置[策略设置](../configure-policy-settings.md)时，为用户或上一部分中的同等高级客户端设置提供自定义权限选项，用户无法查看或更改已在受保护文档中设置的自定义权限。 

创建和配置此高级客户端设置时，用户可以在使用文件资源管理器时查看和更改受保护文档的自定义权限，然后右键单击该文件。 Office 功能区上的“保护”按钮中的“自定义权限”选项仍处于隐藏状态。

若要配置此高级设置，请输入以下字符串：

- 键:**EnableCustomPermissionsForCustomProtectedFiles**

- 值：**True**

## <a name="permanently-hide-the-azure-information-protection-bar"></a>永久隐藏 Azure 信息保护栏

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 仅当“在 Office 应用中显示信息保护栏”这一项[策略设置](../configure-policy-settings.md)设置为“开”时，才使用此配置。

默认情况下，如果用户清除“主页”选项卡、“保护”组、“保护”按钮中的“显示数据条”选项，则信息保护栏将不再显示在该 Office 应用中。 但是，下次打开 Office 应用时，会自动再次显示该栏。

若要防止在用户选择隐藏该栏后再次自动显示该栏，请使用此客户端设置。 如果用户使用“关闭信息保护栏”图标关闭此栏，此设置将不起作用。

即使 Azure 信息保护栏保持隐藏，如果已配置了推荐分类，或者文档或电子邮件必须有标签，用户仍可以从临时显示的栏中选择标签。 

若要配置此高级设置，请输入以下字符串：

- 键:**EnableBarHiding**

- 值：**True**

## <a name="enable-order-support-for-sublabels-on-attachments"></a>启用附件子标签的排序支持

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

如果具有子标签并已配置以下[策略设置](../configure-policy-settings.md)，请使用此设置：

- **对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签**

配置以下字符串：

- 键:**CompareSubLabelsInAttachmentAction**

- 值：**True**

如果不进行此设置，则从具有最高分类的父标签找到的第一个标签将应用于电子邮件。 

如果进行此设置，则具有最高分类的父标签中排在最后的子标签将应用于电子邮件。 如果需要对标签重新排序，以便为此方案应用所需的标签，请参阅[如何删除或重排 Azure 信息保护的标签](../configure-policy-delete-reorder.md)。

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>使 Outlook 邮件免于强制标记

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

默认情况下, 当你启用 "**所有文档和电子邮件都必须具有标签**" 的[策略设置](../configure-policy-settings.md)时, 所有已保存的文档和已发送的电子邮件都必须应用标签。 配置以下高级设置时, 策略设置仅适用于 Office 文档, 而不适用于 Outlook 邮件。

若要配置此高级设置，请输入以下字符串：

- 键:**DisableMandatoryInOutlook**

- 值：**True**

## <a name="enable-recommended-classification-in-outlook"></a>在 Outlook 中启用建议的分类

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 此设置处于预览状态，并且可能会更改。

为建议的分类配置标签时，系统将提示用户接受或关闭 Word、Excel 和 PowerPoint 中建议的标签。 此设置将此标签建议扩展到也在 Outlook 中显示。

若要配置此高级设置，请输入以下字符串：

- 键:**OutlookRecommendationEnabled**

- 值：**True**


## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>在 Outlook 中实施弹出消息，警告、证明或阻止发送电子邮件

此配置使用必须在 Azure 门户中配置的多项[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

当创建并配置以下高级客户端设置时，用户可以在 Outlook 中看到弹出消息，这些消息可以在发送电子邮件之前警告他们，或者要求他们提供发送电子邮件的理由，或者在存在以下任何一种情况时阻止他们发送电子邮件：

- **其电子邮件或电子邮件附件有一个特定的标签**：
    - 附件可以是任何文件类型

- **其电子邮件或电子邮件的附件没有标签**：
    - 附件可以是 Office 文档或 PDF 文档

满足这些条件时, 用户将看到一个弹出消息, 其中包含以下操作之一:

- **警告**：用户可以确认、发送或取消。

- **验证**：提示用户说明理由（预定义选项或自由格式）。  然后，用户可以发送或取消电子邮件。 说明理由的文本被写入电子邮件 x - 标头，以便其他系统可以读取。 例如，数据丢失防护 (DLP) 服务。

- **阻止**：如果上述情况持续，将阻止用户发送电子邮件。 该消息包括阻止电子邮件的原因，以便用户可以解决问题。 例如，删除特定收件人或标记电子邮件。 

当弹出消息用于特定标签时, 可以按域名为收件人配置例外。

弹出消息中生成的操作将记录到本地 Windows 事件日志**应用程序和服务日志** > 中。

- 警告消息：信息 ID 301

- 验证消息：信息 ID 302

- 阻止邮件：信息 ID 303

来自验证消息的事件条目示例：

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Price list.msg
Item Name: Price list
Process Name: OUTLOOK
Action: Justify
User Justification: My manager approved sharing of this content
Action Source: 
User Response: Confirmed
```
以下各节包含每个高级客户端设置的配置说明, 你可以通过[教程查看这些配置说明:使用 Outlook](../infoprotect-oversharing-tutorial.md)配置 Azure 信息保护以控制 oversharing 的信息。

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>若要针对特定标签实现用于警告、验证或阻止的弹出消息：

若要针对特定标签实现弹出消息，必须知道这些标签的标签 ID。 在 Azure 门户中查看或配置 Azure 信息保护策略时，标签 ID 值将显示在“标签”边栏选项卡上。 对于应用了标签的文件，还可运行 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell cmdlet 标识标签 ID（MainLabelId 或 SubLabelId）。 当标签包含子标签时，请始终指定子标签（而非父标签）的 ID。

使用以下键创建以下一个或多个高级客户端设置。 对于值，请按 ID 指定一个或多个标签，每个标签用逗号分隔。

多个标签 ID 的示例值，采用以逗号分隔的字符串形式：`dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- 警告消息：
    
    - 键:**OutlookWarnUntrustedCollaborationLabel**
    
    - 值：\<标签 ID，以逗号分隔>

- 对齐消息：
    
    - 键:**OutlookJustifyUntrustedCollaborationLabel**
    
    - 值：\<标签 ID，以逗号分隔>

- 阻止邮件：
    
    - 键:**OutlookBlockUntrustedCollaborationLabel**
    
    - 值：\<标签 ID，以逗号分隔>

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>为特定标签配置的弹出消息免除域名

对于在这些弹出消息中指定的标签, 可以免除特定域名, 使用户不会看到其电子邮件地址中包含该域名的收件人的邮件。 在这种情况下，发送电子邮件时不会受消息干扰。 若要指定多个域，将其添加为单个字符串，以逗号分隔。

典型配置是仅针对组织外部的收件人或并非组织授权合作伙伴的收件人显示弹出消息。 在这种情况下，可以指定组织和合作伙伴使用的所有电子邮件域。

创建以下高级客户端设置, 为该值指定一个或多个域, 每个域都由逗号分隔。

多个域的示例值，以逗号分隔的字符串表示：`contoso.com,fabrikam.com,litware.com`

- 警告消息：
    
    - 键:**OutlookWarnTrustedDomains**
    
    - 值：\<域名，以逗号分隔>

- 对齐消息：
    
    - 键:**OutlookJustifyTrustedDomains**
    
    - 值：\<域名，以逗号分隔>

- 阻止邮件：
    
    - 键:**OutlookBlockTrustedDomains**
    
    - 值：\<域名，以逗号分隔>

例如, 你为 "**机密 \ 所有员工**" 标签指定了**OutlookBlockUntrustedCollaborationLabel** advanced client 设置。 你现在可以指定**OutlookBlockTrustedDomains**和**contoso.com**的其他高级客户端设置。 因此, 用户可以john@sales.contoso.com在将其标记为 "**机密 \ 所有员工**" 时向其发送电子邮件, 但会阻止向 Gmail 帐户发送具有相同标签的电子邮件。

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>若要针对没有标签的电子邮件或附件实现用于警告、验证或阻止的弹出消息：

使用以下值之一创建高级客户端设置：

- 警告消息：
    
    - 键:**OutlookUnlabeledCollaborationAction**
    
    - 值：**警告**

- 对齐消息：
    
    - 键:**OutlookUnlabeledCollaborationAction**
    
    - 值：**两端对齐**

- 阻止邮件：
    
    - 键:**OutlookUnlabeledCollaborationAction**
    
    - 值：**阻止**

- 关闭这些消息：
    
    - 键:**OutlookUnlabeledCollaborationAction**
    
    - 值：**Off**

#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>为不带标签的电子邮件附件定义 "警告"、"对齐" 或 "阻止" 弹出消息的特定文件扩展名

默认情况下, "警告"、"对齐" 或 "阻止" 弹出消息适用于所有 Office 文档和 PDF 文档。 您可以通过指定哪些文件扩展名应显示警告、调整或阻止具有其他高级客户端属性的消息和以逗号分隔的文件扩展名列表, 来优化此列表。

要定义为逗号分隔字符串的多个文件扩展名的示例值:`.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

在此示例中, 未标记的 PDF 文档不会导致警告、对齐或阻止弹出消息。


- 键:**OutlookOverrideUnlabeledCollaborationExtensions**

- 值： **\<** 文件扩展名以显示消息，以逗号分隔 **>**

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>为不带附件的电子邮件指定其他操作

默认情况下, 你为 OutlookUnlabeledCollaborationAction 指定的值将应用于不带标签的电子邮件或附件。 可以通过为不带附件的电子邮件指定另一高级客户端设置来优化此配置。

使用以下值之一创建高级客户端设置：

- 警告消息：
    
    - 键:**OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 值：**警告**

- 对齐消息：
    
    - 键:**OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 值：**两端对齐**

- 阻止邮件：
    
    - 键:**OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 值：**阻止**

- 关闭这些消息：
    
    - 键:**OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 值：**Off**

如果未指定此客户端设置, 则为 OutlookUnlabeledCollaborationAction 指定的值将用于没有附件的未标记电子邮件以及带有附件的未标记电子邮件。


## <a name="set-a-different-default-label-for-outlook"></a>为 Outlook 设置不同的默认标签

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

配置此设置时，Outlook 不会应用 Azure 信息保护策略中为“选择默认标签”设置配置的默认标签。 相反，Outlook 可应用不同的默认标签，也可不应用标签。

要应用不同的标签，必须指定标签 ID。 在 Azure 门户中查看或配置 Azure 信息保护策略时，标签 ID 值将显示在“标签”边栏选项卡上。 对于应用了标签的文件，还可运行 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell cmdlet 标识标签 ID（MainLabelId 或 SubLabelId）。 当标签包含子标签时，请始终指定子标签（而非父标签）的 ID。

因此 Outlook 不会应用默认标签，请指定“无”。

若要配置此高级设置，请输入以下字符串：

- 键:**OutlookDefaultLabel**

- 值：\<label ID> 或 None

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>将标签配置为在 Outlook 中应用 S/MIME 保护

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

仅当具有有效的 [S/MIME 部署](https://docs.microsoft.com/office365/SecurityCompliance/s-mime-for-message-signing-and-encryption)，且希望标签自动对电子邮件应用此保护方法（而不是 Azure 信息保护中的权限管理保护）时，才使用此设置。 应用的保护与用户通过在 Outlook 中手动选择 S/MIME 选项应用的保护一样。

若要使用此配置，必须为要应用 S/MIME 保护的所有 Azure 信息保护标签都指定“LabelToSMIME”高级客户端设置。 然后，使用以下语法设置每个条目的值：

`[Azure Information Protection label ID];[S/MIME action]`

在 Azure 门户中查看或配置 Azure 信息保护策略时，标签 ID 值将显示在“标签”边栏选项卡上。 若要使用包含子标签的 S/MIME，请始终仅指定子标签（而非父标签）的 ID。 指定子标签时，父标签必须位于同一范围内，或位于全局策略中。

S/MIME 操作可以是：

- `Sign;Encrypt`：应用数字签名和 S/MIME 加密

- `Encrypt`：仅应用 S/MIME 加密

- `Sign`：仅应用数字签名

dcf781ba-727f-4860-b3c1-73479e31912b 的标签 ID 示例值：

- 应用数字签名和 S/MIME 加密：
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign;Encrypt**

- 仅应用 S/MIME 加密：
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Encrypt**
    
- 仅应用数字签名：
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign**

使用此配置的结果是，当你对电子邮件应用标签后，除了标签中的分类，系统还会对电子邮件应用 S/MIME 保护。

如果你在 Azure 门户中为指定的标签配置了权限管理保护，S/MIME 保护仅在 Outlook 中替换权限管理保护。 对于支持标记的其他所有情况，应用的都是权限管理保护。

如果希望标签仅在 Outlook 中可见，请将标签配置为应用“不要转发”的单一用户定义操作，如[快速入门：为用户配置标签以便轻松保护包含敏感信息的电子邮件](../quickstart-label-dnf-protectedemail.md)中所述。

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>使用强制标签时，删除文档的“以后再说”

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

在使用“所有文档和电子邮件都必须有一个标签”的[策略设置](../configure-policy-settings.md)时，当用户首次保存 Office 文档和发送电子邮件，系统会提示选择标签。 对于文档，用户可以选择“以后再说”暂时关闭提示以选择标签，并返回到文档。 但是不能在未选择标签的情况下关闭已保存的文档。 

在配置此设置时，将删除“以后再说”选项，以便首次保存文档时用户必须选择一个标签。

若要配置此高级设置，请输入以下字符串：

- 键:**PostponeMandatoryBeforeSave**

- 值：**False**

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>开启在后台持续运行的分类

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 此设置处于预览状态，并且可能会更改。

在你配置此设置时，它更改 Azure 信息保护客户端向文档应用自动和建议标签的[默认行为](../configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied)： 

- 对于 Word、Excel 和 PowerPoint，自动分类在后台持续运行。  

此行为不会对 Outlook 变化。

如果 Azure 信息保护客户端定期检查你指定的条件规则文档，此行为将为存储在 SharePoint Online 中的文档启用自动和建议的分类以及保护。 由于已运行条件规则，因此大型文件可实现更快保存。 

条件规则不会作为用户类型实时运行。 而会在文档发生修改时作为后台任务定期运行。

若要配置此高级设置，请输入以下字符串：

- 键:**RunPolicyInBackground**

- 值：**True**

## <a name="dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption"></a>不使用 PDF 加密 ISO 标准来保护 PDF 文件

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

当 Azure 信息保护客户端的最新版本保护 PDF 文件时，生成的文件扩展名仍为 .pdf 并遵守 PDF 加密 ISO 标准。 有关此标准的详细信息，请参阅[派生自 ISO 32000-1 的文档](https://www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/PDF32000_2008.pdf)（由 Adobe Systems Incorporated 发布）中的第 7.6 节加密。

如果需要客户端还原为使用 .ppdf 文件扩展名保护 PDF 文件的早期客户端版本行为，请通过输入以下字符串来使用以下高级设置：

- 键:**EnablePDFv2Protection**

- 值：**False**

例如，如果使用不支持 PDF 加密 ISO 标准的 PDF 阅读器，则可能需要为所有用户配置此设置。 或者，在逐步采用支持新格式的 PDF 阅读器中的更改时，可能需要为部分用户配置此设置。 如果需要向已签名的 PDF 文档添加保护，则也可能使用此设置。 已签名的 PDF 文档可能受到 .ppdf 格式的额外保护，因此该保护是作为文件的包装器实现的。 

要使 Azure 信息保护扫描程序使用新设置，必须重启扫描程序服务。 此外，在默认情况下，扫描程序将不再保护 PDF 文档。 如果想要 PDF 文档在 EnablePDFv2Protection 设置为 False 时受扫描程序保护，则必须[编辑注册表](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner)。

有关新 PDF 加密的详细信息，请参阅博客文章[使用 Microsoft 信息保护进行 PDF 加密的新支持](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757)。

有关支持用于 PDF 加密的 ISO 标准的 PDF 阅读器以及支持旧格式的阅读器的列表，请参阅[用于 Microsoft 信息保护的受支持的 PDF 阅读器](protected-pdf-readers.md)。

### <a name="to-convert-existing-ppdf-files-to-protected-pdf-files"></a>将现有的 .ppdf 文件转换为受保护的 .pdf 文件

Azure 信息保护客户端已下载包含该新设置的客户端策略时，可以使用 PowerShell 命令将现有的 .ppdf 文件转换为使用 PDF 加密 ISO 标准的受保护 .pdf 文件。 

用户必须具有从文件删除保护的[权限管理使用权限](../configure-usage-rights.md)或者成为超级用户，才能将以下说明用于自己未保护的文件。 若要启用超级用户功能并将帐户配置为超级用户，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../configure-super-users.md)。

此外，当将这些说明用于自己未保护的文件时，则会成为 [RMS 颁发者](../configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)。 在此情况下，最初保护该文档的用户无法再跟踪和撤销它。 如果用户需要跟踪和撤销自己受保护的 PDF 文档，他们可以手动删除，然后通过使用文件资源管理器并右击，重新应用此标签。

使用 PowerShell 命令将现有的 .ppdf 文件转换为使用 PDF 加密 ISO 标准的受保护 .pdf 文件：

1. 将 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) 用于 .ppdf 文件。 例如：
    
        Get-AIPFileStatus -Path \\Finance\Projectx\sales.ppdf

2. 从输出中记录以下参数值：
    
   - SubLabelId 的值（(GUID)，如果有）。 如果此值为空，表明未使用子标签，则改为记录 MainLabelId 的值。
    
     注意:如果也不存在 MainLabelId 的值，则未标记此文件。 在此情况下，可以使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) 命令和 [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) 命令来代替步骤 3 和步骤 4 中的命令。
    
   - RMSTemplateId 的值。 如果此值为“受限访问”，则用户已使用自定义权限保护该文件，而非为此标签配置的保护设置。 若继续，该标签的保护设置将覆盖这些自定义权限。 决定是继续，还是要求用户（RMSIssuer 的显示值）删除此标签并将此标签和初始自定义权限一起重新应用。

3. 使用 [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) 和 *RemoveLabel* 参数删除此标签。 如果使用的是包含“用户必须提供理由以设置较低分类标签、删除标签或删除保护”的[策略设置](../configure-policy-settings.md)，还必须使用原因指定“理由”参数。 例如： 
    
        Set-AIPFileLabel \\Finance\Projectx\sales.ppdf -RemoveLabel -JustificationMessage 'Removing .ppdf protection to replace with .pdf ISO standard'

4. 为在步骤 1 中标识的标签指定值，重新应用初始标签。 例如：
    
        Set-AIPFileLabel \\Finance\Projectx\sales.pdf -LabelId d9f23ae3-1234-1234-1234-f515f824c57b

文件保留了 .pdf 文件扩展名，但它的分类与之前相同，并且通过使用 PDF 加密 ISO 标准对它进行保护。

## <a name="support-for-files-protected-by-secure-islands"></a>支持受 Secure Islands 保护的文件

此配置选项处于预览阶段, 可能会发生更改。

如果使用 Secure Islands 保护文档，可能因这种保护产生受保护的文本和图片文件以及通常受保护的文件。 例如，文件扩展名为 .ptxt、.pjpeg 或 .pfile 的文件。 按如下方式编辑注册表时，Azure 信息保护可以解密这些文件：


将以下 EnableIQPFormats 的 DWORD 值添加到以下注册表路径，并将值数据设置为 1：

- 64 位版本的 Windows：HKEY_LOCAL_MACHINE\\SOFTWARE\\WOW6432Node\\Microsoft\\MSIP

- 32 位版本的 Windows：HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\MSIP

对注册表进行此编辑后，即支持以下方案：

- Azure 信息保护查看器可打开这些受保护的文件。

- Azure 信息保护扫描程序可以检查这些文件中的敏感信息。

- 文件资源管理器、PowerShell 和 Azure 信息保护扫描程序可以标记这些文件。 因此，可以应用 Azure 信息保护标签来应用来自 Azure 信息保护的新保护，或删除来自 Secure Islands 的现有保护。

- 可使用[标签迁移客户端自定义](#migrate-labels-from-secure-islands-and-other-labeling-solutions)将这些受保护文件上的 Secure Islands 标签自动转换为 Azure 信息保护标签。

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>从 Secure Islands 和其他标记解决方案迁移标签

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

当前此配置与使用 PDF 加密 ISO 标准来保护 PDF 文件的新默认行为不兼容。 在这种情况下，无法通过文件资源管理器、PowerShell 或扫描程序打开 .ppdf 文件。 若要解决此问题，请使用高级客户端设置而[不使用 PDF 加密的 ISO 标准](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)。

对于 Secure Islands 标记的 Office 文档和 PDF 文档，可以使用所定义的映射，利用 Azure 信息保护标签重新标记这些文档。 此外，这种方法还可用于重用其他解决方案对 Office 文档标记的标签。 

> [!NOTE]
> 如果除 PDF 和 Office 文档外，还有其他受 Secure Islands 保护的文件，则可在编辑注册表后重新标记这些文件，如[前面部分](#support-for-files-protected-by-secure-islands)中所述。 

由于有此配置选项，Azure 信息保护客户端按如下所述应用新 Azure 信息保护标签：

- 对于 Office 文档：当文档在桌面应用程序中打开时，新 Azure 信息保护标签显示为已设置，并在文档保存时应用。

- 对于文件资源管理器：在“Azure 信息保护”对话框中，新 Azure 信息保护标签显示为已设置，并在用户选择“应用”时应用。 如果用户选择“取消”，新标签就不会应用。

- 对于 PowerShell：[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) 应用新 Azure 信息保护标签。 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) 不会显示新 Azure 信息保护标签，除非标签由另一种方法设置。

- 对于 Azure 信息保护扫描程序：发现功能可报告何时会设置新 Azure 信息保护标签，此标签可以通过强制模式进行应用。

若要执行此配置，必须为要映射到旧标签的所有 Azure 信息保护标签都指定“LabelbyCustomProperty”高级客户端设置。 然后，使用以下语法设置每个条目的值：

`[Azure Information Protection label ID],[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

在 Azure 门户中查看或配置 Azure 信息保护策略时，标签 ID 值将显示在“标签”边栏选项卡上。 若要指定子标签，父标签必须位于同一范围中，或位于全局策略中。

指定所选的迁移规则名称。 请使用描述性名称，这有助于确定应如何将旧标记解决方案中的一个或多个标签映射到 Azure 信息保护标签。 此名称显示在扫描程序报告和事件查看器中。 请注意，此设置不会从文档中删除原始标签，也不会删除可能已应用原始标签的文档中的任何视觉标记。 若要删除页眉和页脚，请参阅下一部分[删除其他标记解决方案中的页眉和页脚](#remove-headers-and-footers-from-other-labeling-solutions)。

### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>示例 1：相同标签名称的一对一映射

要求：对于 Secure Islands 标记为“机密”的文档，应由 Azure 信息保护重新标记为“机密”。

在此示例中：

- 要使用的 Azure 信息保护标签名为“Confidential”，标签 ID 为“1ace2cc3-14bc-4142-9125-bf946a70542c”。 

- Secure Islands 标签名为“Confidential”，存储在名为“Classification”的自定义属性中。

高级客户端设置：

    
|名称|值|
|---------------------|---------|
|LabelbyCustomProperty|1ace2cc3-14bc-4142-9125-bf946a70542c,"Secure Islands label is Confidential",Classification,Confidential|

### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>示例 2：不同标签名称的一对一映射

要求：对于 Secure Islands 标记为“敏感”的文档，应由 Azure 信息保护重新标记为“高度机密”。

在此示例中：

- 要使用的 Azure 信息保护标签名为“Highly Confidential”，标签 ID为“3e9df74d-3168-48af-8b11-037e3021813f”。

- Secure Islands 标签名为“Sensitive”，存储在名为“Classification”的自定义属性中。

高级客户端设置：

    
|名称|值|
|---------------------|---------|
|LabelbyCustomProperty|3e9df74d-3168-48af-8b11-037e3021813f,"Secure Islands label is Sensitive",Classification,Sensitive|


### <a name="example-3-many-to-one-mapping-of-label-names"></a>示例 3：标签名称的多对一映射

要求：有两个 Secure Islands 标签均包含“内部”一词，并且希望 Azure 信息保护将标有这两个 Secure Islands 标签之一的文档重新标记为“常规”。

在此示例中：

- 要使用的 Azure 信息保护标签名为“General”，标签 ID为“2beb8fe7-8293-444c-9768-7fdc6f75014d”。

- Secure Islands 标签包含单词“Internal”，存储在名为“Classification”的自定义属性中。

高级客户端设置：

    
|名称|值|
|---------------------|---------|
|LabelbyCustomProperty|2beb8fe7-8293-444c-9768-7fdc6f75014d,"Secure Islands label contains Internal",Classification,.\*Internal.\*|


## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>删除其他标记解决方案中的页眉和页脚

此配置使用必须在 Azure 门户中配置的多项[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 这些设置处于预览状态，并且可能会更改。

借助这些设置，可以在其他标记解决方案已应用这些视觉标记的情况下，从文档中删除或替换基于文本的页眉或页脚。 例如，旧页脚包含旧标签的名称，现在使用新的标签名及其自己的页脚将标签迁移到 Azure 信息保护。

当客户端在其策略中获取此配置时，如果文档在 Office 应用中打开并且任何 Azure 信息保护标签已应用到该文档，则删除或替换旧的页眉和页脚。

Outlook 不支持此配置，并且请注意，在 Word、Excel 和 PowerPoint 中使用它时，会对这些应用的性能产生负面影响。 该配置允许你根据应用程序来定义设置，例如，搜索 Word 文档页眉和页脚中的文本，而不是 Excel 电子表格或 PowerPoint 演示文稿中的。

由于该模式匹配会影响用户的性能，建议你将 Office 应用程序类型（Word、Excel、PowerPoint）限制为仅需要在其中进行搜索的那些类型：

- 键:**RemoveExternalContentMarkingInApp**

- 值：\<Office 应用程序类型 WXP> 

例如：

- 若要仅搜索 Word 文档，请指定 W。

- 若要搜索 Word 文档和 PowerPoint 演示文稿，请指定 WP。

然后需要至少一个高级客户端设置 ExternalContentMarkingToRemove，指定页眉或页脚的内容以及如何删除或替换它们。

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>如何配置 ExternalContentMarkingToRemove

指定 ExternalContentMarkingToRemove 键的字符串值时，拥有三个使用正则表达式的选项：

- 用以删除页眉或页脚中所有内容的部分匹配。
    
    例如：页眉或页脚包含字符串 TEXT TO REMOVE。 想要完全删除这些页面或页脚。 可指定值：`*TEXT*`。

- 用以删除页眉或页脚中特定字词的完全匹配。
    
    例如：页眉或页脚包含字符串 TEXT TO REMOVE。 只想删除单词 TEXT，结果使页眉或页脚字符串变为 TO REMOVE。 可指定值：`TEXT `。

- 用以删除页眉或页脚中所有内容的完全匹配。
    
    例如：页眉或页脚具有字符串 TEXT TO REMOVE。 想要删除其字符串为 TEXT TO REMOVE 的页眉或页脚。 可指定值：`^TEXT TO REMOVE$`。
    

指定的字符串的匹配模式不区分大小写。 最大字符串长度为 255 个字符。

因为某些文档可能包括不可见字符或者不同类型的空格或制表符，可能检测不到指定的短语或句子的字符串。 只要有可能，指定单个易区分的单词作为值，并确保在生产环境中部署之前测试结果。

- 键:**ExternalContentMarkingToRemove**

- 值：\<要匹配的字符串，定义为正则表达式> 

#### <a name="multiline-headers-or-footers"></a>多行页眉或页脚

如果页眉或页脚文本不只一行，则为每行创建一个键和值。 例如，下面是具有两行文本的页脚：

The file is classified as Confidential

Label applied manually

若要删除这个多行页脚，可以创建以下两个条目：

- 键 1：**ExternalContentMarkingToRemove**

- 键值 1： **\*Confidential***

- 键 2：**ExternalContentMarkingToRemove**

- 键值 2： **\*Label applied*** 

#### <a name="optimization-for-powerpoint"></a>针对 PowerPoint 的优化

PowerPoint 中的页脚以形状的形式实现。 若要避免删除那些你指定的但不属于页面或页脚的形状，可使用以下附加高级客户端设置：PowerPointShapeNameToRemove。 我们还建议使用此设置来避免检查所有形状中的文本，因为这将占用大量资源。

如果未指定这项附加的高级客户端设置，并且 PowerPoint 包括在 RemoveExternalContentMarkingInApp键值中，将对所有形状检查你在 ExternalContentMarkingToRemove 值中指定的文本。 

查找用作页眉或页脚的形状的名称：

1. 在 PowerPoint 中，显示“选择”窗格：“格式”选项卡 >“排列”组 >“选择”窗格。

2. 选择幻灯片上包含页眉或页脚的形状。 所选形状的名称现在突出显示在“选择”窗格中。

使用形状的名称为 PowerPointShapeNameToRemove 键指定一个字符串字。 

例如：形状名称是 fc。 若要删除具有此名称的形状，则指定值：`fc`。

- 键:**PowerPointShapeNameToRemove**

- 值：\<PowerPoint 形状名称> 

若要删除多个 PowerPoint 形状，则有多少要删除的形状就创建多少个 PowerPointShapeNameToRemove 键。 对于每个条目，指定要删除的形状的名称。

默认情况下，只检查主幻灯片的页眉和页脚。 若要将检查范围扩展到所有幻灯片，将占用大量资源，则可以使用 RemoveExternalContentMarkingInAllSlides 附加高级客户端设置：

- 键:**RemoveExternalContentMarkingInAllSlides**

- 值：**True**

## <a name="label-an-office-document-by-using-an-existing-custom-property"></a>使用现有自定义属性标记 Office 文档

> [!NOTE]
> 如果结合使用此配置和用于[从 Secure Islands 和其他标记解决方案迁移标签](#migrate-labels-from-secure-islands-and-other-labeling-solutions)的配置，将优先考虑标记迁移设置。 

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

配置此设置时，如果 Office 文档具备现有自定义属性且该属性带有与某个标记名称相匹配的值，则可对此文档进行分类（并选择性地保护）。 此自定义属性可通过另一个分类解决方案进行设置，也可由 SharePoint 设置为属性。

凭借此配置，如果某用户在 Office 应用中打开并保存未带 Azure 信息保护标记的文档，则进行文档标记，使其与相应的属性值相匹配。 

此配置要求你指定两个相互配合的高级设置。 第一个设置名为 SyncPropertyName，它是基于另一分类解决方案设置的自定义属性，或是由 SharePoint 设置的属性。 第二个名为 SyncPropertyState 且必须设置为“单向”。

若要配置此高级设置，请输入以下字符串：

- 键 1：**SyncPropertyName**

- 键 1 值：\<属性名称> 

- 键 2：**SyncPropertyState**

- 键 2 值：**OneWay**

仅对一个自定义属性使用这些键和相应的值。

例如，假设有 SharePoint 列“分类”，此列的可取值为以下三个：“公开”、“常规”和“高度机密\所有员工”。 文档存储在 SharePoint 中，且“分类 属性值设置为“公开”、“常规”或“高度机密\所有员工”。

要标记带有上述某个分类值的 Office 文档，请将“SyncPropertyName”设置为“分类”），将“SyncPropertyState”设置为“单向”。 

现在，当用户打开和保存这些 Office 文档之一时，文档标记为“公开”、“常规”或“高度机密\所有员工”，前提是 Azure 信息保护策略已包含有这些名称的标签。 如果没有带这些名称的标记，则不会标记文档。

## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>禁止将文档中发现的敏感信息发送到 Azure 信息保护分析

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

在 Office 应用中使用 Azure 信息保护客户端时, 它会在首次保存文档时查找文档中的敏感信息。 提供的客户端未配置为不发送审核信息, 找到的任何敏感信息类型 (预定义或自定义) 都将发送到[Azure 信息保护分析](../reports-aip.md)。 

用于控制客户端是否发送审核信息的配置是将**审核数据发送到 Azure 信息保护日志分析**的[策略设置](../configure-policy-settings.md)。 当此策略设置为 **"打开"** 时, 如果你想要发送包括标记操作的审核信息, 但不希望发送客户端找到的敏感信息类型, 请输入以下字符串:

- 键:**RunAuditInformationTypesDiscovery**

- 值：**False**

如果你设置此高级客户端设置, 则仍可以从客户端发送审核信息, 但该信息仅限于标记活动。

例如：

- 使用此设置, 可以看到用户访问了名为 "**机密**" 的

- 如果没有此设置, 您可以看到该财经包含6个信用卡号。
    
    - 如果还启用[了对敏感数据的更深入分析](../reports-aip.md#content-matches-for-deeper-analysis), 还可以查看这些信用卡号。

## <a name="disable-sending-information-type-matches-for-a-subset-of-users"></a>禁止为一部分用户发送信息类型匹配项

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

当你为[Azure 信息保护分析](../reports-aip.md)选中此复选框后, 可以更深入地分析你的敏感数据将收集你的敏感信息类型或你的自定义条件的内容匹配项。默认情况下, 此信息由所有用户发送, 其中包括运行 Azure 信息保护扫描程序的服务帐户。 如果你有一些不应发送此数据的用户，请在这些用户的[作用域内策略](../configure-policy-scope.md)中创建以下高级客户端设置： 

- 键:**LogMatchedContent**

- 值：**禁用**


## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>限制扫描程序使用的线程数

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

默认情况下，扫描程序使用运行扫描程序服务的计算机上的所有可用处理器资源。 如果在扫描此服务时需要限制 CPU 使用率，请创建以下高级设置。 

对于该值，请指定扫描程序可以并行运行的并发线程数。 扫描程序为其扫描的每个文件使用单独的线程，因此此限制配置还定义了可以并行扫描的文件数。 

首次配置测试值时，建议为每个核心指定 2 个，然后监视结果。 例如，如果在具有 4 个核心的计算机上运行扫描程序，请先将值设置为 8。 如有必要，请根据扫描程序计算机所需的最终性能和扫描速率相应增减该数量。 

- 键:**ScannerConcurrencyLevel**

- 值： **\<并发线程数>**

## <a name="disable-the-low-integrity-level-for-the-scanner"></a>禁用扫描程序的低完整性级别

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

默认情况下，Azure 信息保护扫描程序在运行时的完整性级别低。 此设置可以提供更强大的安全隔离，但会牺牲性能。 如果你使用具有特权的帐户（例如本地管理员帐户）运行扫描程序，则低完整性级别是适合的，因为此设置有助于保护运行扫描程序的计算机。

但是，当运行扫描程序的服务帐户只在[扫描程序先决条件](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner)中记录了权限时，低完整性级别不是必需的且不推荐使用，因为它会对性能产生负面影响。 

有关 Windows 完整性级别的详细信息，请参阅 [Windows 完整性机制是什么？](https://msdn.microsoft.com/library/bb625957.aspx)

若要配置此高级设置，以便扫描程序以 Windows 自动分配的完整性级别运行（标准用户帐户以中等完整性级别运行），请输入以下字符串：

- 键:**ProcessUsingLowIntegrity**

- 值：**False**

## <a name="change-the-timeout-settings-for-the-scanner"></a>更改扫描程序的超时设置

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

默认情况下, Azure 信息保护扫描程序的超时期限为 00:15:00 (15 分钟), 用于检查每个文件中是否有敏感信息类型或为自定义条件配置的 regex 表达式。 当达到此内容提取过程的超时期限时, 将返回超时前的所有结果, 并对该文件停止进行进一步检查。 在此方案中, 将在%*localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog (如果有多个日志, 则为 zipped) 中记录以下错误消息:**GetContentParts 失败**, 操作在详细信息中**被取消**。

如果由于文件较大而遇到此超时问题, 则可以增加此超时期限以进行完整的内容提取:

- 键:**ContentExtractionTimeout**

- 值:  **\<hh: min: sec >**

文件类型可影响扫描文件所花费的时间。 扫描时间示例:

- 典型的 100 MB Word 文件:0.5-5 分钟

- 典型的 100 MB PDF 文件:5-20 分钟

- 典型的 100 MB Excel 文件:12-30 分钟

对于某些非常大的文件类型 (如视频文件), 请考虑在扫描程序配置文件中将文件扩展名添加到要**扫描的文件类型**选项, 从扫描中排除它们。

此外, Azure 信息保护扫描程序的每个文件处理的超时期限为 00:30:00 (30 分钟)。 此值将考虑从存储库中检索文件所需的时间, 并暂时将其保存在本地, 以执行可包括解密、用于检查、标记和加密的内容提取的操作。

尽管 Azure 信息保护扫描程序可以每分钟扫描数十到数百个文件, 但如果你的数据存储库包含大量非常大的文件, 则扫描程序可以超过此默认超时时间, 在 Azure 门户中, 将在30后停止). 在此方案中, 以下错误消息记录在%*localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog (如果有多个日志, 则为 zipped) 和 scanner .csv 日志文件中:**操作已取消**。

默认情况下, 具有4核处理器的扫描程序有16个线程用于扫描, 在30分钟的时间段内遇到16个大型文件的概率取决于大文件的比率。 例如, 如果扫描速率为每分钟200个文件, 而 1% 的文件超过30分钟超时, 则在超过 85% 的情况下, 扫描程序将遇到30分钟的超时情况。 这些超时可能会导致更长的扫描时间和更高的内存消耗。

在这种情况下, 如果无法将更多的核心处理器添加到扫描仪计算机, 请考虑缩短超时期限以获得更好的扫描速率和更低的内存消耗, 但需确认会排除某些文件。 另外, 请考虑增加超时期限以获得更准确的扫描结果, 但确认此配置可能会导致扫描速率较低且内存消耗更高。

若要更改文件处理的超时时间, 请配置以下高级客户端设置:

- 键:**FileProcessingTimeout**

- 值:  **\<hh: min: sec >**

## <a name="change-the-local-logging-level"></a>更改本地日志记录级别

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。

默认情况下，Azure 信息保护客户端会将客户端日志文件写入 %localappdata%\Microsoft\MSIP 文件夹。 这些文件供 Microsoft 支持部门用来排除故障。
 
若要更改这些文件的日志记录级别，请配置以下高级客户端设置：

- 键:**LogLevel**

- 值：\<日志记录级别>

将日志记录级别设置为以下值之一：

- **关闭**：没有本地日志记录。

- **错误**：只有错误。

- **Info**：最少日志记录，其中不包含事件 ID（扫描程序默认设置）。

- **Debug**：完整信息。

- **Trace**：详细日志记录（客户端默认设置）。 对于扫描程序，此设置会产生很大性能影响，应仅在 Microsoft 支持部门请求时，才为扫描程序启用此设置。 如果系统要求为扫描程序设置此日志记录级别，请务必在已收集相关日志后设置其他值。

此高级客户端设置不会更改发送到 Azure 信息保护用于[集中报告](../reports-aip.md)的信息，也不会更改写入本地[事件日志](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)的信息。

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>与 Exchange 邮件分类集成以实现移动设备标记解决方案

虽然 Outlook 网页版尚不支持本机 Azure 信息保护分类和保护，但在移动用户使用 Outlook 网页版时，可以使用 Exchange 邮件分类，将 Azure 信息保护标签扩展到这些用户。 Outlook Mobile 不支持 Exchange 邮件分类。

要实现此解决方案： 

1. 使用 [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell cmdlet 创建邮件分类，其 Name 属性映射到 Azure 信息保护策略中的标签名称。 

2. 为每个标签创建 Exchange 邮件流规则：在邮件属性包括配置的分类时应用规则，并将邮件属性修改为设置邮件头。 

     对于邮件头，可检查已发送且使用 Azure 信息保护标签进行分类的电子邮件的 Internet 邮件头，查找要指定的信息。 查找邮件头 **msip_labels**，以及紧随其后的字符串，直至分号（包括分号）。 例如：
    
    **msip_labels：MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    然后，对于此规则中的邮件头，将 **msip_labels** 指定为邮件头，此字符串的其余部分指定为邮件头的值。 例如：
    
    ![示例 Exchange Online 邮件流规则，用于为特定 Azure 信息保护标签设置邮件头](../media/exchange-rule-for-message-header.png)
    
    注意:如果标签为子标签，还必须以相同的格式在标头值中的子标签之前指定父标签。 例如，如果你的子标签含有全局唯一标识符 27efdf94-80a0-4 d 02 b88c b615c12d69a9，则值可能如下：`MSIP_Label_ab70158b-bdcc-42a3-8493-2a80736e9cbd_Enabled=True;MSIP_Label_27efdf94-80a0-4d02-b88c-b615c12d69a9_Enabled=True;`

测试此配置前，请注意，创建或编辑邮件流规则时通常都会有延迟（例如，等待一小时）。 如果此规则生效，便会在用户使用 Outlook 网页版时发生以下事件： 

- 用户选择 Exchange 邮件分类，并发送电子邮件。

- Exchange 规则检测 Exchange 分类，并对应修改邮件头以添加 Azure 信息保护分类。

- 如果内部收件人在 Outlook 中查看电子邮件，且已安装 Azure 信息保护客户端，就会看到已分配的 Azure 信息保护标签。 

如果 Azure 信息保护标签应用了保护，请将此保护添加到规则配置中：选择选项来修改邮件安全性，应用权限保护，再选择保护模板或“不转发”选项。

还可以将邮件流规则配置为执行反向映射。 检测到 Azure 信息保护标签时，请设置相应的 Exchange 邮件分类：

- 对于每个 Azure 信息保护标签：请创建在 msip_labels 头包含标签名称（例如 General）时应用的邮件流规则，并应用映射到此标签的邮件分类。


## <a name="next-steps"></a>后续步骤
至此，已自定义 Azure 信息保护客户端。若要了解支持此客户端所需的其他信息，请参阅以下资源：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


