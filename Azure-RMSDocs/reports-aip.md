---
title: 'Azure 信息保护的分析和集中报告 (AIP) '
description: 了解如何使用 Azure 信息保护 (AIP) analytics 和中心报表来跟踪标签使用情况并识别包含敏感信息的文件。
author: batamig
ms.author: bagol
ms.date: 03/01/2021
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7d86ee43b7ccc60922dea88c76e9e0aa68474d26
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446943"
---
# <a name="analytics-and-central-reporting-for-azure-information-protection-public-preview"></a>Azure 信息保护的分析和集中报告 (公开预览版) 

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
>相关内容：*[AIP 统一标记客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

本文介绍如何使用 Azure 信息保护 (AIP) analytics 进行集中报告，这有助于跟踪对组织数据进行分类和保护的标签。 

AIP analytics 还能让你执行以下步骤：

- 监控组织中带标签和受保护的文档以及电子邮件

- 标识包含组织中的敏感信息的文档

- 监控用户对带标签文档和电子邮件的访问，并跟踪文档分类更改。

- 确定包含敏感信息且若未保护则可能给组织带来风险的文档，并按照以下建议缓解风险。

- 确定由内部或外部用户从 Windows 计算机访问受保护的文档的时间，以及是否授予或拒绝访问权限。

你看到的数据是从 Azure 信息保护客户端和扫描程序、从 Microsoft Cloud App Security、使用 Microsoft Defender 高级威胁防护的 Windows 10 计算机以及 [保护使用情况日志](log-analyze-usage.md)聚合而来的。 

用于中心报告的 Azure 信息保护分析目前处于预览阶段。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。 


## <a name="aip-reporting-data"></a>AIP 报表数据

例如，用于集中报表的 Azure 信息保护分析显示以下数据：

|报表  |显示的示例数据 |
|---------|---------|
|**使用情况报告**     |  选择时间段以显示以下任何内容： <br /><br />     -正在应用哪些标签 <br /><br />-正在标记的文档和电子邮件数量 <br /><br />-受保护的文档和电子邮件数量 <br /><br />-为文档和电子邮件标记了多少用户和多少设备 <br /><br />-正在使用哪些应用程序进行标记     |
|**活动日志**     | 选择时间段以显示以下任何内容： <br /><br />      -扫描程序以前发现的哪些文件已从扫描的存储库中删除 <br /> <br /> -特定用户执行了哪些标记操作 <br /><br /> -从特定设备执行了哪些标记操作<br /> <br />    -哪些用户访问了特定标记的文档<br /> <br />-对特定文件路径执行了哪些标记操作<br /> <br />-特定应用程序执行了哪些标签操作，如文件资源管理器和右键单击、PowerShell、扫描仪或 Microsoft Cloud App Security <br /> <br />-用户或拒绝用户访问哪些受保护的文档，即使这些用户未安装 Azure 信息保护客户端或组织外 <br /> <br />-向下钻取到报告文件，查看 **活动详细** 信息以了解其他信息      |
|**数据发现报表**     |      -扫描的数据存储库、Windows 10 计算机或运行 Azure 信息保护客户端的计算机上的文件 <br /><br />-标记和保护哪些文件，以及按标签列出文件的位置 <br /><br />-哪些文件包含已知类别的敏感信息，例如财务数据和个人信息，以及这些类别的文件位置       |
|**建议报表**     | -标识包含已知的敏感信息类型的未受保护的文件。 按照建议操作，可立即对其中一个标签配置相应的条件，以应用自动标签或推荐的标签。 **<br /> 如果遵循建议**：下一次用户打开文件或由 Azure 信息保护扫描程序进行扫描，则可以自动对文件进行分类和保护。 <br /><br /> -哪些数据存储库的文件具有标识的敏感信息，但未被 Azure 信息保护扫描。 按照建议操作，可立即向扫描程序的某个配置文件添加已标识的数据存储。 <br />   **如果遵循建议**：在下一个扫描程序周期中，可以自动对文件进行分类和保护。        |
| | |

报表使用 [Azure Monitor](/azure/log-analytics/log-analytics-overview) 将数据存储在组织拥有的 Log Analytics 工作区中。 如果你熟悉查询语言，可以修改这些查询，并创建新报表和 Power BI 仪表板。 你可能会发现以下教程有助于了解查询语言： [Azure Monitor 日志查询入门](/azure/azure-monitor/log-query/get-started-queries)。

有关详细信息，请参阅以下博客文章： 
- [Microsoft 信息保护中有关所有数据的数据发现、报告和分析](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)

- [通过 Azure 信息保护和 Microsoft Defender ATP 发现和保护敏感数据](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>收集和发送到 Microsoft 的信息

为了生成这些报表，终结点将以下类型的信息发送到 Microsoft：

- 标签操作。 例如，设置标签、更改标签、添加或删除保护、自动和建议的标签。

- 标签操作之前和之后的标签名称。

- 组织的租户 ID。

- 用户 ID（电子邮件地址或 UPN）。

- 用户设备的名称。

- 用户设备的 IP 地址。 

- 相关进程名称，如 **outlook** 或 **policy.msip**。

- 执行标记的应用程序的名称，如 **Outlook** 或 **文件资源管理器**

- 对于文档：被标记的文档的文件路径和文件名。

- 对于电子邮件：已标记的电子邮件的电子邮件主题和电子邮件发件人。 

- 在内容中已检测到的敏感信息类型（[预定义](/office365/securitycompliance/what-the-sensitive-information-types-look-for)和自定义）。

- Azure 信息保护客户端版本。

- 客户端操作系统版本。

此信息存储在组织拥有的 Azure Log Analytics 工作区中，并可供有权访问此工作区的用户从 Azure 信息保护独立查看。 

有关详细信息，请参阅：

- [Azure 信息保护分析必备的先决条件](#permissions-required-for-azure-information-protection-analytics)
- [使用 Azure 权限管理对 Log Analytics 工作区的访问](/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)
- [Azure 信息保护审核日志引用](audit-logs.md)

#### <a name="prevent-the-aip-clients-from-sending-auditing-data"></a>阻止 AIP 客户端发送审核数据

**统一标记客户端** 

若要防止 Azure 信息保护统一标签客户端发送审核数据，请配置标签策略 [高级设置](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics)。

**经典客户端**

若要防止 Azure 信息保护经典客户端发送此数据，请将 "**将审核数据发送到 Azure 信息保护分析**" 的 [策略设置](configure-policy-settings.md)设置为 "**关闭**"：

|要求  |说明  |
|---------|---------|
|**配置大多数用户以发送数据，其中包含无法发送数据的部分用户**     |  在用户子集的作用域内策略中，将 "向 **Azure 信息保护分析发送审核数据** " 设置为 " **关闭** "。 <br><br> 此配置专用于生产方案。     |
|**仅配置发送数据的部分用户**     |  在全局策略中将 "向 **Azure 信息保护分析发送审核数据** " 设置为 " **关闭** "，并在 "用户" 子集的作用域内策略中设置 **"打开** "。 <br><br>此配置专用于测试方案。       |
| | |

#### <a name="content-matches-for-deeper-analysis"></a>更深入分析的内容匹配项

Azure 信息保护允许收集和存储标识为敏感信息类型 (预定义或自定义) 的实际数据。 例如，这可以包括查找到的信用卡号码，以及社会安全号码、护照号码和银行帐户号码。 当你从 **活动日志** 中选择条目并查看 **活动详细信息** 时，将显示内容匹配。 

默认情况下，Azure 信息保护客户端不发送内容匹配项。 若要更改此行为以便发送内容匹配，请执行以下操作：

|客户端  |说明  |
|---------|---------|
|**统一标记客户端**      |  配置标签策略中的 [高级设置](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) 。       |
|**经典客户端**      |   选择一个复选框作为 Azure 信息保护分析 [配置](#configure-a-log-analytics-workspace-for-the-reports) 的一部分。 该复选框名为 " **启用对敏感数据的深度分析**"。 <br><br> 如果希望使用此客户端的大多数用户发送内容匹配项，但部分用户无法发送内容匹配项，请选中该复选框，然后在作用域内策略中为用户子集配置 [高级客户端设置](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) 。     |
|     |         |


## <a name="prerequisites"></a>必备条件
若要查看 Azure 信息保护报表和创建你自己的报表，请确保满足以下要求。

|要求  |详细信息  |
|---------|---------|
|**Azure 订阅**     |   Azure 订阅必须在与 Azure 信息保护相同的租户上包含 Log Analytics。 <br><br> 有关详细信息，请参阅 [Azure Monitor 定价](https://azure.microsoft.com/pricing/details/log-analytics) 页。 <br><br>如果没有 Azure 订阅或当前未使用 Azure Log Analytics，定价页将包含免费试用版的链接。   |
| **审核日志记录 URL 网络连接** | AIP 必须能够访问以下 Url，以便支持 AIP 审核日志：<br>- `https://*.events.data.microsoft.com` <br>- `https://*.aria.microsoft.com` 仅 (Android 设备数据) 
|**Azure 信息保护客户端**    |用于从客户端报告。 <br><br>如果尚未安装客户端，则可以从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载并安装统一的标签客户端。      <br><br>**注意**：支持统一标签客户端和经典客户端。 若要部署 AIP 经典客户端，请打开支持票证以获取下载访问权限。     |
|**Azure 信息保护本地扫描程序**    | 用于从本地数据存储区进行报告。 <br><br>      有关详细信息，请参阅 [部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。   |
|**Microsoft Cloud App Security (MCAS)**     | 用于从基于云的数据存储进行报告。 <br><br>有关详细信息，请参阅 MCAS 文档中的 [Azure 信息保护集成](/cloud-app-security/azip-integration) 。        |
|**Microsoft defender 高级威胁防护 (Microsoft Defender ATP) 的最小内部版本1809**     | 用于从 Windows 10 计算机进行报告。 <br>  <br>   你必须从 Microsoft Defender 安全中心启用 Azure 信息保护集成功能。 <br><br>有关详细信息，请参阅 [Windows 中的信息保护概述](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview)。   |
|     |         |


### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure 信息保护分析必备的先决条件

针对 Azure 信息保护分析，在配置 Azure Log Analytics 工作区后，可以使用安全读取者的 Azure AD 管理员角色替代 Azure 门户中支持管理 Azure 信息保护的其他 Azure AD 角色。 仅当你的租户不在 [统一标签平台](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)上时，才支持此附加角色。

由于 Azure 信息保护分析使用 Azure 监视功能，因此，基于角色的访问控制 (适用于 Azure 的 RBAC) 还可以控制对工作区的访问。 因此，需要 Azure 角色以及 Azure AD 管理员角色来管理 Azure 信息保护分析。 如果刚开始接触 Azure 角色，阅读 [Azure RBAC 角色与 Azure AD 管理员角色的区别](/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)可能会对你有所帮助。

有关详细信息，请参阅：

- [必需 Azure AD 管理员角色](#required-azure-ad-administrator-roles)
- [必需的 Azure Log Analytics 角色](#required-azure-log-analytics-roles)
- [查看报表至少需要的角色](#minimum-roles-to-view-the-reports)

#### <a name="required-azure-ad-administrator-roles"></a>必需 Azure AD 管理员角色

若要访问 Azure 信息保护分析窗格，必须具备以下 [Azure AD 管理员角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) 之一：

- 若要创建 Log Analytics 工作区或创建自定义查询，必须具有以下角色之一：
    
    - **Azure 信息保护管理员**
    - **安全管理员**
    - **法规管理员**
    - **合规性数据管理员**
    - **全局管理员**
    
- 创建工作区后，可以使用具有较少权限的下列角色来查看所收集的数据：
    
    - **安全读者**
    - **全局读取器**

#### <a name="required-azure-log-analytics-roles"></a>必需的 Azure Log Analytics 角色

你必须具有以下 [azure Log Analytics 角色](/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions) 或标准 [azure 角色](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-rbac-roles) 之一才能访问 Azure Log Analytics 工作区：
    
- 若要创建该工作区或创建自定义查询，必须具有以下角色之一：
    
    - **Log Analytics 参与者**
    - **参与者**
    - **所有者**
    
- 创建该工作区后，可以使用具有较少权限的以下角色之一来查看收集的数据：
    
    - **Log Analytics 读者**
    - **读者**

#### <a name="minimum-roles-to-view-the-reports"></a>查看报表至少需要的角色

为 Azure 信息保护分析配置工作区后，查看 Azure 信息保护分析报表至少需要具备以下两种角色：

- Azure AD 管理员角色： **安全读取器**
- Azure 角色： **Log Analytics 读取器**

但是，许多组织的典型角色分配是 Azure AD 角色“安全读取者”以及 Azure 角色“读取者”。

### <a name="storage-requirements-and-data-retention"></a>存储要求和数据保留

在 Azure 信息保护工作区中收集和存储的数据量会因多种因素而异，具体取决于你所拥有的 Azure 信息保护客户端和其他受支持的终结点的数量、你是否正在收集终结点发现数据、你是否已部署扫描程序、所访问的受保护文档的数量等。

然而，作为起点，你可能会发现以下估计非常有用：

- 仅适用于 Azure 信息保护客户端生成的审核数据：每月 2 GB/10000 活动用户。

- 对于 Azure 信息保护客户端、扫描仪和 Microsoft Defender ATP 生成的审核数据：每月 20 GB/10000 活动用户。

如果你使用必需的标签，或者你为大多数用户配置了默认标签，则你的费率可能会显著提高。

Azure Monitor 日志具有 **使用情况和预估成本** 功能，可帮助您估计和查看存储的数据量，还可以控制 Log Analytics 工作区的数据保留期。 有关详细信息，请参阅 [使用 Azure Monitor 日志管理使用情况和成本](/azure/azure-monitor/platform/manage-cost-storage)。

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>配置报表的 Log Analytics 工作区

1. 如果尚未这样做，请打开新的浏览器窗口，使用拥有[执行 Azure 信息保护分析所需权限](#permissions-required-for-azure-information-protection-analytics)的帐户[登录 Azure 门户](https://portal.azure.com)。 然后导航到“Azure 信息保护”窗格。 
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。
    
1. 找到 " **管理** " 菜单选项，然后选择 " **配置 analytics (预览")**。

1. 在 " **Azure 信息保护日志分析** " 窗格中，可以看到租户拥有的任何 Log Analytics 工作区的列表。 执行下列操作之一：
    
    - **若要创建新的 Log Analytics 工作区**：选择 " **创建新工作区**"，然后在 " **Log Analytics 工作区** " 窗格上提供所需的信息。
    
    - **使用现有 Log Analytics 工作区**：从列表中选择工作区。
    
    如果需要关于创建 Log Analytics 工作区的帮助，请参阅[在 Azure 门户中创建 Log Analytics 工作区](/azure/log-analytics/log-analytics-quick-create-workspace)。

1. **仅限 AIP 经典客户端**：如果你想要存储标识为敏感信息类型的实际数据，请选中该复选框， **以便在你的敏感数据中进行更深入的分析** 。 

    有关此设置的详细信息，请参阅此页上的 " [内容匹配" 以获取深入分析](#content-matches-for-deeper-analysis) 部分。

1. 选择“确定”。

你现在可以查看报表。

## <a name="view-the-aip-analytics-reports"></a>查看 AIP 分析报告

在 "Azure 信息保护" 窗格中，找到 " **仪表板** " 菜单选项，然后选择下列选项之一：

|报表  |说明  |
|---------|---------|
|**使用情况报表 (预览)**     |  使用此报表查看标签是如何使用的。       |
|**(预览的活动日志)**     |  使用此报表查看用户执行的标记操作，以及设备上和对文件路径执行的标记操作。 此外，对于受保护的文档，你可以查看在组织内部和外部用户 (成功或拒绝的访问尝试) ，即使他们没有安装 Azure 信息保护客户端。 <br><br>  此报表有“列”选项，可用于显示比默认显示更多的活动信息。 还可以选择它来显示“活动详细信息”，方便查看文件相关的更多详细信息。     |
|**数据发现 (预览)**     |    使用此报表查看扫描程序发现的带标签文件和受支持的终结点的相关信息。  <br><br>**提示**：从收集的信息中，你可能会发现用户从你不知道或当前未扫描的位置访问包含敏感信息的文件： <br><br>-如果位置位于本地，请考虑将位置添加为 Azure 信息保护扫描程序的其他数据存储库。 <br>  -如果位置在云中，请考虑使用 Microsoft Cloud App Security 来对其进行管理。    |
|**建议 (预览)**     | 使用此报告来确定包含敏感信息的文件，并按照建议缓解风险。  <br><br> 选择项目时，“查看数据”选项将显示触发了建议的审核活动。     |
|     |         |


## <a name="modify-the-aip-analytics-reports-and-create-custom-queries"></a>修改 AIP 分析报表并创建自定义查询

选择仪表板中的 "查询" 图标，打开 " **日志搜索** " 窗格： 

![自定义 Azure 信息保护报表的 Log Analytics 图标](./media/log-analytics-icon.png)


Azure 信息保护的记录数据存储在下表中：InformationProtectionLogs_CL

创建你自己的查询时，请使用已作为 InformationProtectionEvents 函数实现的友好架构名称。 这些函数派生自自定义查询支持的属性（某些属性仅供内部使用），它们的名称不会随时间的推移而发生更改，即使在更改基础属性以实现改进功能和新功能时也不例外。

### <a name="friendly-schema-reference-for-event-functions"></a>事件函数的友好架构参考

使用下表来标识可用于通过 Azure 信息保护分析进行自定义查询的事件函数的友好名称。

|列名称|说明|
|-----------|-----------|
|**时间**|事件时间：格式 YYYY-MM-YYYY-MM-DDTHH： MM： SS 中的 UTC|
|**用户**|User：格式 UPN 或 DOMAIN\USER|
|**ItemPath**|完整项目路径或电子邮件主题|
|**ItemName**|文件名或电子邮件主题 |
|**方法**|标签分配方法：手动、自动、建议、默认或强制|
|**活动**|审核活动： DowngradeLabel、UpgradeLabel、RemoveLabel、NewLabel、发现、Access、RemoveCustomProtection、ChangeCustomProtection、NewCustomProtection 或 FileRemoved |
|**ResultStatus**|操作的结果状态：<br /><br /> AIP scanner 报告成功或失败的 (仅) |
|**ErrorMessage_s**|如果 ResultStatus = Failed，则包括错误消息详细信息。 仅由 AIP 扫描程序报告|
|**LabelName**|标签名称 (未本地化) |
|**LabelNameBefore** |更改前的标签名称 (未本地化)  |
|**ProtectionType**|保护类型 [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID"： "GUID" <br /> } <br />|
|**ProtectionBefore**|更改前的保护类型 [JSON] |
|**MachineName** |FQDN （如果可用）;否则为主机名|
|**DeviceRisk**|WDATP 可用时的设备风险评分|
|**平台**|设备平台 (Win、OSX、Android、iOS)  |
|ApplicationName|应用程序友好名称|
|**AIPVersion**|执行审核操作的 Azure 信息保护客户端的版本 |
|**TenantId**|Azure AD 租户 ID |
|**AzureApplicationId**|Azure AD 已注册应用程序 ID (GUID) |
|**ProcessName**|承载 MIP SDK 的进程|
|**面部**|标签 GUID 或 null|
|**IsProtected**|是否受保护：是/否 |
|**ProtectionOwner** |UPN 格式的 Rights Management 所有者|
|**LabelIdBefore**|更改前标记 GUID 或 null|
|**InformationTypesAbove55**|在置信度为55或更高的数据中找到的 [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) 的 JSON 数组 |
|**InformationTypesAbove65**|在置信度为65或更高的数据中找到的 [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) 的 JSON 数组 |
|**InformationTypesAbove75**|在置信度为75或更高的数据中找到的 [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) 的 JSON 数组 |
|**InformationTypesAbove85**|在置信度为85或更高的数据中找到的 [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) 的 JSON 数组 |
|**InformationTypesAbove95**|在置信度为95或更高的数据中找到的 [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) 的 JSON 数组|
|**DiscoveredInformationTypes** |数据中找到的 [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) 的 JSON 数组和它们的匹配内容 (如果已启用) ，其中空数组表示找不到任何信息类型，null 表示无可用信息 |
|**ProtectedBefore**|是否在更改之前保护内容：是/否 |
|**ProtectionOwnerBefore**|更改前 Rights Management 所有者 |
|**UserJustification**|降级或删除标签时的理由|
|**LastModifiedBy**|上次修改文件的 UPN 格式的用户。 仅适用于 Office 和 SharePoint|
|**LastModifiedDate**|格式为 YYYY-MM-DD 的 UTC-YYYY-MM-DDTHH： MM： SS：仅适用于 Office 和 SharePoint |
| | |
#### <a name="examples-using-informationprotectionevents"></a>使用 InformationProtectionEvents 的示例

使用以下示例了解如何使用友好的架构来创建自定义查询。

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>示例1：返回在过去31天内发送审核数据的所有用户 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>示例2：返回在过去31天内每天降级的标签数 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>示例3：返回最近31天内按用户的机密降级的标签数 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

在此示例中，仅当操作前的标签名包含名称“机密”且操作后的标签名不包含名称“机密”时，才会对降级的标签计数。 


## <a name="next-steps"></a>后续步骤
查看报表中的信息后，如果使用的是 Azure 信息保护客户端，则可以决定对标签策略进行更改。 

- **统一标签客户端**：在标签管理中心中对标签策略进行更改，包括 Microsoft 365 安全中心、Microsoft 365 符合性中心或 Microsoft 365 安全 & 符合性中心。 有关详细信息，请参阅 [Microsoft 365 文档](/microsoft-365/compliance/sensitivity-labels)。

- **经典客户端**：在 Azure 门户中对策略进行更改。 有关详细信息，请参阅 [配置 Azure 信息保护策略](configure-policy.md)。

如果你有 Microsoft 365 订阅，则还可以在 Microsoft 365 合规中心和 Microsoft 365 安全中心中查看标签使用情况。 有关详细信息，请参阅[使用标签分析查看标签使用情况](/microsoft-365/compliance/label-analytics)。

AIP 审核日志还将发送到 Microsoft 365 的活动资源管理器中，其中显示的名称可能不同。 有关详细信息，请参阅：

- [公共预览版：活动资源管理器中的 AIP 审核日志](https://www.yammer.com/askipteam/#/Threads/show?threadId=1085834054254592)
- [活动资源管理器入门](/microsoft-365/compliance/data-classification-activity-explorer)。