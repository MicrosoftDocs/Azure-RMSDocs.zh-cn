---
title: 适用于 Azure 信息保护-AIP 客户端
description: Microsoft Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的数据。 客户端（Azure 信息保护客户端或 Rights Management 客户端）与在计算机和移动设备上运行的应用程序集成。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 47a92d57b9408a1ba0a5b2d82240e24783718e60
ms.sourcegitcommit: 1ec4b926885331cb4bb31bbd5074c874205f49d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749986"
---
# <a name="the-client-side-of-azure-information-protection"></a>Azure 信息保护的客户端

>适用对象：  Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的文档和电子邮件：

- 客户端可以是 Azure 信息保护客户端、 Azure 信息保护统一标记客户端或 Rights Management 客户端。 它取这些客户端使用，与计算机和移动设备运行的应用程序集成。 

- 服务驻留在云中（Azure 信息保护，它使用 Azure Rights Management 服务进行数据保护）或本地（Active Directory Rights Management Services，通常称为“AD RMS”）。 

Azure 信息保护客户端和 Azure 信息保护统一标记客户端支持分类和保护的标签。 Azure 信息保护客户端还支持保护，而无需标记。 两个客户端与 Office 应用程序集成，并必须单独安装。

某些应用程序，例如 Office 应用程序、 Azure 信息保护客户端和 Azure 信息保护统一标记客户端，以及启用 RMS 的应用程序将自动安装 Rights Management (RMS) 客户端软件供应商。 但是，它也可以[单独安装](https://www.microsoft.com/en-us/download/details.aspx?id=38396)，以支持[从受 IRM 保护的库和 OneDrive for Business 同步文件](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)，并供希望将权限管理保护集成到业务线应用程序中的开发人员使用。

## <a name="choose-which-azure-information-protection-client-to-use"></a>选择要使用的 Azure 信息保护客户端

**Azure 信息保护客户端**从 Azure 门户下载标签和策略设置。 有关此客户端的详细信息，请参阅[Azure 信息保护客户端：版本发行历史记录和支持策略](client-version-release-history.md)。

Azure 信息保护统一标签客户端  从以下管理中心下载标签和策略设置：Office 365 安全与合规中心、Microsoft 365 安全中心和 Microsoft 365 合规中心。 有关此客户端的详细信息，请参阅[Azure 信息保护统一标记的客户端：版本发布信息](unifiedlabelingclient-version-release-history.md)。

应该安装哪个客户端？

- 安装 Azure 信息保护统一标记客户端还可以使用通过 MacOS、 iOS 和 Android 的标签，并不需要高级的功能，如高级客户端设置，如果用户定义的权限，在本地密钥 (HYOK)，或有关扫描程序的本地数据存储。

- 如果您需要尚不可用统一标记的客户端中的高级的功能，但不能在其他客户端平台上使用标签，请安装 Azure 信息保护客户端。

目前，Azure 信息保护客户端和 Azure 信息保护统一标记客户端不具有其功能的奇偶校验。 但是，之后应该会填补这个缺口，届时新功能将仅添加到 Azure 信息保护统一标记客户端。 出于此原因，我们建议你部署 Azure 信息保护统一标记客户端如果其当前功能集和功能满足业务需求。 如果无法满足你的业务需求，或者如果你已在 Azure 门户中配置了标签，而这些标签尚未[迁移到统一标记存储](../configure-policy-migrate-labels.md)，请使用 Azure 信息保护客户端。

此外可以安装两个客户端在同一环境中以支持不同的业务要求，如以下示例所示。 对于此方案中，我们建议你迁移在 Azure 门户中的标签，以便在客户端这两组共享一组相同的标签为便于管理。

##### <a name="example-deployment-strategy"></a>示例部署策略：

- 对于大多数用户，可以部署 Azure 信息保护统一标记客户端，因为大多数用户不需要的特性或功能仅适用于 Azure 信息保护客户端。 
    
    对于这些用户，其标记体验是 office 的非常相似，如果它们还具有运行 MacOS、 iOS 和 Android 的设备，并且这些设备具有支持敏感度标签版本。

- 对用户的子集，你部署 Azure 信息保护客户端，因为这些用户需要应用的标签保留自己的密钥 (HYOK) 保护或针对用户定义的权限提示。
    
    对于这些用户，它们具有其他特性和功能，但稍有不同的体验，如果他们还拥有运行 MacOS、 iOS 和 Android 的设备和这些设备具有支持敏感度标签的 Office 版本。 例如，他们将看到**保护**按钮而非**敏感度**Office 功能区和信息保护栏上的按钮可以显示默认情况下。

- 必须在本地数据存储的需要进行扫描的敏感信息或分类和保护的文档。 部署 Azure 信息保护客户端在服务器上的，若要运行 Azure 信息保护扫描程序。

### <a name="compare-the-clients"></a>比较客户端

使用下表来比较两个 Azure 信息保护客户端支持的功能。

|功能|Azure 信息保护客户端|Azure Information Protection<br /> 统一标记客户端|
|-------|-----------------------------------|----------------------------------------------------|
|标记操作：手动、建议、自动| 是 | 是 |
|中心报告（分析）：| 是 | 是；但具有限制：<br /><br /> -不支持[内容匹配](../reports-aip.md#content-matches-for-deeper-analysis) |
|重置设置和导出日志：| 是 | 是 |
|用户定义的权限：| 是 | 仅适用于 Outlook（不要转发） |
|自定义权限：| 是 | 仅文件资源管理器 <br /><br /> 在 Office 应用程序中，作为替代方法，用户可以选择“文件信息” > “保护文档”    > “限制访问”  |
|Office 应用中的“信息保护”栏：| 是 | 是；但具有限制：<br /><br /> - 无标题或可自定义的工具提示<br /><br /> - 应用的标签未显示标签颜色|
|标签可应用视觉标记（页眉、页脚、水印）：| 是 | 是；但具有限制：<br /><br /> - 页眉和页脚不支持变量获取动态值 <br /><br /> - 不支持为 Word、Excel、PowerPoint 和 Outlook 设置不同的视觉标记|
|文件资源管理器，右键单击操作：| 是 | 是；但具有限制：<br /><br /> - 无法保护 .ppdf 格式的 PDF 文档 <br /><br />  - 不支持仅保护模式|
|受保护文件的查看器：| 是 | 是；但具有限制：<br /><br /> - 对于通用受保护文件 (.pfile)，无法将更改保存到最初打开的文件，这一点与 Azure 信息保护客户端中的查看器不同。|
|PowerShell 命令：| 是 | 是；但具有限制：<br /><br />- 包含以下 Cmdlet：[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)、[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)、[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />- 不包括直接连接到保护服务的 Cmdlet|
|离线支持保护操作：| 是 | 是；但具有限制： <br /><br />- 对于文件资源管理器和 PowerShell 命令，用户必须连接到 Internet 才能保护文件。 |
|支持使用手动策略文件管理的已断开连接的计算机：| 是 |否 |
|HYOK 支持：| 是 | 否<br /><br /> 从 Azure 门户迁移的标签以及为 HYOK 保护配置的标签通过 Azure 信息保护统一标记客户端显示，但不应用保护。 |
|事件查看器的使用情况日志记录：| 是 | 否|
|来自电子邮件附件的标签继承：| 是 | 否 |
|在 Outlook 中显示“不可转发”按钮| 是 | 否 |
|包括以下内容的[自定义项](client-admin-guide-customizations.md#available-advanced-client-settings)：<br />- 电子邮件的默认标签<br />- 启用自定义权限 <br />- S/MIME 支持<br />- 报告问题选项| 是 | 否 |
|本地数据存储的扫描程序：| 是 | 否 |
|跟踪和撤销：| 是 | 否 |
|仅保护模式（无标签）：| 是 | 否 |
|多语言支持：| 是 | 否 |
|对 AD RMS 的支持：| 是 | 仅支持以下操作：<br /><br /> - 在你部署 [Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))时，查看器可打开受保护的文档|

#### <a name="detailed-comparisons-for-the-clients"></a>客户端的详细的比较

如果两个客户端支持的相同功能，使用下表有助于确定两个客户端之间的一些功能差异。

|功能 |Azure 信息保护客户端|Azure Information Protection<br /> 统一标记客户端|
|--------------|-----------------------------------|-----------------------------------------------------------|
|安装：| 安装本地演示策略的选项 | 没有本地演示策略|
|在 Office 应用程序中应用时的标签选择和显示：|通过功能区上的“保护”按钮  <br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|通过功能区上的“敏感度”  按钮<br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|
|在 Office 应用程序中管理“信息保护”栏：|面向用户： <br /><br />- 从功能区上的“保护”按钮选择显示或隐藏栏 <br /><br />- 如果用户选择隐藏栏，默认情况下，该栏在应用程序中隐藏，但会继续自动显示在新打开的应用程序中 <br /><br /> 面向管理员： <br /><br />- 在应用程序首次打开时，通过策略设置自动显示或隐藏栏，并控制在用户选择隐藏栏后，该栏是否对新打开的应用程序自动保持隐藏状态|面向用户： <br /><br />- 从功能区上的“敏感度”按钮选择显示或隐藏栏 <br /><br />- 当用户选择隐藏栏时，该栏在该应用程序中以及新打开的应用程序中均处于隐藏状态 <br /><br />面向管理员： <br /><br />- 没有可用于管理栏的策略设置|
|标签颜色： | 在 Azure 门户中配置 | 在标签迁移到 Office 365 后保留 <br /><br /> 管理中心中创建的新标签没有颜色|
|策略更新： | 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 24 小时一次 | 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 4 小时一次|
|PDF 支持的格式：| 保护: <br /><br /> - PDF 加密的 ISO 标准（默认） <br /><br /> - .ppdf <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护| 保护: <br /><br /> - PDF 加密的 ISO 标准 <br /><br /> <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护|
|支持的 cmdlet：| [AzureInformatioProtection](/powershell/module/azureinformationprotection) 记录的所有 cmdlet | Set-aipauthentication 不支持的非交互式会话 <br /><br /> Set-AIPFileClassification 和 Set-AIPFileLabel 不支持 Owner  参数或 SharePoint Server 库 <br /><br /> 此外，对于未应用标签的所有场景，都有一条“无适用标签”的注释 <br /><br /> Set-AIPFileLabel 不支持 EnableTracking  参数 <br /><br /> Get-AIPFileStatus 不从其他租户返回标签信息，也不显示 RMSIssuedTime  参数<br /><br />此外， *LabelingMethod* Get-aipfilestatus 的参数将显示**特权**或**标准**而不是**手动**或**自动**。 有关详细信息，请参阅[联机文档](/powershell/module/azureinformationprotection/get-aipfilestatus)。|
|Office 中每个操作的对齐方式提示（如果已配置）： | 频率：每个文件 <br /><br /> 降低敏感度级别 <br /><br /> 删除标签<br /><br /> 删除保护 | 频率：每个会话 <br /><br /> 降低敏感度级别<br /><br /> 删除标签|
|删除已应用的标签操作： | 系统提示用户确认 <br /><br />下次 Office 应用程序打开文件时，不会自动应用默认标签或自动标签（如果已配置）  <br /><br />| 不提示用户确认<br /><br /> 下次 Office 应用程序打开文件时，自动应用默认标签或自动标签（如果已配置）|
|自动和建议标签： | 在 Azure 门户中配置为[标签条件](../configure-policy-classification.md)，其中包含使用短语或正则表达式的内置信息类型和自定义条件 <br /><br />配置选项包括： <br /><br />- 唯一/非唯一计数 <br /><br /> - 最小计数| 在管理中心中配置，包含内置敏感信息类型和[自定义信息类型](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)<br /><br />配置选项包括：  <br /><br />- 仅唯一计数 <br /><br />- 最小和最大计数 <br /><br />- 信息类型支持 AND 和 OR <br /><br />- 关键字字典<br /><br />- 可自定义的可信度和字符接近度|
|自动和建议标签的可自定义策略提示： | 是 <br /><br />使用 Azure 门户将向用户的默认消息 | 否 <br /><br /> 不当前支持此选项虽然管理员中心有一个选项以提供自定义的策略提示，由统一标记客户端|
|更改文件的默认保护级别： | 是 <br /><br />可以使用[注册表编辑](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files)重写本机和常规保护的默认值 | 否 |

有关特定的保护设置的行为差异的详细比较，请参阅[比较的保护设置的标签行为](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label)。

#### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>未计划要在 Azure 信息保护统一标记客户端的功能

尽管 Azure 信息保护统一标记客户端仍处于开发阶段，以下功能和从 Azure 信息保护客户端的行为差异是，目前未计划要在适用于 Azure 的未来版本中可用信息保护统一标记的客户端： 

- 在以下 Office 应用中自定义权限：Word、Excel 和 PowerPoint

- 从 Office 应用和文件资源浏览器中跟踪和撤销

- Azure 信息保护栏标题和工具提示

- 仅保护模式（无标签）

- 将 PDF 文档作为 .ppdf 格式进行保护

- 在 Outlook 中显示“不可转发”按钮

- 演示策略

- 对删除保护的验证

- 出现确认提示**要删除此标签？** 为用户提供理由不使用策略设置时

- 使用现有自定义属性（SyncPropertyName 和 SyncPropertyState 高级客户端设置）标记 Office 文档

- 连接到 Rights Management 服务的单独 PowerShell cmdlet


#### <a name="parent-labels-and-their-sublabels"></a>父标签及其子标签 

Azure 信息保护客户端不支持指定具有子标签的父标签的配置。 这些配置包括指定默认标签和推荐分类或自动分类的标签。 如果某个标签具有子标签，可以指定其中一个子标签，但不能指定父标签。

对于奇偶校验，Azure 信息保护统一标签客户端也不支持应用具有子标签的父标签，即使可以在管理中心中选择这些标签，也无法应用。 在此方案中，Azure 信息保护统一标记客户端将不应用父标签。

## <a name="see-also"></a>请参阅
如需详细了解如何部署和使用这些客户端，请参阅以下文档：

- [Azure 信息保护客户端](AIP-client.md)

- [Azure 信息保护统一标记客户端](unifiedlabelingclient-version-release-history.md)

- [RMS 客户端部署说明](client-deployment-notes.md)

虽然 Azure 信息保护客户端可以与 AD RMS 一起使用，但 Azure 信息保护客户端最适合用于其 Azure 服务；Azure 信息保护及其数据保护服务（Azure 权限管理）。 有关 Azure 信息保护服务端的比较，请参阅[比较 Azure 信息保护与 AD RMS](../compare-on-premise.md)。
