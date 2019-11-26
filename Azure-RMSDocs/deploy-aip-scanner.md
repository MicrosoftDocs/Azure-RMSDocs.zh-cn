---
title: Deploy the Azure Information Protection scanner - AIP
description: Instructions to install, configure, and run the current version of the Azure Information Protection scanner to discover, classify, and protect files on data stores.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0b53c721725f83b8e197552d4c1fa502583fc2f9
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474355"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>部署 Azure 信息保护扫描程序以自动对文件进行分类和保护

>*Applies to: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2*
>
> [!NOTE]
> This article is for the current general availability version of the Azure Information Protection scanner with the Azure Information Protection client (classic), and the preview version of the scanner for the current general availability version of the Azure Information Protection unified labeling client.
> 
> If you have previously installed the scanner and want to upgrade it, use the following upgrade instructions and then use the instructions on this page, omitting the step to install the scanner:
> - For the classic client: [Upgrading the Azure Information Protection scanner](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> - For the unified labeling client: [Upgrading the Azure Information Protection scanner](./rms-client/clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)
> 
> If you have a version of the scanner that is older than 1.48.204.0 and you're not ready to upgrade it, see [Deploying previous versions of the Azure Information Protection scanner to automatically classify and protect files](deploy-aip-scanner-previousversions.md).


利用此信息了解 Azure 信息保护扫描程序，并了解如何成功安装、配置和运行该扫描程序。

此扫描程序在 Windows Server 上作为服务运行，使你能够发现和保护以下数据存储中的文件并对其进行分类：

- 运行扫描程序的 Windows Server 计算机上的本地文件夹。

- 使用服务器消息块 (SMB) 协议的网络共享 UNC 路径。

- Document libraries and folders for SharePoint Server 2019 through SharePoint Server 2013. 对于具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)的客户，还支持 SharePoint 2010。

