---
title: Azure 信息保护客户端-AIP
description: Microsoft Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的数据。 客户端（Azure 信息保护客户端或 Rights Management 客户端）与在计算机和移动设备上运行的应用程序集成。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
search.appverid:
- MET150
ms.openlocfilehash: 75d95df5017c440c06f58c22f59ecad68fc1a4b7
ms.sourcegitcommit: fdc1f3d76b48f4e865a538087d66ee69f0f9888d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141558"
---
# <a name="the-client-side-of-azure-information-protection"></a>Azure 信息保护的客户端

>适用对象：  Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的文档和电子邮件：

- 客户端可以是 Azure 信息保护客户端 (经典)、Azure 信息保护统一标签客户端或 Rights Management 客户端。 无论你使用哪种客户端, 它都将与你在计算机和移动设备上运行的应用程序集成。 
- 服务驻留在云中（Azure 信息保护，它使用 Azure Rights Management 服务进行数据保护）或本地（Active Directory Rights Management Services，通常称为“AD RMS”）。 

Azure 信息保护客户端 (经典) 和 Azure 信息保护统一标签客户端支持标记的分类和保护。 经典客户端还支持无需标记的保护。 这两个客户端都与 Office 应用程序集成, 并且必须单独安装。

Rights Management (RMS) 客户端随某些应用程序自动安装, 如 Office 应用程序、Azure 信息保护客户端 (经典) 和 Azure 信息保护统一标签客户端, 以及启用应用程序来自软件供应商。 但是，它也可以[单独安装](https://www.microsoft.com/en-us/download/details.aspx?id=38396)，以支持[从受 IRM 保护的库和 OneDrive for Business 同步文件](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)，并供希望将权限管理保护集成到业务线应用程序中的开发人员使用。

## <a name="choose-which-azure-information-protection-client-to-use"></a>选择要使用的 Azure 信息保护客户端

**Azure 信息保护客户端 (经典)** 从 Azure 门户下载标签和策略设置。 有关此客户端的详细信息, 请[参阅 Azure 信息保护客户端:版本发行历史记录和支持策略](client-version-release-history.md)。

Azure 信息保护统一标签客户端  从以下管理中心下载标签和策略设置：Office 365 安全与合规中心、Microsoft 365 安全中心和 Microsoft 365 合规中心。 有关此客户端的详细信息, 请[参阅 Azure 信息保护统一标签客户端:版本发布信息](unifiedlabelingclient-version-release-history.md)。

应该安装哪个客户端？

- 安装适用于 MacOS、iOS 和 Android 的标签的 Azure 信息保护统一标签客户端, 如果你不需要某些尚不支持的功能。 这些功能包括使用本地密钥 (HYOK) 和本地数据存储的扫描仪保护内容。

- 如果需要的客户端版本的客户端尚不支持统一标签客户端, 请安装 Azure 信息保护客户端 (经典)。 你的折衷在于, 不能在其他客户端平台上使用标签, 也不能使用其他管理门户进行管理。

目前, 经典客户端和统一标签客户端的功能没有奇偶校验。 但是, 这种缺口正在关闭, 你会希望将新功能仅添加到统一的标签客户端。 出于此原因, 我们建议你在其当前功能集和功能满足你的业务需求的情况下部署统一的标签客户端。 否则, 或者如果已在尚未[迁移到统一标签存储](../configure-policy-migrate-labels.md)的 Azure 门户中配置了标签, 请使用经典客户端。

你还可以在同一环境中安装这两个客户端以支持不同的业务要求, 如以下示例中所示。 对于这种情况, 我们建议你迁移 Azure 门户中的标签, 以便两组客户端共享相同的标签集以便于管理。

##### <a name="example-deployment-strategy"></a>示例部署策略:

- 对于大多数用户, 可以部署 Azure 信息保护统一标签客户端, 因为此客户端满足这些用户的业务需求。 
    
    对于这些用户, 如果他们的标签体验也是运行 MacOS、iOS 和 Android 的设备, 并且这些设备的 Office 版本支持敏感度标签, 则他们的标签体验非常类似。

- 对于用户的子集, 可以部署经典客户端, 因为这些用户需要应用 "保留自己的密钥" (HYOK) 保护的标签。
    
    对于这些用户, 如果他们还具有运行 MacOS、iOS 和 Android 的设备, 并且这些设备的 Office 版本支持敏感度标签, 则他们的体验会略有不同。 例如, 他们将在 Office 功能区上看到 "**保护**" 按钮, 而不是 "**敏感度**" 按钮。 有关其他差异, 请参阅下表。

- 你有本地数据存储, 其中包含需要扫描敏感信息或分类和保护的文档。 在服务器上部署经典客户端以运行 Azure 信息保护扫描程序。

### <a name="compare-the-clients"></a>比较客户端

使用下表来帮助比较两个 Azure 信息保护客户端支持的功能。

|功能|经典客户端|统一标签客户端|
|-------|-----------------------------------|----------------------------------------------------|
|标记操作：手动、建议、自动| 是 | 是 |
|中心报告（分析）：| 是 | 是 |
|标签的多语言支持:| 是 | 是 |
|重置设置和导出日志：| 是 | 是 |
|用户定义的权限：| 是 | 是；但具有限制： <br /><br />-仅适用于 Outlook (请勿转发):支持<br /><br />-适用于 Word、Excel、PowerPoint 和文件资源管理器:在 Azure 门户中配置标签时受支持 |
|自定义权限：| 是 | 文件资源管理器和 PowerShell <br /><br /> 在 Office 应用程序中, 用户可以选择 "**文件信息** > **保护文档** > **限制访问**" 或 "管理员可为用户定义的权限配置标签"。|
|Office 应用中的“信息保护”栏：| 是 | 是；但具有限制：<br /><br /> - 无标题或可自定义的工具提示<br /><br /> - 应用的标签未显示标签颜色|
|标签可应用视觉标记（页眉、页脚、水印）：| 是 | 是；但具有限制：<br /><br /> - 页眉和页脚不支持变量获取动态值 <br /><br /> - 不支持为 Word、Excel、PowerPoint 和 Outlook 设置不同的视觉标记|
|文件资源管理器，右键单击操作：| 是 | 是；但具有限制：<br /><br /> - 无法保护 .ppdf 格式的 PDF 文档 <br /><br />  - 不支持仅保护模式|
|受保护文件的查看器：| 是 | 是；但具有限制：<br /><br /> -对于一般受保护的文件 (.pfile), 与经典客户端的查看器不同, 不能将更改保存到最初打开的文件。|
|PowerShell 命令：| 是 | 是；但具有限制：<br /><br />- 包含以下 Cmdlet：[Get-aipfilestatus](/powershell/module/azureinformationprotection/get-aipfilestatus), [AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions), [set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification), [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel), [set-set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />-当前无法从容器文件 (zip、rar、7z、.msg 和 .pst) 中删除保护|
|离线支持保护操作：| 是 | 是；但具有限制： <br /><br />- 对于文件资源管理器和 PowerShell 命令，用户必须连接到 Internet 才能保护文件。 |
|支持使用手动策略文件管理的已断开连接的计算机：| 是 |否 |
|HYOK 支持：| 是 | 否<br /><br /> 从 Azure 门户迁移的标签以及为 HYOK 保护配置的标签通过 Azure 信息保护统一标记客户端显示，但不应用保护。 |
|事件查看器的使用情况日志记录：| 是 | 否|
|来自电子邮件附件的标签继承：| 是 | 是  |
|在 Outlook 中显示“不可转发”按钮| 是 | 否 |
|包括以下内容的[自定义项](client-admin-guide-customizations.md#available-advanced-client-settings)：<br />- 电子邮件的默认标签<br />- 启用自定义权限 <br />- S/MIME 支持<br />- 报告问题选项| 是 | 是, 使用[PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) |
|本地数据存储的扫描程序：| 是 | 否 |
|跟踪和撤销：| 是 | 否 |
|使用模板的仅保护模式 (无标签):| 是 | 否 |
|对 AD RMS 的支持：| 是 | 仅支持以下操作：<br /><br /> - 在你部署 [Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))时，查看器可打开受保护的文档|

#### <a name="detailed-comparisons-for-the-clients"></a>客户端的详细比较

如果两个客户端都支持相同的功能, 请使用下表来帮助确定两个客户端之间的功能差异。

|功能 |经典客户端|统一标签客户端|
|--------------|-----------------------------------|-----------------------------------------------------------|
|安装：| 安装本地演示策略的选项 | 没有本地演示策略|
|在 Office 应用程序中应用时的标签选择和显示：|通过功能区上的“保护”按钮  <br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|通过功能区上的“敏感度”  按钮<br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|
|在 Office 应用程序中管理“信息保护”栏：|面向用户： <br /><br />- 从功能区上的“保护”按钮选择显示或隐藏栏 <br /><br />- 如果用户选择隐藏栏，默认情况下，该栏在应用程序中隐藏，但会继续自动显示在新打开的应用程序中 <br /><br /> 面向管理员： <br /><br />- 在应用程序首次打开时，通过策略设置自动显示或隐藏栏，并控制在用户选择隐藏栏后，该栏是否对新打开的应用程序自动保持隐藏状态|面向用户： <br /><br />- 从功能区上的“敏感度”按钮选择显示或隐藏栏 <br /><br />- 当用户选择隐藏栏时，该栏在该应用程序中以及新打开的应用程序中均处于隐藏状态 <br /><br />面向管理员： <br /><br />-用于管理栏的 PowerShell 设置 |
|标签颜色： | 在 Azure 门户中配置 | 在将标签迁移到 Office 365 后保留, 并可通过 PowerShell 进行配置 <br /><br /> 可以使用[PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)配置颜色|
|标签支持不同语言:| 在 Azure 门户中配置 | 使用 Office 365 安全性和符合性 PowerShell 进行配置, 为[新标签](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps)和[设置标签](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)使用*LocaleSettings*参数|
|策略更新： | 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 24 小时一次 | 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 4 小时一次|
|PDF 支持的格式：| 保护: <br /><br /> - PDF 加密的 ISO 标准（默认） <br /><br /> - .ppdf <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护| 保护: <br /><br /> - PDF 加密的 ISO 标准 <br /><br /> <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护|
|支持的 cmdlet：| [AzureInformatioProtection](/powershell/module/azureinformationprotection) 记录的所有 cmdlet | Set-aipfileclassification、Set-aipfilelabel 和 Get-aipfilestatus 不支持 SharePoint 路径 <br /><br /> Set-aipfileclassification 和 Set-aipfilelabel 不支持*Owner*参数 <br /><br /> 此外，对于未应用标签的所有场景，都有一条“无适用标签”的注释 <br /><br /> Set-aipfileclassification 支持*WhatIf*参数, 因此它可以在发现模式下运行 <br /><br /> Set-AIPFileLabel 不支持 EnableTracking  参数 <br /><br /> Get-AIPFileStatus 不从其他租户返回标签信息，也不显示 RMSIssuedTime  参数<br /><br />此外, Get-aipfilestatus 的*LabelingMethod*参数显示**特权**或**标准**, 而不是**手动**或**自动**。 有关详细信息，请参阅[联机文档](/powershell/module/azureinformationprotection/get-aipfilestatus)。|
|Office 中每个操作的对齐方式提示（如果已配置）： | 频率：每个文件 <br /><br /> 降低敏感度级别 <br /><br /> 删除标签<br /><br /> 删除保护 | 频率：每个会话 <br /><br /> 降低敏感度级别<br /><br /> 删除标签|
|删除已应用的标签操作： | 系统提示用户确认 <br /><br />下次 Office 应用程序打开文件时，不会自动应用默认标签或自动标签（如果已配置）  <br /><br />| 不提示用户确认<br /><br /> 下次 Office 应用程序打开文件时，自动应用默认标签或自动标签（如果已配置）|
|自动和推荐的标签: | 在 Azure 门户中配置为[标签条件](../configure-policy-classification.md)，其中包含使用短语或正则表达式的内置信息类型和自定义条件 <br /><br />配置选项包括： <br /><br />- 唯一/非唯一计数 <br /><br /> - 最小计数| 在管理中心中配置，包含内置敏感信息类型和[自定义信息类型](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)<br /><br />配置选项包括：  <br /><br />- 仅唯一计数 <br /><br />- 最小和最大计数 <br /><br />- 信息类型支持 AND 和 OR <br /><br />- 关键字字典<br /><br />- 可自定义的可信度和字符接近度|
|自动和建议标签的可自定义策略提示: | 是 <br /><br />使用 Azure 门户将默认消息替换为用户 | 否 <br /><br /> 尽管管理中心提供了提供自定义策略提示的选项, 但统一标签客户端当前不支持此选项|
|更改文件的默认保护级别: | 是 <br /><br />你可以使用[注册表编辑](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files)来替代本机保护和常规保护的默认值 | 否 |

有关特定保护设置的行为差异的详细比较, 请参阅[比较标签的保护设置的行为](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label)。

#### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>未计划在 Azure 信息保护统一标签客户端中的功能

尽管 Azure 信息保护的统一标签客户端仍处于开发阶段, 但当前未计划在未来版本中为统一标签客户端提供以下功能和行为差异: 

- 通过手动策略文件管理为断开连接的计算机支持 Office 应用

- 作为用户可在 Office 应用中选择的选项的自定义权限:Word、Excel 和 PowerPoint

- 从 Office 应用和文件资源浏览器中跟踪和撤销

- Azure 信息保护栏标题和工具提示

- 使用模板的仅保护模式 (无标签)

- 将 PDF 文档作为 .ppdf 格式进行保护

- 在 Outlook 中显示“不可转发”按钮

- 演示策略

- 对删除保护的验证

- 确认提示**是否要删除此标签？** 对于用户, 如果未使用策略设置进行理由,

- 使用现有自定义属性（SyncPropertyName 和 SyncPropertyState 高级客户端设置）标记 Office 文档

- 连接到 Rights Management 服务的单独 PowerShell cmdlet


#### <a name="parent-labels-and-their-sublabels"></a>父标签及其子标签 

Azure 信息保护客户端 (经典) 不支持指定具有子标签的父标签的配置。 这些配置包括指定默认标签和推荐分类或自动分类的标签。 如果某个标签具有子标签，可以指定其中一个子标签，但不能指定父标签。

对于奇偶校验，Azure 信息保护统一标签客户端也不支持应用具有子标签的父标签，即使可以在管理中心中选择这些标签，也无法应用。 在此方案中，Azure 信息保护统一标记客户端将不应用父标签。

## <a name="see-also"></a>请参阅
如需详细了解如何部署和使用这些客户端，请参阅以下文档：

- [Azure 信息保护客户端](AIP-client.md)

- [Azure 信息保护统一标记客户端](unifiedlabelingclient-version-release-history.md)

- [RMS 客户端部署说明](client-deployment-notes.md)

尽管 Azure 信息保护客户端 (经典) 可用于 AD RMS, 但此客户端最适合用于其 Azure 服务;Azure 信息保护及其保护服务, Azure Rights Management。 有关 Azure 信息保护服务端的比较，请参阅[比较 Azure 信息保护与 AD RMS](../compare-on-premise.md)。