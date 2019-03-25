---
title: Azure 信息保护客户端
description: Microsoft Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的数据。 客户端（Azure 信息保护客户端或 Rights Management 客户端）与在计算机和移动设备上运行的应用程序集成。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 03/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ms.suite: ems
ms.openlocfilehash: f797ffc63e38c15649e5bf590ad11dd5a009e957
ms.sourcegitcommit: 3a3f1051c5a58c2bd2f230f1c8ece919df3dc23e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58221008"
---
# <a name="the-client-side-of-azure-information-protection"></a>Azure 信息保护的客户端

>适用范围：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的文档和电子邮件：

- 客户端可以是 Azure 信息保护客户端或 Rights Management 客户端，此客户端与在计算机和移动设备上运行的应用程序集成。 

- 服务驻留在云中（Azure 信息保护，它使用 Azure Rights Management 服务进行数据保护）或本地（Active Directory Rights Management Services，通常称为“AD RMS”）。 

除了无标签保护之外，Azure 信息保护客户端还支持分类和有标签保护。 此客户端与 Office 应用程序集成，必须单独安装。

某些应用程序将自动安装 Rights Management (RMS) 客户端，如 Office 应用程序、Azure 信息保护客户端和软件供应商提供的启用 RMS 的应用程序。 但是，它也可以[单独安装](https://www.microsoft.com/en-us/download/details.aspx?id=38396)，以支持[从受 IRM 保护的库和 OneDrive for Business 同步文件](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)，并供希望将权限管理保护集成到业务线应用程序中的开发人员使用。

## <a name="choose-which-azure-information-protection-client-to-use"></a>选择要使用的 Azure 信息保护客户端

从 Azure 门户下载标签和策略设置的 Azure 信息保护客户端具有普遍适用性，并提供用于测试新功能和修补程序的预览版本。 有关客户端这些版本的详细信息，请参阅 [Azure 信息保护客户端：版本发行历史记录和支持策略](client-version-release-history.md)。 

Azure 信息保护统一标记客户端从 Office 365 安全与合规中心下载标签和策略设置。 此客户端目前处于测试预览状态。 有关客户端此版本的详细信息，请参阅 [Azure 信息保护统一标记客户端：版本发布信息](unifiedlabelingclient-version-release-history.md)。

应该安装哪个客户端？

- 如果要在生产中进行部署，请使用正式发布的 Azure 信息保护客户端。

- 如果你处于测试和评估阶段，请使用其中一个预览客户端。
    
    目前，Azure 信息保护客户端和 Azure 信息保护统一标记客户端的预览版本没有针对功能的奇偶校验。 但是，之后应该会填补这个缺口，届时新功能将仅添加到 Azure 信息保护统一标记客户端。 因此，如果 Azure 信息保护统一标记客户端目前的功能集和功能可满足你的业务需求，建议使用它进行测试。 如果无法满足你的业务希求，或者如果你已在 Azure 门户中配置了标签，而这些标签尚未[迁移到统一标记存储](../configure-policy-migrate-labels.md)，请使用 Azure 信息保护客户端。

### <a name="feature-comparisons-for-the-clients"></a>客户端的功能比较

下表有助于比较两个当前预览版本支持的功能。

|功能|Azure 信息保护客户端|Azure Information Protection<br /> 统一标记客户端|
|-------|-----------------------------------|----------------------------------------------------|
|标记操作：手动、建议、自动| 是 | 是 |
|中心报告（分析）：| 是 | 是 |
|重置设置和导出日志：| 是 | 是 |
|用户定义的权限：| 是 | 仅适用于 Outlook（不要转发） |
|自定义权限：| 是 | 仅文件资源管理器 <br /><br /> 在 Office 应用程序中，作为替代方法，用户可以选择“文件信息” > “保护文档” > “限制访问” |
|Office 应用中的“信息保护”栏：| 是 | 是；但具有限制：<br /><br /> - 无标题或可自定义的工具提示<br /><br /> - 应用的标签未显示标签颜色|
|文件资源管理器，右键单击操作：| 是 | 是；但具有限制：<br /><br /> - 无法保护 .ppdf 格式的 PDF 文档 <br /><br />  - 不支持仅保护模式|
|受保护文件的查看器：| 是 | 是；但具有限制：<br /><br /> - 对于通用受保护文件 (.pfile)，无法将更改保存到最初打开的文件，这一点与 Azure 信息保护客户端中的查看器不同。|
|PowerShell 命令：| 是 | 是；但具有限制：<br /><br />- 包含以下 Cmdlet：[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)、[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)、[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />- 不包括直接连接到保护服务的 Cmdlet|
|离线支持保护操作：| 是 | 是；但具有限制： <br /><br />- 对于文件资源管理器和 PowerShell 命令，用户必须连接到 Internet 才能保护文件。 |
|HYOK 支持：| 是 | 否<br /><br /> 从 Azure 门户迁移的标签以及为 HYOK 保护配置的标签通过 Azure 信息保护统一标记客户端显示，但不应用保护。 |
|事件查看器的使用情况日志记录：| 是 | 否|
|来自电子邮件附件的标签继承：| 是 | 否 |
|在 Outlook 中显示“不可转发”按钮| 是 | 否 |
|包括以下内容的[自定义项](client-admin-guide-customizations.md#available-advanced-client-settings)：<br />- 电子邮件的默认标签<br />- 启用自定义权限 <br />- S/MIME 支持<br />- 报告问题选项| 是 | 否 |
|本地数据存储的扫描程序：| 是 | 否 |
|跟踪和撤销：| 是 | 否 |
|仅保护模式（无标签）：| 是 | 否 |
|Outlook 中的“不可转发”按钮：| 是 | 否 |
|多语言支持：| 是 | 否 |
|对 AD RMS 的支持：| 是 | 仅支持以下操作：<br /><br /> - 在你部署 [Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))时，查看器可打开受保护的文档|

#### <a name="functional-comparison-for-the-clients"></a>客户端的功能比较

如果两个客户端都支持相同的功能，可以查看下表来帮助确定两个当前预览版本之间的一些功能差异。

|功能 |Azure 信息保护客户端|Azure Information Protection<br /> 统一标记客户端|
|--------------|-----------------------------------|-----------------------------------------------------------|
|安装：| 安装本地演示策略的选项 | 没有本地演示策略|
|在 Office 应用程序中应用时的标签选择和显示：|通过功能区上的“保护”按钮 <br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|通过功能区上的“敏感度”按钮<br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|
|在 Office 应用程序中管理“信息保护”栏：|面向用户： <br /><br />- 从功能区上的“保护”按钮选择显示或隐藏栏<br /><br />- 如果用户选择隐藏栏，默认情况下，该栏在应用程序中隐藏，但会继续自动显示在新打开的应用程序中 <br /><br /> 面向管理员： <br /><br />- 在应用程序首次打开时，通过策略设置自动显示或隐藏栏，并控制在用户选择隐藏栏后，该栏是否对新打开的应用程序自动保持隐藏状态|面向用户： <br /><br />- 从功能区上的“敏感度”按钮选择显示或隐藏栏<br /><br />- 当用户选择隐藏栏时，该栏在该应用程序中以及新打开的应用程序中均处于隐藏状态 <br /><br />面向管理员： <br /><br />- 没有可用于管理栏的策略设置|
|标签颜色： | 在 Azure 门户中配置 | 在标签迁移到 Office 365 后保留 <br /><br /> 在安全与合规中心中创建的新标签没有颜色|
|策略更新： | 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 24 小时一次 | 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 4 小时一次|
|PDF 支持的格式：| 保护: <br /><br /> - PDF 加密的 ISO 标准（默认） <br /><br /> - .ppdf <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护| 保护: <br /><br /> - PDF 加密的 ISO 标准 <br /><br /> <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护|
|支持的 cmdlet：| [AzureInformatioProtection](/powershell/module/azureinformationprotection) 记录的所有 cmdlet | Set-AIPFileClassification 和 Set-AIPFileLabel 不支持 Owner 参数或 SharePoint Server 库 <br /><br /> 此外，对于未应用标签的所有场景，都有一条“无适用标签”的注释 <br /><br /> Set-AIPFileLabel 不支持 EnableTracking 参数 <br /><br /> Get-AIPFileStatus 不从其他租户返回标签信息，也不显示 RMSIssuedTime 参数<br /><br />另外，Get-AIPFileStatus 的 LabelingMethod  参数显示“特权”、“标准”或“自动”，而不显示“手动”或“自动”。 有关详细信息，请参阅[联机文档](/powershell/module/azureinformationprotection/get-aipfilestatus)。|
|Office 中每个操作的对齐方式提示（如果已配置）： | 频率:每个文件 <br /><br /> 降低敏感度级别 <br /><br /> 删除标签<br /><br /> 删除保护 | 频率:每个会话 <br /><br /> 降低敏感度级别<br /><br /> 删除标签|
|删除已应用的标签操作： | 系统提示用户确认 <br /><br />下次 Office 应用程序打开文件时，不会自动应用默认标签或自动标签（如果已配置）  <br /><br />| 不提示用户确认<br /><br /> 下次 Office 应用程序打开文件时，自动应用默认标签或自动标签（如果已配置）|
|自动分类和建议分类： | 在 Azure 门户中配置为[标签条件](../configure-policy-classification.md)，其中包含使用短语或正则表达式的内置信息类型和自定义条件 <br /><br />配置选项包括： <br /><br />- 唯一/非唯一计数 <br /><br /> - 最小计数| 在安全与合规中心中配置，包含内置敏感信息类型和[自定义信息类型](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)<br /><br />配置选项包括：  <br /><br />- 仅唯一计数 <br /><br />- 最小和最大计数 <br /><br />- 信息类型支持 AND 和 OR <br /><br />- 关键字字典<br /><br />- 可自定义的可信度和字符接近度|

要更详细地比较特定保护设置以了解其行为差异，请参阅[比较标签保护设置的行为](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label)。

#### <a name="features-that-will-not-be-in-the-azure-information-protection-unified-labeling-client"></a>不属于 Azure 信息保护统一标签客户端的功能

尽管 Azure 信息保护统一标签客户端仍处于开发阶段，但以下不同于 Azure 信息保护客户端的功能和行为，将不再于 Azure 信息保护统一标签客户端的未来发布中推出： 

- 在以下 Office 应用中自定义权限：Word、Excel 和 PowerPoint

- 从 Office 应用和文件资源浏览器中跟踪和撤销

- Azure 信息保护栏标题和工具提示

- PowerShell 和文件资源浏览器中的保护操作的脱机支持

- 仅保护模式（无标签）

- 将 PDF 文档作为 .ppdf 格式进行保护

- 在 Outlook 中显示“不可转发”按钮

- 演示策略

- 对删除保护的验证

- 删除应用的标签之前的确认提示

- “帮助和反馈”对话框中的“报告问题”链接

- 使用现有自定义属性（SyncPropertyName 和 SyncPropertyState 高级客户端设置）标记 Office 文档

- 连接到 Rights Management 服务的单独 PowerShell cmdlet

- AD RMS 仅保护模式


##### <a name="parent-labels-and-their-sublabels"></a>父标签及其子标签 

Azure 信息保护客户端不支持指定具有子标签的父标签的配置。 这些配置包括指定默认标签和推荐分类或自动分类的标签。 如果某个标签具有子标签，可以指定其中一个子标签，但不能指定父标签。

对于奇偶校验，Azure 信息保护统一标记客户端也不支持应用具有子标签的父标签，即使可以在 Office 365 安全与合规中心中选择这些标签，也无法应用。 在此方案中，Azure 信息保护统一标记客户端将不应用父标签。

## <a name="see-also"></a>另请参阅
如需详细了解如何部署和使用这些客户端，请参阅以下文档：

- [Azure 信息保护客户端](AIP-client.md)

- [Azure 信息保护统一标记客户端](unifiedlabelingclient-version-release-history.md)

- [RMS 客户端部署说明](client-deployment-notes.md)

虽然 Azure 信息保护客户端可以与 AD RMS 一起使用，但 Azure 信息保护客户端最适合用于其 Azure 服务；Azure 信息保护及其数据保护服务（Azure 权限管理）。 有关 Azure 信息保护服务端的比较，请参阅[比较 Azure 信息保护与 AD RMS](../compare-on-premise.md)。
