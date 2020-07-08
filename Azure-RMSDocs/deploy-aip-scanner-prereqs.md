---
title: Azure 信息保护（AIP）统一标记扫描器先决条件
description: 列出安装和部署 Azure 信息保护统一标签扫描器的先决条件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/24/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cef1f6f80865f813e613e717ea301176f8fcc317
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86049481"
---
# <a name="prerequisites-for-installing-and-deploying-the-azure-information-protection-unified-labeling-scanner"></a>安装和部署 Azure 信息保护统一标记扫描器的先决条件

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*

>[!NOTE]
> 如果使用的是经典扫描程序，请参阅[安装和部署 Azure 信息保护经典扫描器的先决条件](deploy-aip-scanner-prereqs-classic.md)。

在安装 Azure 信息保护扫描程序之前，请确保你的系统符合以下要求：

- [Windows Server 要求](#windows-server-requirements)
- [服务帐户要求](#service-account-requirements)
- [SQL server 要求](#sql-server-requirements)
- [Azure 信息保护客户端要求](#azure-information-protection-client-requirements)
- [标签配置要求](#label-configuration-requirements)
- [SharePoint 要求](#sharepoint-requirements)
- [Microsoft Office 要求](#microsoft-office-requirements)
- [文件路径要求](#file-path-requirements)
- [使用情况统计信息要求](#usage-statistics-requirements)

如果你无法满足表中的所有要求，因为你的组织策略禁止这些要求，请参阅[备选配置](#deploying-the-scanner-with-alternative-configurations)部分。

在生产中部署扫描仪或测试多个扫描仪的性能时，请参阅[SQL Server 的存储要求和容量规划](#storage-requirements-and-capacity-planning-for-sql-server)。

准备好开始安装和部署扫描程序时，请继续[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner-configure-install.md)。

## <a name="windows-server-requirements"></a>Windows Server 要求

你必须有一台运行扫描程序的 Windows Server 计算机，该计算机具有以下系统规范：

|规格  |详细信息  |
|---------|---------|
|**处理器**     |4核处理器         |
|**RAM**     |8 GB         |
|**硬盘空间**     |临时文件有 10 GB 可用空间（平均值）。 </br></br>扫描程序需要足够的磁盘空间，才能为其扫描的每个文件（每个核心四个文件）创建临时文件。 </br></br>借助建议的 10GB 磁盘空间，4 核处理器可以扫描 16 个文件，每个文件的大小为 625MB。
|**操作系统**     |-Windows Server 2019 </br>- Windows Server 2016 </br>- Windows Server 2012 R2 </br></br>**注意：** 对于非生产环境中的测试或评估目的，还可以使用[Azure 信息保护客户端支持](requirements.md#client-devices)的任何 Windows 操作系统。
|**网络连接**     | 扫描仪计算机可以是物理计算机或虚拟计算机，与要扫描的数据存储进行快速可靠的网络连接。 </br></br> 如果由于组织策略而无法建立 internet 连接，请参阅[用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。 </br></br>否则，请确保此计算机具有 internet 连接，允许通过 HTTPS （端口443）上的以下 Url：</br><br />-  \*。 aadrm.com <br />-  \*。 azurerms.com<br />-  \*。 informationprotection.azure.com <br /> -informationprotection.hosting.portal.azure.net <br /> - \*。 aria.microsoft.com <br />-  \*。 protection.outlook.com |
| ||

## <a name="service-account-requirements"></a>服务帐户要求

您必须具有服务帐户才能在 Windows Server 计算机上运行 scanner 服务，并可 Azure AD 和下载 Azure 信息保护策略。

你的服务帐户必须是 Active Directory 帐户，并同步到 Azure AD。

如果由于组织策略而无法同步此帐户，请参阅[用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。

此服务帐户有以下要求：

|要求  |详细信息  |
|---------|---------|
|**本地登录**用户权限分配     |需要安装和配置扫描程序，但不需要运行扫描。  </br></br>确认扫描程序可以发现、分类和保护文件后，可以从服务帐户中删除此权限。  </br></br>如果由于组织策略的原因而无法在短时间内授予此权限，请参阅[使用替代配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。         |
|作为服务登录**** 的用户权限分配。     |  扫描程序安装过程中会自动将此权限授予服务帐户，此权限是安装、配置和操作扫描程序所必需的。        |
|**数据存储库的权限**     |- **文件共享或本地文件：** 授予 "**读取**"、"**写入**" 和 "**修改**" 权限以扫描文件，然后按配置应用 "分类和保护"。  <br /><br />- **SharePoint：** 授予 "**完全控制**" 权限以扫描文件，然后按配置应用 "分类和保护"。  <br /><br />- **发现模式：** 若要仅在发现模式下运行扫描程序，**读取**权限就足够了。         |
|**对于重新保护或删除保护的标签**     | 若要确保扫描程序始终可以访问受保护的文件，请将此帐户设置为 Azure 信息保护的[超级用户](configure-super-users.md)，并确保已启用超级用户功能。 </br></br>此外，如果已为分阶段部署实现了[载入控件](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，请确保已配置的载入控件中包含该服务帐户。|
| ||

## <a name="sql-server-requirements"></a>SQL server 要求

若要存储扫描程序配置数据，请使用具有以下要求的 SQL server：

- **本地或远程实例。**

    建议在不同的计算机上托管 SQL Server 和扫描程序服务，除非使用的是小型部署。

    SQL Server 2012 是以下版本的最低版本：

    - SQL Server Enterprise
    - SQL Server Standard
    - SQL Server Express （建议仅用于测试环境）

- **具有安装扫描程序的 Sysadmin 角色的帐户。**

    这使安装过程能够自动创建扫描程序配置数据库并向运行该扫描程序的服务帐户授予所需的**db_owner**角色。

    如果无法授予 Sysadmin 角色或组织策略需要手动创建和配置数据库，请参阅[用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。

- **功能.** 有关容量指导，请参阅[SQL Server 的存储要求和容量规划](#storage-requirements-and-capacity-planning-for-sql-server)。

- **[不区分大小写排序规则](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15)**

> [!NOTE]
> 当你为扫描仪指定自定义群集（配置文件）名称时，或使用扫描仪的预览版本时，支持同一 SQL server 上的多个配置数据库。
>
### <a name="storage-requirements-and-capacity-planning-for-sql-server"></a>SQL Server 的存储要求和容量规划

扫描程序配置数据库所需的磁盘空间量以及运行 SQL Server 的计算机的规范可能因每个环境而异，因此，我们鼓励你进行自己的测试。 使用以下指导作为起点。

有关详细信息，请参阅[优化扫描程序的性能](deploy-aip-scanner-configure-install.md#optimizing-scanner-performance)。

对于每个部署，扫描程序配置数据库的磁盘大小将有所不同。 使用以下公式作为指导：

```cli
100 KB + <file count> *(1000 + 4* <average file name length>)
```

例如，若要扫描1000000个文件名长度为250字节的文件，请分配 2 GB 磁盘空间。

对于多个扫描仪：

- **最多10个扫描仪，** 使用：

    - 4核处理器
    - 建议 8 GB RAM

- 超过**10 个扫描仪**（最大40），使用：
    - 8个核心进程
    - 建议使用 16 GB RAM

## <a name="azure-information-protection-client-requirements"></a>Azure 信息保护客户端要求

你必须在 Windows Server 计算机上安装 Azure 信息保护客户端的[当前通用版本](./rms-client/unifiedlabelingclient-version-release-history.md)。

有关详细信息，请参阅[统一标签客户端管理员指南](./rms-client/clientv2-admin-guide.md#installing-the-azure-information-protection-scanner)。

> [!IMPORTANT]
> 必须安装扫描程序的完整客户端。 请勿安装只带有 PowerShell 模块的客户端。
>

## <a name="label-configuration-requirements"></a>标签配置要求

您必须将标签配置为自动应用分类和保护（可选）。

如果未配置这些标签，请参阅[使用替代配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)。

有关详情，请参阅：

- [将敏感度标签自动应用到内容](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)
- [通过在敏感度标签中使用加密来限制对内容的访问](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)

## <a name="sharepoint-requirements"></a>SharePoint 要求

若要扫描 SharePoint 文档库和文件夹，请确保您的 SharePoint 服务器符合以下要求：

- **支持的版本。** 支持的版本包括： SharePoint 2019、SharePoint 2016、SharePoint 2013 和 SharePoint 2010。 扫描程序不支持其他版本的 SharePoint。

- **控制.** 使用[版本控制](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning)时，扫描程序会检查并标记上次发布的版本。 如果扫描程序标签文件和[内容审批](https://docs.microsoft.com/sharepoint/governance/versioning-content-approval-and-check-out-planning#plan-content-approval)是必需的，则必须向用户批准标记为 "文件" 的文件。  

- **大型 SharePoint 场。** 对于大型 SharePoint 场，请检查是否需要增加列表视图阈值（默认为 5,000），以便扫描程序访问所有文件。 有关详细信息，请参阅[在 SharePoint 中管理大型列表和库](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)。

## <a name="microsoft-office-requirements"></a>Microsoft Office 要求

若要扫描 Office 文档，文档必须采用以下格式之一：

- Microsoft Office 97-2003
- Word、Excel 和 PowerPoint 的 Office Open XML 格式

有关详细信息，请参阅[Azure 信息保护统一标签客户端支持的文件类型](./rms-client/clientv2-admin-guide-file-types.md)。

## <a name="file-path-requirements"></a>文件路径要求

若要扫描文件，文件路径的最大长度必须为260个字符，除非在 Windows 2016 上安装了扫描程序，并且该计算机配置为支持长路径

Windows 10 和 windows Server 2016 支持使用以下[组策略设置](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)的路径长度大于260个字符：**本地计算机策略**  >  **计算机配置**  >  **管理模板**  >  **所有设置**  >  **启用 Win32 长路径**

有关支持长文件路径的详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

## <a name="usage-statistics-requirements"></a>使用情况统计信息要求

使用以下方法之一禁用使用情况统计信息：

- 将[AllowTelemetry](https://docs.microsoft.com/azure/information-protection/rms-client/client-admin-guide-install#to-install-the-azure-information-protection-client-by-using-the-executable-installer)参数设置为0

- 请确保在扫描程序安装过程中未选择 "**通过向 Microsoft 发送使用情况统计信息来帮助改进 Azure 信息保护**" 选项。

## <a name="deploying-the-scanner-with-alternative-configurations"></a>使用备用配置部署扫描程序

上面列出的先决条件是扫描程序部署的默认要求，建议使用，因为它们支持最简单的扫描程序配置。

默认要求适用于初始测试，因此您可以检查扫描程序的功能。

但是，在生产环境中，组织的策略可能会禁止这些默认要求。 扫描程序可以通过其他配置来适应以下限制：

- [扫描仪服务器无法建立 internet 连接](#restriction-the-scanner-server-cannot-have-internet-connectivity)

- [限制：扫描仪服务帐户无法同步到 Azure Active Directory 但服务器具有 internet 连接](#restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity)

- [限制：无法向扫描程序的服务帐户授予**本地登录**权限](#restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right)

- [限制：无法获得 Sysadmin 角色，或必须手动创建和配置数据库](#restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually)

### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>限制：扫描仪服务器不能连接到 internet

若要支持断开连接的计算机，请执行以下步骤：

1. 配置策略中的标签，然后使用[set-aipscannerconfiguration](https://docs.microsoft.com/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration?view=azureipps) cmdlet 导入该策略。 尽管统一标签客户端在没有 internet 连接的情况下无法应用保护，但扫描程序仍可以基于导入的策略应用标签。

1. 通过创建扫描仪群集，在 Azure 门户中配置扫描仪。 如果需要此步骤的帮助，请参阅[在 Azure 门户中配置扫描程序](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal)。

1. 使用 "**导出**" 选项，从 " **Azure 信息保护-内容扫描作业**" 窗格导出内容作业。

1. 在 PowerShell 会话中，运行[set-aipscannerconfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)并指定包含导出的设置的文件。

### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>限制：无法获得 Sysadmin 角色，或必须手动创建和配置数据库

如果可以*暂时*授予 Sysadmin 角色以安装扫描程序，则可以在扫描程序安装完成后删除此角色。

根据组织的要求，执行下列操作之一：

- **您可以暂时拥有 Sysadmin 角色。** 如果你暂时拥有 Sysadmin 角色，系统会自动为你创建数据库，并且会自动向扫描程序的服务帐户授予所需的权限。

    但是，配置扫描程序的用户帐户仍需要扫描程序配置数据库的**db_owner**角色。 如果在安装程序完成之前只有 Sysadmin 角色，请[手动向用户帐户授予 db_owner 角色](#create-a-user-and-grant-db_owner-rights-manually)。

- **你根本不能拥有 Sysadmin 角色**。 如果你不能暂时授予 Sysadmin 角色，则必须在安装 scanner 之前要求具有 Sysadmin 权限的用户手动创建数据库。

    对于此配置，必须将**db_owner**角色分配给以下帐户：

    - 扫描程序的服务帐户
    - 用于安装程序的用户帐户
    - 用于配置扫描程序的用户帐户

    用于安装和配置扫描程序的用户帐户通常是相同的。 如果使用不同的帐户，则它们都需要扫描程序配置数据库的 db_owner 角色。 根据需要创建此用户和权限。 如果指定自己的群集（配置文件）名称，则配置数据库将命名**AIPScannerUL_<cluster_name>**。

此外：

- 您必须是将运行扫描程序的服务器上的本地管理员
- 必须为将运行扫描程序的服务帐户授予对以下注册表项的 "完全控制" 权限：

    - HKEY_LOCAL_MACHINE \SOFTWARE\WOW6432Node\Microsoft\MSIPC\Server
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\MSIPC\Server

如果在配置这些权限后出现错误，则在安装扫描程序时，可以忽略该错误，并且可以手动启动 scanner 服务。

#### <a name="populate-the-database-manually"></a>手动填充数据库

使用以下脚本填充数据库：

```cli
if not exists(select * from master.sys.server_principals where sid = SUSER_SID('domain\user')) BEGIN declare @T nvarchar(500) Set @T = 'CREATE LOGIN ' + quotename('domain\user') + ' FROM WINDOWS ' exec(@T) END 
```

#### <a name="create-a-user-and-grant-db_owner-rights-manually"></a>手动创建用户并授予 db_owner 权限

若要创建用户并授予对此数据库的 db_owner 权限，请要求 Sysadmin 执行以下操作：

1. 为扫描程序创建数据库：

    ```cli
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

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>限制：无法向扫描程序的服务帐户授予“本地登录”**** 权限

如果你的组织策略禁止服务帐户在**本地登录**，但允许**作为批处理作业登录**，请使用具有 set-aipauthentication 的*OnBehalfOf*参数。

有关详细信息，请参阅[如何以非交互方式为 Azure 信息保护标记文件](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>限制：扫描仪服务帐户无法同步到 Azure Active Directory 但服务器具有 internet 连接

可以使用一个帐户来运行扫描程序服务，并使用另一个帐户对 Azure Active Directory 进行身份验证：

- **对于 scanner 服务帐户，请**使用本地 Windows 帐户或 Active Directory 帐户。

- **对于 Azure Active Directory 帐户，请**指定具有 Set-aipauthentication 的*OnBehalfOf*参数的本地帐户。 有关详细信息，请参阅[如何以非交互方式为 Azure 信息保护标记文件](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)。

## <a name="next-steps"></a>后续步骤

确认系统符合扫描器先决条件后，请继续[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner-configure-install.md)。

有关扫描仪的概述，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。

**详细信息：**

- 想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

- 您可能想知道： [Windows SERVER FCI 和 Azure 信息保护扫描程序之间的区别是什么？](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- 还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 有关此方案以及使用 PowerShell 的其他方案的详细信息，请参阅[将 PowerShell 与 Azure 信息保护统一标签客户端配合使用](./rms-client/clientv2-admin-guide-powershell.md)。
