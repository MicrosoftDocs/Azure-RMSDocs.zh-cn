---
title: Azure 信息保护的中心报告
description: 如何使用中心报告来跟踪 Azure 信息保护标签的采用和标识包含敏感信息的文件
author: cabailey
ms.author: cabailey
ms.date: 11/25/2019
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7c310122ac72bc7312fe0bd8d41bd3dc80715d76
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474295"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure 信息保护的中心报告

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

> [!NOTE]
> 此功能目前处于预览状态，随时可能更改。

Use Azure Information Protection analytics for central reporting to help you track the adoption of your labels that classify and protect your organization's data. 此外：

- 监控组织中带标签和受保护的文档以及电子邮件

- 标识包含组织中的敏感信息的文档

- 监控用户对带标签文档和电子邮件的访问，并跟踪文档分类更改。

- 确定包含敏感信息且若未保护则可能给组织带来风险的文档，并按照以下建议缓解风险。

- Identify when protected documents are accessed by internal or external users from Windows computers, and whether access was granted or denied.

The data that you see is aggregated from your Azure Information Protection clients and scanners, from Microsoft Cloud App Security, from Windows 10 computers using Microsoft Defender Advanced Threat Protection, and from [protection usage logs](log-analyze-usage.md).

例如，你将能够看到以下数据：

- 在“使用情况报表”中，你可以选择时间段：
    
    - 应用的标签
    
    - 被标记的文档和电子邮件数
    
    - 被保护的文档和电子邮件数
    
    - 标记文档和电子邮件的用户和设备数
    
    - 用于标记的应用程序

- 在可以选择时间段的“活动日志”中：
    
    - 特定用户已执行的标记操作
    
    - 在特定设备中已执行的标记操作
    
    - 已访问特定标记文档的用户
    
    - 已对特定文件路径执行的标记操作
    
    - What labeling actions were performed by a specific application, such File Explorer and right-click, PowerShell, the scanner, or Microsoft Cloud App Security
    
    - Which protected documents were accessed successfully by users or denied access to users, even if those users don't have the Azure Information Protection client installed or are outside your organization

    - 有关更多信息，请进一步查看报告的文件以查看“活动详细信息”

- 在“数据发现”报表中：

    - What files are on your scanned data repositories, Windows 10 computers, or computers running the Azure Information Protection clients
    
    - 被标记和被保护的文件，以及按标签分类的文件的位置
    
    - 包含已知类别的敏感信息（例如财务数据和个人信息）的文件，以及按这些类别分类的文件的位置

- 在“建议”报告中：
    
    - 识别包含已知敏感信息类型但未受保护的文件。 按照建议操作，可立即对其中一个标签配置相应的条件，以应用自动标签或推荐的标签。
        
        If you follow the recommendation: The next time the files are opened by a user or scanned by the Azure Information Protection scanner, the files can be automatically classified and protected.
    
    - 其文件具有已标识的敏感信息但其本身当前未被 Azure 信息保护服务扫描的数据存储库。 按照建议操作，可立即向扫描程序的某个配置文件添加已标识的数据存储。
        
        If you follow the recommendation: On the next scanner cycle, the files can be automatically classified and protected.

报表使用 [Azure Monitor](/azure/log-analytics/log-analytics-overview) 将数据存储在组织拥有的 Log Analytics 工作区中。 如果你熟悉查询语言，可以修改这些查询，并创建新报表和 Power BI 仪表板。 You might find the following tutorial helpful to understand the query language: [Get started with Azure Monitor log queries](/azure/azure-monitor/log-query/get-started-queries).

有关详细信息，请参阅以下博客文章： 
- [Microsoft 信息保护中有关所有数据的数据发现、报告和分析](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)

