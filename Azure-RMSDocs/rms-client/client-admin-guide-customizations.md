---
title: Azure 信息保护客户端的自定义配置
description: 有关自定义适用于 Windows 的 Azure 信息保护客户端的信息。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 80f0b29b05f3a63972f7bc45e14ee721cf289a86
ms.sourcegitcommit: 87d73477b7ae9134b5956d648c390d2027a82010
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>管理员指南：Azure 信息保护客户端的自定义配置

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、带 SP1 的 Windows 7、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

请参阅以下高级配置相关信息，在管理 Azure 信息保护客户端时，可能需要用于特定方案或一部分用户。

其中一些设置需要编辑注册表，一些使用的是高级设置，必须先在 Azure 门户中进行配置，再发布以供客户端下载。  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>在门户中配置高级客户端配置设置的具体步骤

1. 如果尚未这样做，请在新的浏览器窗口中[登录到 Azure 门户](../deploy-use/configure-policy.md#signing-in-to-the-azure-portal)，然后导航到“Azure 信息保护”边栏选项卡。

2. 从“分类” > “标签”菜单选项：选择“策略”。

3. 在“Azure 信息保护 - 策略”边栏选项卡中，选择此策略旁边的上下文菜单 (...)，以添加高级设置。 再选择“高级设置”。
    
    可以为全局策略和作用域内策略配置高级设置。

4. 在“高级设置”边栏选项卡中，键入高级设置名称和值，再选择“保存并关闭”。

5. 确保此策略的用户重启打开过的任何 Office 应用程序。

6. 如果不再需要此设置，并希望还原为默认行为：在“高级设置”边栏选项卡中，选择不再需要的设置旁边的上下文菜单 (...)，再选择“删除”。 然后单击“保存并关闭”。

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>阻止针对仅 AD RMS 计算机出现的登录提示

默认情况下，Azure 信息保护客户端会自动尝试连接到 Azure 信息保护服务。 对于只与 AD RMS 通信的计算机，此配置可能导致不必要的用户登录提示。 可以通过编辑注册表阻止此登录提示：

找到以下值名称，然后将值数据设置为“0”：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

无论此设置如何，Azure 信息保护客户端遵循标准的 [RMS 服务发现进程](../rms-client/client-deployment-notes.md#rms-service-discovery)，查找其 AD RMS 群集。

## <a name="suppress-the-initial-congratulations-welcome-page"></a>禁止显示初始“祝贺你!” “欢迎使用”页

首次在计算机上安装 Azure 信息保护客户端时，如果用户打开 Word、Excel、PowerPoint 或 Outlook，将显示“祝贺你!” 页，其中包含有关如何使用新的信息保护栏选择标签的简短说明。 可以通过编辑注册表来禁止显示此页。

找到以下值名称并将值数据设置为 **0**：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnableWelcomeExperience** 


## <a name="sign-in-as-a-different-user"></a>以其他用户身份登录

在生产环境中，如果用户使用的是 Azure 信息保护客户端，则通常不需要以其他用户身份登录。 不过，作为管理员，你在测试阶段可能需要以其他用户身份登录。 

可以使用“Microsoft Azure 信息保护”对话框验证当前登录的帐户身份：打开 Office 应用程序，在“主页”选项卡上的“保护”组中，单击“保护”，然后单击“帮助和反馈”。 帐户名称会显示在“客户端状态”部分中。

请确保还要检查所显示的登录帐户的域名。 很容易忽视的一点是，使用正确的帐户名登录，但域不正确。 使用错误帐户的症状是，无法下载 Azure 信息保护策略，或看不到预期的标签或行为。

以其他用户身份登录：

1. 导航到 %localappdata%\Microsoft\MSIP 并删除 TokenCache 文件。

2. 重新启动任何打开的 Office 应用程序，并使用其他用户帐户登录。 如果在 Office 应用程序中没有看到登录到 Azure 信息保护服务的提示，请返回“Microsoft Azure信息保护”对话框，然后从更新的“客户端状态”部分中单击“登录”。

此外：

- 此解决方案支持以同一租户中的其他用户身份登录。 不支持以不同租户中的其他用户身份登录。 若要使用多个租户测试 Azure 信息保护，请使用不同的计算机。

- 如果使用的是单一登录，必须在编辑注册表后注销 Windows，再使用其他用户帐户登录。 然后，Azure 信息保护客户端会使用当前登录的用户帐户，自动进行身份验证。

- 可以使用“帮助和反馈”中的“重置设置”选项注销并删除当前已下载的 Azure 信息保护策略。


## <a name="enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses"></a>如果组织拥有组合许可证，则强制执行仅保护模式

如果组织不具有任何 Azure 信息保护许可证，但有包含用于数据保护的 Azure 权限管理服务的 Office 365 许可证，则用于 Windows 的 Azure 信息保护客户端会自动在[仅保护模式](../rms-client/client-protection-only-mode.md)下运行。

但是，如果贵组织已订阅 Azure 信息保护，默认情况下所有 Windows 计算机都可以下载 Azure 信息保护策略。 Azure 信息保护客户端不会进行许可证检查以及强制执行。 

如果某些用户没有 Azure 信息保护许可证，但拥有包含 Azure 权限管理服务的 Office 365 许可证，请在这些用户的计算机上编辑注册表，以防止用户在 Azure 信息保护中运行未经授权的分类和标签功能。

找到以下值名称并将值数据设置为 **0**：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

此外，请确保这些计算机的 %LocalAppData%\Microsoft\MSIP 文件夹中不具有名为 Policy.msip 的文件。 如果此文件存在，请将其删除。 此文件包含 Azure 信息保护策略，并且可能在编辑注册表之前已下载，如果使用演示选项安装了 Azure 信息保护客户端，那么也可能已下载此文件。

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>隐藏 Windows 文件资源管理器中的“分类和保护”菜单选项

创建以下 DWORD 值名称（以及任何数值数据）：

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>对断开连接的计算机的支持

默认情况下，Azure 信息保护客户端会自动尝试连接到 Azure 信息保护服务，以下载最新的 Azure 信息保护策略。 如果你知道你的计算机在一段时间无法内连接到 Internet，可以通过编辑注册表阻止客户端尝试连接到该服务。 

找到以下值名称并将值数据设置为 **0**：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

确保客户端在 %LocalAppData%\Microsoft\MSIP 文件夹中具有一个名为 Policy.msip 的有效策略文件。 如有必要，可以从 Azure 门户中导出策略，并将导出的文件复制到客户端计算机。 此外，还可以使用此方法，将已过时的策略文件替换为已发布的最新策略。

导出策略时，此操作会下载包含多个版本的策略的压缩文件，这些策略对应于不同版本的 Azure 信息保护客户端：

1. 解压缩文件，然后使用下表来确定所需要的策略文件。 
    
    |文件名|相应的客户端版本|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |版本 1.2|
    |Policy1.2.msip |版本 1.3 - 1.7|
    |Policy1.3.msip |1.8 和更高版本|
    
2. 将已标识的文件重命名为 **Policy.msip**，然后将其复制到安装了 Azure 信息保护客户端的计算机上的 **%LocalAppData%\Microsoft\MSIP** 文件夹。 


## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>在 Outlook 中隐藏或显示“不转发”按钮

建议使用“向 Outlook 功能区添加‘不转发’按钮”这一[策略设置](../deploy-use/configure-policy-settings.md)来配置此选项。 但是，也可以使用在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)来配置此选项。

配置此设置后，将在 Outlook 功能区中隐藏或显示“不转发”按钮。 此设置对 Office 菜单中的“不转发”选项没有影响。

若要配置此高级设置，请输入以下字符串：

- 键：DisableDNF

- 值：输入 True 隐藏按钮，输入 False 显示按钮

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>设置用户是否能够使用自定义权限选项

建议使用“设置用户是否能够使用自定义权限选项”这一[策略设置](../deploy-use/configure-policy-settings.md)来配置此选项。 但是，也可以使用在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)来配置此选项。 