若要在云存储库上扫描并标记文件，请使用 [Cloud App Security](https://docs.microsoft.com/cloud-app-security/)，而不是扫描程序。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序概述

When you have configured labels that apply automatic classification, files that this scanner discovers can then be labeled. 标签可应用分类，并且可以应用保护或移除保护：

![Azure 信息保护扫描程序体系结构概述](./media/infoprotect-scanner.png)

通过使用计算机上安装的 iFilter，扫描程序可检查 Windows 能编制索引的任何文件。 然后，为了确定是否需要标记文件，扫描程序会使用 Office 365 内置数据丢失防护 (DLP) 敏感信息类型和模式检测，或 Office 365 正则表达式模式。 Because the scanner uses the Azure Information Protection client (the classic client or unified labeling client), the scanner can classify and protect the same file types:

- The classic client: [File types supported by the Azure Information Protection client](./rms-client/client-admin-guide-file-types.md)

- The unified labeling  client: [File types supported by the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-file-types.md)

可仅在发现模式下运行扫描程序，利用报告确认对文件设置标签时会发生什么情况。 或者，可运行扫描程序自动应用标签。 还可以运行扫描程序来发现包含敏感信息类型的文件，无需配置条件标签来应用自动分类。

注意，扫描程序不会实时发现和标记。 它会系统地浏览指定数据存储中的文件，可将此周期配置为运行一次或多次。

可以通过将文件类型列表定义为扫描程序配置的一部分来指定要扫描的文件类型或从扫描中排除的文件类型。


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序的先决条件
安装 Azure 信息保护扫描程序之前，请确保已满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|运行扫描程序服务的 Windows Server 计算机：<br /><br />- 4 核处理器<br /><br />- 8 GB RAM<br /><br />- 临时文件 10GB 可用空间（平均）|Windows Server 2019, Windows Server 2016, or Windows Server 2012 R2. <br /><br />注意：在非生产环境中出于测试或评估目的时，可以使用 [Azure 信息保护客户端支持的](requirements.md#client-devices) Windows 客户端操作系统。<br /><br />此计算机可以是物理或虚拟计算机，需拥有快速可靠的网络，可连接到要进行扫描的数据存储。<br /><br /> 扫描程序需要足够的磁盘空间，才能为其扫描的每个文件（每个核心四个文件）创建临时文件。 借助建议的 10GB 磁盘空间，4 核处理器可以扫描 16 个文件，每个文件的大小为 625MB。 <br /><br /> If internet connectivity is not possible because of your organization policies, see the [Deploying the scanner with alternative configurations](#deploying-the-scanner-with-alternative-configurations) section. Otherwise, make sure that this computer has internet connectivity that allows the following URLs over HTTPS (port 443):<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com <br /> \*.protection.outlook.com (scanner from the unified labeling client only)|
|运行扫描程序服务的服务帐户|除了在 Windows Server 计算机上运行扫描程序服务外，此 Windows 帐户还对 Azure AD 进行身份验证，并下载 Azure 信息保护策略。 此帐户必须是同步到 Azure AD 的 Active Directory 帐户。 如果由于组织策略而无法同步此帐户，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />此服务帐户有以下要求：<br /><br />- 在本地登录的用户权限分配。 此权限是安装和配置扫描程序所必需的，但不可用于操作。 必须将此权限授予服务帐户，但当确认扫描程序可发现、保护文件并对其进行分类后，可删除此权限。 如果由于组织策略的限制而甚至无法在短时间内授予此权限，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />- 作为服务登录的用户权限分配。 扫描程序安装过程中会自动将此权限授予服务帐户，此权限是安装、配置和操作扫描程序所必需的。 <br /><br />- 数据存储库的权限：必须授予“读取”和“写入”权限才可扫描文件，然后将分类和保护应用到满足 Azure 信息保护策略中条件的文件。 若仅在发现模式下运行扫描程序，则只需“读取”权限即可。<br /><br />- For labels that reprotect or remove protection: To ensure that the scanner always has access to protected files, make this account a [super user](configure-super-users.md) for Azure Information Protection, and ensure that the super user feature is enabled. 此外，如果对分阶段部署实现了[载入控件](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，还请确保已配置的载入控件中包含此帐户。|
|存储扫描程序配置的 SQL Server：<br /><br />- 本地或远程实例<br /><br />- [Case insensitive collation](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15) <br /><br />- 安装扫描程序的 Sysadmin 角色|SQL Server 2012 是以下版本的最低版本：<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />指定扫描程序的自定义配置文件名称时，Azure 信息保护扫描程序支持同一 SQL Server 实例上的多个配置数据库。 When you use the preview version of the scanner from the unified labeling client, multiple scanners can share the same configuration database.<br /><br />如果安装扫描程序且帐户拥有 Sysadmin 角色，那么在安装过程中会自动创建扫描程序配置数据库，并向运行扫描程序的服务帐户授予所需的 db_owner 角色。 如果无法获得 Sysadmin 角色或组织策略要求手动创建和配置数据库，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br /> For capacity guidance, see [Storage requirements and capacity planning for SQL Server](#storage-requirements-and-capacity-planning-for-sql-server).|
|Either of the following Azure Information Protection clients is installed on the Windows Server computer <br /><br /> - Classic client <br /><br /> - Unified labeling client ([current general availability version only](./rms-client/unifiedlabelingclient-version-release-history.md#version-25330)) |必须安装扫描程序的完整客户端。 请勿安装只带有 PowerShell 模块的客户端。<br /><br />For installation and upgrade instructions: <br /> - [Classic client](./rms-client/client-admin-guide.md)<br /> - [Unified labeling client](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner) |
|已配置可应用自动分类和保护（可选）的标签|For instructions for the classic client to configure a label for conditions and to apply protection:<br /> - [如何为自动分类和推荐分类配置条件](configure-policy-classification.md)<br /> - [如何配置标签以进行 Rights Management 保护](configure-policy-protection.md) <br /><br />Tip: You can use the instructions from the [tutorial](infoprotect-quick-start-tutorial.md) to test the scanner with a label that looks for credit card numbers in a prepared Word document. 但是，需要更改标签配置，以便将“选择应用此标签的方式”选项设置为“自动”而不是“推荐”。 然后从文档中删除标签（如果已应用），并将文件复制到扫描程序的数据存储库。 为了快速测试，可以使用扫描程序计算机上的本地文件夹。<br /><br /> For instructions for the unified labeling client to configure a label for auto-labeling and to apply protection:<br /> - [Apply a sensitivity label to content automatically](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)<br /> - [Restrict access to content by using encryption in sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)<br /><br /> 尽管即使你尚未配置应用自动分类的标签，仍然可以运行扫描程序，但这些说明中并未涵盖此方案。 [详细信息](#using-the-scanner-with-alternative-configurations)|
|For SharePoint document libraries and folders to be scanned:<br /><br />- SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|扫描程序不支持其他版本的 SharePoint。<br /><br />When you use [versioning](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning), the scanner inspects and labels the last published version. If the scanner labels a file and [content approval](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) is required, that labeled file must be approved to be available for users. <br /><br />对于大型 SharePoint 场，请检查是否需要增加列表视图阈值（默认为 5,000），以便扫描程序访问所有文件。 For more information, see the following SharePoint documentation: [Manage large lists and libraries in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|对于要扫描的 Office 文档：<br /><br />- Word、Excel 和 PowerPoint 的 97-2003 文件格式和 Office Open XML 格式|For more information about the file types that the scanner supports for these file formats, see the following information: <br />- Classic client: [File types supported by the Azure Information Protection client](./rms-client/client-admin-guide-file-types.md)<br />- Unified labeling client: [File types supported by the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-file-types.md)|
|对于长路径：<br /><br />- 最多 260 个字符，除非扫描程序安装在 Windows 2016 上，并且该计算机配置为支持长路径|Windows 10 and Windows Server 2016 support path lengths greater than 260 characters with the following [group policy setting](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/): **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **All Settings** > **Enable Win32 long paths**<br /><br /> 有关支持长文件路径的详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

If you can't meet all the requirements in the table because they are prohibited by your organization policies, see the [alternative configurations](#deploying-the-scanner-with-alternative-configurations) section.

When you deploy the scanner in production, or you're testing the performance for multiple scanners, see the next section for capacity planning guidance for SQL Server.

However, if you're ready to start deploying the scanner, go straight to [configuring the scanner section](#configure-the-scanner-in-the-azure-portal).

### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>Storage requirements and capacity planning for SQL Server

The amount of disk space required for the scanner's configuration database and the specification of the computer running SQL Server can vary for each environment, so we encourage you to do your own testing. However, you can use the following guidance as a starting point.

See the [Optimizing the performance of the scanner](#optimizing-the-performance-of-the-scanner) section for additional information.

##### <a name="scanner-from-the-classic-client"></a>Scanner from the classic client:

- **Disk size**: The size of the configuration database will vary for each deployment but we recommend you allocate 500 MB for every 1,000,000 files that you want to scan.

- **For each scanner**: 4 core processors; 8 GB RAM recommended (4 GB minimum).

##### <a name="scanner-from-the-unified-labeling-client"></a>Scanner from the unified labeling client:

- **Disk size**: Although the size of the scanner configuration database will vary for each deployment, you can use the following equation as guidance: `100 KB + <file count> *(1000 + 4*<average file name length>)`. 
    
    For example, to scan 1 million files that have an average file name length of 250 bytes, allocate 2 GB disk space.

- **For multiple scanners, up to 12**: 4 core processors; 8 GB RAM recommended (4 GB minimum).

- **For multiple scanners more than 12 (maximum 40)** : 8 core processes; 16 GB RAM recommended (8 GB minimum).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>使用备用配置部署扫描程序

表中列出的先决条件是扫描程序的默认要求，之所以建议是因为它们是用于扫描程序部署的最简单配置。 它们应适用于初始测试，以便能够检查扫描程序的功能。 不过，在产品环境中，组织策略可能会禁止这些默认要求，因为存在下列一个或多个限制：

- Servers are not allowed internet connectivity

- 无法获得 Sysadmin 角色，或必须手动创建和配置数据库

- 无法向服务帐户授予“本地登录”权限

- Service accounts cannot be synchronized to Azure Active Directory but servers have internet connectivity

虽然扫描程序可以适应这些限制，但需要其他配置。


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restriction: The scanner server cannot have internet connectivity

Follow the instructions from the admin guides to support a disconnected computer:

- For the classic client: [Support for disconnected computers](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)
    
    In this configuration, the scanner from the classic client cannot apply protection, remove protection, or inspect protected files by using your organization's cloud-based key. Instead, the scanner is limited to using labels that apply classification only, or apply protection that uses [HYOK](configure-adrms-restrictions.md)

- For the unified labeling client: [Support for disconnected computers](./rms-client/clientv2-admin-guide-customizations.md#support-for-disconnected-computers)
    
    In this configuration, the scanner from the unified labeling client can apply protection, remove protection, and inspect protected files by using the *DelegatedUser* parameter with the [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) cmdlet.

然后，执行以下操作：

1. 通过创建扫描程序配置文件在 Azure 门户中配置扫描程序。 如果需要此步骤的帮助，请参阅[在 Azure 门户中配置扫描程序](#configure-the-scanner-in-the-azure-portal)。

2. Export your scanner profile from the **Azure Information Protection - Profiles** pane, by using the **Export** option.

3. 最后，在 PowerShell 会话中运行 [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)，并指定包含导出设置的文件。

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>限制：无法获得 Sysadmin 角色，或必须手动创建和配置数据库

如果可以获得 Sysadmin 角色来安装扫描程序，就能在扫描程序安装完成后删除此角色。 使用此配置时，数据库会自动创建，而且扫描程序的服务帐户也会自动获得相应权限。 不过，配置扫描程序的用户帐户需要拥有扫描程序配置数据库的 db_owner 角色，你必须手动向用户帐户授予此角色。

If you cannot be granted the Sysadmin role even temporarily, you must ask a user with Sysadmin rights to manually create a database before you install the scanner. For this configuration, the following roles must be assigned:
    
|帐户|数据库级角色|
|--------------------------------|---------------------|
|扫描程序的服务帐户|db_owner|
|用于安装扫描程序的用户帐户|db_owner|
|用于配置扫描程序的用户帐户 |db_owner|

用于安装和配置扫描程序的用户帐户通常是相同的。 不过，如果使用不同的帐户，它们都需要拥有扫描程序配置数据库的 db_owner 角色：

- If you do not specify your own profile name for the scanner (classic client only), the configuration database is named **AIPScanner_\<computer_name>** . 

- If you specify your own profile name, the configuration database is named **AIPScanner_\<profile_name>** (classic client) or **AIPScannerUL_\<profile_name>** (unified labeling client).

To create a user and grant db_owner rights on this database, ask the Sysadmin to run the following SQL script twice. The first time, for the service account that runs the scanner, and the second time for you to install and manage the scanner. Before running the script:
1. Replace *domain\user* with the domain name and user account name of the service account or user account.
2. Replace *DBName* with the name of the scanner configuration database.

SQL script:

    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END

另外：

- You must be a local administrator on the server that will run the scanner
- The service account that will run the scanner must be granted Full Control permissions to the following registry keys:
    
    - HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server

If, after configuring these permissions, you see an error when you install the scanner, the error can be ignored and you can manually start the scanner service.


#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>限制：无法向扫描程序的服务帐户授予“本地登录”权限

If your organization policies prohibit the **Log on locally** right for service accounts but allow the **Log on as a batch job** right, use the following instructions:

- For the classic client: See [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.

- For the unified labeling client: Use the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) in that client's admin guide.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restriction: The scanner service account cannot be synchronized to Azure Active Directory but the server has internet connectivity

可以使用一个帐户来运行扫描程序服务，并使用另一个帐户对 Azure Active Directory 进行身份验证：

- 对于扫描程序服务帐户，可以使用本地 Windows 帐户或 Active Directory 帐户。

- For the Azure Active Directory account, use the following instructions:
    - For the classic client: See [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.
    - For the unified labeling client: Specify your local account for the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) in that client's admin guide.


## <a name="configure-the-scanner-in-the-azure-portal"></a>在 Azure 门户中配置扫描程序

Before you install the scanner, or upgrade it from an older general availability version of the scanner, create a profile for the scanner in the Azure portal. 可以配置扫描程序设置的配置文件以及要扫描的数据存储库。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”窗格。 
    
    For example, in the search box for resources, services, and docs: Start typing **Information** and select **Azure Information Protection**.
    
2. 找到“扫描程序”菜单选项，然后选择“配置文件”。

3. 在“Azure 信息保护 - 配置文件”窗格上，选择“添加”：
    
    ![添加 Azure 信息保护扫描程序的配置文件](./media/scanner-add-profile.png)

4. 在“添加新配置文件”窗格上，指定扫描程序的名称，该名称用于标识扫描程序的配置设置和要扫描的数据存储库。 例如，可以指定“欧洲”来标识扫描程序将涵盖的数据存储库的地理位置。 以后安装或升级扫描程序时，将需要指定相同的配置文件名称。
    
    （可选）指定用于管理的说明，以帮助识别扫描程序的配置文件名称。

5. For this initial configuration, configure the following settings, and then select **Save** but do not close the pane:
    
    For the **Profile settings** section:
    - **Schedule**: Keep the default of **Manual**
    - **Info types to be discovered**: Change to **Policy only**
    - **Configure repositories**: Do not configure at this time because the profile must first be saved.
    
    For the **Policy enforcement** section:
    - **Enforce**: Select **Off**
    - **Label files based on content**: Keep the default of **On**
    - **Default label**: Keep the default of **Policy default**
    - **Relabel files**: Keep the default of **Off**
    
    For the **Configure file settings** section:
    - **Preserve "Date modified", "Last modified" and "Modified by"** : Keep the default of **On**
    - **File types to scan**: Keep the default file types for **Exclude**
    - **Default owner**: Keep the default of **Scanner Account**

6. 现在已创建并保存配置文件，即可返回到“配置存储库”选项以指定要扫描的数据存储。 You can specify local folders, UNC paths, and SharePoint Server URLs for SharePoint on-premises document libraries and folders. 
    
    SharePoint Server 2019, SharePoint Server 2016, and SharePoint Server 2013 are supported for SharePoint. 具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)时，还支持 SharePoint Server 2010。
    
    To add your first data store, still on the **Add a new profile** pane, select **Configure repositories** to open the **Repositories** pane:
    
    ![为 Azure 信息保护扫描程序配置数据存储库](./media/scanner-repositories-bar.png)

7. 在“存储库”窗格上，选择“添加”：
    
    ![为 Azure 信息保护扫描程序添加数据存储库](./media/scanner-repository-add.png)

8. On the **Repository** pane, specify the path for the data repository. 
    
    不支持通配符，也不支持 WebDav 位置。
    
    例如：
    
    - 对于本地路径：`C:\Folder`
    
    - 对于网络共享：`C:\Folder\Filename`
    
    - 对于 UNC 路径：`\\Server\Folder`
    
    - 对于 SharePoint 库：`http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > 如果为“共享文档”添加 SharePoint 路径：
    >
     >- 如果要从“共享文档”扫描所有文档和所有文件夹，请在路径中指定“共享文档”。 例如：`http://sp2013/Shared Documents`
     >
     >- 如果要从“共享文档”下的子文件夹扫描所有文档和所有文件夹，请在路径中指定“文档”。 例如：`http://sp2013/Documents/Sales Reports`
    
    For the remaining settings on this pane, do not change them for this initial configuration, but keep them as **Profile default**. 这意味着数据存储库从扫描程序配置文件继承设置。 
    
    选择“保存”。

9. 如果要添加其他数据存储库，请重复步骤 7 和 8。

10. You can now close **Repositories** pane and your profile pane. Back on the **Azure Information Protection - Profiles** pane, you see your profile name displayed, together with the **SCHEDULE** column showing **Manual** and the **ENFORCE** column is blank.

现在可随时使用刚刚创建的扫描程序配置文件安装扫描程序。

## <a name="install-the-scanner"></a>安装扫描程序

1. 登录到将要运行扫描程序的 Windows Server 计算机。 使用具有本地管理员权限并具有写入到 SQL Server master 数据库权限的帐户。

2. 使用“以管理员身份运行”选项打开 Windows PowerShell 会话。

3. 运行 [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) cmdlet，指定要在其中为 Azure 信息保护扫描程序创建数据库的 SQL Server 实例，以及在上一部分中指定的扫描程序配置文件名称： 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <profile name>
    ```
    
    例如，使用配置文件名称“欧洲”：
    
    - 对于默认实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    - 对于命名实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    - 对于 SQL Server Express：`Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    系统提示时，请提供扫描程序服务帐户的凭据 (\<域\用户名>) 和密码。

4. 使用“管理工具” > “服务”验证服务现在是否已安装。 
    
    已安装的服务被命名为 Azure信息保护扫描程序，并被配置为使用你创建的扫描程序服务帐户运行。

现已安装扫描程序，需获取 Azure AD 令牌以便扫描程序服务帐户进行身份验证，从而扫描程序可以无人参与的方式运行。 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>获取扫描程序的 Azure AD 令牌

The Azure AD token lets the scanner authenticate to the Azure Information Protection service.

1. Return to the Azure portal to create two Azure AD applications (just one Azure AD application for the scanner from the unified labeling client) that are needed to specify an access token for authentication. This token lets the scanner run non-interactively.
    
    To create these applications, follow the instructions in the admin guides for the relevant clients:
    
    - For the classic client: [How to label files non-interactively for Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)
    
    - For the unified labeling client: [How to label files non-interactively for Azure Information Protection](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

2. 在 Windows Server 计算机中，如果你的扫描程序服务帐户已就安装授予了“本地登录”权限：使用此帐户登录并启动 PowerShell 会话。 运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)，指定从上一步骤中复制的值：
    
    **For the classic client:**
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    系统提示时，请为 Azure AD 的服务帐户凭据指定密码，然后单击“接受”。
    
    If your scanner service account cannot be granted the **Log on locally** right for the installation see [Specify and use the Token parameter for Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) from that client's admin guide.
    
    **For the unified labeling client:**
    
    ```
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
    
    If your scanner service account cannot be granted the **Log on locally** right for the installation, use the *OnBehalfOf* parameter with Set-AIPAuthentication, as described in [How to label files non-interactively for Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) from that client's admin guide.

The scanner now has a token to authenticate to Azure AD, which is valid for one year, two years, or never expires, according to your configuration of the **Web app /API** (classic client) or client secret (unified labeling client) in Azure AD. 如果令牌过期，则须重复步骤 1 和步骤 2。

现在可随时在发现模式下运行第一次扫描。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>运行发现周期并查看扫描程序报告

1. In the Azure portal, on the **Azure Information Protection - Profiles** pane, select your scanner's profile, and then the **Scan now** option:
    
    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)
    
    或者，在 PowerShell 会话中，运行以下命令：
    
        Start-AIPScan

2. 等待扫描程序完成其周期。 当扫描程序浏览完指定数据存储中的所有文件时，扫描程序停止（尽管扫描程序服务仍在运行）：
    
    - On the **Azure Information Protection - Profiles** pane, use the **Refresh** option and wait until you see values for the **LAST SCAN RESULTS** column and the **LAST SCAN (END TIME)** column.
    
    - 使用 PowerShell，你可以运行 `Get-AIPScannerStatus` 来监视状态更改。
    
    - Scanner from the classic client only: Check the local Windows **Applications and Services** event log, **Azure Information Protection**. 另外，此日志还会报告扫描程序完成扫描的时间，以及结果摘要。 请查看信息事件 ID 911。

3. 查看存储在 %localappdata%\Microsoft\MSIP\Scanner\Reports 中的报表。 .txt 摘要文件包括扫描所用的时间、扫描的文件数以及匹配信息类型的文件数量。 .csv 文件包含每个文件的更多详细信息。 此文件夹为每个扫描周期最多存储 60 个报表，并且压缩除最新报表之外的所有报表，以帮助最大程度地减少所需的磁盘空间。
    
    > [!NOTE]
    > 可以将ReportLevel 参数和 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) 结合使用来更改日志记录级别，但不能更改报表文件夹位置或名称。 如果要将报表存储在其他卷或分区上，请考虑使用该文件夹的目录交叉点。
    >
    > 例如，使用 [Mklink](/windows-server/administration/windows-commands/mklink) 命令：`mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    使用“要发现的信息类型”的“仅限策略”的设置时，只有满足你为自动分类配置的条件的文件才会被包括在详细报表中。 如果看不到任何应用的标签，请检查标签配置是否包括自动分类而不是推荐分类。
    
    > [!TIP]
    > 扫描程序会每 5 分钟向 Azure 信息保护发送一次此信息，这样你就可以准实时地在 Azure 门户中查看结果。 有关详细信息，请参阅 [Azure 信息保护报表](reports-aip.md)。 
        
    If the results are not as you expect, you might need to reconfigure the conditions that you specified for you labels. 如果是这种情况，请重复步骤 1 到 3，直到可更改配置以应用分类和保护（可选）。 

Azure 门户仅显示有关上次扫描的信息。 如果需要查看先前扫描的结果，请返回到扫描程序计算机上存储的报表，它位于 %localappdata%\Microsoft\MSIP\Scanner\Reports 文件夹中。

如果已准备好对扫描程序发现的文件进行自动标记，请继续下一步。 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>将扫描程序配置为应用分类和保护

如果按照这些说明操作，扫描程序在仅报告模式下运行一次。 若要更改这些设置，请编辑扫描程序配置文件：

1. Back on the **Azure Information Protection - Profiles** pane, select the scanner profile to edit it.

2. On the \<**profile name**> pane, change the following two settings, and then select **Save**:
    
   - From the **Profile settings** section: Change the **Schedule** to **Always**
   - From the **Policy enforcement** section: Change **Enforce** to **On**
    
     你可能还希望更改其他配置设置。 例如，文件属性是否更改，以及扫描程序是否可以重新标记文件。 使用信息弹出通知帮助了解有关每个配置设置的详细信息。

3. Make a note of the current time and start the scanner again from the **Azure Information Protection - Profiles** pane:
    
    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)
    
    或者，可以在 PowerShell 会话中运行以下命令：
    
        Start-AIPScan

4. Scanner from the classic client only: Monitor the event log for the informational type **911** again, with a time stamp later than when you started the scan in the previous step.
    
    然后查看报告，详细了解标记了哪些文件、向每个文件应用了什么分类，以及是否向它们应用了保护。 或者，使用 Azure 门户，更轻松地了解此信息。

因为我们将计划配置为持续运行，所以当扫描程序扫描完所有文件时，它将自动开始一个新周期，以便发现任何新文件和更改的文件。

## <a name="how-files-are-scanned"></a>如何扫描文件

扫描程序在扫描文件时运行以下过程。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. Determine whether files are included or excluded for scanning 
The scanner automatically skips files that are excluded from classification and protection, such as executable files and system files. For more information, see the following admin guides:

- For the classic client: [File types that are excluded from classification and protection](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- For the unified labeling client: [File types that are excluded from classification and protection](./rms-client/clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

可以定义要扫描或不要扫描的文件类型列表，从而更改此行为。 默认情况下，可以为扫描程序指定此列表以应用于所有数据存储库，并且可以为每个数据存储库指定一个列表。 若要指定此列表，请使用扫描程序配置文件中的“要扫描的文件类型”设置：

![配置 Azure 信息保护扫描程序要扫描的文件类型](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2. Inspect and label files

然后，扫描程序使用筛选器来扫描支持的文件类型。 操作系统也可使用这些筛选器来进行 Windows 搜索和索引编制。 无需任何额外配置，即可使用 Windows IFilter 来扫描 Word、Excel、PowerPoint 使用文件类型，以及用于 PDF 文档和文本文件的文件类型。

For a full list of file types that are supported by default, and additional information how to configure existing filters that include .zip files and .tiff files, see the following admin guides:

- For the classic client: [File types supported for inspection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)
- For the unified labeling client: [File types supported for inspection](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection)

检查之后，可以使用为标签指定的条件为这些文件类型设置标签。 或者，如果要使用发现模式，可以报告这些文件，在其中包含为标签指定的条件，或所有已知敏感信息类型。 

但在以下情况下，扫描程序无法为文件设置标签：

- If the label applies classification and not protection, and the file type does not support classification only by the [classic client](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) or [unified labeling client](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- 如果标签应用分类和保护，但扫描程序不保护该文件类型。
    
    默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。 Other file types can be protected when you [change which file types are protected](#change-which-file-types-to-protect) as described in a following section.

例如，检查文件扩展名为 .txt 的文件之后，扫描程序无法应用为分类而非保护配置的标签，因为 .txt 文件类型不支持仅分类。 If the label is configured for classification and protection, and the .txt file name extension is included for the scanner to protect, the scanner can label the file. 

> [!TIP]
> 在此过程中，如果扫描程序停止并且未完成对存储库中大量文件的扫描：
> 
> - 可能需要增加托管文件的操作系统的动态端口数。 SharePoint 的服务器强化可能是导致扫描程序超出允许的网络连接数并因此停止的一个原因。
>     
>     To check whether this is the cause of the scanner stopping, look to see if the following error message is logged for the scanner in %*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog (zipped if there are multiple logs): **Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port**
>    
>     有关如何查看当前端口范围以及增加该范围的详细信息，请参阅[可通过修改设置来提高网络性能](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)。
> 
> - 对于大型 SharePoint 场，可能需要增加列表视图阈值（默认情况下为 5,000）。 For more information, see the following SharePoint documentation: [Manage large lists and libraries in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

### <a name="3-label-files-that-cant-be-inspected"></a>3. Label files that can't be inspected
对于无法检查的文件类型，扫描程序应用 Azure 信息保护策略中的默认标签或为扫描程序配置的默认标签。

与上述步骤相同，在下列情况下，扫描程序无法为文件设置标签：

- If the label applies classification and not protection, and the file type does not support classification only by the [classic client](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only) or [unified labeling client](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- 如果标签应用分类和保护，但扫描程序不保护该文件类型。
    
    默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。 Other file types can be protected when you change which file types to protect, as described next.

## <a name="change-which-file-types-to-protect"></a>Change which file types to protect

By default, the scanner protects Office file types and PDF files only. You can change this behavior so that for example, the scanner protects all file types, which is the same protection behavior as the client. Or, the scanner protects additional file types that you specify, in addition to Office file types and PDF files. 

For configuration instructions, see the following sections.

### <a name="scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected"></a>Scanner from the classic client: Use the registry to change which file types are protected

This section applies to the scanner from the classic client only.

To change the default scanner behavior for protecting file types other than Office files and PDFs, you must edit the registry and specify the additional file types that you want to be protected, and the type of protection (native or generic). 有关说明，请参阅开发人员指南中的[文件 API 配置](develop/file-api-configuration.md)。 对于本文档中的开发人员，常规保护被称为“PFile”。 此外，特定于扫描程序：

- The scanner has its own default behavior: Only Office file formats and PDF documents are protected by default. 如果未修改注册表，则扫描程序不会保护任何其他文件类型或为其设置标签。

- If you want the same default protection behavior as the Azure Information Protection client, where all files are automatically protected with native or generic protection: Specify the `*` wildcard as a registry key, `Encryption` as the value (REG_SZ), and `Default` as the value data.

编辑注册表时，如果 MSIPC 密钥和 FileProtection 密钥不存在，则手动创建这些密钥，并创建每个文件扩展名的密钥。

例如，除了 Office 文件和 PDF 之外，若要使扫描程序还保护 TIFF 图像，编辑后的注册表将与下图类似。 作为图像文件，TIFF 文件支持本机保护，且生成的文件扩展名为 .ptiff。

![编辑扫描程序的注册表以应用保护](./media/editregistry-scanner.png)

For a list of text and images file types that similarly support native protection but must be specified in the registry, see [Supported file types for classification and protection](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection).

对于不支持本机保护的文件，请将文件扩展名指定为新密钥，并为 PFile 获取常规保护。 对于受保护的文件，生成的文件扩展名为 .pfile。

### <a name="scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected"></a>Scanner from the unified labeling client: Use PowerShell to change which file types are protected

This section applies to the scanner from the unified labeling client only.

For a label policy that applies to the user account downloading labels for the scanner, specify a PowerShell advanced setting named **PFileSupportedExtensions**. 

> [!NOTE]
> For a scanner that has access to the internet, this user account is the account that you specify for the *DelegatedUser* parameter with the Set-AIPAuthentication command.

Example 1:  PowerShell command for the scanner to protect all file types, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

Example 2: PowerShell command for the scanner to protect .xml files and .tiff files in addition to Office files and PDF files, where your label policy is named "Scanner":

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}

For detailed instructions, see [Change which file types to protect](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) from the admin guide.


## <a name="when-files-are-rescanned"></a>重新扫描文件时的情况

在第一个扫描周期，扫描程序会检查所配置的数据存储中的所有文件，然后在后续扫描中仅检查新文件或修改后的文件。 

You can force the scanner to inspect all files again from the **Azure Information Protection - Profiles** pane in the Azure portal. Select your scanner profile from the list, and then select the **Rescan all files** option:

![启动 Azure 信息保护扫描程序重新扫描](./media/scanner-rescan-files2.png)

如果希望报告包含所有文件，再次检查所有文件非常有用；且当扫描程序在发现模式下运行时，通常会使用此配置选项。 完成全部扫描后，扫描类型自动更改为“增量”，以便后续扫描仅扫描新文件或修改后的文件。

In addition, all files are inspected when the scanner from the classic client downloads an Azure Information Protection policy that has new or changed conditions and the scanner from the unified labeling client has new or changed settings for automatic and recommended labeling. 

The scanner refreshes the policy according to the following triggers:

- Scanner from the classic client: Every hour and when the service starts and the policy is older than one hour. 

- Scanner from the unified labeling client: Every four hours. 

> [!TIP]
> If you need to refresh the policy sooner than the default interval, for example, during a testing period: 
>
> - Scanner from the classic client: Manually delete the policy file, **Policy.msip** from **%LocalAppData%\Microsoft\MSIP\Policy.msip**.
>
> - Scanner from the unified labeling client: Manually delete the contents from **%LocalAppData%\Microsoft\MSIP\mip\\<*processname*>\mip**.
>
然后重新启动 Azure 信息扫描程序服务。 If you changed protection settings for your labels, also wait 15 minutes from when you saved the protection settings before you restart the service.


## <a name="editing-in-bulk-for-the-data-repository-settings"></a>批量编辑数据存储库设置

对于已添加到扫描程序配置文件的数据存储库，可以使用“导出”和“导入”选项快速更改设置。 例如，对于 SharePoint 数据存储库，你希望添加要从扫描中排除的新文件类型。

Instead of editing each data repository in the Azure portal, use the **Export** option from the **Repositories** pane:

![导出扫描程序的数据存储库设置](./media/export-scanner-repositories.png)

Manually edit the file to make the change, and then use the **Import** option on the same pane.

## <a name="using-the-scanner-with-alternative-configurations"></a>使用具有备选配置的扫描程序

There are three alternative scenarios that the Azure Information Protection scanner supports where labels do not need to be configured for any conditions: 

- 将默认标签应用于数据存储库中的所有文件。
    
    For this configuration, set **Label files based on content** to **Off**. Then set the **Default label** to **Custom**, and select the label to use.
    
    The contents of the files are not inspected and all unlabeled files in the data repository are labeled according to the default label that you specify for the data repository or the scanner profile. 
    
    For the scanner from the unified labeling client, you can also select **Enforce default label** if you want the default label to be applied on all files, even if they are already labeled.
    

- Remove existing labels from all files in a data repository.
    
    Applicable to the scanner from the unified labeling client only, this configuration lets you remove existing labels, which includes protection if it was applied with that label. Protection that was applied independently from a label is retained. Use this configuration if you need to remove all labels from files in a repository.
    
    配置下列设置：
    - **Label files based on content**: **Off**
    - **Default label**: **None**
    - **Relabel files**: **On** with the **Enforce default label** checkbox selected

- 标识所有自定义条件和已知敏感信息类型。
    
    对于此配置，请将“要发现的信息类型”设置为“全部”。
    
    For the scanner from the classic client: The scanner uses any custom conditions that you have specified for labels in the Azure Information Protection policy, and the list of information types that are available to specify for labels in the Azure Information Protection policy. 
    
    For the scanner from the unified labeling client: The scanner uses any custom sensitive info types that you have specified and the list of built-in sensitive info types that are available to select in your labeling management center.
    
    此设置有助于查找你可能没有意识到的敏感信息，但会降低扫描程序的扫描速率。
    
    The following quickstart for the scanner uses this configuration: [Quickstart: Find what sensitive information you have](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>优化扫描程序性能

使用以下指南有助于优化扫描程序的性能。 However, if your priority is the responsiveness of the scanner computer rather than the scanner performance, you can use an advanced client setting to limit the number of threads used by the scanner:

- Scanner from the classic client: [Limit the number of threads used by the scanner](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)

- Scanner from the unified labeling client: [Limit the number of threads used by the scanner](./rms-client/clientv2-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)

若要最大程度实现扫描程序的性能：

- **在扫描程序计算机和被扫描的数据存储之间建立高速可靠的网络连接**
    
    例如，将扫描程序计算机置于所扫描的数据存储所在的 LAN 或（首选）网络段中。
    
    网络连接的质量会影响扫描程序的性能，因为要检查文件，扫描程序需将文件内容传输到运行扫描程序服务的计算机中。 如果减少（或消除）此数据需传输的网络跃点数，网络上的负载随之减少。 

- **确保扫描程序计算机具有可用的处理器资源**
    
    检查文件内容以及进行文件加密和解密是处理器密集型操作。 请监视所指定的数据存储的典型扫描周期，以确定缺少处理器资源是否对扫描程序性能造成负面影响。
    
- **不扫描运行扫描程序服务的计算机上的本地文件夹**
    
    如果 Windows 服务器上具有要扫描的文件夹，请在其他计算机上安装扫描程序，并将这些文件夹配置为要扫描的网络共享。 将承载文件和扫描文件这两大功能分开，这意味着这些服务的计算资源不相互竞争。

如有必要，请安装扫描程序的多个实例。 指定扫描程序的自定义配置文件名称时，Azure 信息保护扫描程序支持同一 SQL Server 实例上的多个配置数据库。 For the scanner from the unified labeling client, multiple scanners can share the same profile, which results in quicker scanning times.

影响扫描程序性能的其他因素：

- 包含要扫描的文件的数据存储的当前负载和响应时间

- 扫描程序是在发现模式还是强制模式下运行
    
    通常，发现模式的扫描速率比强制模式的高，因为发现操作需要单一文件读取操作，而强制模式需要读取和写入操作。

- You change the conditions in the Azure Information Protection policy (classic client) or auto-labeling in the label policy (unified labeling client)
    
    在第一个扫描周期，扫描程序必须检查每个文件，而后续扫描周期默认仅检查新文件和更改的文件，因此第一个周期比后续周期耗时长。 However, if you change the conditions or auto-labeling settings, all files are scanned again, as described in the [preceding section](#when-files-are-rescanned).

- 自定义条件的正则表达式构造
    
    为避免占用过多内存并存在超时风险（每个文件 15 分钟），请查看正则表达式了解有效的模式匹配。 例如：
    
    - 避免[贪婪限定符](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)
    
    - 使用 `(?:expression)` 等非捕获组，而不是 `(expression)`

- 所选的日志记录级别
    
    可对扫描程序报告选择“调试”、“信息”、“错误”或“关闭”。 “关闭”可使性能最佳；“调试”会明显减低扫描程序的速度，应仅用于故障排除。 有关详细信息，请参阅 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet 的 eportLevel 参数。

- 文件自身：
    
    - With the exception of Excel files, Office files are more quickly scanned than PDF files.
    
    - 扫描未受保护的文件比扫描受保护的文件耗时更短。
    
    - 扫描大型文件明显比扫描小文件耗时更多。

- 另外：
    
    - Confirm that the service account that runs the scanner has only the rights documented in the [scanner prerequisites](#prerequisites-for-the-azure-information-protection-scanner) section, and then configure the [advanced client setting](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) to disable the low integrity level for the scanner (classic client only).
    
    - 在使用[备选配置](#using-the-scanner-with-alternative-configurations)将默认标签应用于所有文件时，扫描程序可以更快地运行，因为扫描程序不检查文件内容。
    
    - 如果你使用[替换配置](#using-the-scanner-with-alternative-configurations)标识所有自定义条件和已知敏感信息类型，扫描程序的运行速度会更慢。
    
    - You can decrease the scanner timeouts (classic client only) with [advanced client settings](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner) for better scanning rates and lower memory consumption, but with the acknowledgment that some files might be skipped.

## <a name="list-of-cmdlets-for-the-scanner"></a>适用于扫描程序的 cmdlet 列表

由于现在从 Azure 门户配置扫描程序，因此现已弃用配置的数据存储库的先前版本的 cmdlet 和扫描的文件类型列表。 

保留的 cmdlet 包括用于安装和升级扫描程序、更改扫描程序配置数据库和配置文件、更改本地报告级别以及导入已断开连接的计算机的配置设置的 cmdlet。 

The full list of cmdlets for the scanner: 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Export-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs) - unified labeling client only

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>扫描程序的事件日志 ID 和说明

利用以下部分，确定扫描程序可能的事件 ID 和说明。 这些事件记录在扫描程序服务的服务器上、Windows 应用程序和服务事件日志和 Azure 信息保护中。

> [!NOTE]
> This section applies to the scanner from the classic client only. Currently, the scanner from the unified labeling client doesn't write information to the event log.

-----

信息 910

**扫描程序周期已开始。**

当扫描程序服务启动并开始扫描指定数据存储库中的文件时，会记录此事件。

----

信息 911

**扫描程序周期已结束。**

扫描程序完成手动扫描，或完成连续计划的一个周期后，会记录此事件。

如果扫描程序配置为手动运行（而不是连续运行），要再次扫描文件，请在扫描程序配置文件中将“计划”设置为“手动”或“始终”，然后重启服务。

----

## <a name="next-steps"></a>后续步骤

想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

你可能想知道：[Windows Server FCI 和 Azure 信息保护扫描程序有何区别？](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 For more information about this and other scenarios that use PowerShell, see the following sections from the admin guides:

- For the classic client: [Using PowerShell with the Azure Information Protection client](./rms-client/client-admin-guide-powershell.md)

- For the unified labeling client: [Using PowerShell with the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-powershell.md)
