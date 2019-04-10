---
title: Azure 信息保护的中心报告
description: 如何使用中心报告来跟踪 Azure 信息保护标签的采用和标识包含敏感信息的文件
author: cabailey
ms.author: cabailey
ms.date: 04/02/2019
manager: barbkess
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: e24b143c64957fb4336effc4cac6666b374f3a15
ms.sourcegitcommit: 8da0aa8f9bb9f91375580a703682d23a81a441bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58809958"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure 信息保护的中心报告

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

> [!NOTE]
> 此功能目前处于预览状态，随时可能更改。

下表中的 PDF 阅读器支持具有 .ppdf 文件扩展名的受保护的 PDF 文档和具有 .pdf 文件扩展名的旧格式。 此外：

- 下表中的 PDF 阅读器支持具有 .ppdf 文件扩展名的受保护的 PDF 文档和具有 .pdf 文件扩展名的旧格式。 

- 确定包含敏感信息且若未保护则可能给组织带来风险的文档，并按照以下建议缓解风险。

当前，你看到的数据是从 Azure 信息保护客户端和 Azure 信息保护扫描程序，以及运行 [Windows Defender 高级威胁防护 (Windows Defender ATP)](/windows/security/threat-protection/windows-defender-atp/overview) 的 Windows 计算机聚合的。

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
    
    - 特定应用程序已执行的标记操作，如文件资源管理器（右键单击）或 AzureInformationProtection PowerShell 模块

- 在“数据发现”报表中：

    - 扫描的数据存储库或 Windows 10 计算机上的文件
    
    - 被标记和被保护的文件，以及按标签分类的文件的位置
    
    - 包含已知类别的敏感信息（例如财务数据和个人信息）的文件，以及按这些类别分类的文件的位置

- 在“建议”报告中：
    
    - 识别包含已知敏感信息类型但未受保护的文件。 按照建议操作，可立即对其中一个标签配置相应的条件，以应用自动标签或推荐的标签。
        
        如果按照建议进行操作：在用户下次打开或 Azure 信息保护扫描程序下次扫描文件时，这些文件可自动分类并自动受到保护。
    
    - 其文件具有已标识的敏感信息但其本身当前未被 Azure 信息保护服务扫描的数据存储库。 按照建议操作，可立即向扫描程序的某个配置文件添加已标识的数据存储。
        
        如果按照建议进行操作：在下一次扫描周期，文件可自动分类并自动受到保护。

报表使用 [Azure Monitor](/azure/log-analytics/log-analytics-overview) 将数据存储在组织拥有的 Log Analytics 工作区中。 如果你熟悉查询语言，可以修改这些查询，并创建新报表和 Power BI 仪表板。 以下教程可能有助于你了解查询语言：[Azure Monitor 日志查询入门](/azure/azure-monitor/log-query/get-started-queries)。 

有关详细信息，请参阅以下博客文章： 

- [Microsoft 信息保护中有关所有数据的数据发现、报告和分析](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)