配置此设置并为用户发布策略后，用户就可以使用自定义权限选项选择自己的保护设置，或者无法使用这些选项选择保护设置（除非系统出现提示）。

若要配置此高级设置，请输入以下字符串：

- 键：EnableCustomPermissions

- 值：输入 True 使自定义权限选项可用，输入 False 使其不可用


## <a name="permanently-hide-the-azure-information-protection-bar"></a>永久隐藏 Azure 信息保护栏

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 仅当“在 Office 应用中显示信息保护栏”这一项[策略设置](../deploy-use/configure-policy-settings.md)设置为“开”时，才使用此配置。

配置此设置并为用户发布策略后，如果用户选择不在 Office 应用程序中显示 Azure 信息保护栏，此栏保持隐藏。 当用户通过依次单击“主页”选项卡、“保护组”和“保护”按钮取消选中“显示栏”选项时，就会发生这种情况。 如果用户使用“关闭信息保护栏”图标关闭此栏，此设置将不起作用。

即使 Azure 信息保护栏保持隐藏，如果已配置了推荐分类，或者文档或电子邮件必须有标签，用户仍可以从临时显示的栏中选择标签。 

若要配置此高级设置，请输入以下字符串：

- 键：EnableBarHiding

- 值：True


## <a name="enable-recommended-classification-in-outlook"></a>在 Outlook 中启用建议的分类

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 此设置处于预览状态，并且可能会更改。