- [Discover and protect sensitive data through Azure Information Protection and Microsoft Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>收集和发送到 Microsoft 的信息

为了生成这些报表，终结点将以下类型的信息发送到 Microsoft：

- 标签操作。 例如，设置标签、更改标签、添加或删除保护、自动和建议的标签。

- 标签操作之前和之后的标签名称。

- 组织的租户 ID。

- 用户 ID（电子邮件地址或 UPN）。

- 用户设备的名称。

- 对于文档：被标记的文档的文件路径和文件名。

- For emails: The email subject and email sender  for emails that are labeled. 

- 在内容中已检测到的敏感信息类型（[预定义](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)和自定义）。

- Azure 信息保护客户端版本。

- 客户端操作系统版本。

此信息存储在组织拥有的 Azure Log Analytics 工作区中，并可供有权访问此工作区的用户从 Azure 信息保护独立查看。 有关详细信息，请参阅 [Azure 信息保护分析的必备权限](#permissions-required-for-azure-information-protection-analytics)部分。 要了解如何管理对工作区的访问，请参阅 Azure 文档中的[使用 Azure 权限管理对 Log Analytics 工作区的访问](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)部分。

To prevent Azure Information Protection clients (classic) from sending this data, set the [policy setting](configure-policy-settings.md) of **Send audit data to Azure Information Protection analytics** to **Off**:

- 若要使大多数用户发送此数据，而使一部分用户无法发送审核数据，请执行以下操作： 
    - Set **Send audit data to Azure Information Protection analytics** to **Off** in a scoped policy for the subset of users. 此配置专用于生产方案。

- 若要仅使一部分用户发送审核数据，请执行以下操作： 
    - Set **Send audit data to Azure Information Protection analytics** to **Off** in the global policy, and **On** in a scoped policy for the subset of users. 此配置专用于测试方案。

To prevent Azure Information Protection unified clients from sending this data, configure a label policy [advanced setting](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics).

#### <a name="content-matches-for-deeper-analysis"></a>更深入分析的内容匹配项

Azure Information Protection lets you collect and store the actual data that's identified as being a sensitive information type (predefined or custom). 例如，这可以包括查找到的信用卡号码，以及社会安全号码、护照号码和银行帐户号码。 The content matches are displayed when you select an entry from **Activity logs**, and view the **Activity Details**. 

By default, Azure Information Protection clients don't send content matches. To change this behavior so that content matches are sent:

- For the classic client, select a checkbox as part of the [configuration](#configure-a-log-analytics-workspace-for-the-reports) for Azure Information Protection analytics. The checkbox is named **Enable deeper analytics into your sensitive data**.
    
    If you want most users who are using this client to send content matches but a subset of users cannot send content matches, select the checkbox and then configure an [advanced client setting](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) in a scoped policy for the subset of users.

- For the unified labeling client, configure an [advanced setting](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) in a label policy.

## <a name="prerequisites"></a>必备条件
若要查看 Azure 信息保护报表和创建你自己的报表，请确保满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|包含 Log Analytics 且用于与 Azure 信息保护相同的租户的 Azure 订阅|请参阅 [Azure Monitor 定价](https://azure.microsoft.com/pricing/details/log-analytics)页。<br /><br />如果没有 Azure 订阅或当前未使用 Azure Log Analytics，定价页将包含免费试用版的链接。|
|For reporting information from labeling clients: <br /><br />- Azure Information Protection clients|Both the unified labeling client and the classic client are supported. <br /><br />If not already installed, you can download and install these clients from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|For reporting information from cloud-based data stores: <br /><br />- Microsoft Cloud App Security |To display information from Microsoft Cloud App Security, configure [Azure Information Protection integration](https://docs.microsoft.com/cloud-app-security/azip-integration).|
|For reporting information from on-premises data stores: <br /><br />- Azure Information Protection scanner |有关扫描程序的安装说明，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。 |
|For reporting information from Windows 10 computers:  <br /><br />- Minimum build of 1809 with Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)|You must enable the Azure Information Protection integration feature from Microsoft Defender Security Center. For more information, see [Information protection in Windows overview](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure 信息保护分析必备的先决条件

针对 Azure 信息保护分析，在配置 Azure Log Analytics 工作区后，可以使用安全读取者的 Azure AD 管理员角色替代 Azure 门户中支持管理 Azure 信息保护的其他 Azure AD 角色。 This additional role is supported only if your tenant isn't on the [unified labeling platform](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

Because Azure Information Protection analytics uses Azure Monitoring, role-based access control (RBAC) for Azure also controls access to your workspace. 因此，需要 Azure 角色以及 Azure AD 管理员角色来管理 Azure 信息保护分析。 如果刚开始接触 Azure 角色，阅读 [Azure RBAC 角色与 Azure AD 管理员角色的区别](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)可能会对你有所帮助。

详细信息:

1. One of the following [Azure AD administrator roles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) to access the Azure Information Protection analytics pane:
    
    - 若要创建 Log Analytics 工作区或创建自定义查询，必须具有以下角色之一：
    
        - **Azure Information Protection administrator**
        - **安全管理员**
        - **合规性管理员**
        - **Compliance data administrator**
        - **全局管理员**
    
    - After the workspace has been created, you can then use the following roles with fewer permissions to view the data collected:
    
        - **安全读取者**
        - **Global reader**
    
    > [!NOTE] 
    > You cannot use the Azure Information Protection administrator role, the Security reader role, or the Global reader role if your tenant is on the [unified labeling platform](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

2. 此外，还需要具有以下 [Azure Log Analytics 角色](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)或标准 [Azure 角色](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-rbac-roles)之一才能访问 Azure Log Analytics 工作区：
    
    - 若要创建该工作区或创建自定义查询，必须具有以下角色之一：
    
        - **Log Analytics 参与者**
        - **参与者**
        - **所有者**
    
    - 创建该工作区后，可以使用具有较少权限的以下角色之一来查看收集的数据：
    
        - **Log Analytics 读者**
        - **读者**

#### <a name="minimum-roles-to-view-the-reports"></a>查看报表至少需要的角色

为 Azure 信息保护分析配置工作区后，查看 Azure 信息保护分析报表至少需要具备以下两种角色：

- Azure AD administrator role: **Security reader**
- Azure role: **Log Analytics Reader**

但是，许多组织的典型角色分配是 Azure AD 角色“安全读取者”以及 Azure 角色“读取者”。

### <a name="storage-requirements-and-data-retention"></a>Storage requirements and data retention

The amount of data collected and stored in your Azure Information Protection workspace will vary significantly for each tenant, depending on factors such as how many Azure Information Protection clients and other supported endpoints you have, whether you're collecting endpoint discovery data, you've deployed scanners, the number of protected documents that are accessed, and so on.

However, as a starting point, you might find the following estimates useful:

- For audit data generated by Azure Information Protection clients only: 2 GB per 10,000 active users per month.

- For audit data generated by Azure Information Protection clients, scanners, and Microsoft Defender ATP: 20 GB per 10,000 active users per month.

If you use mandatory labeling or you've configured a default label for most users, your rates are likely to be significantly higher.

Azure Monitor Logs has a **Usage and estimated costs** feature to help you estimate and review the amount of data stored, and you can also control the data retention period for your Log Analytics workspace. For more information, see [Manage usage and costs with Azure Monitor Logs](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>配置报表的 Log Analytics 工作区

1. 如果尚未这样做，请打开新的浏览器窗口，使用拥有[执行 Azure 信息保护分析所需权限](#permissions-required-for-azure-information-protection-analytics)的帐户[登录 Azure 门户](https://portal.azure.com)。 然后导航到“Azure 信息保护”窗格。 
    
    For example, in the search box for resources, services, and docs: Start typing **Information** and select **Azure Information Protection**.
    
2. 找到“管理”菜单选项，然后选择“配置分析（预览版）”。

3. On the **Azure Information Protection log analytics** pane, you see a list of any Log Analytics workspaces that are owned by your tenant. 执行以下操作之一：
    
    - To create a new Log Analytics workspace: Select **Create new workspace**, and on the **Log analytics workspace** pane, supply the requested information.
    
    - 若要使用现有 Log Analytics 工作区：从列表中选择工作区。
    
    如果需要关于创建 Log Analytics 工作区的帮助，请参阅[在 Azure 门户中创建 Log Analytics 工作区](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)。

4. If you have Azure Information Protection clients (classic), select the checkbox **Enable deeper analytics into your sensitive data** if you want to store the actual data that's identified as being a sensitive information type. For more information about this setting, see the [Content matches for deeper analysis](#content-matches-for-deeper-analysis) section on this page.

5. 选择“确定”。

You're now ready to view the reports.

## <a name="how-to-view-the-reports"></a>如何查看报告

From the Azure Information Protection pane, locate the **Dashboards** menu options, and select one of the following options:

- 使用情况报表（预览版）：使用此报表查看标签是如何使用的。

- **活动日志（预览版）** ：使用此报表可查看用户执行的标记操作，以及在设备中和对文件路径执行的标记操作。 In addition, for protected documents, you can see access attempts (successful or denied) for users both inside and outside your organization, even if they don't have the Azure Information Protection client installed
    
    此报表有“列”选项，可用于显示比默认显示更多的活动信息。 还可以选择它来显示“活动详细信息”，方便查看文件相关的更多详细信息。

- **Data discovery (Preview)** : Use this report to see information about labeled files found by scanners and supported endpoints.
    
    Tip: From the information collected, you might find users accessing files that contain sensitive information from location that you didn't know about or aren't currently scanning:
    
    - 如果这些位置在本地环境中，请考虑添加这些位置作为 Azure 信息保护扫描程序的附加数据存储库。
    - 如果这些位置在云中，请考虑使用 Microsoft Cloud App Security 对其进行管理。 
    
- **Recommendations (Preview)** : Use this report to identify files that have sensitive information and mitigate your risk by following the recommendations.
    
    选择项目时，“查看数据”选项将显示触发了建议的审核活动。


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>如何修改报表并创建自定义查询

Select the query icon in the dashboard to open a **Log Search** pane: 

![自定义 Azure 信息保护报表的 Log Analytics 图标](./media/log-analytics-icon.png)


Azure 信息保护的记录数据存储在下表中：InformationProtectionLogs_CL

创建你自己的查询时，请使用已作为 InformationProtectionEvents 函数实现的友好架构名称。 这些函数派生自自定义查询支持的属性（某些属性仅供内部使用），它们的名称不会随时间的推移而发生更改，即使在更改基础属性以实现改进功能和新功能时也不例外。

### <a name="friendly-schema-reference-for-event-functions"></a>事件函数的友好架构参考

使用下表来标识可用于通过 Azure 信息保护分析进行自定义查询的事件函数的友好名称。

|Column name|描述|
|-----------|-----------|
|时间|Event time: UTC in format YYYY-MM-DDTHH:MM:SS|
|User|User: Format UPN or DOMAIN\USER|
|ItemPath|Full item path or email subject|
|ItemName|File name or email subject |
|方法|Label assigned method: Manual, Automatic, Recommended, Default, or Mandatory|
|活动|Audit activity: DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, Discover, Access, RemoveCustomProtection, ChangeCustomProtection, or NewCustomProtection |
|LabelName|Label name (not localized)|
|LabelNameBefore |Label name before change (not localized) |
|ProtectionType|Protection type [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|ProtectionBefore|Protection type before change [JSON] |
|MachineName |FQDN when available; otherwise host name|
|DeviceRisk|Device risk score from WDATP when available|
|平台|Device platform (Win, OSX, Android, iOS) |
|ApplicationName|Application friendly name|
|AIPVersion|Version of the Azure Information Protection client that performed the audit action |
|TenantId|Azure AD 租户 ID |
|AzureApplicationId|Azure AD registered application ID (GUID)|
|ProcessName|Process that hosts MIP SDK|
|LabelId|Label GUID or null|
|IsProtected|Whether protected: Yes/No |
|ProtectionOwner |Rights Management owner in UPN format|
|LabelIdBefore|Label GUID or null before change|
|InformationTypesAbove55|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 55 or above |
|InformationTypesAbove65|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 65 or above |
|InformationTypesAbove75|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 75 or above |
|InformationTypesAbove85|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 85 or above |
|InformationTypesAbove95|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 95 or above|
|DiscoveredInformationTypes |JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data and their matched content (if enabled) where an empty array means no information types found, and null means no information available |
|ProtectedBefore|Whether the content was protected before change: Yes/No |
|ProtectionOwnerBefore|Rights Management owner before change |
|UserJustification|Justification when downgrading or removing label|
|LastModifiedBy|User in UPN format who last modified the file. Available for Office and SharePoint Online only|
|LastModifiedDate|UTC in format YYYY-MM-DDTHH:MM:SS: Available for Office & SharePoint Online only |


#### <a name="examples-using-informationprotectionevents"></a>使用 InformationProtectionEvents 的示例

使用以下示例了解如何使用友好的架构来创建自定义查询。

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>Example 1: Return all users who sent audit data in the last 31 days 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>Example 2: Return the number of labels that were downgraded per day in the last 31 days 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>Example 3: Return the number of labels that were downgraded from Confidential by user, in the last 31 days 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

在此示例中，仅当操作前的标签名包含名称“机密”且操作后的标签名不包含名称“机密”时，才会对降级的标签计数。 


## <a name="next-steps"></a>后续步骤
After reviewing the information in the reports, if you are using the Azure Information Protection client, you might decide to make changes to your Azure Information Protection policy. 有关说明，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

如果你有 Microsoft 365 订阅，则还可以在 Microsoft 365 合规中心和 Microsoft 365 安全中心中查看标签使用情况。 有关详细信息，请参阅[使用标签分析查看标签使用情况](/microsoft-365/compliance/label-analytics)。