- [通过 Azure 信息保护和 Windows Defender ATP 发现和保护敏感数据](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>收集和发送到 Microsoft 的信息

为了生成这些报表，终结点将以下类型的信息发送到 Microsoft：

- 标签操作。 例如，设置标签、更改标签、添加或删除保护、自动和建议的标签。

- 标签操作之前和之后的标签名称。

- 组织的租户 ID。

- 用户 ID（电子邮件地址或 UPN）。

- 用户设备的名称。

- 对于文档：被标记的文档的文件路径和文件名。

- 对于电子邮件：被标记的电子邮件的电子邮件主题、电子邮件发件人和电子邮件收件人。 

- 在内容中已检测到的敏感信息类型（[预定义](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)和自定义）。

- Azure 信息保护客户端版本。

- 客户端操作系统版本。

此信息存储在组织拥有的 Azure Log Analytics 工作区中，并可供有权访问此工作区的用户从 Azure 信息保护独立查看。 有关详细信息，请参阅 [Azure 信息保护分析的必备权限](#permissions-required-for-azure-information-protection-analytics)部分。 要了解如何管理对工作区的访问，请参阅 Azure 文档中的[使用 Azure 权限管理对 Log Analytics 工作区的访问](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions)部分。

若要阻止 Azure 信息保护客户端发送此数据，请将“将审核数据发送到 Azure 信息保护日志分析”的[策略设置](configure-policy-settings.md)设置为“关闭”：

- 若要使大多数用户发送此数据，而使一部分用户无法发送审核数据，请执行以下操作： 
    - 在部分用户的作用域内策略中将“将审核数据发送到 Azure 信息保护日志分析”设置为“关闭”。 此配置专用于生产方案。
    
- 若要仅使一部分用户发送审核数据，请执行以下操作： 
    - 在全局策略中将“将审核数据发送到 Azure 信息保护日志分析”设置为“关闭”，在部分用户的作用域内策略中设置为“打开”。 此配置专用于测试方案。

#### <a name="content-matches-for-deeper-analysis"></a>更深入分析的内容匹配项 

Azure 信息保护的 Azure Log Analytics 工作区包括用于收集和存储由敏感信息类型或自定义条件标识的数据的复选框。 例如，这可以包括查找到的信用卡号码，以及社会安全号码、护照号码和银行帐户号码。 如果不想发送此额外数据，请不要选中此复选框。 如果你希望大多数用户发送此额外数据，而一部分用户无法发送该数据，请选中此复选框并在该部分用户的作用域内策略中配置[高级客户端设置](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)。

收集内容匹配项后，当你向下钻取到活动日志中的文件以显示活动详细信息时，这些匹配项项将显示在报表中。 也可以使用查询来查看和检索此信息。

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Azure 信息保护分析的先决条件
若要查看 Azure 信息保护报表和创建你自己的报表，请确保满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|包含 Log Analytics 的 Azure 订阅|请参阅 [Azure Monitor 定价](https://azure.microsoft.com/pricing/details/log-analytics)页。<br /><br />如果没有 Azure 订阅或当前未使用 Azure Log Analytics，定价页将包含免费试用版的链接。|
|Azure 信息保护客户端（预览版或当前的正式发布版）或 Azure 信息保护统一标签客户端的预览版|如果尚未安装任何版本的客户端，可以从 Microsoft 下载中心下载和安装这些版本：<br /> - [Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018) <br /> - [Azure 信息保护统一标记客户端](https://www.microsoft.com/en-us/download/details.aspx?id=57440)|
|对于“发现和风险”报表： <br /><br />- 要显示本地数据存储中的数据，必须至少部署 Azure 信息保护扫描程序（预览版或当前的正式发布版）的一个实例 <br /><br />- 若要显示 Windows 10 计算机中的数据，这些计算机必须为最低版本 1809，你在使用 Windows Defender 高级威胁防护 (Windows Defender ATP)，并且你已从 Windows Defender 安全中心启用 Azure 信息保护集成功能|有关扫描程序的安装说明，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。 <br /><br />有关从 Windows Defender 安全中心配置和使用 Azure 信息保护集成功能的信息，请参阅 [Windows 中的信息保护概述](/windows/security/threat-protection/windows-defender-atp/information-protection-in-windows-overview)。|
|对于“建议”报告： <br /><br />- 要按照建议的操作通过 Azure 门户添加新的数据存储库，必须使用 Azure 信息保护扫描程序的当前预览版 |要部署扫描程序的预览版，请参阅[部署 Azure 信息保护扫描程序的预览版来自动分类和保护文件](deploy-aip-scanner-preview.md)。|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Azure 信息保护分析必备的先决条件

针对 Azure 信息保护分析，在配置 Azure Log Analytics 工作区后，可以使用安全读取者的 Azure AD 管理员角色替代 Azure 门户中支持管理 Azure 信息保护的其他 Azure AD 角色。

由于此功能使用 Azure 监视，因此 Azure 的基于角色的访问控制 (RBAC) 也控制对工作区的访问。 因此，需要 Azure 角色以及 Azure AD 管理员角色来管理 Azure 信息保护分析。 如果刚开始接触 Azure 角色，阅读 [Azure RBAC 角色与 Azure AD 管理员角色的区别](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles)可能会对你有所帮助。

详细信息:

1. 以下 [Azure AD 管理员角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)之一用于访问 Azure 信息保护分析边栏选项卡：
    
    - 若要创建 Log Analytics 工作区或创建自定义查询，必须具有以下角色之一：
    
        - **信息保护管理员**
        - **安全管理员**
        - **全局管理员**
    
    - 创建该工作区后，可以使用具有较少权限的以下角色来查看收集的数据：
    
        - **安全读取者**
    
    > [!NOTE] 
    > 如果租户已迁移到统一标记存储，帐户必须是全局管理员或所列角色之一，并有权访问 Office 365 安全与合规中心。 [详细信息](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

2. 此外，还需要具有以下 [Azure Log Analytics 角色](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#managing-access-to-log-analytics-using-azure-permissions)或标准 [Azure 角色](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments)之一才能访问 Azure Log Analytics 工作区：
    
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

但是，许多组织的典型角色分配是安全读取者的 Azure AD 角色以及读者的 Azure 角色。

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>配置报表的 Log Analytics 工作区

1. 如果尚未这样做，请打开新的浏览器窗口，使用拥有[执行 Azure 信息保护分析所需权限](#permissions-required-for-azure-information-protection-analytics)的帐户[登录 Azure 门户](https://portal.azure.com)。 然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。
    
2. 找到“管理”菜单选项，然后选择“配置分析（预览版）”。

3. 在“Azure 信息保护日志分析”边栏选项卡上，可以看到由你的租户拥有的任何 Log Analytics 工作区的列表。 执行以下操作之一：
    
    - 创建新的 Log Analytics 工作区：请选择“创建新工作区”，并在“Log Analytics 工作区”边栏选项卡上提供所需信息。
    
    - 使用现有的 Log Analytics 工作区：从列表中选择工作区。

如果需要关于创建 Log Analytics 工作区的帮助，请参阅[在 Azure 门户中创建 Log Analytics 工作区](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)。

配置工作区后，即可开始查看报表。

> [!NOTE]
> 首次在报表中显示数据当前存在已知问题。 如果你遇到这种情况，请在全局策略中将“将审核数据发送到 Azure 信息保护日志分析”的[策略设置](configure-policy-settings.md)设置为“关闭”并保存策略。 然后，将相同设置更改为“打开”并保存策略。 客户端[下载更改](configure-policy.md#making-changes-to-the-policy)后，审核事件可能需要最多 30 分钟才能在 Log Analytics 工作区中显示。

## <a name="how-to-view-the-reports"></a>如何查看报告

在“Azure 信息保护”边栏选项卡中，找到“仪表板”菜单选项，然后选择以下选项之一：

- **使用情况报表(预览版)**：使用此报表查看标签是如何使用的。 

- **活动日志(预览版)**：使用此报表查看用户执行的标记操作，以及设备上和对文件路径执行的标记操作。
    
    此报表有“列”选项，可用于显示默认显示信息之外的更多活动信息。

- **数据发现(预览版)**：使用此报表查看扫描程序或 Windows Defender ATP 找到的文件的相关信息。

- 建议（预览）：使用此报告来确定包含敏感信息的文件，并按照建议缓解风险。
    
    此报表目前正在向租户推出，因此如果看不到它，请在几天后重试。
    
    选择项目时，“查看数据”选项将显示触发了建议的审核活动。

> [!NOTE]
> 当“发送操作系统区域设置”为英语时，会出现一个当前已知的问题，即在路径和文件名中显示问号 (?)，而不是非 ASCII 字符。

## <a name="how-to-modify-the-reports"></a>如何修改报表

选择仪表板中的查询图标以打开“日志搜索”边栏选项卡： 

![自定义 Azure 信息保护报表的 Log Analytics 图标](./media/log-analytics-icon.png)


Azure 信息保护的记录数据存储在下表中：**InformationProtectionLogs_CL**

## <a name="next-steps"></a>后续步骤
查看报表中的信息后，你可能会决定对你的 Azure 信息保护策略进行更改。 有关说明，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

如果你有 Microsoft 365 订阅，则还可以在 Microsoft 365 合规中心和 Microsoft 365 安全中心中查看标签使用情况。 有关详细信息，请参阅[使用标签分析查看标签使用情况](/Office365/SecurityCompliance/label-analytics)。
