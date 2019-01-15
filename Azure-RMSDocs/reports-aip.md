---
title: Azure 信息保护的中心报告
description: 如何使用中心报告来跟踪 Azure 信息保护标签的采用和标识包含敏感信息的文件
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 0c2309fb635a05f6b0c836b7d4caf04d1c17a23a
ms.sourcegitcommit: 6651546fa69538e2099b5c2b92ab0902d568a96a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2018
ms.locfileid: "53815116"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure 信息保护的中心报告

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

> [!NOTE]
> 此功能目前处于预览状态，随时可能更改。 当此功能正式发布后，在此预览期间收集的任何数据可能不再受支持。

下表中的 PDF 阅读器支持具有 .ppdf 文件扩展名的受保护的 PDF 文档和具有 .pdf 文件扩展名的旧格式。 此外：

- 下表中的 PDF 阅读器支持具有 .ppdf 文件扩展名的受保护的 PDF 文档和具有 .pdf 文件扩展名的旧格式。 

- 标识包含必须保护的敏感信息的文档。

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
    
报表使用 [Azure Log Analytics](/azure/log-analytics/log-analytics-overview) 将数据存储在组织拥有的工作区中。 如果你熟悉查询语言，可以修改这些查询，并创建新报表和 Power BI 仪表板。 以下教程可能有助于你了解查询语言：[Analytics 门户入门](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-the-Analytics-portal)。 

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

此信息存储在组织拥有的 Azure Log Analytics 工作区中，并可供有权访问此工作区的用户查看。 有关配置对你的工作区访问权限的信息，请参阅 Azure 文档中的[管理帐户和用户](/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor#manage-accounts-and-users)部分。

> [!NOTE]
> Azure 信息保护的 Azure Log Analytics 工作区包含一个文档内容匹配复选框。 选中此复选框时，还将收集由敏感信息类型或自定义条件标识的实际数据。 例如，这可以包括查找到的信用卡号码，以及社会安全号码、护照号码和银行帐户号码。 如果不想收集此数据，请不要选中此复选框。
>
> 目前，此类信息未在报告中显示，但可以通过查询进行查看和检索。

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Azure 信息保护分析的先决条件
若要查看 Azure 信息保护报表和创建你自己的报表，请确保满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|包含 Log Analytics 的 Azure 订阅|请参阅 [Azure Log Analytics 定价](https://azure.microsoft.com/pricing/details/log-analytics)页面。<br /><br />如果没有 Azure 订阅或当前未使用 Azure Log Analytics，定价页将包含免费试用版的链接。|
|Azure 信息保护客户端的当前正式版。|如果尚未安装此版本的客户端，可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载和安装它。|
|对于“发现和风险”报表： <br /><br />- 若要显示本地数据存储中的数据，你至少已部署其中一个 Azure 信息保护扫描程序的实例（当前 GA 版） <br /><br />- 若要显示 Windows 10 计算机中的数据，这些计算机必须为最低版本 1809，你在使用 Windows Defender 高级威胁防护 (Windows Defender ATP)，并且你已从 Windows Defender 安全中心启用 Azure 信息保护集成功能|有关扫描程序的安装说明，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。 如果从以前版本的扫描程序升级，请参阅[升级 Azure 信息保护扫描程序](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。<br /><br />有关从 Windows Defender 安全中心配置和使用 Azure 信息保护集成功能的信息，请参阅 [Windows 中的信息保护概述](/windows/security/threat-protection/windows-defender-atp/information-protection-in-windows-overview)。|

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>配置报表的 Log Analytics 工作区

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。
    
2. 找到“管理”菜单选项，然后选择“配置分析（预览版）”。

3. 在“Azure 信息保护日志分析”边栏选项卡上，可以看到由你的租户拥有的任何 Log Analytics 工作区的列表。 执行以下操作之一：
    
    - 创建新的 Log Analytics 工作区：请选择“创建新工作区”，并在“Log Analytics 工作区”边栏选项卡上提供所需信息。
    
    - 使用现有的 Log Analytics 工作区：从列表中选择工作区。

如果需要关于创建 Log Analytics 工作区的帮助，请参阅[在 Azure 门户中创建 Log Analytics 工作区](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)。

配置工作区后，即可开始查看报表。

## <a name="how-to-view-the-reports"></a>如何查看报告

在“Azure 信息保护”边栏选项卡中，找到“仪表板”菜单选项，然后选择以下选项之一：

- **使用情况报表(预览版)**：使用此报表查看标签是如何使用的。 

- **活动日志(预览版)**：使用此报表查看用户执行的标记操作，以及设备上和对文件路径执行的标记操作。
    
    此报表目前正在向租户推出，因此如果看不到它，请在几天后重试。
    
    此报表有“列”选项，可用于显示默认显示信息之外的更多活动信息。

- **数据发现(预览版)**：使用此报表查看扫描程序或 Windows Defender ATP 找到的文件的相关信息。

> [!NOTE]
> 当“发送操作系统区域设置”为英语时，会出现一个当前已知的问题，即在路径和文件名中显示问号 (?)，而不是非 ASCII 字符。

## <a name="how-to-modify-the-reports"></a>如何修改报表

选择仪表板中的查询图标以打开“日志搜索”边栏选项卡： 

![自定义 Azure 信息保护报表的 Log Analytics 图标](./media/log-analytics-icon.png)


Azure 信息保护的记录数据存储在下表中：**InformationProtectionLogs_CL**

## <a name="next-steps"></a>后续步骤
查看报表中的信息后，你可能会决定对你的 Azure 信息保护策略进行更改。 有关说明，请参阅[配置 Azure 信息保护策略](configure-policy.md)。