为建议的分类配置标签时，系统将提示用户接受或关闭 Word、Excel 和 PowerPoint 中建议的标签。 此设置将此标签建议扩展到也在 Outlook 中显示。

若要配置此高级设置，请输入以下字符串：

- 键：OutlookRecommendationEnabled

- 值：True


## <a name="set-a-different-default-label-for-outlook"></a>为 Outlook 设置不同的默认标签

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

配置此设置时，Outlook 不会应用 Azure 信息保护策略中为“选择默认标签”设置配置的默认标签。 相反，Outlook 可应用不同的默认标签，也可不应用标签。

要应用不同的标签，必须指定标签 ID。 在 Azure 门户中查看或配置 Azure 信息保护策略时，标签 ID 值将显示在“标签”边栏选项卡上。 对于应用了标签的文件，还可运行 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell cmdlet 标识标签 ID（MainLabelId 或 SubLabelId）。 当标签包含子标签时，请始终指定子标签（而非父标签）的 ID。

因此 Outlook 不会应用默认标签，请指定“无”。

若要配置此高级设置，请输入以下字符串：

- 键：OutlookDefaultLabel

- 值：\<label ID> 或 None

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>使用强制标签时，删除文档的“以后再说”

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

在使用“所有文档和电子邮件都必须有一个标签”的[策略设置](../deploy-use/configure-policy-settings.md)时，当用户首次保存 Office 文档和发送电子邮件，系统会提示选择标签。 对于文档，用户可以选择“以后再说”暂时关闭提示以选择标签，并返回到文档。 但是不能在未选择标签的情况下关闭已保存的文档。 

在配置此设置时，将删除“以后再说”选项，以便首次保存文档时用户必须选择一个标签。

若要配置此高级设置，请输入以下字符串：

- 键：PostponeMandatoryBeforeSave

- 值：False

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>开启在后台持续运行的分类

此配置选项目前处于预览状态，可能随时更改。

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

在配置此设置时，将更改 Azure 信息保护客户端应用自动和建议标签方式的[默认行为](../deploy-use/configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied)，如下所示：

- 自动分类应用于 Word、Excel、PowerPoint 和 Outlook。 对于文档，自动分类在后台持续运行。 对于 Outlook，自动分类在发送电子邮件时运行。 
    
    如果文档之前已手动添加标签（或之前已使用更高级别的分类添加标签），则不能使用自动分类。 但也有例外情况，如果使用 Azure 信息保护扫描程序并且其 OverrideLabel 参数设置为开启，则可以使用自动分类。

- 建议的分类应用于 Word、Excel 和 PowerPoint。 对于这些文档，建议的分类在后台持续运行。 不能将建议的分类用于 Outlook。
    
    对于之前已设置标签（无论是否是更高级别的分类标签）的文档，可使用建议的分类。 

如果 Azure 信息保护客户端定期检查你指定的条件规则文档，此行为将为存储在 SharePoint Online 中的文档启用自动和建议的分类以及保护。 由于已运行条件规则，因此大型文件可实现更快保存。 

条件规则不会作为用户类型实时运行。 而会在文档发生修改时作为后台任务定期运行。

