---
title: Azure 信息保护的中心报告
description: 如何使用中心报告来跟踪 Azure 信息保护标签的采用和标识包含敏感信息的文件
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/07/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 4cb496e6cca01d7a4ad6636acc315bd40dc4c58c
ms.sourcegitcommit: 8e43a41998045fe574710e9da0b7747eaeccdba1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2018
ms.locfileid: "51273576"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure 信息保护的中心报告

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

> [!NOTE]
> 此功能目前处于预览状态，随时可能更改。 当此功能正式发布后，在此预览期间收集的任何数据可能不再受支持。


为中心报告使用 Azure 信息保护分析，以跟踪 Azure 信息保护标签的采用，并监视用户对标记的文档和电子邮件的访问，以及对其分类所做的任何更改。 此外，还可以标识包含敏感信息的文档（必须对这些文档进行保护）。

你看到的数据是从 Azure 信息保护客户端、Azure 信息保护扫描程序以及[支持统一标记的客户端](configure-policy-migrate-labels.md#clients-that-support-unified-labeling)聚合的。

例如，你将能够看到以下数据：

- 在“使用情况报表”中，你可以选择时间段：
    
    - 应用的标签
    
    - 被标记的文档和电子邮件数
    
    - 被保护的文档和电子邮件数
    
    - 标记文档和电子邮件的用户和设备数
    
    - 用于标记的应用程序

- 在“数据发现”报表中：

    - 扫描的数据存储库上的文件
    
    - 被标记和被保护的文件，以及按标签分类的文件的位置
    
    - 包含已知类别的敏感信息（例如财务数据和个人信息）的文件，以及按这些类别分类的文件的位置
    
报表使用 [Azure Log Analytics](/azure/log-analytics/log-analytics-overview) 将数据存储在你拥有的工作区中。 如果你熟悉查询语言，可以修改这些查询，并创建新报表和 Power BI 仪表板。 以下教程可能有助于你了解查询语言：[Analytics 门户入门](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-the-Analytics-portal)。 

有关详细信息，请参阅博客文章：[Microsoft 信息保护中有关你的所有数据的数据发现、报告和分析](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)。

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

此信息存储在由你拥有并且可以由具有此工作区访问权限的用户查看的 Azure Log Analytics 工作区中。 有关配置对你的工作区访问权限的信息，请参阅 Azure 文档中的[管理帐户和用户](/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor#manage-accounts-and-users)部分。

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Azure 信息保护分析的先决条件
若要查看 Azure 信息保护报表和创建你自己的报表，请确保满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|包含 Log Analytics 的 Azure 订阅|请参阅 [Azure Log Analytics 定价](https://azure.microsoft.com/pricing/details/log-analytics)页面。<br /><br />如果没有 Azure 订阅或当前未使用 Azure Log Analytics，定价页将包含免费试用版的链接。|
|Azure 信息保护客户端的当前预览版。|如果你尚未安装客户端的当前预览版，可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载和安装它。|
|对于“发现和风险”报表： <br /><br />- 你至少已部署其中一个 Azure 信息保护扫描程序的实例（当前预览版）|有关安装说明，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。 <br /><br />如果从以前版本的扫描程序升级，请参阅[升级 Azure 信息保护扫描程序](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。|


## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>配置报表的 Log Analytics 工作区

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。
    
2. 找到“管理”菜单选项，然后选择“配置分析（预览版）”。

3. 在“Azure 信息保护日志分析”边栏选项卡上，可以看到由你的租户拥有的任何 Log Analytics 工作区的列表。 执行以下操作之一：
    
    - 若要新建 Log Analytics 工作区，请选择“创建新工作区”，并在“Log Analytics 工作区”边栏选项卡上提供所需信息。
    
    - 若要使用现有 Log Analytics 工作区：从列表中选择工作区。

如果需要创建 Log Analytics 工作区的帮助，请参阅[在 Azure 门户中创建 Log Analytics 工作区](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)。

配置工作区后，即可开始查看报表。

## <a name="how-to-view-the-reports"></a>如何查看报告

在“Azure 信息保护”边栏选项卡中，找到“仪表板”菜单选项，然后选择以下选项之一：

- 使用情况报表（预览版）：使用此报表查看标签是如何使用的。 

- 数据发现（预览版）：使用此报表以查看有关扫描程序找到的文件的信息。

## <a name="how-to-modify-the-reports"></a>如何修改报表

选择仪表板中的查询图标以打开“日志搜索”边栏选项卡： 

![自定义 Azure 信息保护报表的 Log Analytics 图标](./media/log-analytics-icon.png)


Azure 信息保护的记录数据存储在下表中：InformationProtectionLogs_CL

## <a name="next-steps"></a>后续步骤
查看报表中的信息后，你可能会决定对你的 Azure 信息保护策略进行更改。 有关说明，请参阅[配置 Azure 信息保护策略](configure-policy.md)。