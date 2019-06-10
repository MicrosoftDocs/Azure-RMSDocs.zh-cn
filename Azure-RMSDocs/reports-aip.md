---
title: Azure 信息保护的中心报告
description: 如何使用中心报告来跟踪 Azure 信息保护标签的采用和标识包含敏感信息的文件
author: cabailey
ms.author: cabailey
ms.date: 06/08/2019
manager: barbkess
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 84e3e4231c07f2234baa717d1be2c29386ed44ca
ms.sourcegitcommit: 886aebde3b2df0f54b7bd41105823db44aea72d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815606"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure 信息保护的中心报告

>适用对象： *[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> 此功能目前处于预览状态，随时可能更改。

使用 Azure 信息保护分析的中心报告，帮助跟踪 Azure 信息保护标签的采用情况。 此外：

- 监控组织中带标签和受保护的文档以及电子邮件

- 标识包含组织中的敏感信息的文档

- 监控用户对带标签文档和电子邮件的访问，并跟踪文档分类更改。

- 确定包含敏感信息且若未保护则可能给组织带来风险的文档，并按照以下建议缓解风险。

您看到的数据聚合从你的 Azure 信息保护客户端和 Azure 信息保护扫描程序，从运行的 Windows 计算机[Microsoft Defender 高级威胁防护 (Microsoft Defender ATP)](/windows/security/threat-protection/microsoft-defender-atp/overview)，并从[支持统一进行标记的客户端](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)。

例如，你将能够看到以下数据：

- 在“使用情况报表”  中，你可以选择时间段：
    
    - 应用的标签
    
    - 被标记的文档和电子邮件数
    
    - 被保护的文档和电子邮件数
    
    - 标记文档和电子邮件的用户和设备数
    
    - 用于标记的应用程序

- 在可以选择时间段的“活动日志”  中：
    
    - 特定用户已执行的标记操作
    
    - 在特定设备中已执行的标记操作
    
    - 已访问特定标记文档的用户
    
    - 已对特定文件路径执行的标记操作
    
    - 特定应用程序已执行的标记操作，如文件资源管理器（右键单击）或 AzureInformationProtection PowerShell 模块
    
    - 有关更多信息，请进一步查看报告的文件以查看“活动详细信息” 

- 在“数据发现”  报表中：

    - 哪些文件位于您的扫描的数据存储库，Windows 10 计算机或运行 Azure 信息保护客户端计算机或[支持统一进行标记的客户端](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)
    
    - 被标记和被保护的文件，以及按标签分类的文件的位置
    
    - 包含已知类别的敏感信息（例如财务数据和个人信息）的文件，以及按这些类别分类的文件的位置

- 在“建议”报告中  ：
    
    - 识别包含已知敏感信息类型但未受保护的文件。 按照建议操作，可立即对其中一个标签配置相应的条件，以应用自动标签或推荐的标签。
        
        如果按照建议进行操作：在用户下次打开或 Azure 信息保护扫描程序下次扫描文件时，这些文件可自动分类并自动受到保护。
    
    - 其文件具有已标识的敏感信息但其本身当前未被 Azure 信息保护服务扫描的数据存储库。 按照建议操作，可立即向扫描程序的某个配置文件添加已标识的数据存储。
        
        如果按照建议进行操作：在下一次扫描周期，文件可自动分类并自动受到保护。

报表使用 [Azure Monitor](/azure/log-analytics/log-analytics-overview) 将数据存储在组织拥有的 Log Analytics 工作区中。 如果你熟悉查询语言，可以修改这些查询，并创建新报表和 Power BI 仪表板。 以下教程可能有助于你了解查询语言：[Azure Monitor 日志查询入门](/azure/azure-monitor/log-query/get-started-queries)。

有关详细信息，请参阅以下博客文章： 
- [Microsoft 信息保护中有关所有数据的数据发现、报告和分析](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)

- [发现和保护敏感数据通过 Azure 信息保护和 Microsoft Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>收集和发送到 Microsoft 的信息

为了生成这些报表，终结点将以下类型的信息发送到 Microsoft：

- 标签操作。 例如，设置标签、更改标签、添加或删除保护、自动和建议的标签。

- 标签操作之前和之后的标签名称。

- 组织的租户 ID。

- 用户 ID（电子邮件地址或 UPN）。

- 用户设备的名称。

- 对于文档：被标记的文档的文件路径和文件名。

- 对于电子邮件：带标签的电子邮件的电子邮件主题和电子邮件发件人。 

- 在内容中已检测到的敏感信息类型（[预定义](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)和自定义）。

- Azure 信息保护客户端版本。

- 客户端操作系统版本。

此信息存储在组织拥有的 Azure Log Analytics 工作区中，并可供有权访问此工作区的用户从 Azure 信息保护独立查看。 有关详细信息，请参阅 [Azure 信息保护分析的必备权限](#permissions-required-for-azure-information-protection-analytics)部分。 要了解如何管理对工作区的访问，请参阅 Azure 文档中的[使用 Azure 权限管理对 Log Analytics 工作区的访问](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions)部分。

若要阻止 Azure 信息保护客户端发送此数据，请将“将审核数据发送到 Azure 信息保护日志分析”  的[策略设置](configure-policy-settings.md)设置为“关闭”  ：

- 若要使大多数用户发送此数据，而使一部分用户无法发送审核数据，请执行以下操作： 
    - 在部分用户的作用域内策略中将“将审核数据发送到 Azure 信息保护日志分析”  设置为“关闭”  。 此配置专用于生产方案。

- 若要仅使一部分用户发送审核数据，请执行以下操作： 
    - 在全局策略中将“将审核数据发送到 Azure 信息保护日志分析”  设置为“关闭”  ，在部分用户的作用域内策略中设置为“打开”  。 此配置专用于测试方案。

#### <a name="content-matches-for-deeper-analysis"></a>更深入分析的内容匹配项 

Azure 信息保护的 Azure Log Analytics 工作区包括用于收集和存储由敏感信息类型或自定义条件标识的数据的复选框。 例如，这可以包括查找到的信用卡号码，以及社会安全号码、护照号码和银行帐户号码。 如果不想发送此额外数据，请不要选中此复选框。 如果你希望大多数用户发送此额外数据，而一部分用户无法发送该数据，请选中此复选框并在该部分用户的作用域内策略中配置[高级客户端设置](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)。

收集内容匹配项后，当你向下钻取到活动日志中的文件以显示活动详细信息  时，这些匹配项项将显示在报表中。 也可以使用查询来查看和检索此信息。

## <a name="prerequisites"></a>先决条件
若要查看 Azure 信息保护报表和创建你自己的报表，请确保满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|包含 Log Analytics 且用于与 Azure 信息保护相同的租户的 Azure 订阅|请参阅 [Azure Monitor 定价](https://azure.microsoft.com/pricing/details/log-analytics)页。<br /><br />如果没有 Azure 订阅或当前未使用 Azure Log Analytics，定价页将包含免费试用版的链接。|
|Azure 信息保护客户端或 Azure 信息保护统一标记客户端|如果没有这些客户端，您可以下载并安装它们从[Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。 <br /><br /> 请确保你具有要支持的最新版本[所有功能](#features-that-require-a-minimum-version-of-the-client)用于 Azure 信息保护分析。|
|对于“发现和风险”  报表： <br /><br />-若要显示在本地数据存储中的数据，你已部署 Azure 信息保护扫描程序至少一个的实例 <br /><br />-若要显示 Windows 10 计算机中的数据必须是最小的 1809年生成、 使用 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 和已启用 microsoft Azure 信息保护集成功能Defender 安全中心|有关扫描程序的安装说明，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。 <br /><br />有关配置和使用来自 Microsoft Defender 安全中心的 Azure 信息保护集成功能的信息，请参阅[Windows 概述中的信息保护](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview)。|
|对于“建议”报告  ： <br /><br />-若要从 Azure 门户中，如下的建议的操作添加新的数据存储库，你必须使用 Azure 信息保护扫描程序的最新正式发布版本 |若要部署扫描程序，请参阅[部署 Azure 信息保护扫描程序以自动分类和保护文件](deploy-aip-scanner.md)。|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure 信息保护分析必备的先决条件

针对 Azure 信息保护分析，在配置 Azure Log Analytics 工作区后，可以使用安全读取者的 Azure AD 管理员角色替代 Azure 门户中支持管理 Azure 信息保护的其他 Azure AD 角色。

由于此功能使用 Azure 监视，因此 Azure 的基于角色的访问控制 (RBAC) 也控制对工作区的访问。 因此，需要 Azure 角色以及 Azure AD 管理员角色来管理 Azure 信息保护分析。 如果刚开始接触 Azure 角色，阅读 [Azure RBAC 角色与 Azure AD 管理员角色的区别](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)可能会对你有所帮助。

详细信息:

1. 以下 [Azure AD 管理员角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)之一用于访问 Azure 信息保护分析边栏选项卡：
    
    - 若要创建 Log Analytics 工作区或创建自定义查询，必须具有以下角色之一：
    
        - **Azure 信息保护管理员**
        - **安全管理员**
        - **合规性管理员**
        - **符合性数据管理器**
        - **全局管理员**
    
    - 创建该工作区后，可以使用具有较少权限的以下角色来查看收集的数据：
    
        - **安全读取者**
    
    > [!NOTE] 
    > 如果你的租户已迁移到统一的标记存储，则无法使用 Azure 信息保护管理员角色。 [详细信息](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

2. 此外，还需要具有以下 [Azure Log Analytics 角色](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions)或标准 [Azure 角色](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments)之一才能访问 Azure Log Analytics 工作区：
    
    - 若要创建该工作区或创建自定义查询，必须具有以下角色之一：
    
        - **Log Analytics 参与者**
        - **参与者**
        - **所有者**
    
    - 创建该工作区后，可以使用具有较少权限的以下角色之一来查看收集的数据：
    
        - **Log Analytics 读者**
        - **读者**

#### <a name="minimum-roles-to-view-the-reports"></a>查看报表至少需要的角色

为 Azure 信息保护分析配置工作区后，查看 Azure 信息保护分析报表至少需要具备以下两种角色：

- Azure AD 管理员角色：**安全读取者**
- Azure 角色：**Log Analytics 读者**

但是，许多组织的典型角色分配是 Azure AD 角色“安全读取者”  以及 Azure 角色“读取者”  。

### <a name="features-that-require-a-minimum-version-of-the-client"></a>需要最小版本的客户端的功能。

可以使用的版本历史记录信息[Azure 信息保护统一标记的客户端](./rms-client/unifiedlabelingclient-version-release-history.md)并[Azure 信息保护客户端](./rms-client/client-version-release-history.md)以确认是否您的客户端版本支持所有主要的报告功能。 客户端最低版本：

Azure 信息保护统一标记客户端：

- 对审核和终结点发现的支持：版本 2.0.778.0

对于 Azure 信息保护客户端：

- 对审核的支持：版本 1.41.51.0
- 对终结点发现的支持：版本 1.48.204.0

### <a name="storage-requirements-and-data-retention"></a>存储要求和数据保留期

收集和存储在 Azure 信息保护工作区中的数据量将为每个租户显著变化，具体取决于因素，例如如何多个 Azure 信息保护客户端和其他受支持的终结点必须无论你是收集终结点的发现数据，您已经部署了扫描仪，等等。

但是，作为起点，您可能会发现以下估计值非常有用：

- 对于 Azure 信息保护客户端生成的审核数据：每个每月 10,000 个活动用户的 2 GB。

- 对于 Azure 信息保护客户端、 扫描仪和 Microsoft Defender ATP 生成的审核数据：每个每月 10,000 个活动用户 20 GB。

如果使用强制标签或已在全局策略中配置默认标签，你的费率很可能要高得多。

Azure Monitor 日志已**使用情况和预估的成本**功能来帮助你估计并查看的数据存储量，你还可以控制 Log Analytics 工作区的数据保留期。 有关详细信息，请参阅[管理使用情况和成本与 Azure Monitor 日志](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)。

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>配置报表的 Log Analytics 工作区

1. 如果尚未这样做，请打开新的浏览器窗口，使用拥有[执行 Azure 信息保护分析所需权限](#permissions-required-for-azure-information-protection-analytics)的帐户[登录 Azure 门户](https://portal.azure.com)。 然后导航到“Azure 信息保护”  边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”   。 选择“Azure 信息保护”。 
    
2. 找到“管理”菜单选项，然后选择“配置分析（预览版）”   。

3. 在“Azure 信息保护日志分析”  边栏选项卡上，可以看到由你的租户拥有的任何 Log Analytics 工作区的列表。 执行以下操作之一：
    
    - 创建新的 Log Analytics 工作区：请选择“创建新工作区”，并在“Log Analytics 工作区”边栏选项卡上提供所需信息   。
    
    - 使用现有的 Log Analytics 工作区：从列表中选择工作区。

如果需要关于创建 Log Analytics 工作区的帮助，请参阅[在 Azure 门户中创建 Log Analytics 工作区](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)。

配置工作区后，即可开始查看报表。

> [!NOTE] 
> 首次在报表中显示数据当前存在已知问题。 如果你遇到这种情况，请在全局策略中将“将审核数据发送到 Azure 信息保护日志分析”  的[策略设置](configure-policy-settings.md)设置为“关闭”  并保存策略。 然后，将相同设置更改为“打开”  并保存策略。 客户端[下载更改](configure-policy.md#making-changes-to-the-policy)后，审核事件可能需要最多 30 分钟才能在 Log Analytics 工作区中显示。

## <a name="how-to-view-the-reports"></a>如何查看报告

在“Azure 信息保护”边栏选项卡中，找到“仪表板”菜单选项，然后选择以下选项之一  ：

- **使用情况报表(预览版)** ：使用此报表查看标签是如何使用的。

- **活动日志(预览版)** ：使用此报表查看用户执行的标记操作，以及设备上和对文件路径执行的标记操作。
    
    此报表有“列”  选项，可用于显示比默认显示更多的活动信息。 还可以选择它来显示“活动详细信息”，方便查看文件相关的更多详细信息  。

- **数据发现(预览版)** ：使用此报表查看扫描程序发现的带标签文件和受支持的终结点的相关信息。
    
    你可以配置[高级客户端设置](./rms-client/client-admin-guide-customizations.md#enable-azure-information-protection-analytics-to-discover-sensitive-information-in-documents)包含敏感信息的报表文件的 Azure 信息保护客户端。
    
    提示：在收集的信息中，你可能会发现用户从你不知道或当前未扫描的位置访问包含敏感信息的文件：
    
    - 如果这些位置在本地环境中，请考虑添加这些位置作为 Azure 信息保护扫描程序的附加数据存储库。
    - 如果这些位置在云中，请考虑使用 Microsoft Cloud App Security 对其进行管理。 
    
- 建议（预览）  ：使用此报告来确定包含敏感信息的文件，并按照建议缓解风险。
    
    选择项目时，“查看数据”选项将显示触发了建议的审核活动  。


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>如何修改报表并创建自定义查询

选择仪表板中的查询图标以打开“日志搜索”  边栏选项卡： 

![自定义 Azure 信息保护报表的 Log Analytics 图标](./media/log-analytics-icon.png)


Azure 信息保护的记录数据存储在下表中：**InformationProtectionLogs_CL**

创建你自己的查询时，请使用已作为 InformationProtectionEvents  函数实现的友好架构名称。 这些函数派生自自定义查询支持的属性（某些属性仅供内部使用），它们的名称不会随时间的推移而发生更改，即使在更改基础属性以实现改进功能和新功能时也不例外。

### <a name="friendly-schema-reference-for-event-functions"></a>事件函数的友好架构参考

使用下表来标识可用于通过 Azure 信息保护分析进行自定义查询的事件函数的友好名称。

|列名|描述|
|-----------|-----------|
|Time|事件时间：以 YYYY 格式的 UTC-MM-DDTHH:MM:SS|
|“用户”|用户：UPN 或域 \ 用户格式|
|ItemPath|项目的完整路径或电子邮件主题|
|ItemName|文件名称或电子邮件主题 |
|方法|分配方法的标签：手动、 自动、 建议、 默认情况下或强制性|
|activities|审核活动：DowngradeLabel、 UpgradeLabel、 RemoveLabel、 NewLabel，发现、 访问、 RemoveCustomProtection、 ChangeCustomProtection 或 NewCustomProtection |
|LabelName|标签名称 （未本地化）|
|LabelNameBefore |更改 （未本地化） 之前的标签名称 |
|ProtectionType|保护类型 [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID":"GUID" <br /> } <br />|
|ProtectionBefore|保护类型更改 [JSON] 之前 |
|InformationTypesMatches|JSON 数组[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)数据中发现其中一个空数组表示没有信息类型找到，和 null 表示没有可用的信息|
|MachineName |如果可用; 的 FQDN否则为主机名|
|DeviceRisk|从 WDATP 时可用的设备风险评分|
|平台|设备平台 (Win，OSX、 Android、 iOS) |
|ApplicationName|应用程序的友好名称|
|AIPVersion|执行审核操作的 Azure 信息保护客户端版本 |
|TenantId|Azure AD 租户 ID |
|AzureApplicationId|Azure AD 注册应用程序 ID (GUID)|
|ProcessName|承载 MIP SDK 进程|
|LabelId|标签 GUID 或 null|
|IsProtected|是否受保护的：是/否 |
|ProtectionOwner |以 UPN 格式的 rights Management 所有者|
|LabelIdBefore|标签 GUID 或更改之前，则为 null|
|InformationTypesAbove55|JSON 数组[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)置信度 55 或更高版本的数据中找到 |
|InformationTypesAbove65|JSON 数组[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)置信度级别为 65 或更高版本的数据中找到 |
|InformationTypesAbove75|JSON 数组[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)置信度 75 或更高版本的数据中找到 |
|InformationTypesAbove85|JSON 数组[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)置信度 85 或更高版本的数据中找到 |
|InformationTypesAbove95|JSON 数组[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)置信度 95 或更高版本的数据中找到|
|DiscoveredInformationTypes |JSON 数组[SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) （如果启用） 中数据和其匹配的内容找到其中一个空数组表示没有信息类型找到，和 null 意味着没有可用的信息 |
|ProtectedBefore|是否更改之前保护内容：是/否 |
|ProtectionOwnerBefore|在更改之前的 rights Management 所有者 |
|UserJustification|降级或删除标签时的理由|
|LastModifiedBy|以 UPN 格式上次修改该文件的用户。 适用于 Office 和 SharePoint Online 仅|
|LastModifiedDate|以 YYYY 格式的 UTC-MM-DDTHH:MM:SS:适用于 Office 和 SharePoint Online 仅 |


#### <a name="examples-using-informationprotectionevents"></a>使用 InformationProtectionEvents 的示例

使用以下示例了解如何使用友好的架构来创建自定义查询。

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>示例 1：返回在过去 31 天内发送审核数据的所有用户 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>示例 2：返回在过去 31 天内按天降级的标签数 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>示例 3：返回在过去 31 天内用户从“机密”降级的标签数 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

在此示例中，仅当操作前的标签名包含名称“机密”且操作后的标签名不包含名称“机密”时，才会对降级的标签计数   。 


## <a name="next-steps"></a>后续步骤
查看在报表中的信息后，如果使用 Azure 信息保护客户端，您可能会决定对你的 Azure 信息保护策略进行更改。 有关说明，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

如果你有 Microsoft 365 订阅，则还可以在 Microsoft 365 合规中心和 Microsoft 365 安全中心中查看标签使用情况。 有关详细信息，请参阅[使用标签分析查看标签使用情况](/Office365/SecurityCompliance/label-analytics)。
