---
title: 教程 - 使用 Azure 信息保护 (AIP) 扫描程序发现敏感内容
description: 使用 Azure 信息保护 (AIP) 扫描程序查找可能面临风险的存储库。 然后，向下钻取以扫描这些文件共享来查看敏感内容。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: b55178f6cd0bef2fa14eb7fcf9ecaefa3ea75f7a
ms.sourcegitcommit: df6ee1aca02e089e3a72006ecf0747f14213979c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "94503666"
---
# <a name="tutorial-discovering-your-sensitive-content-with-the-azure-information-protection-aip-scanner"></a>教程：使用 Azure 信息保护 (AIP) 扫描程序发现敏感内容

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：[用于 Windows 的 Azure 信息保护统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

Azure 信息保护客户端提供了本地扫描程序，这样系统管理员就可以扫描网络和本地文件存储库，以发现敏感内容。 

本教程介绍以下操作：

> [!div class="checklist"]
> * 创建网络扫描作业并扫描有风险的存储库
> * 将找到的任何有风险的存储库添加到内容扫描作业
> * 扫描内容共享以获取敏感内容并理解找到的结果

> [!NOTE]
> 网络发现仅在统一标记客户端的 [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 版本中开始提供，目前为预览版。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。
>
> 如果未安装此版本的客户端和扫描程序，请查看[教程先决条件](#tutorial-prerequisites)，然后直接转到[定义并运行内容扫描作业](#define-and-run-your-content-scan-job)。


所需时间：在 15 分钟内即可完成此配置。

## <a name="tutorial-prerequisites"></a>教程先决条件

|要求  |说明  |
|---------|---------|
|支持订阅     |  你需要包含 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection/)的 Azure 订阅。 <br /><br />如果没有上述任一订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。       |
|对 Azure 门户的管理员访问权限 |请确保可以使用受支持的管理员帐户登录到 [Azure 门户](https://portal.azure.com/)，并已启用保护。 受支持的管理员帐户包括： <br /><br />- 合规性管理员<br />- 合规性数据管理员<br />- 安全管理员<br />- 全局管理员   |
|AIP 客户端、扫描程序和网络发现服务   |   若要完全完成本教程，你需要安装 Azure 信息保护统一标记客户端和扫描程序，以及网络发现服务（公共预览版）。 <br /><br />有关详情，请参阅： <br /><br />- [快速入门：部署 Azure 信息保护 (AIP) 统一标记客户端](quickstart-deploy-client.md) <br />- [教程：安装 Azure 信息保护 (AIP) 统一标记扫描程序](tutorial-install-scanner.md) |
|内容扫描作业 | 请确保你有可用于测试的基本内容扫描作业。 [安装扫描程序](tutorial-install-scanner.md)时，可能已创建了这样一个作业。<br /><br />如果需要现在创建，可以使用[在 Azure 门户中配置 Azure 信息保护](tutorial-install-scanner.md#configure-azure-information-protection-in-the-azure-portal)中的说明。 当你拥有基本的内容扫描作业时，请返回此处完成本教程。 |
|**SQL Server**     | 若要运行扫描程序，你需要在扫描程序计算机上安装 SQL Server。 <br /><br /> 若要安装，请转到 [SQL Server 下载页](https://www.microsoft.com/sql-server/sql-server-downloads)，然后选择要安装的安装选项下的“立即下载”。 在安装程序中，选择“基本”安装类型。 <br /><br />**注意**：我们建议为生产环境安装 SQL Server Enterprise，仅为测试安装 Express。    |
|**Azure Active Directory 帐户**     |  使用标准的云连接环境时，域帐户必须同步到 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)。 如果正在脱机工作，则不需要这样做。 <br /><br />如果你不确定你的帐户，请联系你的系统管理员来验证同步状态。 有关详细信息，请参阅[使用备用配置部署扫描程序](deploy-aip-scanner-prereqs.md#deploying-the-scanner-with-alternative-configurations)。  |
|敏感度标签和已发布的策略 |必须已创建敏感度标签，并将至少有一个标签的策略发布到标记管理中心，用于扫描程序服务帐户。 <br /><br />在标记管理中心（包括 Microsoft 365 合规中心、Microsoft 365 安全中心或 Microsoft 365 安全与合规中心）配置敏感度标签。 有关详细信息，请参阅 [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels)。 |
| | | 


准备就绪后，请继续[创建网络扫描作业](#create-a-network-scan-job)。

## <a name="create-a-network-scan-job"></a>创建网络扫描作业

创建网络扫描作业以扫描指定的 IP 地址或 IP 范围以获取有风险的存储库。

> [!NOTE]
> 此功能仅从版本 [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 开始提供，并且当前处于预览阶段。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。
> 

若要创建网络扫描作业：

1. 作为[受支持的管理员](#tutorial-prerequisites)登录到 [Azure 门户](https://portal.azure.com/)，然后导航到“Azure 信息保护”区域。
        
1. 在左侧的“扫描程序”菜单中，选择 :::image type="icon" source="media/qs-tutor/i-network-scan-jobs.png" border="false":::“网络扫描作业(预览版)” 。

1. 选择 :::image type="icon" source="media/i-add.PNG" border="false":::“添加”以添加新规则。 在“添加新网络扫描作业”窗格中，输入以下详细信息：
    
    |选项  |说明  |
    |---------|---------|
    |“网络扫描作业名称”和“说明”      |输入有意义的名称（例如 `Quickstart`）和可选说明。         |
    |选择群集     | 从下拉列表中选择群集名称。<br /><br /> 例如，如果你已完成[教程：安装 Azure 信息保护 (AIP) 统一标记扫描程序](tutorial-install-scanner.md)，并仍可使用该群集，请选择“快速入门”。       |
    |**配置要发现的 IP 范围**     | 选择打开“选择 IP 范围”窗格的行。 在此处输入要扫描的 IP 地址或 IP 范围。 <br /><br />**注意**：确保输入可从扫描程序计算机访问的 IP 地址。      |
    |设置计划     | 保留默认值“一次”。        |
    |设置开始时间 (UTC)     |  计算当前 UTC 时间，考虑当前时区，然后将运行开始时间设置为从现在开始的 5 分钟后。     |
    |     |         |

    例如： 

    :::image type="content" source="media/qs-tutor/network-scan-job.png" alt-text="输入网络扫描作业的详细信息":::

1. 选择页面顶部的 :::image type="icon" source="media/qs-tutor/save-icon.png" border="false":::“保存”。

1. 返回到 :::image type="icon" source="media/qs-tutor/i-network-scan-jobs.png" border="false":::“网络扫描作业(预览版)”网格，然后等待扫描开始运行。

扫描完成后，将更新网格数据。 例如：

:::image type="content" source="media/qs-tutor/scanned-network.png" alt-text="已刷新的网络扫描作业":::

> [!TIP]
> 如果网络扫描作业未运行，请检查并确保在扫描程序计算机上[已正确安装网络发现服务](tutorial-install-scanner.md#install-the-network-discovery-service)。

继续[将有风险的存储库添加到内容扫描作业](#add-risky-repositories-to-a-content-scan-job)。

## <a name="add-risky-repositories-to-a-content-scan-job"></a>将有风险的存储库添加到内容扫描作业

完成网络扫描作业后，可以检查找到的任何有风险的存储库。 

例如，如果发现存储库同时具有读取和写入公共访问权限，可能需要进一步扫描并确认没有在其中存储敏感数据。

> [!NOTE]
> 此功能仅从版本 [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 开始提供，并且当前处于预览阶段。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。
> 

将有风险的存储库添加到内容扫描作业：

1. 作为[受支持的管理员](#tutorial-prerequisites)登录到 [Azure 门户](https://portal.azure.com/)，然后导航到“Azure 信息保护”窗格。
        
1. 在左侧的“扫描程序”菜单中，选择 :::image type="icon" source="media/qs-tutor/i-repos.png" border="false":::“存储库(预览版)” 。

    :::image type="content" source="media/small/risky-repos-small.png" alt-text="查看网络扫描作业找到的存储库" lightbox="media/qs-tutor/risky-repos.png":::

1. 在图表下方的网格中，找到尚未由扫描程序管理的存储库。 未由扫描程序管理意味着它们不包括在内容扫描作业中，不会扫描其中的敏感内容。

    > [!TIP]
    > 例如，发现为 R（读取）或 RW（读/写）的有效公共访问权限的存储库可供公众使用，并且可能有敏感内容存在风险  。
    > 

1. 选择行，然后在网格的上方选择 :::image type="icon" source="media/i-add.PNG" border="false":::“分配所选项”。 

1. 在右侧显示的“分配到内容扫描作业”窗格中，从下拉列表中选择内容扫描作业，然后选择 :::image type="icon" source="media/qs-tutor/save-icon.png" border="false":::“保存” 。

    例如：

    :::image type="content" source="media/qs-tutor/assign-content-scan-job.png" alt-text="将有风险的存储库分配到内容扫描作业":::

下次运行内容扫描作业时，它现在将包括此新发现的存储库，并识别、标记、分类和保护策略中配置的任何敏感内容。

继续[定义并运行内容扫描作业](#define-and-run-your-content-scan-job)。

## <a name="define-and-run-your-content-scan-job"></a>定义并运行内容扫描作业

使用通过[教程先决条件](#tutorial-prerequisites)准备的内容扫描作业来扫描内容。 

如果还没有内容扫描作业，请执行[在 Azure 门户中配置初始设置](tutorial-install-scanner.md#configure-initial-scanner-settings-in-the-azure-portal)，然后返回到此处以继续。


1. 作为[受支持的管理员](#tutorial-prerequisites)登录到 [Azure 门户](https://portal.azure.com/)，然后导航到“Azure 信息保护”窗格。
        
1. 在左侧的“扫描程序”菜单中，选择 :::image type="icon" source="media/i-content-scan-jobs.png" border="false":::“内容扫描作业”，然后选择你的内容扫描作业 。
 
1. 编辑内容扫描作业设置，确保提供有意义的名称和可选说明。 

    保留大多数设置的默认值，但进行以下更改：

    -  将推荐标记视为自动。 设置为“开”。
    
    - 配置存储库。 确保至少定义了一个存储库。 
    
        > [!TIP]
        > 如果扫描网络后向内容扫描作业添加了其他存储库，如[将有风险的存储库添加到内容扫描作业](#add-risky-repositories-to-a-content-scan-job)中所述，可以选择立即在这里列出这些存储库。 

    - 强制执行。 设置为“打开”
    
1. 选择 :::image type="icon" source="media/qs-tutor/save-icon.png" border="false":::“保存”，然后返回到 :::image type="icon" source="media/i-content-scan-jobs.PNG" border="false":::“内容扫描作业”网格 。

1. 若要扫描内容，请返回到 :::image type="icon" source="media/i-content-scan-jobs.png" border="false":::“内容扫描作业”区域，然后选择你的内容扫描作业。

    在网格上方的工具栏中，选择 :::image type="icon" source="media/i-scan-now.PNG" border="false":::“立即扫描”以开始扫描。

    扫描完成后，继续[查看扫描结果](#view-scan-results)。

### <a name="view-scan-results"></a>查看扫描结果

扫描完成后，在 Azure 门户中“Azure 信息保护”>“分析”区域查看报告。

例如：

:::image type="content" source="media/qs-tutor/content-scan-job-data-discovery.PNG" alt-text="扫描程序结果分析数据发现报告":::
    
> [!TIP]
> 如果结果为空，并且你想要运行有意义的扫描，请在内容扫描作业包含的其中一个存储库中创建名为“付款信息”的文件。 保存内容如下的文件：
> 
> 信用卡：2384 2328 5436 3489
>
> 再次运行扫描以查看结果中的差异。
> 

有关详细信息，请参阅 [Azure 信息保护的中心报告（公共预览版）](reports-aip.md)

#### <a name="local-scanner-reports"></a>本地扫描程序报告

日志还本地存储在扫描程序计算机上的“%localappdata%\Microsoft\MSIP\Scanner\Reports directory”中，并包括：

|类型  |说明  |
|---------|---------|
|.txt 摘要文件     |  包括扫描所用的时间、扫描的文件数以及匹配信息类型的文件数量。       |
|.csv 详细信息文件。     | 包含扫描的每个文件的详细说明。 对于每个扫描周期，目录最多可容纳 60 个报告。         |
|     |         |

## <a name="next-steps"></a>后续步骤

有关更多教程，请参阅：

- [教程：使用 Azure 信息保护 (AIP) 防止过度共享](tutorial-preventing-oversharing.md)
- [教程：从 Azure 信息保护 (AIP) 经典客户端迁移到统一标记客户端](tutorial-migrating-to-ul.md)

**请参阅：**

- [什么是 Azure 信息保护统一标记扫描程序？](deploy-aip-scanner.md)
- [安装和部署 Azure 信息保护统一标记扫描程序的先决条件](deploy-aip-scanner-prereqs.md)
- [配置和安装 Azure 信息保护统一标记扫描程序](deploy-aip-scanner-configure-install.md)
- [运行 Azure 信息保护扫描程序](deploy-aip-scanner-manage.md)
