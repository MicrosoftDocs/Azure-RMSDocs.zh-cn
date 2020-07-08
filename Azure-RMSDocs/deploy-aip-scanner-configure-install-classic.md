---
title: 安装和配置 Azure 信息保护（AIP）扫描程序
description: 说明如何安装和配置 Azure 信息保护扫描程序，以便发现、分类和保护数据存储中的文件。
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
ms.openlocfilehash: c10aed757d625cf78fadc2b3d5889025c460ab75
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86049489"
---
# <a name="configuring-and-installing-the-azure-information-protection-classic-scanner"></a>配置和安装 Azure 信息保护经典扫描程序

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*

>[!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>
> 如果使用的是统一标签扫描程序，请参阅[安装和配置 Azure 信息保护统一标签扫描器](deploy-aip-scanner-configure-install.md)。

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

    :::image type="content" source="media/scanner-add-profile.png" alt-text="添加内容扫描作业（fo Azure 信息保护扫描程序）":::

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

    ```ps
    Install-AIPScanner -SqlServerInstance <name> -Profile <cluster name>
    ```

    例如，使用配置文件名称“欧洲”****：

    - 对于默认实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`

    - 对于命名实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`

    - 对于 SQL Server Express：`Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`

    出现提示时，请提供扫描程序服务帐户（ `\<domain\user name>` ）和密码的凭据。

1. 使用**管理工具**服务验证是否已安装该服务  >  **Services**。

    已安装的服务被命名为 Azure信息保护扫描程序，并被配置为使用你创建的扫描程序服务帐户运行****。

现在，你已安装了扫描仪，你需要[获取一个 Azure AD 令牌，以便扫描程序](#get-an-azure-ad-token-for-the-scanner)服务帐户进行身份验证，以便扫描程序可以在无人参与的情况下运行。

## <a name="get-an-azure-ad-token-for-the-scanner"></a>获取扫描程序的 Azure AD 令牌

Azure AD 令牌允许扫描程序对 Azure 信息保护服务进行身份验证。

获取 Azure AD 令牌：

1. 返回 Azure 门户，以创建两个 Azure AD 应用程序来指定用于身份验证的访问令牌。 此令牌允许扫描程序以非交互方式运行。

    有关详细信息，请参阅[如何以非交互方式为 Azure 信息保护标记文件](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)。

2. 在 Windows Server 计算机中，如果你的扫描程序服务帐户已被授予**本地登录**的权限，请使用此帐户登录并启动 PowerShell 会话。

    运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)，指定从上一步骤中复制的值：

    ```ps
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    系统提示时，请为 Azure AD 的服务帐户凭据指定密码，然后单击“接受”****。

    例如：

    ```powershell
    Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f").token | clip
    Acquired application access token on behalf of the user
    ```

> [!TIP]
> 如果你的扫描仪服务帐户无法被授予**本地登录**权限，请[指定并使用 set-aipauthentication 的 Token 参数](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)。
>

现在，扫描器提供了一个用于对 Azure AD 进行身份验证的令牌，此令牌根据你在 Azure AD 中配置的**Web 应用**的配置，该令牌的有效期为一年、两年或从不。

如果令牌过期，则须重复步骤 1 和步骤 2。

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

    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)

    或者，在 PowerShell 会话中运行以下命令：

    ```ps
    Start-AIPScan
    ```

4. 若要查看标记的文件、应用了哪些分类以及是否应用了保护的报告，请监视事件日志中的信息类型**911**和最新的时间戳。

    检查报表详细信息，或使用 Azure 门户查找此信息。

现在，扫描器计划为连续运行。 当扫描程序在所有配置的文件中工作时，它会自动启动一个新循环，以便发现所有新文件和更改的文件。

## <a name="change-which-file-types-to-protect"></a>更改要保护的文件类型

默认情况下，AIP 扫描器仅保护 Office 文件类型和 PDF 文件。 若要更改此行为（例如，若要将扫描仪配置为保护所有文件类型，就像客户端一样）或保护特定的其他文件类型，请按如下所示编辑注册表：

- 指定要保护的其他文件类型
- 指定要应用的保护类型（本机或常规）

有关详细信息，请参阅开发人员指南中的[文件 API 配置](develop/file-api-configuration.md)。 对于本文档中的开发人员，常规保护被称为“PFile”。

若要使受支持的文件类型与客户端保持一致，则所有文件都将自动通过本机或一般保护进行保护：

1. 指定：

    - `*`作为注册表项的通配符
    - `Encryption`作为值（REG_SZ）
    - `Default`作为值数据

1. 验证**MSIPC**和**FileProtection**项是否存在。 如果不是，则手动创建它们，然后为每个文件扩展名创建一个子项。

    例如，若要让扫描仪保护除 Office 文件和 Pdf 之外的 TIFF 图像，在编辑后，注册表将如下所示：

    ![编辑扫描程序的注册表以应用保护](./media/editregistry-scanner.png)

    > [!NOTE]
    > 作为图像文件，TIFF 文件支持本机保护，生成的文件扩展名为**ptiff。**
    >

    对于不支持本机保护的文件，请将文件扩展名指定为新密钥，并为 PFile 获取常规保护****。 受保护文件的生成文件扩展名为 **.pfile。**

有关类似于支持本机保护，但必须在注册表中指定的文本和图像文件类型的列表，请参阅[支持分类和保护的文件类型](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection)。

## <a name="upgrading-your-scanner"></a>升级扫描仪

如果以前安装了扫描仪并想要升级，请参阅[升级 Azure 信息保护扫描程序](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。

然后，按常规方式[配置](deploy-aip-scanner-configure-install-classic.md)和[使用扫描仪](deploy-aip-scanner-manage-classic.md)，跳过安装扫描程序的步骤。

>[!NOTE]
> 如果扫描仪版本早于1.48.204.0，但尚未准备好进行升级，请参阅[部署以前版本的 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner-previousversions.md)。

## <a name="editing-data-repository-settings-in-bulk"></a>批量编辑数据存储库设置

使用 "**导出**" 和 "**导入**" 按钮可以在多个存储库中对扫描程序进行更改。

这样一来，就不需要在 Azure 门户中手动进行相同的更改。

例如，如果在多个 SharePoint 数据存储库上有一个新的文件类型，则可能需要批量更新这些存储库的设置。

跨存储库批量进行更改：

1. 在 "**存储库**" 窗格的 "Azure 门户" 中，选择 "**导出**" 选项。 例如：

    :::image type="content" source="media/export-scanner-repositories.png" alt-text="导出扫描程序的数据存储库设置":::

1. 手动编辑导出的文件以进行更改。

1. 使用同一页面上的 "**导入**" 选项将更新导入到存储库中。

## <a name="using-the-scanner-with-alternative-configurations"></a>使用具有备选配置的扫描程序

Azure 信息保护扫描程序通常会查找为标签指定的条件，以便根据需要对内容进行分类和保护。

在以下情况下，Azure 信息保护扫描程序还可以扫描内容并管理标签，而不会配置任何条件：

- [将默认标签应用于数据存储库中的所有文件](#apply-a-default-label-to-all-files-in-a-data-repository)
- [标识所有自定义条件和已知的敏感信息类型](#identify-all-custom-conditions-and-known-sensitive-information-types)

### <a name="apply-a-default-label-to-all-files-in-a-data-repository"></a>将默认标签应用于数据存储库中的所有文件

在此配置中，存储库中所有未标记的文件都标有为存储库或内容扫描作业指定的默认标签。 文件标记为 "无检查"。

配置下列设置：

- **基于内容标记文件：** 设置为**Off**
- **默认标签：** 设置为 "**自定义**"，然后选择要使用的标签

### <a name="identify-all-custom-conditions-and-known-sensitive-information-types"></a>标识所有自定义条件和已知的敏感信息类型

此配置使你能够查找你可能未意识到的敏感信息，因为扫描程序的扫描速率很高。

将要**发现的信息类型**设置为 "**所有**"。

为了识别用于标记的条件和信息类型，扫描程序使用为标签指定的自定义条件，以及可为标签指定的信息类型列表，如 Azure 信息保护策略中所列。

有关详细信息，请参阅[快速入门：查找您拥有的敏感信息](quickstart-findsensitiveinfo.md)。

## <a name="optimizing-scanner-performance"></a>优化扫描程序性能

> [!NOTE]
> 如果希望提高扫描仪计算机的响应能力而不是扫描程序性能，请使用 "高级客户端设置"[限制扫描程序使用的线程数](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)。
>

使用以下选项和指南来帮助优化扫描程序性能：

|选项  |说明  |
|---------|---------|
|**在扫描程序计算机和被扫描的数据存储之间建立高速可靠的网络连接**     |  例如，将扫描仪计算机放在与扫描的数据存储相同的网络段中，或者在同一网段中放置。 </br></br>由于要检查文件，扫描程序会将文件内容传输到运行 scanner 服务的计算机，因此网络连接的质量会影响扫描程序性能。 </br></br>减少或消除传输数据所需的网络跃点还可以减少网络上的负载。      |
|**确保扫描程序计算机具有可用的处理器资源**     | 检查文件内容并对文件进行加密和解密是处理密集型操作。 </br></br>监视指定数据存储的典型扫描周期，以确定缺乏处理器资源是否会对扫描程序性能产生负面影响。        |
|**安装扫描程序的多个实例** | 当你为扫描程序指定自定义群集（配置文件）名称时，Azure 信息保护扫描程序在相同的 SQL server 实例上支持多个配置数据库。 |
|**授予特定权限并禁用低完整性级别**|确认运行扫描程序的服务帐户只包含[服务帐户要求](deploy-aip-scanner-prereqs.md#service-account-requirements)中所述的权限。 </br></br>然后，配置 "[高级客户端" 设置](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner)以禁用扫描程序的低完整性级别。|
|**检查备选配置用法** |在使用[备选配置](#using-the-scanner-with-alternative-configurations)将默认标签应用于所有文件时，扫描程序可以更快地运行，因为扫描程序不检查文件内容。 <br/></br>如果你使用[替换配置](#using-the-scanner-with-alternative-configurations)标识所有自定义条件和已知敏感信息类型，扫描程序的运行速度会更慢。|
|**减少扫描程序超时** | 减少扫描程序超时和[高级客户端设置](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner)。缩短扫描程序超时可提供更好的扫描速率和更低的内存消耗。 </br></br>**注意：** 减少扫描程序超时意味着可能会跳过某些文件。
| | |

<!-- removed with local folders
|**Do not scan local folders on the computer running the scanner service**     | If you have folders to scan on a Windows server, install the scanner on a different computer and configure those folders as network shares to scan. </br></br>Separating the two functions of hosting files and scanning files means that the computing resources for these services are not competing with one another.        |
-->

### <a name="additional-factors-that-affect-performance"></a>影响性能的其他因素

影响扫描程序性能的其他因素包括：

|因子  |说明  |
|---------|---------|
|**加载/响应时间**     |包含要扫描的文件的数据存储的当前负载和响应时间也会影响扫描程序性能。         |
|**扫描仪模式**（发现/强制）    | 发现模式的扫描速度通常比 "强制" 模式高。 </br></br>发现需要单个文件读取操作，而 "强制" 模式需要读取和写入操作。        |
|**策略更改**     |如果你已更改 Azure 信息保护策略中的条件，则你的扫描程序性能可能会受到影响。 </br></br>当扫描程序必须检查每个文件时，第一个扫描周期的时间比默认情况下的后续扫描周期长，仅检查新文件和更改的文件。 </br></br>如果更改条件，将再次扫描所有文件。 有关详细信息，请参阅重新[扫描文件](deploy-aip-scanner-manage-classic.md#rescanning-files)。|
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

想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

您可能想知道： [Windows SERVER FCI 和 Azure 信息保护扫描程序之间的区别是什么？](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 要详细了解此方案及使用 PowerShell 的其他方案，请参阅[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。
