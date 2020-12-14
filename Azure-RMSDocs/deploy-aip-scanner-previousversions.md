---
title: 部署 Azure 信息保护扫描程序-以前的版本
description: 早于当前正式发行版的 Azure 信息保护扫描程序版本的部署说明。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 085fac334348e0d13381571c9622b64a2b20e172
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382728"
---
# <a name="deploying-previous-versions-of-the-azure-information-protection-classic-client-scanner"></a>部署以前版本的 Azure 信息保护经典客户端扫描器

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2019、Windows Server 2016、windows server 2012 R2 *
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 对于 unfied 标签客户端的扫描程序，请参阅 [什么是 AIP 统一标记扫描器？](deploy-aip-scanner.md)。*

> [!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月31日** 被 **弃用**。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>
> 本文适用于低于版本 **1.48.204.0** 但仍在支持中的 Azure 信息保护扫描程序的版本。 若要将早期版本升级到当前版本，请参阅 [升级 Azure 信息保护扫描程序](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。

利用此信息了解 Azure 信息保护扫描程序，并了解如何成功安装、配置和运行该扫描程序。

此扫描程序在 Windows Server 上作为服务运行，使你能够发现和保护以下数据存储中的文件并对其进行分类：

- 使用服务器消息块 (SMB) 协议的网络共享 UNC 路径。

- 通过 SharePoint Server 2013 为 SharePoint Server 2019 的文档库和文件夹提供文档。 如果客户[扩展了针对此版 SharePoint 的支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)，则 SharePoint 2010 也会受到支持。

若要在云存储库上扫描并标记文件，请使用 [Cloud App Security](/cloud-app-security/)，而不是扫描程序。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序概述

为应用自动分类的标签配置 [Azure 信息保护策略](configure-policy.md)后，可为此扫描程序发现的文件设置标签。 标签可应用分类，并且可以应用保护或移除保护：

![Azure 信息保护扫描程序体系结构概述](./media/infoprotect-scanner.png)

通过使用计算机上安装的 iFilter，扫描程序可检查 Windows 能编制索引的任何文件。 然后，若要确定是否需要标记文件，扫描程序会使用 Microsoft 365 内置数据丢失防护 (DLP) 敏感度信息类型和模式检测，或 Microsoft 365 regex 模式。 因为扫描程序使用 Azure 信息保护客户端，所以它可以对相同[文件类型](./rms-client/client-admin-guide-file-types.md)进行分类和保护。

可仅在发现模式下运行扫描程序，利用报告确认对文件设置标签时会发生什么情况。 或者，可运行扫描程序自动应用标签。 还可以运行扫描程序来发现包含敏感信息类型的文件，无需配置条件标签来应用自动分类。

注意，扫描程序不会实时发现和标记。 它会系统地浏览指定数据存储中的文件，可将此周期配置为运行一次或多次。

可以指定要扫描或排除不进行扫描的文件类型。 若要限制扫描程序检查的文件，可使用 **Set-AIPScannerScannedFileTypes** 定义一个文件类型列表。

## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序的先决条件

安装 Azure 信息保护扫描程序之前，请确保已满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|运行扫描程序服务的 Windows Server 计算机：<br /><br />- 4 核处理器<br /><br />- 8 GB RAM<br /><br />- 临时文件 10GB 可用空间（平均）|Windows Server 2019、Windows Server 2016 或 Windows Server 2012 R2。 <br /><br />**注意**：对于非生产环境中的测试或评估目的，可以使用 [Azure 信息保护客户端支持](requirements.md#client-devices)的 Windows 客户端操作系统。<br /><br />此计算机可以是物理或虚拟计算机，需拥有快速可靠的网络，可连接到要进行扫描的数据存储。<br /><br /> 扫描程序需要足够的磁盘空间，才能为其扫描的每个文件（每个核心四个文件）创建临时文件。 借助建议的 10GB 磁盘空间，4 核处理器可以扫描 16 个文件，每个文件的大小为 625MB。 <br /><br />如果由于组织策略而无法建立 internet 连接，请参阅 [部署带有备用配置的扫描程序](#deploying-the-scanner-with-alternative-configurations) 部分。 否则，请确保此计算机具有 internet 连接，允许通过 HTTPS (端口 443) 的以下 Url：<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com|
|运行扫描程序服务的服务帐户 |除了在 Windows Server 计算机上运行扫描程序服务外，此 Windows 帐户还对 Azure AD 进行身份验证，并下载 Azure 信息保护策略。 此帐户必须是同步到 Azure AD 的 Active Directory 帐户。 如果由于组织策略而无法同步此帐户，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />此服务帐户有以下要求：<br /><br />- 在本地登录的用户权限分配。 此权限是安装和配置扫描程序所必需的，但不可用于操作。 必须将此权限授予服务帐户，但当确认扫描程序可发现、保护文件并对其进行分类后，可删除此权限。 如果由于组织策略的限制而甚至无法在短时间内授予此权限，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />- 作为服务登录的用户权限分配。 扫描程序安装过程中会自动将此权限授予服务帐户，此权限是安装、配置和操作扫描程序所必需的。 <br /><br />-对数据存储库的权限：对于本地 SharePoint 上的数据存储库，如果为站点选择了 "**添加" 和 "自定义" 页**，则始终授予 **编辑** 权限，或授予 **设计** 权限。 对于其他数据存储库，请授予 " **读取** " 和 " **写入** " 权限以扫描文件，然后将分类和保护应用到满足 Azure 信息保护策略中的条件的文件。 若要仅在发现模式下运行扫描程序的其他数据存储库，请 **阅读** 权限。<br /><br />- 对于可重新保护或移除保护的标签：要确保扫描程序始终能够访问受保护的文件，请将此帐户设置为 Azure Rights Management 服务的[超级用户](configure-super-users.md)，并确保已启用超级用户功能。 要详细了解应用保护的帐户要求，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。 此外，如果对分阶段部署实现了[载入控件](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，还请确保已配置的载入控件中包含此帐户。|
|存储扫描程序配置的 SQL Server：<br /><br />- 本地或远程实例<br /><br />- [不区分大小写排序规则](/sql/relational-databases/collations/collation-and-unicode-support) <br /><br />- 安装扫描程序的 Sysadmin 角色|SQL Server 2012 是以下版本的最低版本：<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />如果安装了多个扫描程序实例，则每个扫描程序实例都需要自己的 SQL Server 实例。<br /><br />如果安装扫描程序且帐户拥有 Sysadmin 角色，那么在安装过程中会自动创建 AzInfoProtectionScanner 数据库，并向运行扫描程序的服务帐户授予相应 db_owner 角色。 如果无法获得 Sysadmin 角色或组织策略要求手动创建和配置数据库，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />每个部署的配置数据库大小不同，建议为要扫描的每 1 百万个文件分配 500 MB。 |
|在 Windows Server 计算机上安装 Azure 信息保护经典客户端|必须安装扫描程序的完整客户端。 请勿安装只带有 PowerShell 模块的客户端。<br /><br />有关客户端安装说明，请参阅[管理员指南](./rms-client/client-admin-guide.md)。 如果现在需要将已安装的旧扫描程序升级到更高版本，请参阅[升级 Azure 信息保护扫描程序](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。|
|已配置可应用自动分类和保护（可选）的标签|有关如何为条件配置标签以及如何应用保护的更多信息：<br /> - [如何为自动和建议分类配置条件](configure-policy-classification.md)<br /> - [如何为 Rights Management 保护配置标签](configure-policy-protection.md) <br /><br />**提示**：可以使用 [教程](infoprotect-quick-start-tutorial.md) 中的说明来测试扫描仪，并在已准备好的 Word 文档中查找信用卡号。 但是，需要更改标签配置，以便将“选择应用此标签的方式”设置为“自动”而不是“推荐”。 然后从文档中删除标签（如果已应用），并将文件复制到扫描程序的数据存储库。 <br /><br /> 尽管即使你尚未配置应用自动分类的标签，仍然可以运行扫描程序，但这些说明中并未涵盖此方案。 [详细信息](#using-the-scanner-with-alternative-configurations)|
|对于要扫描的 SharePoint 文档库和文件夹：<br /><br />-SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|扫描程序不支持其他版本的 SharePoint。<br /><br />使用 [版本控制](/sharepoint/governance/versioning-content-approval-and-check-out-planning)时，扫描程序会检查并标记上次发布的版本。 如果扫描程序标签文件和 [内容审批](/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) 是必需的，则必须向用户批准标记为 "文件" 的文件。 <br /><br />对于大型 SharePoint 场，请检查是否需要增加列表视图阈值（默认为 5,000），以便扫描程序访问所有文件。 有关详细信息，请参阅以下 SharePoint 文档： [在 sharepoint 中管理大型列表和库](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|对于要扫描的 Office 文档：<br /><br />- Word、Excel 和 PowerPoint 的 97-2003 文件格式和 Office Open XML 格式|有关扫描程序为这些文件格式支持的文件类型的详细信息，请参阅 [Azure 信息保护客户端支持的文件类型](./rms-client/client-admin-guide-file-types.md)|
|对于长路径：<br /><br />- 最多 260 个字符，除非扫描程序安装在 Windows 2016 上，并且该计算机配置为支持长路径|Windows 10 和 windows Server 2016 支持使用以下 [组策略设置](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)的路径长度大于260个字符：**本地计算机策略**  >  **计算机配置**  >  **管理模板**  >  **所有设置**  >  **启用 Win32 长路径**<br /><br /> 有关支持长文件路径的详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

如果由于组织策略禁止而无法满足表中的所有要求，请参阅下一部分中介绍的备用配置。

如果满足所有要求，请直接转到[安装部分](#install-the-scanner)。

### <a name="deploying-the-scanner-with-alternative-configurations"></a>使用备用配置部署扫描程序

表中列出的先决条件是扫描程序的默认要求，之所以建议是因为它们是用于扫描程序部署的最简单配置。 它们应适用于初始测试，以便能够检查扫描程序的功能。 不过，在产品环境中，组织策略可能会禁止这些默认要求，因为存在下列一个或多个限制：

- 不允许服务器连接到 internet

- 无法向你授予 Sysadmin 角色或者必须手动创建并配置数据库

- 无法将服务帐户授予 **本地登录** 权限

- 服务帐户无法同步到 Azure Active Directory 但服务器具有 internet 连接

虽然扫描程序可以适应这些限制，但需要其他配置。

#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>限制：扫描仪服务器不能连接到 internet

请按照适用于[已断开连接的计算机](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)的说明操作。

请注意，在此配置中，扫描程序无法使用组织的基于云的密钥来应用（或删除）保护配置。 相反，扫描程序只能使用应用分类或 [HYOK](configure-adrms-restrictions.md) 保护的标签。

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>限制：无法获得 Sysadmin 角色，或必须手动创建和配置数据库

如果可以获得 Sysadmin 角色来安装扫描程序，就能在扫描程序安装完成后删除此角色。 使用此配置时，数据库会自动创建，而且扫描程序的服务帐户也会自动获得相应权限。 不过，配置扫描程序的用户帐户需要拥有 AzInfoProtectionScanner 数据库的 db_owner 角色，你必须手动向用户帐户授予此角色。

如果你不能暂时授予 Sysadmin 角色，则必须在安装 scanner 之前要求具有 Sysadmin 权限的用户手动创建名为 Azinfoprotectionscanner.exe 的数据库。 对于此配置，必须分配以下角色：

|帐户|数据库级角色|
|--------------------------------|---------------------|
|扫描程序的服务帐户|db_owner|
|用于安装扫描程序的用户帐户|db_owner|
|用于配置扫描程序的用户帐户 |db_owner|

用于安装和配置扫描程序的用户帐户通常是相同的。 不过，如果使用不同的帐户，它们都需要拥有 AzInfoProtectionScanner 数据库的 db_owner 角色。

若要创建用户并授予对此数据库的 db_owner 权限，请要求 Sysadmin 运行以下 SQL 脚本两次。 第一次，对于运行扫描程序的服务帐户，以及第二次用于安装和管理扫描仪。 运行该脚本之前，请将 *domain\user* 替换为服务帐户或用户帐户的域名和用户帐户名：

```sql
if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
USE AzInfoProtectionScanner IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
```

此外：

- 您必须是将运行扫描程序的服务器上的本地管理员
- 必须为将运行扫描程序的服务帐户授予对以下注册表项的 "完全控制" 权限：

    - HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server

如果在配置这些权限后出现错误，则在安装扫描程序时，可以忽略该错误，并且可以手动启动 scanner 服务。

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>限制：无法向扫描程序的服务帐户授予“本地登录”权限

如果组织策略禁止向服务帐户授予“本地登录”权限，但允许授予“以批处理作业形式登录”权限，请按照管理员指南内[对 Set-AIPAuthentication 指定和使用 Token 参数](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)一文中的说明操作。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>限制：扫描仪服务帐户无法同步到 Azure Active Directory 但服务器具有 internet 连接

可以使用一个帐户来运行扫描程序服务，并使用另一个帐户对 Azure Active Directory 进行身份验证：

- 对于扫描程序服务帐户，可以使用本地 Windows 帐户或 Active Directory 帐户。

- 如果使用 Azure Active Directory 帐户，请按照管理员指南内[对 Set-AIPAuthentication 指定和使用 Token 参数](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)一文中的说明操作。

## <a name="install-the-scanner"></a>安装扫描程序

1. 登录到将要运行扫描程序的 Windows Server 计算机。 使用具有本地管理员权限并具有写入到 SQL Server master 数据库权限的帐户。

2. 使用“以管理员身份运行”选项打开 Windows PowerShell 会话。

3. 运行 **install-aipscanner** cmdlet，并指定要在其中为 Azure 信息保护扫描程序创建数据库的 SQL Server 实例：

    ```ps
    Install-AIPScanner -SqlServerInstance <name>
    ```

    例如：

    - 对于默认实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1`

    - 对于命名实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`

    - 对于 SQL Server Express：`Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`

    出现提示时，请提供扫描程序服务帐户的凭据 (\<domain\user name>) 和密码。

4. 使用 **管理工具** 服务验证是否已安装该服务  >  。

    已安装的服务被命名为 Azure信息保护扫描程序，并被配置为使用你创建的扫描程序服务帐户运行。

现已安装扫描程序，需获取 Azure AD 令牌以便扫描程序服务帐户进行身份验证，从而实现以无人参与的方式运行。

## <a name="get-an-azure-ad-token-for-the-scanner"></a>获取扫描程序的 Azure AD 令牌

借助 Azure AD 令牌，Azure 信息保护服务可以验证扫描程序服务帐户。

1. 通过同一台 Windows Server 计算机或通过桌面登录 Azure 门户，创建 2 个 Azure AD 应用程序 - 指定用于身份验证的访问令牌时需使用这两个应用程序。 首次以交互方式登录后，此令牌将允许扫描程序以非交互方式运行。

    要创建这些应用程序，请按照管理员指南中[如何以非交互方式为 Azure 信息保护标记文件](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)的说明执行操作。

2. 在 Windows Server 计算机中，如果你的扫描程序服务帐户已就安装授予了“本地登录”权限：使用此帐户登录并启动 PowerShell 会话。 运行 **Set-AIPAuthentication**，指定从上一步骤中复制的值：

    ```ps
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    系统提示时，请为 Azure AD 的服务帐户凭据指定密码，然后单击“接受”。

    如果你的扫描程序服务帐户无法就安装授予“本地登录”权限：请按照管理员指南中[指定和使用 Set-AIPAuthentication 的令牌参数](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)一节中的说明来操作。

扫描程序现已拥有一个令牌，可向 Azure AD 进行身份验证。该令牌的有效期为 1 年、2 年或永不过期，具体取决于 Azure AD 中“Web 应用/API”的配置。 如果令牌过期，则须重复步骤 1 和步骤 2。

现可指定要扫描的数据存储。

## <a name="specify-data-stores-for-the-scanner"></a>指定扫描程序的数据存储

使用 **Add-AIPScannerRepository** cmdlet 指定将由 Azure 信息保护扫描程序进行扫描的数据存储。 您可以为 SharePoint 文档库和文件夹指定 UNC 路径和 SharePoint Server Url。

SharePoint 支持的 SharePoint 版本： SharePoint Server 2019、SharePoint Server 2016 和 SharePoint Server 2013。 对于具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)的客户，还支持 SharePoint Server 2010。

1. 在同一台 Windows Server 计算机中，通过在 PowerShell 会话中运行以下命令来添加第一个数据存储：

    ```ps
    Add-AIPScannerRepository -Path <path>
    ```

    例如： `Add-AIPScannerRepository -Path \\NAS\Documents`

    有关其他示例，请使用此 cmdlet 的 PowerShell help 命令 `Get-Help Add-AIPScannerRepository -examples` 。

2. 对想要扫描的所有数据存储重复此命令。 如果要删除已添加的数据存储，请使用 **Remove-AIPScannerRepository** cmdlet。

3. 确认已正确指定所有数据存储，方法是运行 **Get-AIPScannerRepository** cmdlet：
    
    ```ps
    Get-AIPScannerRepository
    ```

利用扫描程序的默认配置，现在可在发现模式下运行首次扫描。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>运行发现周期并查看扫描程序报告

1. 在 PowerShell 会话中，通过运行以下命令启动扫描程序：

    ```ps
    Start-AIPScan
    ```

    或者，可以从 Azure 门户启动扫描程序。 从 " **Azure 信息保护-节点** " 窗格中，选择扫描仪节点，然后单击 " **立即扫描** " 选项：

    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)

2. 运行以下命令，等待扫描程序完成其周期：

    ```ps
    Get-AIPScannerStatus
    ```

    或者，你可以通过检查 "**状态**" 列，在 "Azure 门户中的" **Azure 信息保护-节点**"窗格中查看状态。

    查找显示“空闲”而非“正在扫描”的状态。

    当扫描程序浏览完指定数据存储中所有文件时，扫描程序停止（尽管扫描程序服务仍在运行）。

    查看本地 Windows 应用程序和服务事件日志和 Azure 信息保护。 另外，此日志还会报告扫描程序完成扫描的时间，以及结果摘要。 请查看信息事件 ID 911。

3. 查看存储在 %localappdata%\Microsoft\MSIP\Scanner\Reports 中的报表。 .txt 摘要文件包括扫描所用的时间、扫描的文件数以及匹配信息类型的文件数量。 .csv 文件包含每个文件的更多详细信息。 此文件夹为每个扫描周期最多存储 60 个报表，并且压缩除最新报表之外的所有报表，以帮助最大程度地减少所需的磁盘空间。

    > [!NOTE]
    > 可以将 ReportLevel 参数和 **Set-AIPScannerConfiguration** 结合使用来更改日志记录级别，但不能更改报表文件夹位置或名称。 如果要将报表存储在其他卷或分区上，请考虑使用该文件夹的目录交叉点。
    >
    > 例如，使用 [Mklink](/windows-server/administration/windows-commands/mklink) 命令：`mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`

    使用默认设置时，只有满足为自动分类配置的条件的文件才会被包括在详细报表中。 如果未在这些报表中看到应用任何标签，请检查标签配置是否包括自动分类而不是推荐分类。

    > [!TIP]
    > 扫描程序会每 5 分钟向 Azure 信息保护发送一次此信息，这样你就可以准实时地在 Azure 门户中查看结果。 有关详细信息，请参阅 [Azure 信息保护报表](reports-aip.md)。

    如果结果与预期不符，建议对在 Azure 信息保护策略中指定的条件进行微调。 如果是这种情况，请重复步骤 1 到 3，直到可更改配置以应用分类和保护（可选）。

Azure 门户仅显示有关上次扫描的信息。 如果需要查看先前扫描的结果，请返回到扫描程序计算机上存储的报表，它位于 %localappdata%\Microsoft\MSIP\Scanner\Reports 文件夹中。

如果已准备好对扫描程序发现的文件进行自动标记，请继续下一步。

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>将扫描程序配置为应用分类和保护

在其默认设置中，扫描程序在仅报告模式下运行一次。 若要更改这些设置，请使用 **set-aipscannerconfiguration**：

1. 在 Windows Server 计算机上的 PowerShell 会话中，运行以下命令：

    ```ps
    Set-AIPScannerConfiguration -Enforce On -Schedule Always
    ```

    你可能还希望更改其他配置设置。 例如，是否更改文件属性，以及报告中应记录的内容。 此外，如果 Azure 信息保护策略包括需要理由信息以降低分类级别或移除保护的设置，请使用此 cmdlet 指定该信息。 有关每个配置设置的详细信息，请使用以下 PowerShell 帮助命令： `Get-Help Set-AIPScannerConfiguration -detailed`

2. 记录当前时间，并通过运行以下命令重新启动扫描程序：
    
    ```ps
    Start-AIPScan
    ```

    或者，可以从 Azure 门户启动扫描程序。 从 " **Azure 信息保护-节点** " 窗格中，选择扫描仪节点，然后单击 " **立即扫描** " 选项：

    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)

3. 重新监视 911 信息类型的事件日志，并且时间戳要晚于上个步骤启动扫描时的时间。

    然后查看报告，详细了解标记了哪些文件、向每个文件应用了什么分类，以及是否向它们应用了保护。 或者，使用 Azure 门户，更轻松地了解此信息。

因为我们将计划配置为持续运行，所以当扫描程序扫描完所有文件时，它将开始一个新周期，以便发现任何新文件和更改的文件。

## <a name="how-files-are-scanned"></a>如何扫描文件

扫描程序在扫描文件时运行以下过程。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. 确定是包括还是排除文件以进行扫描

扫描程序自动跳过[从分类和保护中排除](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)的文件，如可执行文件和系统文件。

可以定义要扫描或不要扫描的文件类型列表，从而更改此行为。 在指定此列表并且不指定数据存储库时，该列表适用于未指定其自己列表的所有数据存储库。 若要指定此列表，请使用 **Set-AIPScannerScannedFileTypes**。

指定文件类型列表后，可以使用 **Add-AIPScannerScannedFileTypes** 向列表添加新文件类型，并能使用 **Remove-AIPScannerScannedFileTypes** 从列表中删除文件类型。

### <a name="2-inspect-and-label-files"></a>2. 检查并标记文件

然后，扫描程序使用筛选器来扫描支持的文件类型。 操作系统也可使用这些筛选器来进行 Windows 搜索和索引编制。 无需任何额外配置，即可使用 Windows IFilter 来扫描 Word、Excel、PowerPoint 使用文件类型，以及用于 PDF 文档和文本文件的文件类型。

有关默认支持的文件类型的完整列表，以及有关如何配置包括 .zip 文件和 .tiff 文件的现有筛选器的详细信息，请参阅[支持检查的文件类型](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)。

检查之后，可以使用为标签指定的条件为这些文件类型设置标签。 或者，如果要使用发现模式，可以报告这些文件，在其中包含为标签指定的条件，或所有已知敏感信息类型。

但在以下情况下，扫描程序无法为文件设置标签：

- 如果标签应用分类而不应用保护，并且文件类型不[只支持分类](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)。

- 如果标签应用分类和保护，但扫描程序不保护该文件类型。

    默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。 可通过[编辑注册表](#editing-the-registry-for-the-scanner)来保护其他文件类型，如下一节所述。

例如，检查文件扩展名为 .txt 的文件之后，扫描程序无法应用为分类而非保护配置的标签，因为 .txt 文件类型不支持仅分类。 如果为分类和保护配置了标签，并且针对 .txt 文件类型编辑了注册表，则扫描程序可为文件设置标签。

> [!TIP]
> 在此过程中，如果扫描程序停止并且未完成对存储库中大量文件的扫描：
>
> - 可能需要增加托管文件的操作系统的动态端口数。 SharePoint 的服务器强化可能是导致扫描程序超出允许的网络连接数并因此停止的一个原因。
>  
>     若要检查这是否是扫描程序停止的原因，请查看是否在%*localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog 中为扫描程序记录以下错误消息 (如果有多个日志) ： **无法连接到远程---服务器 > 系统 SocketException：每个套接字地址 (协议/网络地址/端口) 通常只允许使用 IP：端口**
>  
>     有关如何查看当前端口范围并增加范围的详细信息，请参阅 [可修改的设置以提高网络性能](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)。
>
> - 对于大型 SharePoint 场，可能需要增加列表视图阈值（默认情况下为 5,000）。 有关详细信息，请参阅以下 SharePoint 文档： [在 sharepoint 中管理大型列表和库](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)。

### <a name="3-label-files-that-cant-be-inspected"></a>3. 无法检查的标签文件

对于无法检查的文件类型，扫描程序应用 Azure 信息保护策略中的默认标签或为扫描程序配置的默认标签。

与上述步骤相同，在下列情况下，扫描程序无法为文件设置标签：

- 如果标签应用分类而不应用保护，并且文件类型不[只支持分类](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)。

- 如果标签应用分类和保护，但扫描程序不保护该文件类型。

    默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。 可通过[编辑注册表](#editing-the-registry-for-the-scanner)来保护其他文件类型，如下文所述。

### <a name="editing-the-registry-for-the-scanner"></a>编辑扫描程序的注册表

若要更改默认扫描程序行为以保护 Office 文件和 PDF 以外的文件类型，必须手动编辑注册表并指定想要保护的其他文件类型以及保护类型（本机或泛型）。 有关说明，请参阅开发人员指南中的[文件 API 配置](develop/file-api-configuration.md)。 对于本文档中的开发人员，常规保护被称为“PFile”。 此外，特定于扫描程序：

- 扫描仪具有其自己的默认行为：默认情况下仅保护 Office 文件格式和 PDF 文档。 如果未修改注册表，则扫描程序不会保护任何其他文件类型或为其设置标签。

- 如果你希望 Azure 信息保护客户端使用与 Azure 信息保护客户端相同的默认保护行为，其中所有文件都自动使用本机保护或常规保护进行保护：将通配符指定为 `*` 注册表项， `Encryption` 作为值 (REG_SZ) ，并 `Default` 作为值数据。

编辑注册表时，如果 MSIPC 密钥和 FileProtection 密钥不存在，则手动创建这些密钥，并创建每个文件扩展名的密钥。

例如，除了 Office 文件和 PDF 之外，若要使扫描程序还保护 TIFF 图像，编辑后的注册表将与下图类似。 作为图像文件，TIFF 文件支持本机保护，且生成的文件扩展名为 .ptiff。

![编辑扫描程序的注册表以应用保护](./media/editregistry-scanner.png)

有关同样支持本机保护但必须在注册表中进行指定的文本和图像文件类型列表，请参阅管理员指南中的[分类和保护的支持文件类型](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection)。

对于不支持本机保护的文件，请将文件扩展名指定为新密钥，并为 PFile 获取常规保护。 对于受保护的文件，生成的文件扩展名为 .pfile。

## <a name="when-files-are-rescanned"></a>重新扫描文件时的情况

在第一个扫描周期，扫描程序会检查所配置的数据存储中的所有文件，然后在后续扫描中仅检查新文件或修改后的文件。

可以通过使用 *Reset* 参数运行 **AIPScan** 来强制扫描程序再次检查所有文件。 必须为手动计划配置扫描仪，这需要使用 **set-aipscannerconfiguration** 将 *schedule* 参数设置为 "**手动**"。

或者，你可以强制扫描程序再次从 Azure 门户中的 " **Azure 信息保护-节点** " 窗格检查所有文件。 从列表中选择扫描程序，然后选择“重新扫描所有文件”选项：

![启动 Azure 信息保护扫描程序重新扫描](./media/scanner-rescan-files.png)

如果希望报告包含所有文件，再次检查所有文件非常有用；且当扫描程序在发现模式下运行时，通常会使用此配置选项。 完成全部扫描后，扫描类型自动更改为“增量”，以便后续扫描仅扫描新文件或修改后的文件。

此外，在扫描程序下载具有新条件或更改后的条件时，会检查所有文件。 扫描程序每小时刷新一次策略，当服务启动时以及策略执行一小时之后，也会刷新。  

> [!TIP]
> 如需以低于一小时的间隔刷新策略（例如在测试期间）：请从 **%LocalAppData%\Microsoft\MSIP\Policy.msip** 和 **%LocalAppData%\Microsoft\MSIP\Scanner** 手动删除策略文件 **Policy.msip**。 然后重新启动 Azure 信息扫描程序服务。
>
> 如果更改了此策略中的保护设置，请在保存保护设置后等待 15 分钟，再重新启动该服务。

如果扫描程序下载了未配置任何自动条件的策略，不会更新扫描程序文件夹中的策略文件副本。 在此方案中，必须从 **%LocalAppData%\Microsoft\MSIP\Policy.msip** 和 **%LocalAppData%\Microsoft\MSIP\Scanner** 中删除策略文件 **Policy.msip**，然后扫描程序才能够使用正确配置了自动条件标签的新下载的策略文件。

## <a name="using-the-scanner-with-alternative-configurations"></a>使用具有备选配置的扫描程序

Azure 信息保护扫描程序支持两种备选方案，在任何一种方案中都无需配置标签：

- 将默认标签应用于数据存储库中的所有文件。

    对于此配置，使用 **Set-AIPScannerRepository** cmdlet，并将“MatchPolicy” 参数设置为“关闭”。

    根据为数据存储库指定的默认标签（通过 SetDefaultLabel参数），不会检查文件的内容并会标记数据存储库中的所有文件；如果未指定，则将该默认标签指定为扫描程序帐户的策略设置。

- 标识所有自定义条件和已知敏感信息类型。

    对于此配置，使用 **Set-AIPScannerConfiguration** cmdlet，并将“DiscoverInformationTypes”参数设置为“全部”。

    扫描程序使用为 Azure 信息保护策略中的标签指定的任何自定义条件以及可指定用于 Azure 信息保护策略中的标签的信息类型列表。

    以下快速入门使用此配置，但它适用于当前版本的扫描程序： [快速入门：查找您拥有的敏感信息](quickstart-findsensitiveinfo.md)。

## <a name="optimizing-the-performance-of-the-scanner"></a>优化扫描程序性能

使用以下指南有助于优化扫描程序的性能。 但是，如果你的优先级是扫描仪计算机的响应性而不是扫描程序性能，你可以使用 [高级客户端设置](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner) 来限制扫描程序使用的线程数。

若要最大程度实现扫描程序的性能：

- **在扫描程序计算机和被扫描的数据存储之间建立高速可靠的网络连接**

    例如，将扫描程序计算机置于所扫描的数据存储所在的 LAN 或（首选）网络段中。

    网络连接的质量会影响扫描程序的性能，因为要检查文件，扫描程序需将文件内容传输到运行扫描程序服务的计算机中。 如果减少（或消除）此数据需传输的网络跃点数，网络上的负载随之减少。

- **确保扫描程序计算机具有可用的处理器资源**

    检查文件内容是否与你配置的条件相匹配，以及进行文件加密和解密，这些操作都是处理器密集型操作。 请监视所指定的数据存储的典型扫描周期，以确定缺少处理器资源是否对扫描程序性能造成负面影响。


影响扫描程序性能的其他因素：

- 包含要扫描的文件的数据存储的当前负载和响应时间

- 扫描程序是在发现模式还是强制模式下运行

    通常，发现模式的扫描速率比强制模式的高，因为发现操作需要单一文件读取操作，而强制模式需要读取和写入操作。

- 更改 Azure 信息保护中的条件

    在第一个扫描周期，扫描程序必须检查每个文件，而后续扫描周期默认仅扫描新文件和更改的文件，因此第一个周期明显比后续周期耗时长。 但是，如果更改 Azure 信息保护中的条件，则重新扫描所有文件，如[上一部分](#when-files-are-rescanned)所述。

- 自定义条件的正则表达式构造

    为避免占用过多内存并存在超时风险（每个文件 15 分钟），请查看正则表达式了解有效的模式匹配。 例如：

    - 避免[贪婪限定符](/dotnet/standard/base-types/quantifiers-in-regular-expressions)

    - 使用 `(?:expression)` 等非捕获组，而不是 `(expression)`

- 所选的日志记录级别

    可对扫描程序报告选择“调试”、“信息”、“错误”或“关闭”。 “关闭”可使性能最佳；“调试”会明显减低扫描程序的速度，应仅用于故障排除。 有关详细信息，请参阅通过运行 Set-AIPScannerConfiguration cmdlet 的 *eportlevel* 参数 `Get-Help Set-AIPScannerConfiguration -detailed` 。

- 文件自身：

    - 除了 Excel 文件，Office 文件的扫描速度比 PDF 文件更快。

    - 扫描未受保护的文件比扫描受保护的文件耗时更短。

    - 扫描大型文件明显比扫描小文件耗时更多。

- 此外：

    - 确认运行扫描程序的服务帐户仅具有 " [扫描仪先决条件](#prerequisites-for-the-azure-information-protection-scanner) " 部分中所述的权限，然后配置 " [高级客户端" 设置](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) 以禁用扫描程序的低完整性级别。

    - 在使用[备选配置](#using-the-scanner-with-alternative-configurations)将默认标签应用于所有文件时，扫描程序可以更快地运行，因为扫描程序不检查文件内容。

    - 如果你使用[替换配置](#using-the-scanner-with-alternative-configurations)标识所有自定义条件和已知敏感信息类型，扫描程序的运行速度会更慢。

    - 您可以使用 [高级客户端设置](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner) 减少扫描程序超时，以获得更好的扫描速率和更低的内存消耗，但有确认可能会跳过某些文件。

## <a name="list-of-cmdlets-for-the-scanner"></a>适用于扫描程序的 cmdlet 列表

利用其他适用于扫描程序的 cmdle，可更改该扫描程序的服务帐户和数据库、获取扫描程序的当前设置，以及卸载扫描程序服务。 扫描程序使用以下 cmdlet：

- Add-AIPScannerScannedFileTypes

- Add-AIPScannerRepository

- Get-AIPScannerConfiguration

- Get-AIPScannerRepository

- Get-AIPScannerStatus

- Install-AIPScanner

- Remove-AIPScannerRepository

- Remove-AIPScannerScannedFileTypes

- Set-AIPScanner

- Set-AIPScannerConfiguration

- Set-AIPScannerScannedFileTypes

- Set-AIPScannerRepository

- Start-AIPScan

- Uninstall-AIPScanner

- Update-AIPScanner

> [!NOTE]
> 目前，当前版本的扫描程序中已不推荐使用其中的许多 cmdlet，扫描程序 cmdlet 的联机帮助将反映此更改。 对于早于 scanner 版本1.48.204.0 的 cmdlet 帮助，请 `Get-Help <cmdlet name>` 在 PowerShell 会话中使用内置命令。

## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>扫描程序的事件日志 ID 和说明

利用以下部分，确定扫描程序可能的事件 ID 和说明。 这些事件记录在扫描程序服务的服务器上、Windows 应用程序和服务事件日志和 Azure 信息保护中。

-----

信息 910

**扫描程序周期已开始。**

当扫描程序服务启动并开始扫描指定数据存储库中的文件时，会记录此事件。

----

信息 911

**扫描程序周期已结束。**

扫描程序完成手动扫描，或完成连续计划的一个周期后，会记录此事件。

如果扫描程序配置为手动运行而不是连续运行，那么若要运行新的扫描，请使用 **Start-AIPScan** cmdlet。 若要更改计划，请使用 **Set-AIPScannerConfiguration** cmdlet 和 Schedule 参数。

----

## <a name="next-steps"></a>后续步骤

想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

您可能想知道： [Windows SERVER FCI 和 Azure 信息保护扫描程序之间的区别是什么？](faqs-classic.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 要详细了解此方案及使用 PowerShell 的其他方案，请参阅[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。