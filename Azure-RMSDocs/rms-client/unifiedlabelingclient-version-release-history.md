---
title: Azure 信息保护统一标签客户端版本历史记录 & 支持策略
description: 了解 Azure 信息保护的新功能 (AIP) 适用于 Windows 的统一标签客户端。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7da6699fb2640791f78972f4271a6d846405731a
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583670"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure 信息保护统一标签客户端-版本发行历史记录和支持策略

>***适用于**： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，Windows 8，Windows Server 2019，Windows Server 2016，windows Server 2012 R2，windows server 2012 *
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP For Windows And office 版本中的扩展支持](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)。*
>
>***相关的**： [仅限 AIP 统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 对于经典客户端，请参阅 [AIP 经典客户端版本发行历史记录和支持策略](client-version-release-history.md)。 *

你可以从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载 Azure 信息保护统一标签客户端。

在通常几周的短暂延迟后，最新的正式发行版也包含在 Microsoft 更新目录中。 Azure 信息保护版本具有 Microsoft Azure 信息保护的产品名  >  **Microsoft Azure 信息保护统一标签客户端** 和 **更新** 分类。

如果在目录中包括 Azure 信息保护，则意味着可以使用 WSUS 或 Configuration Manager 或使用 Microsoft 更新的其他软件部署机制来升级客户端。

有关详细信息，请参阅 [升级和维护 Azure 信息保护统一标签客户端](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)。

## <a name="servicing-information-and-timelines"></a>维护信息和日程表

版本的 Azure 信息保护统一标签客户端 (GA) 版本的每个正式发行版在发布后续版本后的六个月内受支持。 文档不包括关于不支持的客户端版本的信息。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

所述的 Azure 信息保护功能目前以预览版提供。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。

### <a name="general-availability-versions-that-are-no-longer-supported"></a>不再支持的常规可用性版本

|客户端版本|发布日期|
|--------------|-------------|
|2.5.33.0 |2019/10/23|
|2.2.21.0|09/03/2019|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|
| | |

此页上使用的日期格式为 *月/日/年*。

### <a name="release-information"></a>发布信息

使用以下信息可查看 Windows 的支持版本的 Azure 信息保护统一标签客户端的新增功能或更改的内容。 最新版本会最先列出。 此页上使用的日期格式为 *月/日/年*。

最新版本的 Azure 信息保护当前为预览版。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。

> [!NOTE]
> 不会列出小修补程序，因此，如果你遇到与统一标签客户端有关的问题，我们建议你检查是否已通过最新的 GA 版本修复了此问题。 如果问题仍然存在，请检查当前预览版本 (（如果有）) 。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

统一标签客户端取代了 Azure 信息保护经典客户端。 若要将特性和功能与经典客户端进行比较，请参阅 [比较适用于 Windows 计算机的标记解决方案](use-client.md#compare-the-labeling-solutions-for-windows-computers)。

## <a name="version-291090-public-preview"></a>版本 2.9.109.0 (公共预览版) 

统一标记扫描器和客户端版本2.9.109。0

**版本** 12/16/2020

此版本包括以下新功能、修补程序和增强功能，适用于统一标记扫描器和客户端：

- **用于扫描程序的新功能**：

    - [对断开连接的扫描程序服务器的 PowerShell 支持](#powershell-support-for-disconnected-scanner-servers)
    - [内容扫描作业中的 NFS 存储库支持](#support-for-nfs-repositories-in-content-scan-jobs)
    - [添加了对其他敏感信息类型的支持](#added-support-for-additional-sensitive-information-types)

- **适用于客户端的新功能**：

    - [跟踪文档访问权限并撤消访问权限](#track-document-access-and-revoke-access)
    - [添加了对其他敏感信息类型的支持](#added-support-for-additional-sensitive-information-types)

- **修补和改进：**

    - [统一标签扫描程序的修复和改进](#fixes-and-improvements-for-the-unified-labeling-scanner)
    - [统一标签客户端的修复和改进](#fixes-and-improvements-for-the-unified-labeling-client)

### <a name="powershell-support-for-disconnected-scanner-servers"></a>对断开连接的扫描程序服务器的 PowerShell 支持

[Azure 信息保护本地扫描器](../deploy-aip-scanner.md)现在支持管理内容扫描作业，适用于无法通过 PowerShell 连接到 internet 的扫描仪服务器。

为了支持断开连接的扫描程序服务器，我们添加了以下新 cmdlet：

|Cmdlet  |说明  |
|---------|---------|
|**[AIPScannerRepository](/powershell/module/azureinformationprotection/add-aipscannerrepository)**     | 将新存储库添加到内容扫描作业。        |
|**[AIPScannerContentScanJob](/powershell/module/azureinformationprotection/get-aipscannercontentscanjob)**     |      获取有关内容扫描作业的详细信息。   |
|**[AIPScannerRepository](/powershell/module/azureinformationprotection/get-aipscannerrepository)**     |  获取有关为内容扫描作业定义的存储库的详细信息。       |
|**[AIPScannerContentScanJob](/powershell/module/azureinformationprotection/remove-aipscannercontentscanjob)**       |    删除内容扫描作业。     |
| **[AIPScannerRepository](/powershell/module/azureinformationprotection/remove-aipscannerrepository)**    |   从内容扫描作业中删除存储库。      |
|**[AIPScannerContentScanJob](/powershell/module/azureinformationprotection/set-aipscannercontentscanjob)**     |   定义内容扫描作业的设置。      |
**[Set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository)**     |   定义内容扫描作业中现有存储库的设置。      |
| | |

还添加了 [**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/set-mipnetworkdiscovery) cmdlet 以提供额外支持，使你能够通过 PowerShell 更新网络发现服务的安装设置。

有关详细信息，请参阅 [扫描程序服务器何时无法建立 internet 连接](../deploy-aip-scanner-prereqs.md#restriction-the-scanner-server-cannot-have-internet-connectivity) 和 [配置扫描仪](../deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal)。

### <a name="support-for-nfs-repositories-in-content-scan-jobs"></a>内容扫描作业中的 NFS 存储库支持

现在，除了 SMB 文件共享和 SharePoint 存储库外，还可以将 NFS 存储库添加到内容扫描作业。

若要支持对 NFS 共享的扫描，必须在扫描仪计算机上部署 NFS 服务：

1. 在计算机上，导航到 **Windows 功能 (打开或关闭 windows 功能) 设置 "** 对话框。

1. 选择以下项：

    - **NFS 服务**
        - **管理工具**
        - **NFS 客户端**

有关详细信息，请参阅 [创建内容扫描作业](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job)。

### <a name="added-support-for-additional-sensitive-information-types"></a>添加了对其他敏感信息类型的支持

我们在 Azure 信息保护中添加了对其他敏感信息类型的支持，如 **澳大利亚商业号码**、 **澳大利亚公司编号** 或 **奥地利标识卡。**

有关详细信息，请参阅 Microsoft 365 文档中的 [敏感信息类型实体定义](/microsoft-365/compliance/sensitive-information-type-entity-definitions) 。

### <a name="track-document-access-and-revoke-access"></a>跟踪文档访问权限并撤消访问权限

升级到版本2.9.109.0 后，尚未注册跟踪的所有文档将在下一次在安装了 AIP 统一标签客户端的计算机上打开。

让你的文档注册到跟踪使管理员能够使用 PowerShell 来跟踪文档访问，并在需要时撤销访问权限。

升级后，最终用户还可以撤消对已保护文档的访问权限。 若要撤消 Microsoft Office 应用的访问权限，请使用 "**敏感度**" 菜单上的 "新建 **吊销访问权限**" 选项。

有关详细信息，请参阅：

- [管理员指南：使用 Azure 信息保护跟踪和撤消文档访问](track-and-revoke-admin.md)
- [用户指南：使用 Azure 信息保护撤销文档访问](revoke-access-user.md)
- [跟踪和撤消文档访问的已知问题](../known-issues.md#tracking-and-revoking-document-access-public-preview)

### <a name="fixes-and-improvements-for-the-unified-labeling-scanner"></a>统一标签扫描程序的修复和改进

[Azure 信息保护统一标记扫描器](../deploy-aip-scanner.md)的版本2.9.109.0 中提供了以下修补程序：

- 添加了对 **-**) [扫描程序数据库](../deploy-aip-scanner-prereqs.md) 名称中的连字符 (的支持
- 当 "**[基于内容的标签文件](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job)**" 选项设置为 "**关闭**" 时，报表中的更新
- [改进了](../deploy-aip-scanner-configure-install.md#optimizing-scanner-performance) 大量信息类型匹配的内存消耗
- 支持以斜杠 (结尾的 [SharePoint 本地](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) 路径 **/**) 
- 提高了 SharePoint 扫描 [速度](../deploy-aip-scanner-configure-install.md#optimizing-scanner-performance)

- 支持在扫描 SharePoint 服务器时 [避免超时](clientv2-admin-guide-customizations.md#avoid-scanner-timeouts-in-sharepoint) 。

### <a name="fixes-and-improvements-for-the-unified-labeling-client"></a>统一标签客户端的修复和改进

- 已修复 Office MSI [电子邮件](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-emails) 中的标签问题，例如答复或转发电子邮件。

- [NewLabel 审核日志](../audit-logs.md#new-label-audit-logs) 事件现在包含操作源，适用于从 Outlook 发送的电子邮件生成的事件。

- [在 Microsoft 365 中更改标签策略](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)后，在不清除缓存的情况下，已修复的问题。

- Outlook 预览模式现在 [为发现事件生成审核日志](../audit-logs.md#discover-audit-logs)

- [建议的标签](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) 和 [水印](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) 在 Outlook 中按预期方式应用。 

- 为通讯组列表中的联系人添加了对 [OutlookBlockTrustedDomains](clientv2-admin-guide-customizations.md#to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels) 和 [OutlookBlockUntrustedCollaborationLabel](clientv2-admin-guide-customizations.md#to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels) 设置的支持。

    若要对此进行配置，请将 [EnableOutlookDistributionListExpansion](clientv2-admin-guide-customizations.md#to-implement-block-messages-for-recipients-inside-an-outlook-distribution-list-public-preview) 值设置为 **true**。 你可能还希望引发默认超时值，如 [OutlookGetEmailAddressesTimeOutMSProperty](clientv2-admin-guide-customizations.md#to-implement-block-messages-for-recipients-inside-an-outlook-distribution-list-public-preview) 设置中所定义。

- 如果为用户配置了多个标签策略，每个标签策略都有冲突的高级设置，则将更新为使用的 [优先级顺序](clientv2-admin-guide-customizations.md#order-of-precedence---how-conflicting-settings-are-resolved) 。

    在这种情况下，将始终应用来自第一个策略的高级设置，具体取决于管理中心中策略的顺序。 现已删除 *OutlookDefaultLabel* 的异常。

- 在 **% APPDATA% (AppData\Roaming)** 指向非默认 Windows 文件夹结构的方案中，现在，映射到用户目录的文件夹中的文件会根据配置，按预期方式 [从标记和保护中排除](clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection) 。

- [新的高级客户端设置](clientv2-admin-guide-customizations.md#remove-all-shapes-of-a-specific-shape-name) (**PowerPointRemoveAllShapesByShapeName**) ，通过使用形状名称而不是形状内的文本，将其添加到从 PowerPoint 页眉或页脚中删除形状。

## <a name="version-28850"></a>版本2.8.85。0

统一标记扫描器和客户端版本2.8.85。0

**发布** 09/22/2020

此版本包括以下新功能、修复和增强功能，适用于统一标记扫描器和客户端：

- **用于扫描程序的新功能**：

    - [对检测到的更改进行可选的完全重新扫描](#optional-full-rescans-for-changes-detected)
    - [配置 SharePoint 超时](#configure-sharepoint-timeouts)
    - [网络发现支持](#network-discovery-support)

- **适用于客户端的新功能**：

    - [Outlook 中 AIP 弹出窗口的管理员自定义](#administrator-customizations-for-aip-popups-in-outlook)
    - [针对理由提示的管理员自定义](#administrator-customizations-for-justification-prompts)
    - [审核日志更新](#audit-log-updates)
    - [基于 DKE 模板的标记更新](#dke-template-based-labeling-updates)

- **修补和改进：**

    - [扫描程序的修复和改进](#azure-information-protection-scanner-fixed-issues-version-28850)
    - [客户端修复和改进](#azure-information-protection-client-fixed-issues-version-28850)


### <a name="optional-full-rescans-for-changes-detected"></a>对检测到的更改进行可选的完全重新扫描

管理员现在可以在对策略或内容扫描作业进行更改后跳过完全重新扫描。 跳过完全重新扫描仅对自上次扫描以来已修改或创建的文件应用所做的更改。

例如，你可能已进行了更改，这些更改仅影响最终用户（例如在视觉标记中），并且不需要花费时间立即运行完全扫描。

跳过完全、立即重新扫描，稍后返回以 [运行完整的重新扫描](../deploy-aip-scanner-manage.md#rescanning-files) 并将更改应用到存储库。

> [!IMPORTANT]
> 更改其策略和内容扫描作业的管理员现在必须了解这些更改对内容的影响，并确定是否需要完全重新扫描。
>
> 例如，如果你已将 "**强制 = 关闭**"**策略强制** 设置更改为 **"强制 = 启用**"，请确保运行完整的 "重新扫描" 以在内容中应用标签。
>

### <a name="configure-sharepoint-timeouts"></a>配置 SharePoint 超时

SharePoint 交互的默认超时时间已更新为两分钟，超过此时间后，尝试的 AIP 操作将失败。

AIP 管理员现在还可以为所有 web 请求和文件 web 请求单独配置 SharePoint 超时。

有关详细信息，请参阅 [配置 SharePoint 超时](clientv2-admin-guide-customizations.md#configure-sharepoint-timeouts)。

### <a name="network-discovery-support"></a>网络发现支持

统一的标记扫描器现在包含一个新的 **网络发现** 服务，使用它可以扫描指定的 IP 地址或可能包含敏感内容的网络文件共享的范围。

**网络发现** 服务会根据发现的权限和访问权限，使用可能存在风险的共享位置列表更新 **存储库** 报告。 检查更新的 **存储库** 报告，以确保内容扫描作业包括需要扫描的所有存储库。

> [!TIP]
> 有关详细信息，请参阅 [网络发现 cmdlet](#network-discovery-cmdlets)。

**使用网络发现服务**

1. 升级扫描仪版本，并确保扫描仪群集配置正确。 有关详细信息，请参阅：
    - [升级扫描仪](../deploy-aip-scanner-configure-install.md#upgrading-your-scanner)
    - [创建扫描仪群集](../deploy-aip-scanner-configure-install.md#create-a-scanner-cluster)

1. 请确保已启用 Azure 信息保护分析。

    在 Azure 门户中，请参阅 **Azure 信息保护 > 管理 > 配置分析 (预览版) 。**

    有关详细信息，请参阅 [Azure 信息保护的中心报告 (公共预览版) ](../reports-aip.md)。

1. 通过运行 [**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) PowerShell Cmdlet 启用网络发现。

    > [!IMPORTANT]
    > 运行此 cmdlet 时，请确保使用弱用户作为 **StandardDomainsUserAccount** 参数的值，以确保报告对存储库的任何公共访问。
    >
    > 此用户必须是 " **域用户** " 组的成员，并且用于模拟对存储库的公共访问权限。

1. 在 Azure 门户中，请参阅 Azure 信息保护 > **网络扫描作业** ，并 [创建作业来扫描网络的特定区域](../deploy-aip-scanner-configure-install.md#create-a-network-scan-job-public-preview)。

1. 使用 "新建 [**存储库**](../deploy-aip-scanner-configure-install.md#analyze-risky-repositories-found-public-preview) " 窗格上生成的报表查找可能存在风险的其他网络文件共享。 将所有危险的文件共享添加到 [内容扫描作业](../deploy-aip-scanner-configure-install.md#create-a-content-scan-job) ，以扫描添加的存储库中的敏感内容。

#### <a name="network-discovery-cmdlets"></a>网络发现 cmdlet

为网络发现添加的 PowerShell cmdlet 包括：

|Cmdlet  |说明  |
|---------|---------|
|[**MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryConfiguration)     |   获取网络发现服务是否从默认的、联机配置或从 Azure 门户导出的脱机文件中提取网络扫描数据的当前设置。      |
|[**MIPNetworkDiscoveryJobs**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryJobs)     |    获取当前配置的网络扫描作业的列表。     |
|[**MIPNetworkDiscoveryStatus**](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryStatus)     |     获取租户中配置的所有网络扫描作业的当前状态。    |
| [**导入-MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Import-MIPNetworkDiscoveryConfiguration)     |    从文件导入网络扫描作业的配置。     |
| [**安装-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery)| 安装网络发现服务 |
|[**MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Set-MIPNetworkDiscoveryConfiguration)     |   设置网络发现服务是否从默认的、联机配置或从 Azure 门户导出的脱机文件中提取网络扫描数据的配置。      |
|[**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Start-MIPNetworkDiscovery)     |  立即运行特定网络扫描作业。       |
|[**卸载-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Uninstall-MIPNetworkDiscovery)     |  卸载网络发现服务。       |
| | |


### <a name="administrator-customizations-for-aip-popups-in-outlook"></a>Outlook 中 AIP 弹出窗口的管理员自定义

AIP 管理员现在可以为最终用户自定义显示在 Outlook 中的弹出窗口，如用于阻止的电子邮件、警告消息和理由提示的弹出窗口。

有关常见用例方案的详细信息（包括几个示例规则），请参阅 [自定义 Outlook 弹出消息](clientv2-admin-guide-customizations.md#customize-outlook-popup-messages)。

### <a name="administrator-customizations-for-justification-prompts"></a>针对理由提示的管理员自定义

AIP 管理员现在可以在最终用户更改文档和电子邮件的分类标签时显示的理由提示中自定义其中一个选项。

有关详细信息，请参阅 [自定义已修改标签的理由提示文本](clientv2-admin-guide-customizations.md#customize-justification-prompt-texts-for-modified-labels)。

### <a name="audit-log-updates"></a>审核日志更新

现在，仅当用户打开标记或受保护的文件时，才会发送来自统一标签客户端的访问事件的审核日志，提供用户访问的更清晰的指示。

有关详细信息，请参阅 [访问审核日志](../audit-logs.md#access-audit-logs)。

### <a name="dke-template-based-labeling-updates"></a>基于 DKE 模板的标记更新

Azure 信息保护现在支持使用双密钥加密 (DKE 在扫描仪中进行基于) 模板的标记，以及使用文件资源管理器和 PowerShell。

有关详细信息，请参阅：

- [规划和实现 Azure 信息保护租户密钥](../plan-implement-tenant-key.md)
- Microsoft 365 文档中的[双密钥加密](/microsoft-365/compliance/double-key-encryption)

### <a name="azure-information-protection-scanner-fixed-issues-version-28850"></a>Azure 信息保护扫描程序修复了版本2.8.85.0 的问题

Azure 信息保护统一标记扫描器的版本2.8.85.0 中提供了以下修补程序：

- [扫描包含长路径的文件](../deploy-aip-scanner-prereqs.md#file-path-requirements)的改进
- 如果有多个 ContentDatabases，AIP 扫描器现在会扫描完整的 [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) 环境。
- AIP 扫描器现在支持在路径中有句点的 [SharePoint](../deploy-aip-scanner-prereqs.md#sharepoint-requirements) 文件，但不支持扩展。 例如， `https://sharepoint.contoso.com/shared documents/meeting-notes` 现在已成功扫描路径为、无扩展名的文件。
- AIP 扫描器现在支持在 Microsoft 安全性和符合性中心创建的 [自定义敏感信息类型](../deploy-aip-scanner-configure-install.md#identify-all-custom-conditions-and-known-sensitive-information-types) ，并且不属于任何策略。

### <a name="azure-information-protection-client-fixed-issues-version-28850"></a>Azure 信息保护客户端已修复问题，版本2.8.85。0

Azure 信息保护统一标签客户端的版本2.8.85.0 中提供了以下修补程序：

- 新的解说指示，适用于 Office 应用中的 "**敏感度**![列" 图标](../media/selected-sensitivity-options.png "列图标")菜单中当前选定的任何项。 有关详细信息，请参阅 [Microsoft 365 文档中有关敏感度标签](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do)的页面。
- 用于在[AIP 查看器](clientv2-view-use-files.md)中查看 JPEG 文件的修复
- 降级标签现在会自动在 [审核事件](../audit-logs.md#downgrade-label-audit-logs)中包含 **ProtectionOwnerBefore**
- 更改事件现在包含 [审核日志](../audit-logs.md#change-protection-audit-logs)中的 **LastModifiedDate**
- 添加了在使用代理获取令牌时对 **代理 pac** 文件的支持。 有关详细信息，请参阅 [防火墙和网络基础结构要求](../requirements.md#firewalls-and-network-infrastructure)。
- [刷新策略](../configure-policy.md#making-changes-to-the-policy)时进行身份验证的修复
- 用于在只读模式下标记 PowerPoint 更新的 [自动内容](../configure-policy-markings.md) 的修复
- 弹出窗口和错误文本的改进
- 工具提示将更新以显示 [电子邮件附件](../faqs-infoprotect.md#when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling)的最高分类，同时考虑电子邮件和附件的分类。
- 当使用 [**LabelPolicy**](/powershell/module/exchange/set-labelpolicy) cmdlet 修改敏感度标记策略时 **报告问题** 文本
- 修复了 [**set-aipfilelabel**](/powershell/module/azureinformationprotection/set-aipfilelabel) cmdlet 与无效标签 ID 一起使用时显示的错误。
- 用于在 Outlook 阅读窗格中解密 SMIME 电子邮件的性能修复。 若要实现此修补程序，请启用 [**OutlookSkipSmimeOnReadingPaneEnabled**](clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) 高级属性。
- 用于解密包含密码加密文件的 [PST 文件](clientv2-admin-guide-file-types.md) 的修补程序。 如果 PST 文件包含受密码保护的文件，则无法再对 PST 文件进行解密。
- 删除未包含在作用域内策略中的保护标签现在会同时从内容中删除标签和保护。

## <a name="version-271010"></a>版本2.7.101。0

统一标记扫描器和客户端版本2.7.101。0

**发布** 08/23/2020

**修复**：

修复了 PPT、Excel 和 Word 用户的问题，该问题导致文件冻结、崩溃或强制重复与配置了保护、水印和/或内容标记的必需标签相关的保存。

## <a name="version-27990"></a>版本2.7.99。0

统一标记扫描器和客户端版本2.7.99。0

**发布** 07/20/2020

**修补和改进**：

修复了 **新标签** 审核日志的文件标记操作中的问题。

有关详细信息，请参阅 [版本 2.7.96.0](#version-27960) 和 [Azure 信息保护审核日志参考 (公共预览版) ](../audit-logs.md)。

## <a name="version-27960"></a>版本2.7.96。0

统一标记扫描器和客户端版本2.7.96。0

**发布** 06/29/2020

- [适用于统一标签客户端的新功能，版本2.7.96。0](#new-features-for-the-unified-labeling-client-version-27960)
- [适用于统一标记扫描器的新功能，版本2.7.96。0](#new-features-for-the-unified-labeling-scanner-version-27960)
- [为删除的文件生成的新审核日志](#new-audit-logs-generated-for-removed-files)
- [强制执行 TLS 1.2](#tls-12-enforcement)
- [修补和改进，版本2.7.96。0](#fixes-and-improvements-version-27960)
### <a name="new-features-for-the-unified-labeling-scanner-version-27960"></a>适用于统一标记扫描器的新功能，版本2.7.96。0

- [使用扫描器基于建议的条件应用标签](../deploy-aip-scanner-prereqs.md)。 AIP 客户现可选择仅实现服务端 autolabeling。 此功能可让 AIP 最终用户始终遵循建议，而不是上一方案，只是在用户端启用了自动标记。

- [了解扫描程序以前发现的哪些文件已从扫描的存储库中删除](../reports-aip.md) 这些删除的文件之前未在 AIP 分析中报告，现已在 "扫描程序发现报告" 中提供。

- [在出现故障时从扫描仪获取报告以应用操作事件](../reports-aip.md#friendly-schema-reference-for-event-functions)。 使用报表来了解失败的操作事件，并发现阻止将来出现的方法。

- 介绍了 AIP scanner 诊断分析器工具，用于检测和分析常见扫描程序错误。 若要开始使用 AIP scanner 诊断，请 [运行新的 **AIPScannerDiagnostics** cmdlet](../deploy-aip-scanner-manage.md#troubleshooting-using-the-scanner-diagnostic-tool)。

- 你现在可以管理和限制扫描仪计算机上的最大 CPU 消耗。 了解如何使用 [两个新的高级设置 **ScannerMaxCPU** 和 **ScannerMinCPU**](./clientv2-admin-guide-customizations.md#limit-cpu-consumption)阻止100% 的 cpu 使用率并管理 cpu 使用情况。

- 现在，你可以根据文件属性配置统一标记扫描器来跳过特定文件。 定义文件属性列表，这些属性使用 new **[ScannerFSAttributesToSkip](clientv2-admin-guide-customizations.md#skip-or-ignore-files-during-scans-depending-on-file-attributes)** advanced 设置触发要跳过的文件。

### <a name="new-features-for-the-unified-labeling-client-version-27960"></a>适用于统一标签客户端的新功能，版本2.7.96。0

- 现在，在对统一标签客户端中的默认标签所做的更改时，将显示 [**对齐弹出窗口**](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)。

- 与 Office 应用的视觉内容标记更流畅地集成。 有关在 Office 文档中配置内容标记的详细信息，请参阅 [如何为 Azure 信息保护配置用于视觉标记的标签](../configure-policy-markings.md)。

- 新的 **WordShapeNameToRemove** advanced 属性允许删除第三方应用程序进行的 Word 文档中的内容标记。 详细了解如何 [识别现有的形状名称，以及如何使用 **WordShapeNameToRemove** 将其定义为删除](./clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)。

-  (公共预览版) **(DKE) 支持双重密钥加密** 。

    现在，你可以使用统一的标签客户端来保护高度敏感的内容，同时保持对密钥的完全控制。 DKE 要求使用两个密钥来访问受保护的内容：一个密钥存储在 Azure 中，另一个密钥由客户持有。

    有关默认的基于云的租户根密钥的详细信息，请参阅 [计划和实现 Azure 信息保护租户密钥](../plan-implement-tenant-key.md)。 有关实现双重密钥加密的信息，请参阅 Microsoft 365 文档中的 [双密钥加密](/microsoft-365/compliance/double-key-encryption) 。

### <a name="new-audit-logs-generated-for-removed-files"></a>为删除的文件生成的新审核日志

现在，每次扫描程序检测到现在已被删除的文件之前，都会生成审核日志。

有关详细信息，请参阅：

- [文件已删除审核日志](../audit-logs.md#file-removed-audit-logs)
- [Azure 信息保护的中央报告](../reports-aip.md)

> [!IMPORTANT]
> 在此版本中，文件标记操作不会生成 **新的标签** 审核日志。
> 如果在 **强制 = On** 模式下运行扫描程序，我们建议升级到 [版本 2.7.99.0](#version-27990)。
>

### <a name="tls-12-enforcement"></a>强制执行 TLS 1.2

从此版本的 Azure 信息保护客户端开始，仅支持 TLS 版本1.2 或更高版本。

TLS 安装程序不支持 TLS 1.2 的客户必须转到支持 TLS 1.2 的安装程序，才能使用 Azure 信息保护策略、令牌、审核和保护，并接收基于 Azure 信息保护的通信。

有关更多要求详细信息，请参阅 [防火墙和网络基础结构要求](../requirements.md#firewalls-and-network-infrastructure)。

### <a name="fixes-and-improvements-version-27960"></a>修补和改进，版本2.7.96。0

- 的扫描程序 SQL 改进：
    - 性能
    - 具有大量信息类型的文件

- 的 SharePoint 扫描改进：
    - 扫描性能
    - 路径中包含特殊字符的文件
    - 文件计数较大的库

    若要查看有关通过 SharePoint 使用 Azure 信息保护的快速入门，请参阅 [快速入门：查找本地存储的文件中的敏感信息](../quickstart-findsensitiveinfo.md)。

- 改善了缺少策略的用户通知。 有关统一标签客户端的标签策略的详细信息，请参阅 Microsoft 365 文档中的 [标签策略](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do) 。

- 现在，在 Excel 中，[自动标签](../configure-policy-classification.md)应用于用户在不保存的情况下开始关闭文件的情况，就像用户活动保存文件时。

- 当配置 [ExternalContentMarkingToRemove](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) 设置时，将按预期删除页眉和页脚，而不是在每个文档上保存。

- [动态用户变量](../configure-policy-markings.md#using-variables-in-the-text-string) 现在按预期方式显示在文档的视觉标记中。

- 只有 PDF 内容的第一页用于应用 autoclassification 规则的问题现已得到解决，基于 PDF 中所有内容的 autoclassification 现在按预期继续进行。 有关分类和标签的详细信息，请参阅 [分类和标签常见问题解答](../faqs-infoprotect.md)。

- 当配置了多个 Exchange 帐户并且启用了 Azure 信息保护 Outlook 客户端时，会按预期方式从辅助帐户发送邮件。 若要详细了解如何配置 Outlook 的统一标签客户端，请参阅 [Azure 信息保护统一标签客户端的其他先决条件](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)。

- 如果将具有较高机密性标签的文档拖放到电子邮件中，则该电子邮件现在会自动按预期方式接收更高的机密性标签。 有关对客户端功能进行标记的详细信息，请参阅 [标签客户端比较表](use-client.md#compare-the-labeling-solutions-for-windows-computers)。

- 如果电子邮件地址同时包含撇号 ( ") 和句点 (，则现在会按预期将自定义权限应用于电子邮件。 ) 有关使用 Outlook 配置统一标签客户端的详细信息，请参阅 [Azure 信息保护统一标签客户端的其他先决条件](clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)。

- 默认情况下，当文件由统一的标记扫描器、PowerShell 或文件资源管理器扩展标记时，文件的 NTFS 所有者将丢失。 现在，你可以通过将新的 **[UseCopyAndPreserveNTFSOwner](clientv2-admin-guide-customizations.md#preserve-ntfs-owners-during-labeling-public-preview)** advanced 设置设置为 **true**，将系统配置为保留文件的 NTFS 所有者。

    **UseCopyAndPreserveNTFSOwner** 高级设置要求在扫描仪和扫描的存储库之间具有低延迟、可靠的网络连接。

## <a name="version-261110"></a>版本2.6.111。0

**发布** 03/09/2020

支持，12/29/2020

### <a name="new-features-version-261110"></a>新功能，版本2.6.111。0

- [Scanner](../deploy-aip-scanner.md)的通用版本，用于检查和标记本地数据存储中的文档。

- [扫描仪](../deploy-aip-scanner.md) 相关：
    - [更轻松地进行本地 SharePoint 和子网站发现](../quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories)。 不再需要设置每个特定站点。
    - 添加了 [SQL 块区大小](../deploy-aip-scanner-prereqs.md#storage-requirements-and-capacity-planning-for-sql-server) 的高级属性。
    - 如果更改了默认标签，则管理员现在能够 [停止现有扫描并执行重新扫描](../deploy-aip-scanner-manage.md#stopping-a-scan) 。
    - 默认情况下，现在，扫描器会设置最小遥测数据，以提高扫描速度，缩短日志大小，并且信息类型现在会缓存在数据库中。 了解有关 [扫描仪优化](../deploy-aip-scanner-configure-install.md#optimizing-scanner-performance)的详细信息。
    - 现在，扫描仪支持对数据库和服务进行单独的部署，而只有数据库部署需要 **Sysadmin** 权限。
    - 对扫描程序性能的改进。

- 修改了 [PowerShell](./clientv2-admin-guide-powershell.md) cmdlet **set-aipfilelabel** 以允许从 PST、RAR、7zip 和 MSG 文件删除保护。 此功能在默认情况下处于禁用状态，必须使用[LabelPolicy](./clientv2-admin-guide-customizations.md) cmdlet 启用此功能[，如下所述。](./clientv2-admin-guide-customizations.md#enable-removal-of-protection-from-compressed-files)  

- 增加了 Azure 信息保护管理员控制何时使用 .pfile 扩展的能力。 详细了解如何 [更改受保护的文件类型](./clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)。

- 为应用程序和变量添加了动态视觉标记支持。 详细了解如何为 [视觉标记配置标签](../configure-policy-markings.md)。

- 对 [自动和建议标签的可自定义策略提示](use-client.md)进行了改进。

- 在统一标签客户端中，为 Office 应用添加了对 [脱机标签功能](./clientv2-admin-guide-customizations.md#support-for-disconnected-computers) 的支持。

### <a name="fixes-and-improvements-version-261110"></a>修补和改进，版本2.6.111。0

- 如果用户尝试不成功地打开受保护的 TIFF 文件，并且 tiff 文件是由 RightFax 创建的，则 TIFF 文件现在会打开并保持稳定。  
- 已解决受保护的 txt 和 PDF 文件的以前损坏。
- 更正了 Log Analytics 中的 **自动** 和 **手动** 标记之间的不一致标签。
- 新电子邮件和用户上一次打开的电子邮件之间确定的意外继承问题现已解决。  
- 将 **.msg** 文件作为 **pfile** 的保护现在按预期方式工作。
- 现在按预期方式应用从 Office 用户定义的设置中添加的共同所有者权限。
- 当输入权限降级理由时，如果已选择其他选项，则无法再输入文本。

## <a name="next-steps"></a>后续步骤

不确定是否要安装适合的客户端？  请参阅 [选择 Windows 标记解决方案](use-client.md#choose-your-windows-labeling-solution)。

有关安装和使用统一标签客户端的详细信息：

- 用户请参阅：[下载并安装客户端](install-unifiedlabelingclient-app.md)

- 对于管理员： [Azure 信息保护统一标签客户端管理员指南](clientv2-admin-guide.md)
