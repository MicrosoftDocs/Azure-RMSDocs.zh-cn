---
title: 教程 - 安装 Azure 信息保护 (AIP) 统一标记扫描程序
description: 安装 Azure 信息保护 (AIP) 统一标记扫描程序，以发现存储在本地网络共享中的敏感数据。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 73bcb5e636b8a5e4456ad80f8435a27dfc898339
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384768"
---
# <a name="tutorial-installing-the-azure-information-protection-aip-unified-labeling-scanner"></a>教程：安装 Azure 信息保护 (AIP) 统一标记扫描程序

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 相关内容：**[用于 Windows 的 Azure 信息保护统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

本教程介绍如何安装 Azure 信息保护 (AIP) 本地扫描程序。 通过扫描程序，AIP 管理员能够扫描其网络和内容共享以获取敏感数据，并应用组织策略中配置的分类和保护标签。

所需时间：可在 30 分钟内完成本教程。

## <a name="tutorial-prerequisites"></a>教程先决条件

若要安装统一标记扫描程序并完成本教程，你需要：

|要求  |说明  |
|---------|---------|
|支持订阅     |  你需要包含 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection/)的 Azure 订阅。 <br /><br />如果没有上述任一订阅，则请为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。       |
|对 Azure 门户的管理员访问权限 |请确保可以通过以下管理员帐户之一登录到 [Azure 门户](https://portal.azure.com/)： <br /><br />- 合规性管理员<br />- 合规性数据管理员<br />- 安全管理员<br />- 全局管理员 |
|客户端已安装    |   在计算机上安装 AIP 统一标记客户端以访问扫描程序安装。 <br /><br />从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载并运行 AzInfoProtection_UL.exe。 <br /><br />安装完成后，系统可能会提示你重启计算机或 Office 软件。 根据需要重启以继续。 <br /><br />有关详细信息，请参阅[快速入门：部署 Azure 信息保护 (AIP) 统一标记客户端](quickstart-deploy-client.md)。|
|**SQL Server**     | 若要运行扫描程序，你需要在扫描程序计算机上安装 SQL Server。 <br /><br /> 若要安装，请转到 [SQL Server 下载页](https://www.microsoft.com/sql-server/sql-server-downloads)，然后选择要安装的安装选项下的“立即下载”。 在安装程序中，选择“基本”安装类型。 <br /><br />**注意**：我们建议为生产环境安装 SQL Server Enterprise，仅为测试环境安装 Express。       |
|**Azure Active Directory 帐户**     |  使用标准的云连接环境时，要用于扫描程序的域服务帐户必须同步到 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)。 如果正在脱机工作，则不需要这样做。 <br /><br />如果你不确定你的帐户，请联系你的系统管理员来验证同步状态。   |
|敏感度标签和已发布的策略 |必须已创建敏感度标签，并将至少有一个标签的策略发布到标记管理中心，用于扫描程序服务帐户。 <br /><br />在标记管理中心（包括 Microsoft 365 合规中心、Microsoft 365 安全中心或 Microsoft 365 安全与合规中心）配置敏感度标签。 有关详细信息，请参阅 [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels)。 |
| | |

确认先决条件后，[在 Azure 门户中配置 Azure 信息保护](#configure-azure-information-protection-in-the-azure-portal)。

## <a name="configure-azure-information-protection-in-the-azure-portal"></a>在 Azure 门户中配置 Azure 信息保护

Azure 信息保护可能在 Azure 门户中不可用，或者当前可能未激活保护。 

根据需要执行以下步骤一二：

- [将 Azure 信息保护添加到 Azure 门户](#add-azure-information-protection-to-the-azure-portal)
- [确认已激活保护](#confirm-that-protection-is-activated)

然后[继续在 Azure 门户中配置初始扫描程序设置](#configure-initial-scanner-settings-in-the-azure-portal)。

### <a name="add-azure-information-protection-to-the-azure-portal"></a>将 Azure 信息保护添加到 Azure 门户

1. 使用[支持的管理员帐户](#tutorial-prerequisites)登录到 [Azure 门户](https://portal.azure.com)。

1. 选择“+ 创建资源”。  在搜索框中，搜索然后选择“Azure 信息保护”。 在“Azure 信息保护”页上，选择“创建”，然后再次选择“创建”。

    :::image type="content" source="media/gifs/quickstart-add-aip-to-portal.gif" alt-text="将 Azure 信息保护添加到 Azure 门户":::

    > [!TIP]
    > 如果这是你第一次执行此步骤，你将会在窗格名称旁看到“固定到仪表板”![固定到仪表板](media/qs-tutor/pin-to-dashboard.png "固定到仪表板图标")图标。 选择“固定”图标以在仪表板上创建磁贴，以便你下一次可以直接导航到此处。

继续[确认已激活保护](#confirm-that-protection-is-activated)。

### <a name="confirm-that-protection-is-activated"></a>确认已激活保护

如果已有可用的 Azure 信息保护，请确保已激活保护：

1. 在“Azure 信息保护”区域中的左侧“管理”下，选择“保护激活” 。

1. 确认是否已为租户激活保护。 例如：

    :::image type="content" source="media/qs-tutor/confirm-activation.PNG" alt-text="确认 AIP 激活":::

如果保护未激活，请选择![激活 AIP](media/qs-tutor/activate.png "激活 AIP") 激活。 激活完成后，信息栏将显示“激活已成功完成”。

继续[在 Azure 门户中配置初始扫描程序设置](#configure-initial-scanner-settings-in-the-azure-portal)。

### <a name="configure-initial-scanner-settings-in-the-azure-portal"></a>在Azure 门户中配置初始扫描程序设置

在计算机上安装扫描程序之前，请先在 Azure 门户中准备初始扫描程序设置。

1. 在“Azure 信息保护”区域中的左侧“扫描程序”下，选择 :::image type="icon" source="media/i-clusters.png" border="false":::“群集” 。

1. 在“群集”页上，选择 :::image type="icon" source="media/i-add.PNG" border="false":::“添加”以创建新群集来管理扫描程序。

1. 在右侧打开的“添加新群集”窗格中，输入有意义的群集名称和可选说明。

    > [!IMPORTANT]
    > 安装扫描程序时，需要此群集的名称。
    > 
    
    例如：

    :::image type="content" source="media/qs-tutor/qs-add-new-cluster.png" alt-text="添加用于教程的新群集":::

1. 创建初始内容扫描作业。 在左侧的“扫描程序”菜单中，选择 :::image type="icon" source="media/i-content-scan-jobs.png" border="false":::“内容扫描作业”，然后选择 :::image type="icon" source="media/i-add.PNG" border="false":::“添加”。

1. 在“添加新的内容扫描作业”窗格中，输入内容扫描作业有意义的名称和可选说明。

    然后，向下滚动页面到“策略强制”，然后选择“关闭” 。

    完成后，保存所做的更改。 

    此默认扫描作业将扫描所有已知的敏感信息类型。

1. 关闭内容扫描作业的详细信息窗格，然后返回到 :::image type="icon" source="media/i-content-scan-jobs.png" border="false":::“内容扫描作业”网格。 

    在为内容扫描作业显示的新行中的“群集名称”列中，选择“+ 分配到群集”。 然后，在右侧显示的“分配到群集”窗格中，选择群集。 

    :::image type="content" source="media/qs-tutor/assign-cluster-all.png" alt-text="分配到群集":::

现在，你已准备好[安装 AIP 统一标记扫描程序](#install-the-aip-unified-labeling-scanner)。

## <a name="install-the-aip-unified-labeling-scanner"></a>安装 AIP 统一标记扫描程序

[在 Azure 门户中配置基本扫描程序设置](#configure-azure-information-protection-in-the-azure-portal)后，在 AIP 客户端计算机上安装统一标记扫描程序。

1. 在客户端计算机上，使用“以管理员身份运行”选项打开 PowerShell 会话。

1. 使用以下命令安装扫描程序。 在命令中，指定要安装的扫描程序的位置，以及[在 Azure 门户中创建的群集](#configure-initial-scanner-settings-in-the-azure-portal)的名称。

    ```PowerShell
    Install-AIPScanner -SqlServerInstance <your SQL installation location>\SQLEXPRESS -Cluster <cluster name>
    ```
    例如：

    ```powershell
    Install-AIPScanner -SqlServerInstance localhost\SQLEXPRESS -Cluster Quickstart
    ```

    当 PowerShell 提示你输入凭据时，请输入用户名和密码。 

    对于“用户名称”字段，请使用以下语法：`<domain\user name>`。 例如：`emea\contososcanner`。

1. 返回到 Azure 门户。 在左侧“扫描程序”菜单中，选择 :::image type="icon" source="media/qs-tutor/i-nodes.png" border="false":::“节点” 。 

    现在应会看到扫描程序添加到了网格。 例如：

    :::image type="content" source="media/qs-tutor/qs-post-install-scanner.png" alt-text="节点网格上显示的新安装的扫描程序":::

继续[获取用于扫描程序的 Azure Active Directory 令牌](#get-an-azure-active-directory-token-for-the-scanner)，以使扫描程序服务帐户能够以非交互方式运行。

## <a name="get-an-azure-active-directory-token-for-the-scanner"></a>获取扫描程序的 Azure Active directory 令牌

当你使用标准的云连接环境时，请执行此过程，以允许扫描程序对 AIP 服务进行身份验证，使服务能够以非交互方式运行。

如果仅脱机工作，则不需要此过程。

有关详细信息，请参阅[如何以非交互方式为 Azure 信息保护标记文件](rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)。

若要获取扫描程序的 Azure AD 令牌，请执行以下操作：

1. 在 Azure 门户中，创建 Azure AD 应用程序来指定用于身份验证的访问令牌。

1. 在扫描程序计算机上，使用已被授予“本地登录”权限的扫描程序服务帐户进行登录，并启动 PowerShell 会话。

1. 启动 PowerShell 会话，并使用从 Azure AD 应用程序复制的值运行以下命令。

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
    > 如果无法向扫描程序服务帐户授予“本地登录”的安装权限，请将 OnBehalfOf 参数与 Set-AIPAuthentication（而非 DelegatedUser 参数）一起使用。

扫描程序现在具有要对 Azure AD 进行身份验证的令牌。 只要在 Azure Active Directory 中配置过，此令牌就有效。 如果令牌过期，则必须重复此过程。

继续[安装可选的网络发现服务](#install-the-network-discovery-service)，通过该服务，你能够扫描网络存储库中可能存在风险的内容，然后将这些存储库添加到内容扫描作业中。

## <a name="install-the-network-discovery-service"></a>安装网络发现服务

从 AIP 统一标记客户端的版本 [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 开始，管理员可以使用 AIP 扫描程序扫描网络存储库，然后添加任何看似对内容扫描作业有风险的存储库。

网络扫描作业通过尝试同时作为管理员和公共用户访问已配置的存储库，帮助你了解内容可能面临的风险。

例如，如果发现存储库同时具有读取和写入公共访问权限，可能需要进一步扫描并确认没有在其中存储敏感数据。

> [!NOTE]
> 此功能目前处于预览状态。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。

若要安装网络发现服务，请执行以下操作：

1. 在扫描程序计算机上，以管理员的身份打开 PowerShell 会话。

1. 定义你希望 AIP 在运行网络发现服务时以及模拟管理员和公共用户访问时使用的凭据。 

    使用以下语法提示时，请输入每个命令的凭据：`domain\user`。 例如： `emea\msanchez`

    运行： 

    运行网络发现服务的凭据：

    ``` PowerShell 
    $serviceacct= Get-Credential 
    ``` 

    模拟管理员访问权限的凭据：

    ``` PowerShell 
    $shareadminacct= Get-Credential 
    ``` 

    模拟公共用户访问权限的凭据：

    ``` PowerShell  
    $publicaccount= Get-Credential 
    ``` 

1. 若要安装网络发现服务，请运行：

    ```PowerShell
    Install-MIPNetworkDiscovery [-ServiceUserCredentials] <PSCredential> [[-StandardDomainsUserAccount] <PSCredential>] [[-ShareAdminUserAccount] <PSCredential>] [-SqlServerInstance] <String> -Cluster <String> [-WhatIf] [-Confirm] [<CommonParameters>]

    For example:

    ```PowerShell
    Install-MIPNetworkDiscovery -SqlServerInstance SQLSERVER1\SQLEXPRESS -Cluster Quickstart -ServiceUserCredentials $serviceacct  -ShareAdminUserAccount $shareadminacct -StandardDomainsUserAccount $publicaccount
 
    ```

安装完成后，系统将显示确认消息。

## <a name="next-steps"></a>后续步骤

安装扫描程序和网络发现服务后，即可开始扫描。 

有关详细信息，请参阅[教程：使用 Azure 信息保护 (AIP) 扫描程序发现敏感内容](tutorial-scan-networks-and-content.md)。

> [!TIP]
> 如果你安装了版本 [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850)，建议扫描网络以发现可能包含有风险的内容的存储库。 
>
>若要扫描有风险的存储库以寻找敏感数据，然后进行分类并避免外部用户使用这些数据，请使用找到的存储库的详细信息更新内容扫描作业。
>

另请参阅：

- [什么是 Azure 信息保护统一标记扫描程序？](deploy-aip-scanner.md)
- [安装和部署 Azure 信息保护统一标记扫描程序的先决条件](deploy-aip-scanner-prereqs.md)
- [教程：使用 Azure 信息保护 (AIP) 防止过度共享](tutorial-preventing-oversharing.md)
- [教程：从 Azure 信息保护 (AIP) 经典客户端迁移到统一标记客户端](tutorial-migrating-to-ul.md)
