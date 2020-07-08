---
title: 安装和配置 Azure 信息保护（AIP）统一标记扫描器
description: 说明如何安装和配置 Azure 信息保护统一标记扫描器，以发现、分类和保护数据存储中的文件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e786b30075f7a72781dd6cac13af4e14b70fc2db
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86049487"
---
# <a name="configuring-and-installing-the--azure-information-protection-unified-labeling-scanner"></a>配置和安装 Azure 信息保护统一标记扫描器

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*

>[!NOTE] 
> 如果使用的是 AIP 经典扫描程序，请参阅[安装和配置 Azure 信息保护经典扫描器](deploy-aip-scanner-configure-install-classic.md)。

在开始配置和安装 Azure 信息保护扫描程序之前，请确保系统符合[所需的先决条件](deploy-aip-scanner-prereqs.md)。

准备就绪后，请继续执行以下步骤：

1. [在 Azure 门户中配置扫描程序](#configure-the-scanner-in-the-azure-portal)

1. [安装扫描程序](#install-the-scanner)

1. [获取扫描程序的 Azure AD 令牌](#get-an-azure-ad-token-for-the-scanner)

1. [配置扫描程序以应用分类和保护](#configure-the-scanner-to-apply-classification-and-protection)
 
根据系统需要执行以下附加配置过程：

|过程  |说明  |
|---------|---------|
|[更改要保护的文件类型](#change-which-file-types-to-protect) |你可能想要扫描、分类或保护不同于默认文件类型的文件类型。 有关详细信息，请参阅[AIP 扫描进程](deploy-aip-scanner.md#aip-scanning-process)。 |
|[升级扫描仪](#upgrading-your-scanner) | 升级扫描仪以利用最新的功能和改进。|
|[批量编辑数据存储库设置](#editing-data-repository-settings-in-bulk)| 使用导入和导出选项可以批量更改多个数据存储库。|
|[使用带有备用配置的扫描程序](#using-the-scanner-with-alternative-configurations)| 在不使用任何条件配置标签的情况下使用扫描程序 |
|[优化性能](#optimizing-scanner-performance)| 优化扫描程序性能的指导|
| | |

有关详细信息，请参阅[扫描器的 Cmdlet 列表](#list-of-cmdlets-for-the-scanner)。

## <a name="configure-the-scanner-in-the-azure-portal"></a>在 Azure 门户中配置扫描程序

在安装扫描程序之前，或者从扫描程序的旧版本升级它，请在 Azure 门户中为扫描仪创建群集和内容扫描作业。 

然后，将群集和内容扫描作业配置为扫描程序设置和要扫描的数据存储库。

若要配置扫描仪： 

1. [登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)，导航到 " **Azure 信息保护**" 窗格。 
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”**** 并选择“Azure 信息保护”****。
    
1. 找到 "**扫描仪**" 菜单选项，然后选择 "**群集**"。

1. 在 " **Azure 信息保护-群集**" 窗格上，选择 "**添加**"：
    
    :::image type="content" source="media/scanner-add-profile.png" alt-text="为 Azure 信息保护扫描程序添加内容扫描作业":::

1. 在 "**添加新群集**" 窗格上：

    1. 为扫描程序指定一个有意义的名称。 此名称用于标识扫描仪的配置设置和要扫描的数据存储库。 

        例如，可以指定“欧洲”**** 来标识扫描程序将涵盖的数据存储库的地理位置。 以后安装或升级扫描程序时，需要指定相同的群集名称。
   
    2. （可选）指定用于管理目的的说明，以帮助你确定扫描仪的群集名称。

    3. 选择“保存”。
1. 找到 "**扫描仪**" 菜单选项，然后选择 "**内容扫描作业**"。
1. 在 " **Azure 信息保护-内容扫描作业**" 窗格上，选择 "**添加**"。
 
1. 对于此初始配置，请配置以下设置，然后选择 "**保存**"，但不要关闭窗格：
    
    |部分  |设置  |
    |---------|---------|
    |**内容扫描作业设置**     |    - **Schedule**：保留默认值 "**手动**" </br>- **要发现的信息类型**：仅更改为**策略** </br>- **配置存储库**：此时不配置，因为必须先保存内容扫描作业。         |
    |**策略强制**     | - **强制**：选择 "**关闭**" </br>- **基于内容标记文件**：将默认值设置为**on** </br>- **默认标签**：保留默认的**策略**默认值 </br>- 重新**标记文件**：保持默认值为**Off**        |
    |**配置文件设置**     | - **保留 "修改日期"、"上次修改时间" 和 "修改者"**：**保留的默认**值 </br>- **要扫描的文件类型**：保留默认文件类型以**排除** </br>- **默认所有者**：保留**扫描仪帐户**的默认值        |
    | | |


1. 既然已创建并保存了内容扫描作业，你就可以返回到 "**配置存储库**" 选项来指定要扫描的数据存储。 

    指定 UNC 路径，以及 sharepoint 本地文档库和文件夹的 SharePoint Server Url。 
    
    > [!NOTE]
    > Sharepoint 支持 sharepoint Server 2019、SharePoint Server 2016 和 SharePoint Server 2013。 具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)时，还支持 SharePoint Server 2010。
    >     
    要添加第一个数据存储，请在 "**添加新的内容扫描作业**" 窗格上，选择 "**配置存储库**" 以打开 "**存储库**" 窗格：
    
    :::image type="content" source="media/scanner-repositories-bar.png" alt-text="为 Azure 信息保护扫描程序配置数据存储库":::

1. 在“存储库”**** 窗格上，选择“添加”****：
    
    :::image type="content" source="media/scanner-repository-add.png" alt-text="为 Azure 信息保护扫描程序添加数据存储库":::

1. 在 "**存储库**" 窗格上，指定数据存储库的路径，然后选择 "**保存**"。

    例如： 

    - 对于网络共享，请使用 `\\Server\Folder` 。 
    - 对于 SharePoint 库，请使用 `http://sharepoint.contoso.com/Shared%20Documents/Folder` 。

    > [!NOTE]
    > 不支持通配符，也不支持 WebDav 位置。
    >     

    添加 SharePoint 路径时，请使用以下语法：
    
    |路径  |语法  |
    |---------|---------|
    |**根路径**     | `http://<SharePoint server name>` </br></br>扫描所有站点，包括任何允许用于扫描程序用户的站点集合。 </br>需要[额外的权限](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories)来自动发现根内容        |
    |**特定 SharePoint 子网站或集合**     | 下列情况之一： </br>- `http://<SharePoint server name>/<subsite name>` </br>- `http://SharePoint server name>/<site collection name>/<site name>` </br></br>需要[额外的权限](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories)来自动发现网站集内容         |
    |**特定 SharePoint 库**     | 下列情况之一： </br>- `http://<SharePoint server name>/<library name>` </br>- `http://SharePoint server name>/.../<library name>`       |
    |**特定 SharePoint 文件夹**     | `http://<SharePoint server name>/.../<folder name>`        |
    | | |

    对于此窗格上的其余设置，请不要更改此初始配置的设置，但请将其保留为**内容扫描作业默认值**。 默认设置表示数据存储库从内容扫描作业继承设置。

    <!--
        > [!IMPORTANT]
        > While the local file system can be scanned, this configuration is not recommended for production deployments and can **only** be used in single node clusters.
        >
        > Scanning of local folders by multi-node clusters is not supported. If you need to scan a folder on the local file system, we recommend creating a share, and scanning it using a network URL.
    -->

1. 如果要添加另一个数据存储库，请重复步骤8和9。 

1. 关闭 "**存储库**" 窗格和 "**内容扫描作业**" 窗格。 

返回 " **Azure 信息保护-内容扫描作业**" 窗格，显示你的内容扫描名称，以及显示为 "**手动**" 和 "**强制**" 列为空的 "**计划**" 列。

你现在已准备好在已创建的内容扫描程序作业中安装扫描程序。 继续[安装扫描仪](#install-the-scanner)。

## <a name="install-the-scanner"></a>安装扫描程序

[在 Azure 门户中配置 Azure 信息保护扫描程序](#configure-the-scanner-in-the-azure-portal)之后，请执行以下步骤安装扫描仪：

1. 登录到将要运行扫描程序的 Windows Server 计算机。 使用具有本地管理员权限并具有写入到 SQL Server master 数据库权限的帐户。

    > [!IMPORTANT]
    > 有关详细信息，请参阅[安装和部署 Azure 信息保护扫描程序的先决条件](deploy-aip-scanner-prereqs.md)。
    >
 
1. 使用“以管理员身份运行”选项打开 Windows PowerShell 会话****。

1. 运行[install-aipscanner](/powershell/module/azureinformationprotection/Install-AIPScanner) cmdlet，指定要在其中为 Azure 信息保护扫描程序创建数据库的 SQL Server 实例，以及在上一节中指定的扫描仪群集名称： 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <cluster name>
    ```
    
    例如，使用配置文件名称“欧洲”****：
    
    - 对于默认实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    - 对于命名实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    - 对于 SQL Server Express：`Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    出现提示时，请提供扫描程序服务帐户（ \<domain\user name> ）和密码的凭据。

1. 使用**管理工具**服务验证是否已安装该服务  >  **Services**。 
    
    已安装的服务被命名为 Azure信息保护扫描程序，并被配置为使用你创建的扫描程序服务帐户运行****。

现在，你已安装了扫描仪，你需要[获取一个 Azure AD 令牌，以便扫描程序](#get-an-azure-ad-token-for-the-scanner)服务帐户进行身份验证，以便扫描程序可以在无人参与的情况下运行。 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>获取扫描程序的 Azure AD 令牌

Azure AD 令牌允许扫描程序对 Azure 信息保护服务进行身份验证。

获取 Azure AD 令牌：

1. 返回 Azure 门户，以创建 Azure AD 应用程序以指定用于身份验证的访问令牌。 此令牌允许扫描程序以非交互方式运行。 有关详细信息，请参阅[如何以非交互方式为 Azure 信息保护标记文件](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)。

2. 在 Windows Server 计算机中，如果你的扫描程序服务帐户已被授予**本地登录**的权限，请使用此帐户登录并启动 PowerShell 会话。 

    运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)，指定从上一步骤中复制的值：
    
    ```ps
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
        
    例如：

    ```ps
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
    Acquired application access token on behalf of CONTOSO\scanner.
    ```

> [!TIP]
> 如果你的扫描仪服务帐户无法被授予**本地登录**的权限，请使用[set-aipauthentication](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipauthentication)的*OnBehalfOf*参数，如[如何为 Azure 信息保护以非交互方式标记文件](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)中所述。

现在，扫描器提供了一个用于对 Azure AD 进行身份验证的令牌，此令牌根据你在 Azure AD 中配置的**Web 应用/API**客户端密码在一年内有效。 

当令牌过期时，必须重复此过程。

现在可随时在发现模式下运行第一次扫描。 有关详细信息，请参阅[运行发现周期和查看扫描程序报告](deploy-aip-scanner-manage.md#run-a-discovery-cycle-and-view-reports-for-the-scanner)。

如果已运行发现扫描，请继续[配置扫描仪以应用分类和保护](#configure-the-scanner-to-apply-classification-and-protection)。

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>将扫描程序配置为应用分类和保护

默认设置将扫描程序配置为运行一次，并将其配置为仅报告模式。

若要更改这些设置，请编辑内容扫描作业：

1. 在 Azure 门户的 " **Azure 信息保护-内容扫描作业**" 窗格上，选择要编辑的群集和内容扫描作业。

2. 在 "内容扫描作业" 窗格上，更改以下内容，然后选择 "**保存**"：
    
   - 从 "**内容扫描作业**" 部分：将**计划**更改为 "**始终**"
   - 从**策略强制**部分：将**强制**更改为**开启**
    
    > [!TIP]
    > 你可能需要更改此窗格上的其他设置，例如是否更改文件属性以及扫描程序是否可以重新标记文件。 使用信息弹出通知帮助了解有关每个配置设置的详细信息。

3. 记下当前时间，然后从 " **Azure 信息保护-内容扫描作业**" 窗格中再次启动扫描仪：

    :::image type="content" source="media/scanner-scan-now.png" alt-text="启动 Azure 信息保护扫描程序扫描":::
    
    或者，在 PowerShell 会话中运行以下命令：
    
    ```ps
    Start-AIPScan
    ```

现在，扫描器计划为连续运行。 当扫描程序在所有配置的文件中工作时，它会自动启动一个新循环，以便发现所有新文件和更改的文件。

## <a name="change-which-file-types-to-protect"></a>更改要保护的文件类型

默认情况下，AIP 扫描器仅保护 Office 文件类型和 PDF 文件。

根据需要使用 PowerShell 命令来更改此行为，例如，将扫描仪配置为保护所有文件类型，就像客户端一样，或保护其他特定文件类型。 

对于适用于为扫描程序下载标签的用户帐户的标签策略，请指定名为**PFileSupportedExtensions**的 PowerShell 高级设置。 

对于有权访问 internet 的扫描仪，此用户帐户是你为*DelegatedUser*参数指定的、带有 set-aipauthentication 命令的帐户。

**示例1：** 用于扫描程序的 PowerShell 命令，用于保护所有文件类型，其中标签策略命名为 "Scanner"：

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

**示例2：** 用于扫描程序的 PowerShell 命令，用于保护 .xml 文件和 tiff 文件以及 Office 文件和 PDF 文件，其中标签策略命名为 "Scanner"：

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}
```

有关详细信息，请参阅[更改要保护的文件类型](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)。

## <a name="upgrading-your-scanner"></a>升级扫描仪
 
如果以前安装了扫描程序并想要升级，请使用[升级 Azure 信息保护扫描程序](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)中所述的说明。

然后，按常规方式[配置](deploy-aip-scanner-configure-install.md)和[使用扫描仪](deploy-aip-scanner-manage.md)，跳过安装扫描程序的步骤。

## <a name="editing-data-repository-settings-in-bulk"></a>批量编辑数据存储库设置

使用 "**导出**" 和 "**导入**" 按钮可以在多个存储库中对扫描程序进行更改。 

这样一来，就不需要在 Azure 门户中手动进行相同的更改。

例如，如果在多个 SharePoint 数据存储库上有一个新的文件类型，则可能需要批量更新这些存储库的设置。

跨存储库批量进行更改：

1. 在 "**存储库**" 窗格的 "Azure 门户" 中，选择 "**导出**" 选项。 例如：

    :::image type="content" source="media/export-scanner-repositories.png" alt-text="导出 Azure 信息保护扫描程序的数据存储库设置":::

1. 手动编辑导出的文件以进行更改。 

1. 使用同一页面上的 "**导入**" 选项将更新导入到存储库中。

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
|**基于内容标记文件**    |设置为**Off**         |
|**默认标签**     | 设置为 "**自定义**"，然后选择要使用的标签       |
|**强制默认标签**     | 选择此值可将默认标签应用到所有文件，即使它们已标记。        |
| | |

### <a name="remove-existing-labels-from-all-files-in-a-data-repository"></a>从数据存储库中的所有文件删除现有标签

在此配置中，如果对标签应用了保护，则将删除所有现有标签，包括保护。 保留单独应用的保护。

配置下列设置： 

|设置  |说明  |
|---------|---------|
|**基于内容标记文件**    |设置为**Off**         |
|**默认标签**     | 设置为**None**  |
|**重新标记文件** | 在选中 "**强制默认标签**" 复选框的情况下，设置为**On**|
| | |

### <a name="identify-all-custom-conditions-and-known-sensitive-information-types"></a>标识所有自定义条件和已知的敏感信息类型

此配置使你能够查找你可能未意识到的敏感信息，因为扫描程序的扫描速率很高。 

将要**发现的信息类型**设置为 "**所有**"。 

为了识别用于标记的条件和信息类型，扫描程序使用指定的任何自定义敏感信息类型以及可供选择的内置敏感信息类型列表，如您在标记管理中心中定义的那样。

## <a name="optimizing-scanner-performance"></a>优化扫描程序性能

> [!NOTE]
> 如果希望提高扫描仪计算机的响应能力而不是扫描程序性能，请使用 "高级客户端设置"[限制扫描程序使用的线程数](./rms-client/clientv2-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)。
> 

使用以下选项和指南来帮助优化扫描程序性能：

|选项  |说明  |
|---------|---------|
|**在扫描程序计算机和被扫描的数据存储之间建立高速可靠的网络连接**     |  例如，将扫描仪计算机放在与扫描的数据存储相同的网络段中，或者在同一网段中放置。 </br></br>由于要检查文件，扫描程序会将文件内容传输到运行 scanner 服务的计算机，因此网络连接的质量会影响扫描程序性能。 </br></br>减少或消除传输数据所需的网络跃点还可以减少网络上的负载。      |
|**确保扫描程序计算机具有可用的处理器资源**     | 检查文件内容并对文件进行加密和解密是处理密集型操作。 </br></br>监视指定数据存储的典型扫描周期，以确定缺乏处理器资源是否会对扫描程序性能产生负面影响。        |
|**安装扫描程序的多个实例** | 当你为扫描程序指定自定义群集（配置文件）名称时，Azure 信息保护扫描程序在相同的 SQL server 实例上支持多个配置数据库。 </br></br>多个扫描程序还可以共享同一群集（配置文件），从而缩短扫描时间。|
|**检查备选配置用法** |在使用[备选配置](#using-the-scanner-with-alternative-configurations)将默认标签应用于所有文件时，扫描程序可以更快地运行，因为扫描程序不检查文件内容。 <br/></br>如果你使用[替换配置](#using-the-scanner-with-alternative-configurations)标识所有自定义条件和已知敏感信息类型，扫描程序的运行速度会更慢。|
| | |

<!-- removed when removing local folders
|**Do not scan local folders on the computer running the scanner service**     | If you have folders to scan on a Windows server, install the scanner on a different computer and configure those folders as network shares to scan. </br></br>Separating the two functions of hosting files and scanning files means that the computing resources for these services are not competing with one another.        |
-->

### <a name="additional-factors-that-affect-performance"></a>影响性能的其他因素

影响扫描程序性能的其他因素包括：

|因子  |说明  |
|---------|---------|
|**加载/响应时间**     |包含要扫描的文件的数据存储的当前负载和响应时间也会影响扫描程序性能。         |
|**扫描仪模式**（发现/强制）    | 发现模式的扫描速度通常比 "强制" 模式高。 </br></br>发现需要单个文件读取操作，而 "强制" 模式需要读取和写入操作。        |
|**策略更改**     |如果已对标签策略中的 autolabeling 进行更改，则扫描程序性能可能会受到影响。 </br></br>当扫描程序必须检查每个文件时，第一个扫描周期的时间比默认情况下的后续扫描周期长，仅检查新文件和更改的文件。 </br></br>如果更改了 "条件" 或 "autolabeling" 设置，将再次扫描所有文件。 有关详细信息，请参阅重新[扫描文件](deploy-aip-scanner-manage.md#rescanning-files)。|
|**Regex 构造**    | 扫描程序性能会受到构造自定义条件的正则表达式的影响。 </br></br> 为避免占用过多内存并存在超时风险（每个文件 15 分钟），请查看正则表达式了解有效的模式匹配。 </br></br>例如： </br>-避免[贪婪限定符](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions) </br>-使用非捕获组，例如 `(?:expression)` 而不是`(expression)`    |
|**日志级别**     |  日志级别选项包括扫描器报表的**调试**、**信息**、**错误**和**关闭**。</br></br>- **禁用**会获得最佳性能 </br>- **调试**大大降低了扫描程序的速度，只应使用进行故障排除。 </br></br>有关详细信息，请参阅 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet 的 eportLevel 参数**。       |
|**正在扫描的文件**     |-除了 Excel 文件，Office 文件的扫描速度比 PDF 文件更快。 </br></br>与受保护的文件相比，-不受保护的文件的扫描速度更快。 </br></br>-大型文件比小文件需要更长的时间来扫描。         |
| | |

## <a name="list-of-cmdlets-for-the-scanner"></a>适用于扫描程序的 cmdlet 列表

本部分列出 Azure 信息保护扫描程序支持的 PowerShell cmdlet。

> [!NOTE]
> Azure 信息保护扫描程序是从 Azure 门户配置的。 因此，在以前的版本中用于配置数据存储库的 cmdlet 和 "扫描的文件类型" 列表现已弃用。
> 

扫描程序支持的 cmdlet 包括：

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [导出-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs)

- [导入-Set-aipscannerconfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [AIPScanDiagnostics](/powershell/module/azureinformationprotection/Start-AIPScanDiagnostics)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [停止-AIPScan](/powershell/module/azureinformationprotection/Stop-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)

## <a name="next-steps"></a>后续步骤

安装并配置了扫描仪后，开始[扫描文件](deploy-aip-scanner-manage.md)。

另请参阅：[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。

**详细信息：**

- 想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

- 您可能想知道： [Windows SERVER FCI 和 Azure 信息保护扫描程序之间的区别是什么？](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- 使用 PowerShell 以交互方式对台式计算机上的文件进行分类和保护。 有关此方案以及使用 PowerShell 的其他方案的详细信息，请参阅[将 PowerShell 与 Azure 信息保护统一标签客户端配合使用](./rms-client/clientv2-admin-guide-powershell.md)。
