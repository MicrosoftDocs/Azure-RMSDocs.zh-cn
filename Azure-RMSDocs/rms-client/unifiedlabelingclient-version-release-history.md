---
title: Azure 信息保护统一标签客户端版本历史记录 & 支持策略
description: 请参阅适用于 Windows 的 Azure 信息保护统一标签客户端的发布信息。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b1e91bcbfca3d4f925750fd8d1f135bd8f4ff2c4
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/01/2020
ms.locfileid: "84250029"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure 信息保护统一标签客户端-版本发行历史记录和支持策略

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012*
>
> *适用于以下内容的说明： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

你可以从[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载 Azure 信息保护统一标签客户端。

在通常几周的短暂延迟后，最新的正式发行版还会包含在 Microsoft 更新目录中，该目录中包含产品名称**Microsoft Azure 信息保护**  >  **Microsoft Azure 信息保护统一标签客户端**和**更新**分类。 此目录包含此内容意味着可利用 WSUS/Configuration Manager 或其他使用 Microsoft 更新的软件部署机制来升级客户端。

有关详细信息，请参阅[升级和维护 Azure 信息保护统一标签客户端](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

Azure 信息保护统一标签客户端的每个正式发行版（GA）在发布后续版本后，最多可支持六个月。 文档不包括关于不支持的客户端版本的信息。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

不应在生产网络上为最终用户部署预览版本。 而是使用最新预览版来查看和试用即将在下一 GA 版本中推出的新功能或修补程序。 仅支持当前预览版。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>不再支持的常规可用性版本：

|客户端版本|发布日期|
|--------------|-------------|
|2.2.21.0|09/03/2019|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|

此页上使用的日期格式为*月/日/年*。


### <a name="release-information"></a>发布信息

使用以下信息可查看 Windows 的支持版本的 Azure 信息保护统一标签客户端的新增功能或更改的内容。 最新版本会最先列出。 此页上使用的日期格式为*月/日/年*。

> [!NOTE]
> 不会列出小修补程序，因此，如果你遇到与统一标签客户端有关的问题，我们建议你检查是否已通过最新的 GA 版本修复了此问题。 如果问题仍然存在，请检查当前预览版本（如果有）。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

此客户端正在替换 Azure 信息保护客户端（经典）。 若要将特性和功能与经典客户端进行比较，请参阅[比较适用于 Windows 计算机的标记客户端](use-client.md#compare-the-labeling-clients-for-windows-computers)。

## <a name="version-27950-public-preview"></a>版本2.7.95.0 公共预览版

统一标记扫描器和客户端（公共预览版）版本2.7.95。0

**发布**06/01/2020

**统一标记扫描器的新功能：**

- [使用扫描器基于建议的条件应用标签](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#prerequisites-for-the-azure-information-protection-scanner)。 AIP 客户现在可以选择实现仅自动标记服务端。 此功能使 AIP 的最终用户可以始终遵循建议，而不是在以前的方案中，仅在用户端启用了自动标记。

- [了解扫描程序以前发现的哪些文件已从扫描的存储库中删除](https://docs.microsoft.com/azure/information-protection/reports-aip)这些删除的文件之前未在 AIP 分析中报告，现已在 "扫描程序发现报告" 中提供。

- [在出现故障时从扫描仪获取报告以应用操作事件](https://docs.microsoft.com/azure/information-protection/reports-aip#friendly-schema-reference-for-event-functions)。 使用报表来了解失败的操作事件，并发现阻止将来出现的方法。 

- 介绍了 AIP scanner 诊断分析器工具，用于检测和分析常见扫描程序错误。 若要开始使用 AIP scanner 诊断，请[运行新的**AIPScannerDiagnostics** cmdlet](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#troubleshooting-using-scanner-diagnostic-tool)。 

- 你现在可以管理和限制扫描仪计算机上的最大 CPU 消耗。 了解如何使用[两个新的高级设置**ScannerMaxCPU**和**ScannerMinCPU**](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#limit-cpu-consumption)阻止100% 的 cpu 使用率并管理 cpu 使用情况。 

- 现在，你可以根据文件属性配置统一标记扫描器来跳过特定文件。 定义文件属性列表，这些属性使用 new **[ScannerFSAttributesToSkip](clientv2-admin-guide-customizations.md#skip-or-ignore-files-during-scans-depending-on-file-attributes-public-preview)** advanced 设置触发要跳过的文件。

**统一标签客户端的新功能：**

- 现在，在对统一标签客户端中的默认标签所做的更改时，将显示[对齐弹出窗口](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)。
    
- 与 Office 应用的视觉内容标记更流畅地集成。 有关在 Office 文档中配置内容标记的详细信息，请参阅[如何为 Azure 信息保护配置用于视觉标记的标签](../configure-policy-markings.md)。

- 新的**WordShapeNameToRemove** advanced 属性允许删除第三方应用程序进行的 Word 文档中的内容标记。 详细了解如何[识别现有的形状名称，以及如何使用**WordShapeNameToRemove**将其定义为删除](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#remove-headers-and-footers-from-other-labeling-solutions)。

**为删除的文件生成的新审核日志**

现在，每次扫描程序检测到现在已被删除的文件之前，都会生成审核日志。

有关详细信息，请参见:
- [文件已删除审核日志](../audit-logs.md#file-removed-audit-logs)
- [Azure 信息保护的中央报告](../reports-aip.md)

**强制执行 TLS 1.2**

从此版本的 Azure 信息保护客户端开始，仅支持 TLS 版本1.2 或更高版本。
    
TLS 安装程序不支持 TLS 1.2 的客户必须转到支持 TLS 1.2 的安装程序，以使用 Azure 信息保护策略、令牌、审核和保护，并接收基于 Azure 信息保护的通信。 
    
有关更多要求详细信息，请参阅[防火墙和网络基础结构要求](../requirements.md#firewalls-and-network-infrastructure)。

**修复和改进** 
- 的扫描程序 SQL 改进：
    - 性能
    - 具有大量信息类型的文件
    
- 的 SharePoint 扫描改进：
    - 扫描性能
    - 路径中包含特殊字符的文件
    - 文件计数较大的库
    
    若要查看有关通过 SharePoint 使用 Azure 信息保护的快速入门，请参阅[快速入门：查找本地存储的文件中的敏感信息](../quickstart-findsensitiveinfo.md)。
        
- 改善了缺少策略的用户通知。 有关统一标签客户端的标签策略的详细信息，请参阅 Microsoft 365 文档中的[标签策略](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do)。

- 现在，在 Excel 中，[自动标签](../configure-policy-classification.md)应用于用户在不保存的情况下开始关闭文件的情况，就像用户活动保存文件时。

- 当配置[ExternalContentMarkingToRemove](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)设置时，将按预期删除页眉和页脚，而不是在每个文档上保存。

- [动态用户变量](../configure-policy-markings.md#using-variables-in-the-text-string)现在按预期方式显示在文档的视觉标记中。

- 当配置了多个 Exchange 帐户并且启用了 Azure 信息保护 Outlook 客户端时，会按预期方式从辅助帐户发送邮件。 若要详细了解如何配置 Outlook 的统一标签客户端，请参阅[Azure 信息保护统一标签客户端的其他先决条件](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)。

- 如果将具有较高机密性标签的文档拖放到电子邮件中，则该电子邮件现在会自动按预期方式接收更高的机密性标签。 有关对客户端功能进行标记的详细信息，请参阅[标签客户端比较表](use-client.md#compare-the-labeling-clients-for-windows-computers)。

- 如果电子邮件地址同时包含撇号（'）和句点（.），则现在会按预期将自定义权限应用于电子邮件。若要详细了解如何配置 Outlook 的统一标签客户端，请参阅[Azure 信息保护统一标签客户端的其他先决条件](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)。

- 默认情况下，当文件由统一的标记扫描器、PowerShell 或文件资源管理器扩展标记时，文件的 NTFS 所有者将丢失。 现在，你可以通过将新的**[UseCopyAndPreserveNTFSOwner](clientv2-admin-guide-customizations.md#preserve-ntfs-owners-during-labeling-public-preview)** advanced 设置设置为**true**，将系统配置为保留文件的 NTFS 所有者。 

    **UseCopyAndPreserveNTFSOwner**高级设置要求在扫描仪和扫描的存储库之间具有低延迟、可靠的网络连接。


## <a name="version-261110"></a>版本2.6.111。0 

**发布**03/09/2020

**新功能：**

- [Scanner](../deploy-aip-scanner.md)的通用版本，用于检查和标记本地数据存储中的文档。 

- [扫描仪](../deploy-aip-scanner.md)相关：
    - [更轻松地进行本地 SharePoint 和子网站发现](https://docs.microsoft.com/azure/information-protection/quickstart-findsensitiveinfo#permission-users-to-scan-sharepoint-repositories)。 不再需要设置每个特定站点。 
    - 添加了[SQL 块区大小](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#storage-requirements-and-capacity-planning-for-sql-server)的高级属性。
    - 管理员现在可以[停止现有扫描，并](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#stop-a-scan)在对默认标签进行更改时执行重新扫描。
    - 默认情况下，现在，扫描器会设置最小遥测数据，以提高扫描速度，缩短日志大小，并且信息类型现在会缓存在数据库中。 了解有关[扫描仪优化](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#optimizing-the-performance-of-the-scanner)的详细信息。 
    - 现在，扫描仪支持对数据库和服务进行单独的部署，而只有数据库部署需要**Sysadmin**权限。
    - 对扫描程序性能的改进。 

- 修改[PowerShell](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-powershell) cmdlet **set-aipfilelabel**以允许从 PST、RAR、7zip 和 MSG 文件中删除保护。 此功能在默认情况下处于禁用状态，必须使用[LabelPolicy](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations) cmdlet 启用此功能[，如下所述。](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#enable-removal-of-protection-from-compressed-files)  

- 增加了 Azure 信息保护管理员控制何时使用 .pfile 扩展的能力。 详细了解如何[更改受保护的文件类型](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#change-which-file-types-to-protect)。 

- 为应用程序和变量添加了动态视觉标记支持。 详细了解如何为[视觉标记配置标签](https://docs.microsoft.com/azure/information-protection/configure-policy-markings)。 

- 对[自动和建议标签的可自定义策略提示](use-client.md)进行了改进。   

- 在统一标签客户端中，为 Office 应用添加了对[脱机标签功能](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#support-for-disconnected-computers)的支持。

**纠正**

- 如果用户尝试不成功地打开受保护的 TIFF 文件，并且 tiff 文件是由 RightFax 创建的，则 TIFF 文件现在会打开并保持稳定。  
- 已解决受保护的 txt 和 PDF 文件的以前损坏。
- 更正了 Log Analytics 中的**自动**和**手动**标记之间的不一致标签。 
- 新电子邮件和用户上一次打开的电子邮件之间确定的意外继承问题现已解决。  
- 将 .msg 文件作为 pfile 的保护现在按预期方式工作。 
- 现在按预期方式应用从 Office 用户定义的设置中添加的共同所有者权限。 
- 当输入权限降级理由时，如果已选择其他选项，则无法再输入文本。 


## <a name="version-25330"></a>版本2.5.33。0

**发布**日期：10/23/2019

支持，09/09/2020

**新功能：**

- 预览版本的[扫描仪](../deploy-aip-scanner.md)，用于检查和标记文档本地数据存储。 对于此版本的扫描仪：
    
    - 将扫描仪配置为使用同一扫描程序配置文件时，多个扫描程序可以共享相同的 SQL Server 数据库。 此配置可以更轻松地管理多个扫描仪，并缩短扫描时间。 当你使用此配置时，请始终等待扫描仪完成安装，然后再使用同一配置文件安装另一个扫描程序。
    
    - 安装扫描程序时必须指定配置文件，并将扫描程序数据库命名为**AIPScannerUL_ \<profile_name> **。 *配置文件*参数对于 install-aipscanner 是必需的。
    
    - 即使已标记文档，也可以在所有文档上设置一个默认标签。 在 "扫描程序配置文件" 或 "存储库设置" 中，将 "重新**标记文件**" 选项设置为 "**打开**"，并选择 "新建**强制默认标签**
    
    - 您可以删除所有文档中的现有标签，此操作包括删除保护（如果以前已被标签应用）。 将保留独立于标签的保护。 此扫描程序配置是在扫描程序配置文件或存储库设置中通过以下设置实现的：
        - **基于内容标记文件**：**关**
        - **默认标签**：**无**
        - 重新**标记文件**：**打开**并选中 "**强制默认标签**" 复选框
    
    - 与经典客户端的扫描程序一样，默认情况下，扫描程序可保护 Office 文件和 PDF 文件。 使用[PowerShell 高级设置](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)时，可保护其他文件类型。
    
    - 扫描程序周期的开始和完成时间的事件 Id 不写入 Windows 事件日志。 请改用 Azure 门户获取此信息。
    
    - 已知问题：不能将新的和重命名的标签选作扫描仪配置文件或存储库设置的默认标签。 解决方法：
        - 对于新标签：在 Azure 门户中，将要使用的[标签添加](../configure-policy-add-remove-label.md)到全局策略或作用域内策略。
        - 对于重命名标签：关闭再重新打开 Azure 门户。
    
    你可以从 Azure 信息保护客户端（经典）升级扫描仪。 在升级后，这会创建一个新的数据库，扫描程序在第一次运行时重新扫描所有文件。 有关说明，请参阅管理员指南中[的升级 Azure 信息保护扫描程序](clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)。
    
    有关其他信息，请参阅博客文章公告：[统一标签 AIP 扫描程序预览版增加了扩展功能！](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Unified-labeling-AIP-scanner-preview-brings-scaling-out-and-more/ba-p/862552)

- 如果要以非交互方式对文件进行标记，以及在 Azure AD 中注册应用的新过程，则 PowerShell cmdlet [set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)具有新参数（*AppId*、 *AppSecret*、 *TenantId*、 *DelegatedUser*和*OnBehalfOf*）。 示例方案包括用于标记文档的扫描程序和自动 PowerShell 脚本。 有关说明，请参阅如何从管理员指南以[非交互方式标记文件](clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)。
    
    请注意， *DelegatedUser*是自上次预览版本的统一标签客户端以来的新参数，并且已注册应用的 API 权限已更改。

- 新 PowerShell 标签策略高级设置，用于[更改要保护的文件类型](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)。

- 新 PowerShell 标签策略高级设置，用于将[标签迁移规则扩展到 SharePoint 属性](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-sharepoint-properties)。

- 将匹配的自定义敏感信息类型发送到[Azure 信息保护分析](../reports-aip.md)。

- 如果已[配置了颜色](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)，则应用的标签将显示该标签的配置颜色。

- 向标签中添加或更改保护设置时，客户端会在下一次保存文档时使用这些最新的保护设置重新应用标签。 同样，当下一次在 "强制" 模式下扫描文档时，扫描程序会将标签重新应用为这些最新的保护设置。

- 通过从一个客户端导出文件并手动将它们复制到断开连接的计算机上，[对断开连接的计算机的支持](clientv2-admin-guide-customizations.md#support-for-disconnected-computers)。 请注意，此配置支持通过文件资源管理器、PowerShell 和扫描器进行标记。 对于 Office 应用程序，不支持此配置。

- 新 cmdlet [AIPLogs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs)，用于从%localappdata%\Microsoft\MSIP\Logs 收集所有日志文件并将其保存到具有 .zip 格式的单个压缩文件中。 如果请求发送日志文件来帮助调查报告的问题，则可以将此文件发送到 Microsoft 支持部门。

**纠正**

- 您可以使用文件资源管理器成功地更改受保护的文件，并在删除该文件的密码之后右键单击。

- 您可以在查看器中成功打开本机保护的文件，而无需使用 "另存为"、"导出（导出）"[权限](../configure-usage-rights.md#usage-rights-and-descriptions)。

- 标签和策略设置按预期刷新，而不必运行[set-aipauthentication](/powershell/module/azureinformationprotection/clear-aipauthentication?)，或手动删除%LocalAppData%\Microsoft\MSIP\mip 文件夹。

**其他更改**

- [重置设置](clientv2-admin-guide.md#more-information-about-the-reset-settings-option)现在会删除%LocalAppData%\Microsoft\MSIP\mip \\ *\<ProcessName.exe\>* 文件夹，而不是%LocalAppData%\Microsoft\MSIP\mip \\ *\<ProcessName\>* \mip 文件夹。

- [Get-aipfilestatus](/powershell/module/azureinformationprotection/get-aipfilestatus)现在包含受保护文档的内容 ID。


## <a name="next-steps"></a>后续步骤

不确定是否要安装适合的客户端？  请参阅[选择要用于 Windows 计算机的标记客户端](use-client.md#choose-which-labeling-client-to-use-for-windows-computers)。

有关安装和使用统一标签客户端的详细信息： 

- 用户请参阅：[下载并安装客户端](install-unifiedlabelingclient-app.md)

- 对于管理员： [Azure 信息保护统一标签客户端管理员指南](clientv2-admin-guide.md)