若要配置此高级设置，请输入以下字符串：

- 键：RunPolicyInBackground

- 值：True

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>从 Secure Islands 和其他标记解决方案迁移标签

此配置选项目前处于预览状态，可能随时更改。 另外，必须有预览版的客户端或 Azure 信息保护扫描程序，才能使用此配置选项。

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

对于 Secure Islands 标记的 Office 文档和 PDF 文档，可以使用所定义的映射，利用 Azure 信息保护标签重新标记这些文档。 此外，这种方法还可用于重用其他解决方案对 Office 文档标记的标签。 

由于有此配置选项，Azure 信息保护客户端按如下所述应用新 Azure 信息保护标签：

- 对于 Office 文档：当文档在桌面应用程序中打开时，新 Azure 信息保护标签显示为已设置，并在文档保存时应用。

- 对于文件资源管理器：在“Azure 信息保护”对话框中，新 Azure 信息保护标签显示为已设置，并在用户选择“应用”时应用。 如果用户选择“取消”，新标签就不会应用。

- 对于 Powershell：[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) 应用新 Azure 信息保护标签。 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) 不会显示新 Azure 信息保护标签，除非标签由另一种方法设置。

- 对于 Azure 信息保护扫描程序：发现功能可报告何时会设置新 Azure 信息保护标签，此标签可以通过强制模式进行应用。

若要执行此配置，必须为要映射到旧标签的所有 Azure 信息保护标签都指定“LabelbyCustomProperty”高级客户端设置。 然后，使用以下语法设置每个条目的值：

