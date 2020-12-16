---
title: 安装和配置 Azure 信息保护 (AIP) 统一标记扫描器
description: 说明如何安装和配置 Azure 信息保护统一标记扫描器，以发现、分类和保护数据存储中的文件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e17e42850904590df6a0c223032fd07306e0815b
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583704"
---
# <a name="configuring-and-installing-the--azure-information-protection-unified-labeling-scanner"></a>配置和安装 Azure 信息保护统一标记扫描器

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2019、Windows Server 2016、windows server 2012 R2 *
>
>***相关的**： [仅限 AIP 统一标签客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关经典扫描程序，请参阅 [配置和安装 Azure 信息保护经典扫描程序](deploy-aip-scanner-configure-install-classic.md)。 *

在开始配置和安装 Azure 信息保护扫描程序之前，请确保系统符合 [所需的先决条件](deploy-aip-scanner-prereqs.md)。 

准备就绪后，请继续执行以下步骤：

1. [在 Azure 门户中配置扫描程序](#configure-the-scanner-in-the-azure-portal)

1. [安装扫描程序](#install-the-scanner)

1. [获取扫描程序的 Azure AD 令牌](#get-an-azure-ad-token-for-the-scanner)

1. [配置扫描程序以应用分类和保护](#configure-the-scanner-to-apply-classification-and-protection)
 
根据系统需要执行以下附加配置过程：

|过程  |说明  |
|---------|---------|
|[更改要保护的文件类型](#change-which-file-types-to-protect) |你可能想要扫描、分类或保护不同于默认文件类型的文件类型。 有关详细信息，请参阅 [AIP 扫描进程](deploy-aip-scanner.md#aip-scanning-process)。 |
|[升级扫描仪](#upgrading-your-scanner) | 升级扫描仪以利用最新的功能和改进。|
|[批量编辑数据存储库设置](#editing-data-repository-settings-in-bulk)| 使用导入和导出选项可以批量更改多个数据存储库。|
|[使用带有备用配置的扫描程序](#using-the-scanner-with-alternative-configurations)| 在不使用任何条件配置标签的情况下使用扫描程序 |
|[优化性能](#optimizing-scanner-performance)| 优化扫描程序性能的指导|
| | |

有关详细信息，请参阅 [扫描器的 Cmdlet 列表](#list-of-cmdlets-for-the-scanner)。

## <a name="configure-the-scanner-in-the-azure-portal"></a>在 Azure 门户中配置扫描程序

在安装扫描程序或从较旧的通用版本升级之前，请在 Azure 门户的 "Azure 信息保护" 区域中配置或验证扫描仪设置。

若要配置扫描仪： 

1. 用下列角色之一登录到 [Azure 门户](https://portal.azure.com) ：

    - **法规管理员**
    - **合规性数据管理员**
    - **安全管理员**
    - **全局管理员**

    然后，导航到 " **Azure 信息保护** " 窗格。
    
    例如，在资源、服务和文档的搜索框中，开始键入“信息”并选择“Azure 信息保护”。

1. [创建扫描仪群集](#create-a-scanner-cluster)。 此群集定义你的扫描仪，并用于识别 scanner 实例，例如在安装、升级和其他进程期间。

1.  (可选) [扫描您的网络中有风险的存储库](#create-a-network-scan-job-public-preview)。 创建一个网络扫描作业来扫描指定的 IP 地址或范围，并提供可能包含要保护的敏感内容的危险存储库的列表。  

    运行网络扫描作业，然后 [分析找到的所有有风险的存储库](#analyze-risky-repositories-found-public-preview)。

1. [创建内容扫描作业](#create-a-content-scan-job) 以定义要扫描的存储库。

### <a name="create-a-scanner-cluster"></a>创建扫描仪群集  

1. 从左侧的 "**扫描仪**" 菜单中，选择 "**群集**![群集" 图标](media/i-clusters.png "群集图标")。

1. 在 " **Azure 信息保护-群集** " 窗格上，选择 " **添加**" " ![添加图标](media/i-add.png "添加图标")"。
    
1. 在 " **添加新群集** " 窗格上，为扫描仪输入有意义的名称，并输入可选描述。 
    
    群集名称用于标识扫描程序的配置和存储库。 例如，你可以输入 **欧洲** 来识别要扫描的数据存储库的地理位置。 

    稍后将使用此名称来确定要安装或升级扫描仪的位置。

1. 选择 " **保存** 保存" ![图标](media/qs-tutor/save-icon.png "保存图标") 以保存所做的更改。

### <a name="create-a-network-scan-job-public-preview"></a> (公共预览版创建网络扫描作业) 

从版本 [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850)开始，你可以在网络中扫描有风险的存储库。 添加一个或多个发现内容扫描作业的存储库，以扫描敏感内容。

- [网络发现先决条件](#network-discovery-prerequisites)
- [创建网络扫描作业](#creating-a-network-scan-job)

> [!NOTE]
> Azure 信息保护网络发现功能目前处于预览阶段。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。 
> 

#### <a name="network-discovery-prerequisites"></a>网络发现先决条件

|先决条件  |说明  |
|---------|---------|
|**安装网络发现服务**     |   如果最近升级了扫描仪，可能仍需要安装网络发现服务。 <br /><br />运行 [**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) cmdlet 以启用网络扫描作业。      |
|**Azure 信息保护分析**     | 请确保已启用 Azure 信息保护分析。 <br /><br />在 Azure 门户中，请参阅 **Azure 信息保护 > 管理 > 配置分析 (预览版)**。 <br /><br />有关详细信息，请参阅 [Azure 信息保护的中心报告 (公共预览版) ](reports-aip.md)。|
| | |

#### <a name="creating-a-network-scan-job"></a>创建网络扫描作业

1. 登录到 Azure 门户，并中转到 " **Azure 信息保护**"。 在左侧的 " **扫描仪** " 菜单下，选择 " **网络扫描作业" (预览)** ![网络扫描作业 "图标](media/i-network-scan-jobs.png "网络扫描作业图标")。
    
1. 在 " **Azure 信息保护-网络扫描作业** " 窗格上，选择 " **添加**" " ![添加图标](media/i-add.png "添加图标")"。
    
1. 在 " **添加新的网络扫描作业** " 页上，定义以下设置：
        
    |设置  |说明  |
    |---------|---------|
    |**网络扫描作业名称**     |为此作业输入有意义的名称。  此字段为必需字段。       |
    |**说明**     |   输入有意义的说明。      |
    |选择群集     |从下拉列表中，选择要用于扫描已配置网络位置的群集。  <br /><br />**提示**：选择群集时，请确保分配的群集中的节点可以通过 SMB 访问配置的 IP 范围。      |
    |**配置要发现的 IP 范围**     |   单击定义 IP 地址或范围。 <br /><br />在 " **选择 IP 范围** " 窗格中，输入一个可选名称，然后输入范围的起始 ip 地址和结束 ip 地址。 <br /><br />**提示**：若要仅扫描特定 ip 地址，请在 " **起始 ip** " 和 " **结束 ip** " 字段中输入相同的 ip 地址。      |
    |设置计划     | 定义希望此网络扫描作业运行的频率。  <br /><br />如果选择 " **每周**"，则会出现 " **运行网络扫描作业** " 设置。 选择要在一周中的哪几天运行网络扫描作业。       |
    |设置开始时间 (UTC)     |定义希望此网络扫描作业开始运行的日期和时间。 如果已选择每日、每周或每月运行该作业，则该作业将在所选的重复周期内的指定时间运行。 <br /><br />**注意**：将日期设置为该月结束时的任何日子。 如果选择 **31**，则网络扫描作业不会在具有30天或更少30天的任何月份中运行。    |
    | | |

1. 选择 " **保存** 保存" ![图标](media/qs-tutor/save-icon.png "保存图标") 以保存所做的更改。

> [!TIP]
> 如果要使用不同的扫描程序运行相同的网络扫描，请更改在网络扫描作业中定义的群集。
> 
> 返回到 " **网络扫描作业** " 窗格，选择 " **分配到群集** " 以选择其他群集，或 **取消分配群集** ，以后再进行其他更改。 
>     

### <a name="analyze-risky-repositories-found-public-preview"></a>分析)  (公共预览版发现的危险存储库

通过网络扫描作业、内容扫描作业或在日志文件中检测到的用户访问来找到的存储库将聚合起来并在 **Scanner > 存储** 库 [图标](media/i-repositories.png "存储库图标") 窗格中列出。

如果已 [定义网络扫描作业](#create-a-network-scan-job-public-preview) ，并将其设置为在特定日期和时间运行，请等待它运行完毕，以检查结果。 运行 [内容扫描作业](#create-a-content-scan-job) 后，还可以在此处返回以查看更新后的数据。

> [!NOTE]
> Azure 信息保护 **存储库** 功能目前处于预览阶段。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。 
> 

1. 在左侧的 "**扫描仪**" 菜单下，选择 "**存储库**![存储库" 图标](media/i-repositories.png "存储库图标")。
    
    找到的存储库如下所示：
    - " **按状态显示的存储库** " 关系图显示已为内容扫描作业配置的存储库数，以及有多少存储库未配置。
    - **Access Graph 前10个非托管存储库** 列出了当前未分配到内容扫描作业的前10个存储库，以及有关其访问级别的详细信息。 访问级别可以指示存储库的风险。
    - "关系图" 列表下的表列出了找到的每个存储库及其详细信息。

1. 执行以下任一操作：
    
    |选项  |说明  |
    |---------|---------|
    |![列图标](media/i-columns.png "列图标")    | 选择要更改显示的表列的 **列** 。        |
    |![刷新图标](media/i-refresh.png "刷新图标")   | 如果扫描仪最近运行过网络扫描结果，请选择 " **刷新** " 以刷新页面。      |
    |![添加图标](media/i-add.png "添加图标")   | 选择表中列出的一个或多个存储库，然后选择 " **分配选定项** "，将其分配到内容扫描作业。          |
    |**Filter**     |   "筛选器" 行显示当前应用的任何筛选条件。 选择用于修改其设置的任何条件，或选择 " **添加筛选器** " 以添加新的筛选条件。 <br /><br />选择 " **筛选器** " 以应用所做的更改，并使用更新的筛选器刷新该表。       |
    |![Log Analytics 图标](media/i-log-analytics.png "Log Analytics 图标") |在 "非托管存储库" 关系图的右上角，单击 " **Log Analytics** " 图标以跳转到这些存储库的 Log Analytics 数据。 |
    | | |

#### <a name="repositories-with-public-access"></a>具有公共访问权限的存储库

发现 **公共访问** 具有 **读取** 或 **读/写** 功能的存储库可能具有必须保护的敏感内容。 如果 **公共访问** 为 false，则根本无法通过公共方式访问存储库。

仅当已在 [**MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery)或 [**MIPNetworkDiscoveryConfiguration**](/powershell/module/azureinformationprotection/Set-MIPNetworkDiscoveryConfiguration) cmdlet 的 **StandardDomainsUserAccount** 参数中设置弱帐户时，才会报告对存储库的公共访问。

- 这些参数中定义的帐户用于模拟将弱用户访问存储库的权限。 如果定义的弱用户可以访问存储库，这意味着可以公开访问存储库。 

- 若要确保正确报告公共访问权限，请确保在这些参数中指定的用户仅是 **域用户** 组的成员。

### <a name="create-a-content-scan-job"></a>创建内容扫描作业

深入了解你的内容，扫描敏感内容的特定存储库。 

你可能只想在运行网络扫描作业来分析网络中的存储库之后执行此操作，但也可以自行定义存储库。

**若要在 Azure 门户上创建内容扫描作业：**

1. 在左侧的 " **扫描仪** " 菜单下，选择 " **内容扫描作业**"。 
   
1. 在 " **Azure 信息保护-内容扫描作业** " 窗格上，选择 " **添加**" " ![添加图标](media/i-add.png "保存图标")"。
 
1. 对于此初始配置，请配置以下设置，然后选择 " **保存** "，但不要关闭窗格。
    
    |设置  |说明  |
    |---------|---------|
    |**内容扫描作业设置**     |    - **Schedule**：保留默认值 "**手动**" <br />- **要发现的信息类型**：仅更改为 **策略** <br />- **配置存储库**：此时不配置，因为必须先保存内容扫描作业。         |
    |**策略强制执行**     | - **强制**：选择 "**关闭**" <br />- **基于内容标记文件**：将默认值设置为 **on** <br />- **默认标签**：保留默认的 **策略** 默认值 <br />- 重新 **标记文件**：保持默认值为 **Off**        |
    |**配置文件设置**     | - **保留 "修改日期"、"上次修改时间" 和 "修改者"**：**保留的默认** 值 <br />- **要扫描的文件类型**：保留默认文件类型以 **排除** <br />- **默认所有者**：保留 **扫描仪帐户** 的默认值        |
    | | |

1. 既然已创建并保存了内容扫描作业，你就可以返回到 " **配置存储库** " 选项来指定要扫描的数据存储。 

    为 SharePoint 本地文档库和文件夹指定 UNC 路径和 SharePoint Server Url。 
    
    > [!NOTE]
    > Sharepoint 支持 sharepoint Server 2019、SharePoint Server 2016 和 SharePoint Server 2013。 具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)时，还支持 SharePoint Server 2010。
    >     
    要添加第一个数据存储，请在 " **添加新的内容扫描作业** " 窗格上，选择 " **配置存储库** " 以打开 " **存储库** " 窗格：
    
    :::image type="content" source="media/scanner-repositories-bar.png" alt-text="为 Azure 信息保护扫描程序配置数据存储库":::

    1. 在“存储库”窗格上，选择“添加”：
    
        :::image type="content" source="media/scanner-repository-add.png" alt-text="为 Azure 信息保护扫描程序添加数据存储库":::

    1. 在 " **存储库** " 窗格上，指定数据存储库的路径，然后选择 " **保存**"。
    
        
        - 对于网络共享，请使用 `\\Server\Folder` 。 
        - 对于 SharePoint 库，请使用 `http://sharepoint.contoso.com/Shared%20Documents/Folder` 。
        - 对于本地路径：`C:\Folder`
        - 对于 UNC 路径： `\\Server\Folder`

    > [!NOTE]
    > 不支持通配符，也不支持 WebDav 位置。
    >  
  
    如果为 **共享文档** 添加 SharePoint 路径：
    - 如果要从“共享文档”扫描所有文档和所有文件夹，请在路径中指定“共享文档”。 
    例如： `http://sp2013/SharedDocuments`
    - 如果要从“共享文档”下的子文件夹扫描所有文档和所有文件夹，请在路径中指定“文档”。 
    例如： `http://sp2013/Documents/SalesReports`
    - 或者，仅指定 Sharepoint 的 **FQDN** ，例如， `http://sp2013` 在此 url 下 [发现和扫描特定 url 和副标题下的所有 Sharepoint 网站和子网站](deploy-aip-scanner-prereqs.md#discover-and-scan-all-sharepoint-sites-and-subsites-under-a-specific-url) 。 授予扫描器 **站点收集器审核员** 权限以启用此权限。 
    >


    对于此窗格上的其余设置，请不要更改此初始配置的设置，但请将其保留为 **内容扫描作业默认值**。 默认设置表示数据存储库从内容扫描作业继承设置。

    添加 SharePoint 路径时，请使用以下语法：
    
    |路径  |语法  |
    |---------|---------|
    |**根路径**     | `http://<SharePoint server name>` <br /><br />扫描所有站点，包括任何允许用于扫描程序用户的站点集合。 <br />需要 [额外的权限](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) 来自动发现根内容        |
    |**特定 SharePoint 子网站或集合**     | 下列类型作之一： <br />- `http://<SharePoint server name>/<subsite name>` <br />- `http://SharePoint server name>/<site collection name>/<site name>` <br /><br />需要 [额外的权限](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) 来自动发现网站集内容         |
    |**特定 SharePoint 库**     | 下列类型作之一： <br />- `http://<SharePoint server name>/<library name>` <br />- `http://SharePoint server name>/.../<library name>`       |
    |**特定 SharePoint 文件夹**     | `http://<SharePoint server name>/.../<folder name>`        |
    | | |
    

1. 重复上述步骤，根据需要添加任意数量的存储库。

    完成后，关闭 " **存储库** " 和 " **内容扫描作业** " 窗格。 

返回 " **Azure 信息保护-内容扫描作业**" 窗格，显示你的内容扫描名称，以及显示为 "**手动**" 和 "**强制**" 列为空的 "**计划**" 列。

你现在已准备好在已创建的内容扫描程序作业中安装扫描程序。 继续 [安装扫描仪](#install-the-scanner)。

## <a name="install-the-scanner"></a>安装扫描程序

[在 Azure 门户中配置 Azure 信息保护扫描程序](#configure-the-scanner-in-the-azure-portal)之后，请执行以下步骤安装扫描仪：

1. 登录到将要运行扫描程序的 Windows Server 计算机。 使用具有本地管理员权限并具有写入到 SQL Server master 数据库权限的帐户。

    > [!IMPORTANT]
    > 安装 scanner 之前，必须在计算机上安装 AIP 统一标签客户端。 
    >
    > 有关详细信息，请参阅 [安装和部署 Azure 信息保护扫描程序的先决条件](deploy-aip-scanner-prereqs.md)。
    >
 
1. 使用“以管理员身份运行”选项打开 Windows PowerShell 会话。

1. 运行 [install-aipscanner](/powershell/module/azureinformationprotection/Install-AIPScanner) cmdlet，指定要在其中为 Azure 信息保护扫描程序创建数据库的 SQL Server 实例，以及在 [上一节中指定](#create-a-scanner-cluster)的扫描仪群集名称： 
    
    ```PowerShell
    Install-AIPScanner -SqlServerInstance <name> -Cluster <cluster name>
    ```
    
    示例，使用 **欧洲** 的扫描仪群集名称：
    
    - 对于默认实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1 -Cluster Europe`
    
    - 对于命名实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Cluster Europe`
    
    - 对于 SQL Server Express：`Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Cluster Europe`
    
    出现提示时，请提供扫描程序服务帐户的 Active Directory 凭据。

    使用以下语法： `\<domain\user name>` 。 例如： `contoso\scanneraccount`

1. 使用 **管理工具** 服务验证是否已安装该服务  >  。 
    
    已安装的服务被命名为 Azure信息保护扫描程序，并被配置为使用你创建的扫描程序服务帐户运行。

现在，你已安装了扫描仪，你需要 [获取一个 Azure AD 令牌，以便扫描程序](#get-an-azure-ad-token-for-the-scanner) 服务帐户进行身份验证，以便扫描程序可以在无人参与的情况下运行。 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>获取扫描程序的 Azure AD 令牌

使用 Azure AD 令牌，扫描程序可以对 Azure 信息保护服务进行身份验证，从而使扫描仪以非交互方式运行。

有关详细信息，请参阅[如何以非交互方式为 Azure 信息保护标记文件](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)。

获取 Azure AD 令牌：

1. 返回 Azure 门户，以创建 Azure AD 应用程序以指定用于身份验证的访问令牌。

1. 在 Windows Server 计算机中，如果你的扫描程序服务帐户已被授予 **本地登录** 的权限，请使用此帐户登录并启动 PowerShell 会话。 

    运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)，指定从上一步骤中复制的值：
    
    ```PowerShell
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
        
    例如：

    ```PowerShell
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
    Acquired application access token on behalf of CONTOSO\scanner.
    ```

> [!TIP]
> 如果你的扫描仪服务帐户无法被授予 **本地登录** 的权限，请使用 [set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)的 *OnBehalfOf* 参数，如 [如何为 Azure 信息保护以非交互方式标记文件](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)中所述。

扫描程序现在具有要对 Azure AD 进行身份验证的令牌。 此令牌的有效期为一年、两年或从不，根据你在 Azure AD 中配置的 **Web 应用/API** 客户端密码。 

当令牌过期时，必须重复此过程。

现在可随时在发现模式下运行第一次扫描。 有关详细信息，请参阅 [运行发现周期和查看扫描程序报告](deploy-aip-scanner-manage.md#run-a-discovery-cycle-and-view-reports-for-the-scanner)。

运行初始发现扫描后，请继续 [配置扫描仪以应用分类和保护](#configure-the-scanner-to-apply-classification-and-protection)。

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>将扫描程序配置为应用分类和保护

默认设置将扫描程序配置为运行一次，并将其配置为仅报告模式。

若要更改这些设置，请编辑内容扫描作业：

1. 在 Azure 门户的 " **Azure 信息保护-内容扫描作业** " 窗格上，选择要编辑的群集和内容扫描作业。

2. 在 "内容扫描作业" 窗格上，更改以下内容，然后选择 " **保存**"：
    
   - 从 "**内容扫描作业**" 部分：将 **计划** 更改为 "**始终**"
   - 从 **策略强制** 部分：将 **强制** 更改为 **开启**
    
    > [!TIP]
    > 你可能需要更改此窗格上的其他设置，例如是否更改文件属性以及扫描程序是否可以重新标记文件。 使用信息弹出通知帮助了解有关每个配置设置的详细信息。

3. 记下当前时间，然后从 " **Azure 信息保护-内容扫描作业** " 窗格中再次启动扫描仪：

    :::image type="content" source="media/scanner-scan-now.png" alt-text="启动 Azure 信息保护扫描程序扫描":::
    
    或者，在 PowerShell 会话中运行以下命令：
    
    ```PowerShell
    Start-AIPScan
    ```

现在，扫描器计划为连续运行。 当扫描程序在所有配置的文件中工作时，它会自动启动一个新循环，以便发现所有新文件和更改的文件。

## <a name="change-which-file-types-to-protect"></a>更改要保护的文件类型

默认情况下，AIP 扫描器仅保护 Office 文件类型和 PDF 文件。

根据需要使用 PowerShell 命令来更改此行为，例如，将扫描仪配置为保护所有文件类型，就像客户端一样，或保护其他特定文件类型。 

对于适用于为扫描程序下载标签的用户帐户的标签策略，请指定名为 **PFileSupportedExtensions** 的 PowerShell 高级设置。 

对于有权访问 internet 的扫描仪，此用户帐户是使用 Set-AIPAuthentication 命令为 *DelegatedUser* 参数指定的帐户。

**示例 1**：用于扫描程序的 PowerShell 命令，用于保护所有文件类型，其中标签策略命名为 "scanner"：

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

**示例 2**：用于扫描程序的 PowerShell 命令，用于保护 .xml 文件和 tiff 文件以及 Office 文件和 PDF 文件，其中的标签策略命名为 "scanner"：

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}
```

有关详细信息，请参阅 [更改要保护的文件类型](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)。

## <a name="upgrading-your-scanner"></a>升级扫描仪
 
如果以前安装了扫描程序并想要升级，请使用 [升级 Azure 信息保护扫描程序](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)中所述的说明。

然后，按常规方式 [配置](deploy-aip-scanner-configure-install.md) 和 [使用扫描仪](deploy-aip-scanner-manage.md) ，跳过安装扫描程序的步骤。

## <a name="editing-data-repository-settings-in-bulk"></a>批量编辑数据存储库设置

使用 " **导出** " 和 " **导入** " 按钮可以在多个存储库中对扫描程序进行更改。 

这样一来，就不需要在 Azure 门户中手动进行相同的更改。

例如，如果在多个 SharePoint 数据存储库上有一个新的文件类型，则可能需要批量更新这些存储库的设置。

跨存储库批量进行更改：

1. 在 " **存储库** " 窗格的 "Azure 门户" 中，选择 " **导出** " 选项。 例如：

    :::image type="content" source="media/export-scanner-repositories.png" alt-text="导出 Azure 信息保护扫描程序的数据存储库设置":::

1. 手动编辑导出的文件以进行更改。 

1. 使用同一页面上的 " **导入** " 选项将更新导入到存储库中。

## <a name="using-the-scanner-with-alternative-configurations"></a>使用具有备选配置的扫描程序

Azure 信息保护扫描程序通常会查找为标签指定的条件，以便根据需要对内容进行分类和保护。

在以下情况下，Azure 信息保护扫描程序还可以扫描内容并管理标签，而不会配置任何条件：

- [将默认标签应用于数据存储库中的所有文件](#apply-a-default-label-to-all-files-in-a-data-repository)
- [从数据存储库中的所有文件删除现有标签](#remove-existing-labels-from-all-files-in-a-data-repository)
- [标识所有自定义条件和已知的敏感信息类型](#identify-all-custom-conditions-and-known-sensitive-information-types)

### <a name="apply-a-default-label-to-all-files-in-a-data-repository"></a>将默认标签应用于数据存储库中的所有文件

在此配置中，存储库中所有未标记的文件都标有为存储库或内容扫描作业指定的默认标签。 文件标记为 "无检查"。 

配置下列设置： 

|设置  |说明  |
|---------|---------|
|**基于内容标记文件**    |设置为 **Off**         |
|**默认标签**     | 设置为 " **自定义**"，然后选择要使用的标签       |
|**强制默认标签**     | 选择此值可将默认标签应用到所有文件，即使它们已标记。        |
| | |

### <a name="remove-existing-labels-from-all-files-in-a-data-repository"></a>从数据存储库中的所有文件删除现有标签

在此配置中，如果对标签应用了保护，则将删除所有现有标签，包括保护。 保留单独应用的保护。

配置下列设置： 

|设置  |说明  |
|---------|---------|
|**基于内容标记文件**    |设置为 **Off**         |
|**默认标签**     | 设置为 **None**  |
|**重新标记文件** | 在选中 "**强制默认标签**" 复选框的情况下，设置为 **On**|
| | |

### <a name="identify-all-custom-conditions-and-known-sensitive-information-types"></a>标识所有自定义条件和已知的敏感信息类型

此配置使你能够查找你可能未意识到的敏感信息，因为扫描程序的扫描速率很高。 

将要 **发现的信息类型** 设置为 " **所有**"。 

为了识别用于标记的条件和信息类型，扫描程序使用指定的任何自定义敏感信息类型以及可供选择的内置敏感信息类型列表，如您在标记管理中心中定义的那样。

## <a name="optimizing-scanner-performance"></a>优化扫描程序性能

> [!NOTE]
> 如果希望提高扫描仪计算机的响应能力而不是扫描程序性能，请使用 "高级客户端设置" [限制扫描程序使用的线程数](./rms-client/clientv2-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)。
> 

使用以下选项和指南来帮助优化扫描程序性能：

|选项  |说明  |
|---------|---------|
|**在扫描程序计算机和被扫描的数据存储之间建立高速可靠的网络连接**     |  例如，将扫描仪计算机放在与扫描的数据存储相同的网络段中，或者在同一网段中放置。 <br /><br />由于要检查文件，扫描程序会将文件内容传输到运行 scanner 服务的计算机，因此网络连接的质量会影响扫描程序性能。 <br /><br />减少或消除传输数据所需的网络跃点还可以减少网络上的负载。      |
|**确保扫描程序计算机具有可用的处理器资源**     | 检查文件内容并对文件进行加密和解密是处理密集型操作。 <br /><br />监视指定数据存储的典型扫描周期，以确定缺乏处理器资源是否会对扫描程序性能产生负面影响。        |
|**安装扫描程序的多个实例** | 当你为扫描仪指定自定义群集名称时，Azure 信息保护扫描程序在相同的 SQL server 实例上支持多个配置数据库。 <br /><br />多个扫描程序还可以共享同一群集，从而缩短扫描时间。|
|**检查备选配置用法** |在使用[备选配置](#using-the-scanner-with-alternative-configurations)将默认标签应用于所有文件时，扫描程序可以更快地运行，因为扫描程序不检查文件内容。 <br/><br />如果你使用[替换配置](#using-the-scanner-with-alternative-configurations)标识所有自定义条件和已知敏感信息类型，扫描程序的运行速度会更慢。|
| | |


### <a name="additional-factors-that-affect-performance"></a>影响性能的其他因素

影响扫描程序性能的其他因素包括：

|因子  |说明  |
|---------|---------|
|**加载/响应时间**     |包含要扫描的文件的数据存储的当前负载和响应时间也会影响扫描程序性能。         |
|**扫描模式** (发现/强制)     | 发现模式的扫描速度通常比 "强制" 模式高。 <br /><br />发现需要单个文件读取操作，而 "强制" 模式需要读取和写入操作。        |
|**策略更改**     |如果已对标签策略中的 autolabeling 进行更改，则扫描程序性能可能会受到影响。 <br /><br />当扫描程序必须检查每个文件时，第一个扫描周期的时间比默认情况下的后续扫描周期长，仅检查新文件和更改的文件。 <br /><br />如果更改了 "条件" 或 "autolabeling" 设置，将再次扫描所有文件。 有关详细信息，请参阅重新 [扫描文件](deploy-aip-scanner-manage.md#rescanning-files)。|
|**Regex 构造**    | 扫描程序性能会受到构造自定义条件的正则表达式的影响。 <br /><br /> 为避免占用过多内存并存在超时风险（每个文件 15 分钟），请查看正则表达式了解有效的模式匹配。 <br /><br />例如： <br />-避免 [贪婪限定符](/dotnet/standard/base-types/quantifiers-in-regular-expressions) <br />-使用非捕获组，例如 `(?:expression)` 而不是 `(expression)`    |
|**日志级别**     |  日志级别选项包括扫描器报表的 **调试**、 **信息**、 **错误** 和 **关闭** 。<br /><br />- **禁用** 会获得最佳性能 <br />- **调试** 大大降低了扫描程序的速度，只应使用进行故障排除。 <br /><br />有关详细信息，请参阅 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet 的 eportLevel 参数。       |
|**正在扫描的文件**     |-除了 Excel 文件，Office 文件的扫描速度比 PDF 文件更快。 <br /><br />与受保护的文件相比，-不受保护的文件的扫描速度更快。 <br /><br />-大型文件比小文件需要更长的时间来扫描。         |
| | |

## <a name="list-of-cmdlets-for-the-scanner"></a>适用于扫描程序的 cmdlet 列表

本部分列出 Azure 信息保护扫描程序支持的 PowerShell cmdlet。

扫描程序支持的 cmdlet 包括：

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/add-aipscannerrepository)

- [导出-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [AIPScannerContentScanJob](/powershell/module/azureinformationprotection/get-aipscannercontentscanjob)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/get-aipscannerrepository)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryConfiguration)

- [MIPNetworkDiscoveryJobs](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryJobs)

- [MIPNetworkDiscoveryStatus](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryStatus)

- [MIPScannerContentScanJob](/powershell/module/azureinformationprotection/get-mipscannercontentscanjob)

- [MIPScannerRepository](/powershell/module/azureinformationprotection/get-mipscannerrepository)

- [导入-Set-aipscannerconfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [MIPNetworkDiscovery](/powershell/module/azureinformationprotection/set-mipnetworkdiscovery)

- [导入-MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/Import-MIPNetworkDiscoveryConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [安装-MIPNetworkDiscovery](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery)

- [MIPScannerContentScanJob](/powershell/module/azureinformationprotection/remove-mipscannercontentscanjob)

- [MIPScannerRepository](/powershell/module/azureinformationprotection/remove-mipscannerrepository)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [AIPScannerContentScanJob](/powershell/module/azureinformationprotection/set-aipscannercontentscanjob)

- [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/set-aipscannerrepository)

- [MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/Set-MIPNetworkDiscoveryConfiguration)

- [MIPScannerContentScanJob](/powershell/module/azureinformationprotection/set-mipscannercontentscanjob)

- [MIPScannerRepository](/powershell/module/azureinformationprotection/set-mipscannerrepository)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [AIPScanDiagnostics](/powershell/module/azureinformationprotection/Start-AIPScannerDiagnostics)

- [MIPNetworkDiscovery](/powershell/module/azureinformationprotection/Start-MIPNetworkDiscovery)

- [停止-AIPScan](/powershell/module/azureinformationprotection/Stop-AIPScan)

- [AIPScannerContentScanJob](/powershell/module/azureinformationprotection/remove-aipscannercontentscanjob)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/remove-aipscannerrepository)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [卸载-MIPNetworkDiscovery](/powershell/module/azureinformationprotection/Uninstall-MIPNetworkDiscovery)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="next-steps"></a>后续步骤

安装并配置了扫描仪后，开始 [扫描文件](deploy-aip-scanner-manage.md)。

另请参阅： [部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。

**详细信息**：

- 想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

- 使用 PowerShell 以交互方式对台式计算机上的文件进行分类和保护。 有关此方案以及使用 PowerShell 的其他方案的详细信息，请参阅 [将 PowerShell 与 Azure 信息保护统一标签客户端配合使用](./rms-client/clientv2-admin-guide-powershell.md)。