---
title: Azure 信息保护 (AIP) 经典扫描器必备组件
description: 列出安装和部署 Azure 信息保护经典扫描器的先决条件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4c466fbbad6314a6b0ea0dddb85d07d359a42467
ms.sourcegitcommit: 72694afc0e74fd51662e40db2844cdb322632428
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2020
ms.locfileid: "95566529"
---
# <a name="prerequisites-for-installing-and-deploying-the-azure-information-protection-classic-scanner"></a>安装和部署 Azure 信息保护经典扫描器的先决条件

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。 
> 
> 如果使用的是统一标签扫描程序，请参阅 [安装和部署 Azure 信息保护统一标签扫描器的先决条件](deploy-aip-scanner-prereqs.md)。

在安装 Azure 信息保护本地扫描器之前，请确保你的系统符合基本的 [Azure 信息保护要求](requirements.md)，以及特定于扫描程序的以下要求：

- [Windows Server 要求](#windows-server-requirements)
- [服务帐户要求](#service-account-requirements)
- [SQL server 要求](#sql-server-requirements)
- [Azure 信息保护客户端要求](#azure-information-protection-client-requirements)
- [标签配置要求](#label-configuration-requirements)
- [SharePoint 要求](#sharepoint-requirements)
- [Microsoft Office 要求](#microsoft-office-requirements)
- [文件路径要求](#file-path-requirements)
- [使用情况统计信息要求](#usage-statistics-requirements)

如果你无法满足表中的所有要求，因为你的组织策略禁止这些要求，请参阅 [备选配置](#deploying-the-scanner-with-alternative-configurations) 部分。

在生产中部署扫描仪或测试多个扫描仪的性能时，请参阅 [SQL Server 的存储要求和容量规划](#storage-requirements-and-capacity-planning-for-sql-server)。

准备好开始安装和部署扫描程序时，请继续 [部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner-configure-install-classic.md)。

## <a name="windows-server-requirements"></a>Windows Server 要求

你必须有一台运行扫描程序的 Windows Server 计算机，该计算机具有以下系统规范：

|规范  |详细信息  |
|---------|---------|
|**处理器**     |4核处理器         |
|**RAM**     |8 GB         |
|**磁盘空间**     |10 GB 可用空间 (临时文件的平均) 。 </br></br>扫描程序需要足够的磁盘空间，才能为其扫描的每个文件（每个核心四个文件）创建临时文件。 </br></br>借助建议的 10GB 磁盘空间，4 核处理器可以扫描 16 个文件，每个文件的大小为 625MB。 
|**操作系统**     |-Windows Server 2019 </br>- Windows Server 2016 </br>- Windows Server 2012 R2 </br></br>**注意：** 对于非生产环境中的测试或评估目的，还可以使用 [Azure 信息保护客户端支持](requirements.md#client-devices)的任何 Windows 操作系统。
|**网络连接**     | 扫描仪计算机可以是物理计算机或虚拟计算机，与要扫描的数据存储进行快速可靠的网络连接。 </br></br> 如果由于组织策略而无法建立 internet 连接，请参阅 [用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。 </br></br>否则，请确保此计算机具有 internet 连接，允许通过 HTTPS (端口 443) 的以下 Url：</br><br />-  \*。 aadrm.com <br />-  \*。 azurerms.com<br />-  \*。 informationprotection.azure.com <br /> -informationprotection.hosting.portal.azure.net <br /> - \*。 aria.microsoft.com|
| ||

## <a name="service-account-requirements"></a>服务帐户要求

您必须具有服务帐户才能在 Windows Server 计算机上运行 scanner 服务，并可 Azure AD 和下载 Azure 信息保护策略。

你的服务帐户必须是 Active Directory 帐户，并同步到 Azure AD。

如果由于组织策略而无法同步此帐户，请参阅 [用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。

此服务帐户有以下要求：

|要求  |详细信息  |
|---------|---------|
|**本地登录** 用户权限分配     |需要安装和配置扫描程序，但不需要运行扫描。  </br></br>确认扫描程序可以发现、分类和保护文件后，可以从服务帐户中删除此权限。  </br></br>如果由于组织策略的原因而无法在短时间内授予此权限，请参阅 [使用替代配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。         |
|作为服务登录的用户权限分配。     |  扫描程序安装过程中会自动将此权限授予服务帐户，此权限是安装、配置和操作扫描程序所必需的。        |
|**数据存储库的权限**     |- **文件共享或本地文件：** 授予 " **读取**"、" **写入**" 和 " **修改** " 权限以扫描文件，然后按配置应用 "分类和保护"。  <br /><br />- **SharePoint：** 授予 " **完全控制** " 权限以扫描文件，然后按配置应用 "分类和保护"。  <br /><br />- **发现模式：** 若要仅在发现模式下运行扫描程序， **读取** 权限就足够了。         |
|**对于重新保护或删除保护的标签**     | 若要确保扫描程序始终可以访问受保护的文件，请将此帐户设置为 Azure 信息保护的 [超级用户](configure-super-users.md) ，并确保已启用超级用户功能。 </br></br>此外，如果已为分阶段部署实现了 [载入控件](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) ，请确保已配置的载入控件中包含该服务帐户。|
| ||

## <a name="sql-server-requirements"></a>SQL server 要求

若要存储扫描程序配置数据，请使用具有以下要求的 SQL server：

- **本地或远程实例。**

    建议在不同的计算机上托管 SQL server 和 scanner 服务，除非使用的是小型部署。 此外，我们建议使用仅为扫描程序数据库提供服务且不与其他应用程序共享的专用 SQL 实例。

    如果正在使用共享服务器，请确保建议使用的 [核心数](#windows-server-requirements) 可供扫描程序数据库使用。

    SQL Server 2012 是以下版本的最低版本：

    - SQL Server Enterprise
    - SQL Server Standard
    - 仅建议 SQL Server Express (用于测试环境) 

- **具有安装扫描程序的 Sysadmin 角色的帐户。**

    这使安装过程能够自动创建扫描程序配置数据库并向运行该扫描程序的服务帐户授予所需的 **db_owner** 角色。 

    如果无法授予 Sysadmin 角色或组织策略需要手动创建和配置数据库，请参阅 [用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。

- **容量。** 有关容量指导，请参阅 [SQL Server 的存储要求和容量规划](#storage-requirements-and-capacity-planning-for-sql-server)。

- **[不区分大小写排序规则](/sql/relational-databases/collations/collation-and-unicode-support)**

> [!NOTE]
> 为扫描程序指定自定义群集 (配置文件) 名称时，支持同一 SQL server 上的多个配置数据库。
> 

### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>SQL Server 的存储要求和容量规划

扫描程序配置数据库所需的磁盘空间量以及运行 SQL Server 的计算机的规范可能因每个环境而异，因此，我们鼓励你进行自己的测试。 使用以下指导作为起点。

有关详细信息，请参阅 [优化扫描程序的性能](deploy-aip-scanner-configure-install-classic.md#optimizing-scanner-performance)。

对于每个部署，配置数据库的磁盘大小将有所不同。 建议为要扫描的每个1000000文件分配 500 MB。 

对于每个扫描仪，使用：

- 4核处理器
- 8 GB RAM (最少 4 GB) 

## <a name="azure-information-protection-client-requirements"></a>Azure 信息保护客户端要求

你必须在 Windows Server 计算机上安装 Azure 信息保护客户端。

有关详细信息，请参阅 [经典客户端管理员指南](./rms-client/client-admin-guide.md)。

> [!IMPORTANT]
> 必须安装扫描程序的完整客户端。 请勿安装只带有 PowerShell 模块的客户端。
> 

## <a name="label-configuration-requirements"></a>标签配置要求

您必须将标签配置为自动应用分类和保护（可选）。

如果未配置这些标签，请参阅 [使用替代配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。

有关详细信息，请参阅：

- [如何为自动和建议分类配置条件](configure-policy-classification.md)
- [如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)

> [!TIP] 
> 使用 [教程](infoprotect-quick-start-tutorial.md) 中的说明，使用一个在已准备好的 Word 文档中查找信用卡号的标签来测试扫描仪。 但是，你将需要更改标签配置，以使选项 " **选择如何应用此标签** " 设置为 " **自动**"，而不是 " **建议** " 或 "将 **建议标记视为自动** (在扫描仪版本 2.7. x. x. x. x 和更高版本中可用) 。 
>
> 然后从文档中删除标签（如果已应用），并将文件复制到扫描程序的数据存储库。 

## <a name="sharepoint-requirements"></a>SharePoint 要求

若要扫描 SharePoint 文档库和文件夹，请确保您的 SharePoint 服务器符合以下要求：

- **支持的版本。** 支持的版本包括： SharePoint 2019、SharePoint 2016 和 SharePoint 2013。 扫描程序不支持其他版本的 SharePoint。

- **控制.** 使用 [版本控制](/sharepoint/governance/versioning-content-approval-and-check-out-planning)时，扫描程序会检查并标记上次发布的版本。 如果扫描程序标签文件和 [内容审批](/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval) 是必需的，则必须向用户批准标记为 "文件" 的文件。  

- **大型 SharePoint 场。** 对于大型 SharePoint 场，请检查是否需要增加列表视图阈值（默认为 5,000），以便扫描程序访问所有文件。 有关详细信息，请参阅 [在 SharePoint 中管理大型列表和库](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)。


## <a name="microsoft-office-requirements"></a>Microsoft Office 要求

若要扫描 Office 文档，文档必须采用以下格式之一：

- Microsoft Office 97-2003 
- Word、Excel 和 PowerPoint 的 Office Open XML 格式

有关详细信息，请参阅 [Azure 信息保护客户端支持的文件类型](./rms-client/client-admin-guide-file-types.md)。

## <a name="file-path-requirements"></a>文件路径要求

若要扫描文件，文件路径的最大长度必须为260个字符，除非在 Windows 2016 上安装了扫描程序，并且该计算机配置为支持长路径

Windows 10 和 windows Server 2016 支持使用以下 [组策略设置](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)的路径长度大于260个字符：**本地计算机策略**  >  **计算机配置**  >  **管理模板**  >  **所有设置**  >  **启用 Win32 长路径**

有关支持长文件路径的详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

## <a name="usage-statistics-requirements"></a>使用情况统计信息要求

使用以下方法之一禁用使用情况统计信息：

- 将 [AllowTelemetry](./rms-client/client-admin-guide-install.md#to-install-the-azure-information-protection-client-by-using-the-executable-installer) 参数设置为0

- 请确保在扫描程序安装过程中未选择 " **通过向 Microsoft 发送使用情况统计信息来帮助改进 Azure 信息保护** " 选项。


## <a name="deploying-the-scanner-with-alternative-configurations"></a>使用备用配置部署扫描程序

上面列出的先决条件是扫描程序部署的默认要求，建议使用，因为它们支持最简单的扫描程序配置。

默认要求适用于初始测试，因此您可以检查扫描程序的功能。 

但是，在生产环境中，组织的策略可能会禁止这些默认要求。 扫描程序可以通过其他配置来适应以下限制：

- [扫描仪服务器无法建立 internet 连接](#restriction-the-scanner-server-cannot-have-internet-connectivity)

- [限制：扫描仪服务帐户无法同步到 Azure Active Directory 但服务器具有 internet 连接](#restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity)

- [限制：无法向扫描程序的服务帐户授予 **本地登录** 权限](#restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right)

- [限制：无法获得 Sysadmin 角色，或必须手动创建和配置数据库](#restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually)

- [限制：标签没有自动标记条件](#restriction-your-labels-do-not-have-auto-labeling-conditions)

### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>限制：扫描仪服务器不能连接到 internet

若要支持断开连接的计算机，请执行以下步骤：

1. 配置仅应用分类的标签，或使用 [HYOK 保护](configure-adrms-restrictions.md)的应用保护。 

    如果没有 internet 连接，扫描仪将无法使用组织的基于云的密钥来应用保护、删除保护或检查受保护的文件。 相反，扫描器仅限于使用仅应用分类的标签，或使用 HYOK 保护的应用保护。
    
    有关详细信息，请参阅 [对断开连接的计算机的支持](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)。

1. 通过创建扫描仪群集，在 Azure 门户中配置扫描仪。 如果需要此步骤的帮助，请参阅[在 Azure 门户中配置扫描程序](deploy-aip-scanner-configure-install-classic.md#configure-the-scanner-in-the-azure-portal)。

2. 使用 "**导出**" 选项，从 " **Azure 信息保护-内容扫描作业**" 窗格导出内容作业。

3. 在 PowerShell 会话中，运行 [set-aipscannerconfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) 并指定包含导出的设置的文件。

### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>限制：无法获得 Sysadmin 角色，或必须手动创建和配置数据库

如果可以 *暂时* 授予 Sysadmin 角色以安装扫描程序，则可以在扫描程序安装完成后删除此角色。

根据组织的要求，执行下列操作之一：

- **您可以暂时拥有 Sysadmin 角色。** 如果你暂时拥有 Sysadmin 角色，系统会自动为你创建数据库，并且会自动向扫描程序的服务帐户授予所需的权限。

    但是，配置扫描程序的用户帐户仍需要扫描程序配置数据库的 **db_owner** 角色。 如果在安装程序完成之前只有 Sysadmin 角色，请 [手动向用户帐户授予 db_owner 角色](#create-a-user-and-grant-db_owner-rights-manually)。

- **你根本不能拥有 Sysadmin 角色**。 如果你不能暂时授予 Sysadmin 角色，则必须在安装 scanner 之前要求具有 Sysadmin 权限的用户手动创建数据库。 

    对于此配置，必须将 **db_owner** 角色分配给以下帐户： 

    - 扫描程序的服务帐户

    - 用于安装程序的用户帐户

    - 用于配置扫描程序的用户帐户
      
    用于安装和配置扫描程序的用户帐户通常是相同的。 如果使用不同的帐户，则它们都需要扫描程序配置数据库的 db_owner 角色。 根据需要创建此用户和权限。 

    如果没有为扫描仪指定自己的群集 (配置文件) 名称，则配置数据库将命名为 " **AIPScanner_ \<computer_name>**"。 </br>继续 [创建用户并授予对数据库的 db_owner 权限](#create-a-user-and-grant-db_owner-rights-manually)。 

此外：

- 您必须是将运行扫描程序的服务器上的本地管理员
- 必须为将运行扫描程序的服务帐户授予对以下注册表项的 "完全控制" 权限：
    
    - HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server

如果在配置这些权限后出现错误，则在安装扫描程序时，可以忽略该错误，并且可以手动启动 scanner 服务。

#### <a name="populate-the-database-manually"></a>手动填充数据库

使用以下脚本填充数据库： 

```sql
if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END 
```

#### <a name="create-a-user-and-grant-db_owner-rights-manually"></a>手动创建用户并授予 db_owner 权限

若要创建用户并授予对此数据库的 db_owner 权限，请要求 Sysadmin 执行以下操作：

1. 为扫描程序创建数据库：

    ```sql
    **CREATE DATABASE AIPScannerUL_[clustername]**
    
    **ALTER DATABASE AIPScannerUL_[clustername] SET TRUSTWORTHY ON**
    ```
    
2. 向运行 install 命令的用户授予权限，并用于运行扫描程序管理命令。

    SQL 脚本：
    
    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    USE DBName IF NOT EXISTS (select * from sys.database_principals where sid = SUSER_SID('domain\user')) BEGIN declare @X nvarchar(500) Set @X = 'CREATE USER ' + quotename('domain\user') + ' FROM LOGIN ' + quotename('domain\user'); exec sp_addrolemember 'db_owner', 'domain\user' exec(@X) END
    ```

3. 向扫描程序服务帐户授予权限。

    SQL 脚本：

    ```sql
    if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END
    ```

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>限制：无法向扫描程序的服务帐户授予“本地登录”权限

如果你的组织策略禁止服务帐户在 **本地登录** ，但允许 **作为批处理作业登录** 权限，请参阅 [指定并使用 set-aipauthentication 的 Token 参数](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>限制：扫描仪服务帐户无法同步到 Azure Active Directory 但服务器具有 internet 连接

可以使用一个帐户来运行扫描程序服务，并使用另一个帐户对 Azure Active Directory 进行身份验证：

- **对于 scanner 服务帐户，请** 使用本地 Windows 帐户或 Active Directory 帐户。

- **对于 Azure Active Directory 帐户，请**[指定并使用 set-aipauthentication 的 Token 参数](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)。

#### <a name="restriction-your-labels-do-not-have-auto-labeling-conditions"></a>限制：标签没有自动标记条件

如果标签没有任何自动标记条件，请在配置扫描仪时计划使用以下选项之一：

|选项  |说明  |
|---------|---------|
|**发现所有信息类型**     |  在 [内容扫描作业](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)中，将 "要 **发现的信息类型** " 选项设置为 " **所有**"。 </br></br>此选项设置内容扫描作业，以扫描所有敏感信息类型的内容。      |
|**定义默认标签**     |   定义 [策略](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do)、 [内容扫描作业](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)或 [存储库](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository)中的默认标签。 </br></br>在这种情况下，扫描器会对找到的所有文件应用默认标签。       |
| | |

## <a name="next-steps"></a>后续步骤

确认系统符合扫描器先决条件后，请继续 [部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner-configure-install-classic.md)。

有关扫描仪的概述，请参阅 [部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner-classic.md)。

**详细信息：**

想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

您可能想知道： [Windows SERVER FCI 和 Azure 信息保护扫描程序之间的区别是什么？](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 有关此方案以及使用 PowerShell 的其他方案的详细信息，请参阅 [将 PowerShell 与 Azure 信息保护经典客户端配合使用](./rms-client/client-admin-guide-powershell.md)