`[Azure Information Protection label ID],[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

在 Azure 门户中查看或配置 Azure 信息保护策略时，标签 ID 值将显示在“标签”边栏选项卡上。 若要指定子标签，父标签必须位于同一范围中，或位于全局策略中。

指定所选的迁移规则名称。 请使用描述性名称，这有助于确定应如何将旧标记解决方案中的一个或多个标签映射到 Azure 信息保护标签。 此名称显示在扫描程序报告和事件查看器中。 

### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>示例 1：相同标签名称的一对一映射

对于 Secure Islands 标记为“机密”的文档，应由 Azure 信息保护重新标记为“机密”。

在此示例中：

- Azure 信息保护标签“机密”的标签 ID 为 1ace2cc3-14bc-4142-9125-bf946a70542c。 

- Secure Islands 标签存储在“Classification”自定义属性中。

高级客户端设置：

    
|名称|值|
|---------------------|---------|
|LabelbyCustomProperty|1ace2cc3-14bc-4142-9125-bf946a70542c,"Secure Islands label is Confidential",Classification,Confidential|

### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>示例 2：不同标签名称的一对一映射

对于 Secure Islands 标记为“敏感”的文档，应由 Azure 信息保护重新标记为“高度机密”。

在此示例中：

- Azure 信息保护标签“高度机密”的标签 ID 为 3e9df74d-3168-48af-8b11-037e3021813f。

- Secure Islands 标签存储在“Classification”自定义属性中。

高级客户端设置：

    
|名称|值|
|---------------------|---------|
|LabelbyCustomProperty|3e9df74d-3168-48af-8b11-037e3021813f,"Secure Islands label is Sensitive",Classification,Sensitive|


### <a name="example-3-many-to-one-mapping-of-label-names"></a>示例 3：标签名称的多对一映射

有两个 Secure Islands 标签均包含“内部”一词，并且希望 Azure 信息保护将标有这两个 Secure Islands 标签之一的文档重新标记为“常规”。

在此示例中：

- Azure 信息保护标签“常规”的标签 ID 为 2beb8fe7-8293-444c-9768-7fdc6f75014d。

- Secure Islands 标签存储在“Classification”自定义属性中。

高级客户端设置：

    
|名称|值|
|---------------------|---------|
|LabelbyCustomProperty|2beb8fe7-8293-444c-9768-7fdc6f75014d,"Secure Islands label contains Internal",Classification,.\*Internal.\*|


## <a name="label-an-office-document-by-using-an-existing-custom-property"></a>使用现有自定义属性标记 Office 文档

> [!NOTE]
> 如果结合使用此配置和上一部分中的配置，从另一个标记解决方案进行迁移，将优先考虑标记迁移设置。 

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

配置此设置时，如果 Office 文档具备现有自定义属性且该属性带有与某个标记名称相匹配的值，则可对此文档进行分类（并选择性地保护）。 此自定义属性可从另一分类解决方案进行设置，也可由 SharePoint 设置为属性。

凭借此配置，如果某用户在 Office 应用中打开并保存未带 Azure 信息保护标记的文档，则进行文档标记，使其与相应的属性值相匹配。 

此配置要求你指定两个相互配合的高级设置。 第一个设置名为 SyncPropertyName，它是基于另一分类解决方案设置的自定义属性，或是由 SharePoint 设置的属性。 第二个名为 SyncPropertyState 且必须设置为“单向”。

若要配置此高级设置，请输入以下字符串：

- 键 1：SyncPropertyName

- 键 1 值：\<属性名称> 

- 键 2：SyncPropertyState

- 键 2 值：单向

仅对一个自定义属性使用这些键和相应的值。

例如，你有一个名为“分类”的 SharePoint 列，该列可能有三个值：“公共”、“常规”和“机密”。 文档存储在 SharePoint 中，且具有为分类属性设置的某个值。

要标记带有上述某个分类值的 Office 文档，请将“SyncPropertyName”设置为“分类”），将“SyncPropertyState”设置为“单向”。 

随后，当用户打开和保存上述某个 Office 文档时，该文档将标记为“公共”、“常规”或“机密”（若在 Azure 信息保护策略中具备带这些名称的标签）。 如果没有带这些名称的标记，则不会标记文档。

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>与 Exchange 邮件分类集成以实现移动设备标记解决方案

虽然 Outlook 网页版尚不支持本机 Azure 信息保护分类和保护，但在移动用户使用 Outlook 网页版时，可以使用 Exchange 邮件分类，将 Azure 信息保护标签扩展到这些用户。 Outlook Mobile 不支持 Exchange 邮件分类。

要实现此解决方案： 

1. 使用 [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell cmdlet 创建邮件分类，其 Name 属性映射到 Azure 信息保护策略中的标签名称。 

2. 为每个标签创建 Exchange 邮件流规则：在邮件属性包括配置的分类时应用规则，并将邮件属性修改为设置邮件头。 

    对于邮件头，可检查已发送且使用 Azure 信息保护标签进行分类的电子邮件的 Internet 邮件头，查找要指定的信息。 查找邮件头 **msip_labels**，以及紧随其后的字符串，直至分号（包括分号）。 以上述示例为例：
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    然后，对于此规则中的邮件头，将 **msip_labels** 指定为邮件头，此字符串的其余部分指定为邮件头的值。 例如：
    
    ![示例 Exchange Online 邮件流规则，用于为特定 Azure 信息保护标签设置邮件头](../media/exchange-rule-for-message-header.png)

测试此配置前，请注意，创建或编辑邮件流规则时通常都会有延迟（例如，等待一小时）。 当规则生效后，如果用户使用 Outlook 网页版或支持 Exchange ActiveSync IRM 的移动设备客户端，则会发生以下事件： 

- 用户选择 Exchange 邮件分类，并发送电子邮件。

- Exchange 规则检测 Exchange 分类，并对应修改邮件头以添加 Azure 信息保护分类。

- 当收件人在 Outlook 中查看电子邮件，且已安装 Azure 信息保护客户端时，他们将看到分配的 Azure 信息保护标签，以及所有对应的电子邮件头、页脚或水印。 

如果 Azure 信息保护标签应用保护，请将此保护添加到规则配置，具体方法是选择用于修改邮件安全性的选项，应用权限保护，再选择 RMS 模板或“不转发”选项。

还可以将邮件流规则配置为执行反向映射。 检测到 Azure 信息保护标签时，请设置相应的 Exchange 邮件分类：

- 对于每个 Azure 信息保护标签，请创建在 msip_labels 头包含标签名称（例如 General）时应用的邮件流规则，并应用映射到此标签的邮件分类。


## <a name="next-steps"></a>后续步骤
至此，已自定义 Azure 信息保护客户端。若要了解支持此客户端所需的其他信息，请参阅以下资源：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
