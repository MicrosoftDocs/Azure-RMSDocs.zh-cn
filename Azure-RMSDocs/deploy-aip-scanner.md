---
title: 部署 Azure 信息保护扫描程序-AIP
description: 如何安装、 配置和运行当前版本的 Azure 信息保护扫描程序来发现、 分类和保护数据存储上的文件。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/06/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: f86c1622e19b0ab5dc7bf274bd020203043bea0f
ms.sourcegitcommit: d4540d8c535cd858550d6f62149fb8096b0ccd40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719845"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>部署 Azure 信息保护扫描程序以自动对文件进行分类和保护

>适用对象： *[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，Windows Server 2019、 Windows Server 2016、 Windows Server 2012 R2*
>
> 说明：  [适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

> [!NOTE]
> 本文适用于 Azure 信息保护扫描程序的当前正式发布版本。
> 
> 若要从早于 1.48.204.0 扫描程序的正式发布版本升级，请参阅[升级 Azure 信息保护扫描程序](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。 你可以然后使用说明在此页上，忽略步骤来安装扫描程序。
> 
> 如果已准备好升级从以前的版本，请参见[部署的 Azure 信息保护扫描程序以自动分类和保护文件的以前版本](deploy-aip-scanner-previousversions.md)。


利用此信息了解 Azure 信息保护扫描程序，并了解如何成功安装、配置和运行该扫描程序。

此扫描程序在 Windows Server 上作为服务运行，使你能够发现和保护以下数据存储中的文件并对其进行分类：

- 运行扫描程序的 Windows Server 计算机上的本地文件夹。

- 使用服务器消息块 (SMB) 协议的网络共享 UNC 路径。

- 站点和库，用于通过 SharePoint Server 2013 的 SharePoint Server 2019。 对于具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)的客户，还支持 SharePoint 2010。

若要在云存储库上扫描并标记文件，请使用 [Cloud App Security](https://docs.microsoft.com/cloud-app-security/)，而不是扫描程序。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序概述

为应用自动分类的标签配置 [Azure 信息保护策略](configure-policy.md)后，可为此扫描程序发现的文件设置标签。 标签可应用分类，并且可以应用保护或移除保护：

![Azure 信息保护扫描程序体系结构概述](./media/infoprotect-scanner.png)

通过使用计算机上安装的 iFilter，扫描程序可检查 Windows 能编制索引的任何文件。 然后，为了确定是否需要标记文件，扫描程序会使用 Office 365 内置数据丢失防护 (DLP) 敏感信息类型和模式检测，或 Office 365 正则表达式模式。 因为扫描程序使用 Azure 信息保护客户端，所以它可以对相同[文件类型](./rms-client/client-admin-guide-file-types.md)进行分类和保护。

可仅在发现模式下运行扫描程序，利用报告确认对文件设置标签时会发生什么情况。 或者，可运行扫描程序自动应用标签。 还可以运行扫描程序来发现包含敏感信息类型的文件，无需配置条件标签来应用自动分类。

注意，扫描程序不会实时发现和标记。 它会系统地浏览指定数据存储中的文件，可将此周期配置为运行一次或多次。

可以通过将文件类型列表定义为扫描程序配置的一部分来指定要扫描的文件类型或从扫描中排除的文件类型。


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序的先决条件
安装 Azure 信息保护扫描程序之前，请确保已满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|运行扫描程序服务的 Windows Server 计算机：<br /><br />- 4 核处理器<br /><br />- 8 GB RAM<br /><br />- 临时文件 10GB 可用空间（平均）|Windows Server 2019、 Windows Server 2016 中或 Windows Server 2012 R2。 <br /><br />注意：出于在非生产环境中进行测试或评估的目的，可以使用[受 Azure 信息保护客户端支持](requirements.md#client-devices)的 Windows 客户端操作系统。<br /><br />此计算机可以是物理或虚拟计算机，需拥有快速可靠的网络，可连接到要进行扫描的数据存储。<br /><br /> 扫描程序需要足够的磁盘空间，才能为其扫描的每个文件（每个核心四个文件）创建临时文件。 借助建议的 10GB 磁盘空间，4 核处理器可以扫描 16 个文件，每个文件的大小为 625MB。 <br /><br />如果由于组织策略而无法连接到 Internet，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。 否则，请确保此计算机具有 Internet 连接，可允许以下 URL 通过 HTTPS（端口 443）连接：<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com|
|运行扫描程序服务的服务帐户|除了在 Windows Server 计算机上运行扫描程序服务外，此 Windows 帐户还对 Azure AD 进行身份验证，并下载 Azure 信息保护策略。 此帐户必须是同步到 Azure AD 的 Active Directory 帐户。 如果由于组织策略而无法同步此帐户，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />此服务帐户有以下要求：<br /><br />- 在本地登录  的用户权限分配。 此权限是安装和配置扫描程序所必需的，但不可用于操作。 必须将此权限授予服务帐户，但当确认扫描程序可发现、保护文件并对其进行分类后，可删除此权限。 如果由于组织策略的限制而甚至无法在短时间内授予此权限，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />- 作为服务登录  的用户权限分配。 扫描程序安装过程中会自动将此权限授予服务帐户，此权限是安装、配置和操作扫描程序所必需的。 <br /><br />- 针对数据存储库的权限：必须授予“读取”和“写入”权限才能扫描文件，然后将分类和保护应用到满足 Azure 信息保护策略中的条件的文件   。 若仅在发现模式下运行扫描程序，则只需“读取”权限即可  。<br /><br />- 对于重新保护或删除保护的标签：若要确保扫描程序始终有权访问受保护的文件，请将此帐户设置为 Azure Rights Management 服务的[超级用户](configure-super-users.md)，并确保已启用超级用户功能。 要详细了解应用保护的帐户要求，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。 此外，如果对分阶段部署实现了[载入控件](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，还请确保已配置的载入控件中包含此帐户。|
|存储扫描程序配置的 SQL Server：<br /><br />- 本地或远程实例<br /><br />- 安装扫描程序的 Sysadmin 角色|SQL Server 2012 是以下版本的最低版本：<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />指定扫描程序的自定义配置文件名称时，Azure 信息保护扫描程序支持同一 SQL Server 实例上的多个配置数据库。<br /><br />如果安装扫描程序且帐户拥有 Sysadmin 角色，那么在安装过程中会自动创建扫描程序配置数据库，并向运行扫描程序的服务帐户授予所需的 db_owner 角色。 如果无法获得 Sysadmin 角色或组织策略要求手动创建和配置数据库，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />每个部署的配置数据库大小不同，建议为要扫描的每 1 百万个文件分配 500 MB。 |
|在 Windows Server 计算机上安装 Azure 信息保护客户端|必须安装扫描程序的完整客户端。 请勿安装只带有 PowerShell 模块的客户端。<br /><br />有关客户端安装说明，请参阅[管理员指南](./rms-client/client-admin-guide.md)。 如果现在需要将已安装的旧扫描程序升级到更高版本，请参阅[升级 Azure 信息保护扫描程序](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。|
|已配置可应用自动分类和保护（可选）的标签|有关如何为条件配置标签以及如何应用保护的更多信息：<br /> - [如何为自动分类和推荐分类配置条件](configure-policy-classification.md)<br /> - [如何配置标签以进行 Rights Management 保护](configure-policy-protection.md) <br /><br />提示：可以使用[教程](infoprotect-quick-start-tutorial.md)中的说明来测试带有标签的扫描程序，在准备好的 Word 文档中查找信用卡号。 但是，需要更改标签配置，以便将“选择应用此标签的方式”选项  设置为“自动”  而不是“推荐”  。 然后从文档中删除标签（如果已应用），并将文件复制到扫描程序的数据存储库。 为了快速测试，可以使用扫描程序计算机上的本地文件夹。<br /><br /> 尽管即使你尚未配置应用自动分类的标签，仍然可以运行扫描程序，但这些说明中并未涵盖此方案。 [详细信息](#using-the-scanner-with-alternative-configurations)|
|对于要扫描的 SharePoint 网站和库：<br /><br />- SharePoint 2019<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|扫描程序不支持其他版本的 SharePoint。<br /><br />对于大型 SharePoint 场，请检查是否需要增加列表视图阈值（默认为 5,000），以便扫描程序访问所有文件。 有关详细信息，请参阅下列 SharePoint 文档：[管理 SharePoint 中的大型列表和库](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|对于要扫描的 Office 文档：<br /><br />- Word、Excel 和 PowerPoint 的 97-2003 文件格式和 Office Open XML 格式|若要详细了解扫描程序对这些文件格式支持的文件类型，请参阅 [Azure 信息保护客户端支持的文件类型](./rms-client/client-admin-guide-file-types.md)|
|对于长路径：<br /><br />- 最多 260 个字符，除非扫描程序安装在 Windows 2016 上，并且该计算机配置为支持长路径|Windows 10 和 Windows Server 2016 使用以下[组策略设置](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)，支持超过 260 个字符的路径长度：**本地计算机策略** > **计算机配置** > **管理模板** > **所有设置**  > **启用 Win32 长路径**<br /><br /> 有关支持长文件路径的详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

如果由于组织策略禁止而无法满足表中的所有要求，请参阅下一部分中介绍的备用配置。

如果满足所有要求，请直接转到[配置扫描程序部分](#configure-the-scanner-in-the-azure-portal)。

### <a name="deploying-the-scanner-with-alternative-configurations"></a>使用备用配置部署扫描程序

表中列出的先决条件是扫描程序的默认要求，之所以建议是因为它们是用于扫描程序部署的最简单配置。 它们应适用于初始测试，以便能够检查扫描程序的功能。 不过，在产品环境中，组织策略可能会禁止这些默认要求，因为存在下列一个或多个限制：

- 禁止服务器连接到 Internet

- 无法获得 Sysadmin 角色，或必须手动创建和配置数据库

- 无法向服务帐户授予“本地登录”  权限

- 服务帐户无法同步到 Azure Active Directory，但服务器可以连接到 Internet

虽然扫描程序可以适应这些限制，但需要其他配置。


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>限制：扫描程序服务器不能连接到 Internet

请按照适用于[已断开连接的计算机](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)的说明操作。 然后，执行下列操作：

1. 通过创建扫描程序配置文件在 Azure 门户中配置扫描程序。 如果需要此步骤的帮助，请参阅[在 Azure 门户中配置扫描程序](#configure-the-scanner-in-the-azure-portal)。

2. 使用“导出”  选项从“Azure 信息保护 - 配置文件(预览)”  边栏选项卡导出扫描程序配置文件。

3. 最后，在 PowerShell 会话中运行 [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)，并指定包含导出设置的文件。

请注意，在此配置中，扫描程序无法使用组织的基于云的密钥来应用（或删除）保护配置。 相反，扫描程序只能使用应用分类或 [HYOK](configure-adrms-restrictions.md) 保护的标签。 

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>限制：无法获得 Sysadmin 角色，或必须手动创建和配置数据库

如果可以获得 Sysadmin 角色来安装扫描程序，就能在扫描程序安装完成后删除此角色。 使用此配置时，数据库会自动创建，而且扫描程序的服务帐户也会自动获得相应权限。 不过，配置扫描程序的用户帐户需要拥有扫描程序配置数据库的 db_owner 角色，你必须手动向用户帐户授予此角色。

如果无法临时获得 Sysadmin 角色，则必须在安装扫描程序前手动创建数据库。 使用此配置时，请分配以下角色：
    
|帐户|数据库级角色|
|--------------------------------|---------------------|
|扫描程序的服务帐户|db_owner|
|用于安装扫描程序的用户帐户|db_owner|
|用于配置扫描程序的用户帐户 |db_owner|

用于安装和配置扫描程序的用户帐户通常是相同的。 不过，如果使用不同的帐户，它们都需要拥有扫描程序配置数据库的 db_owner 角色：

- 如果没有为扫描程序指定自己的配置文件名称，则会将配置数据库命名为  AIPScanner_\<computer_name>。 

- 如果指定自己的配置文件名称，则会将配置数据库命名为  AIPScanner_\<profile_name>。

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>限制：无法向扫描程序的服务帐户授予“本地登录”权限 

如果组织策略禁止向服务帐户授予“本地登录”  权限，但允许授予“以批处理作业形式登录”  权限，请按照管理员指南内[对 Set-AIPAuthentication 指定和使用 Token 参数](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)一文中的说明操作。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>限制：扫描程序服务帐户不能同步到 Azure Active Directory，但服务器可以连接到 Internet

可以使用一个帐户来运行扫描程序服务，并使用另一个帐户对 Azure Active Directory 进行身份验证：

- 对于扫描程序服务帐户，可以使用本地 Windows 帐户或 Active Directory 帐户。

- 如果使用 Azure Active Directory 帐户，请按照管理员指南内[对 Set-AIPAuthentication 指定和使用 Token 参数](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)一文中的说明操作。


## <a name="configure-the-scanner-in-the-azure-portal"></a>在 Azure 门户中配置扫描程序

在安装扫描程序或从扫描程序的正式发布版本升级扫描程序之前，请在 Azure 门户中为扫描程序创建配置文件。 可以配置扫描程序设置的配置文件以及要扫描的数据存储库。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”  边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”   。 选择“Azure 信息保护”。 
    
2. 找到“扫描程序”  菜单选项，然后选择“配置文件”  。

3. 在“Azure 信息保护 - 配置文件”  边栏选项卡上，选择“添加”  ：
    
    ![添加 Azure 信息保护扫描程序的配置文件](./media/scanner-add-profile.png)

4. 在“添加新配置文件”  边栏选项卡上，指定扫描程序的名称，该名称用于标识扫描程序的配置设置和要扫描的数据存储库。 例如，可以指定“欧洲”  来标识扫描程序将涵盖的数据存储库的地理位置。 以后安装或升级扫描程序时，将需要指定相同的配置文件名称。
    
    （可选）指定用于管理的说明，以帮助识别扫描程序的配置文件名称。

5. 对于此初始配置，请配置以下设置，然后选择“保存”  ，但不要关闭边栏选项卡：
    
    - **计划**:保留默认值“手动” 
    - **要发现的信息类型**：更改为“仅限策略” 
    - **配置存储库**：目前不要配置，因为必须先保存配置文件。
    - **强制执行**：选择“关闭” 
    - **基于内容标记文件**：保留默认值“启用” 
    - **默认标签**：保留默认值“策略默认值” 
    - **重新标记文件**：保留默认值“关闭” 
    - **保留“修改日期”、“上次修改时间”和“修改者”** ：保留默认值“启用” 
    - **要扫描的文件类型**：保留“排除”的默认文件类型 
    - **默认所有者**：保留默认值“扫描程序帐户” 

6. 现在已创建并保存配置文件，即可返回到“配置存储库”  选项以指定要扫描的数据存储。 可指定本地文件夹、UNC 路径以及 SharePoint 本地站点和库的 SharePoint Server URL。 
    
    SharePoint 支持 SharePoint Server 2019、 SharePoint Server 2016 和 SharePoint Server 2013。 具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)时，还支持 SharePoint Server 2010。
    
    若要添加第一个数据存储，则仍在“添加新配置文件”  边栏选项卡上，选择“配置存储库”  以打开“存储库”  边栏选项卡：
    
    ![为 Azure 信息保护扫描程序配置数据存储库](./media/scanner-repositories-bar.png)

7. 在“存储库”  边栏选项卡上，选择“添加”  ：
    
    ![为 Azure 信息保护扫描程序添加数据存储库](./media/scanner-repository-add.png)

8. 在“存储库”  边栏选项卡上，指定数据存储库的路径。 
    
    不支持通配符，也不支持 WebDav 位置。
    
    例如：
    
    对于本地路径：`C:\Folder`
    
    对于网络共享：`C:\Folder\Filename`
    
    对于 UNC 路径：`\\Server\Folder`
    
    对于 SharePoint 库：`http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > 如果为“共享文档”添加 SharePoint 路径：
    >
     >- 如果要从“共享文档”扫描所有文档和所有文件夹，请在路径中指定“共享文档”  。 例如：`http://sp2013/Shared Documents`
     >
     >- 如果要从“共享文档”下的子文件夹扫描所有文档和所有文件夹，请在路径中指定“文档”  。 例如：`http://sp2013/Documents/Sales Reports`
    
    对于此边栏选项卡上的其余设置，请不要为此初始配置更改它们，而是将其保留为“配置文件默认值”  。 这意味着数据存储库从扫描程序配置文件继承设置。 
    
    选择“保存”。 

9. 如果要添加其他数据存储库，请重复步骤 7 和 8。

10. 现在可以关闭“添加新配置文件”  边栏选项卡，并会看到在“Azure 信息保护 - 配置文件”  边栏选项卡中显示的配置文件名称，同时“计划”  列显示“手动”  且“强制执行”  列为空。

现在可随时使用刚刚创建的扫描程序配置文件安装扫描程序。

## <a name="install-the-scanner"></a>安装扫描程序

1. 登录到将要运行扫描程序的 Windows Server 计算机。 使用具有本地管理员权限并具有写入到 SQL Server master 数据库权限的帐户。

2. 使用“以管理员身份运行”选项打开 Windows PowerShell 会话  。

3. 运行 [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) cmdlet，指定要在其中为 Azure 信息保护扫描程序创建数据库的 SQL Server 实例，以及在上一部分中指定的扫描程序配置文件名称： 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <profile name>
    ```
    
    例如，使用配置文件名称“欧洲”  ：
    
    对于默认实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    对于命名实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    对于 SQL Server Express：`Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    系统提示时，请提供扫描程序服务帐户的凭据 (\<域\用户名>) 和密码。

4. 使用“管理工具” > “服务”验证服务现在是否已安装   。 
    
    已安装的服务被命名为 Azure信息保护扫描程序，并被配置为使用你创建的扫描程序服务帐户运行  。

现已安装扫描程序，需获取 Azure AD 令牌以便扫描程序服务帐户进行身份验证，从而扫描程序可以无人参与的方式运行。 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>获取扫描程序的 Azure AD 令牌

借助 Azure AD 令牌，Azure 信息保护服务可以验证扫描程序服务帐户。

1. 返回到 Azure 门户，创建指定用于身份验证的访问令牌需使用的 2 个 Azure AD 应用程序。 首次以交互方式登录后，此令牌将允许扫描程序以非交互方式运行。
    
    要创建这些应用程序，请按照管理员指南中[如何以非交互方式为 Azure 信息保护标记文件](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)的说明执行操作。

2. 在 Windows Server 计算机中，如果你的扫描程序服务帐户被授予了“本地登录”权限以用于安装  ：使用此帐户登录，并启动 PowerShell 会话。 运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)，指定从上一步骤中复制的值：
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```
    
    系统提示时，请为 Azure AD 的服务帐户凭据指定密码，然后单击“接受”  。
    
    如果无法向你的扫描程序服务帐户授予“本地登录”权限以用于安装  ：请按照管理员指南中的[对 Set-AIPAuthentication 指定和使用 Token 参数](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)中的说明进行操作。 

扫描程序现已拥有一个令牌，可向 Azure AD 进行身份验证。该令牌的有效期为 1 年、2 年或永不过期，具体取决于 Azure AD 中“Web 应用/API”的配置  。 如果令牌过期，则须重复步骤 1 和步骤 2。

现在可随时在发现模式下运行第一次扫描。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>运行发现周期并查看扫描程序报告

1. 在 Azure 门户中，返回到 Azure 信息保护以启动扫描程序。 在“扫描程序”  菜单选项中，选择“节点”  。 选择扫描程序节点，然后选择“立即扫描”  选项：
    
    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)
    
    或者，在 PowerShell 会话中，运行以下命令：
    
        Start-AIPScan

2. 等待扫描程序完成其周期。 当扫描程序浏览完指定数据存储中的所有文件时，扫描程序停止（尽管扫描程序服务仍在运行）：
    
    - 在“Azure 信息保护 - 节点”边栏选项卡中，“STATUS”列的值会从“正在扫描”更改为“空闲”     。
    
    - 使用 PowerShell，你可以运行 `Get-AIPScannerStatus` 来监视状态更改。
    
    - 查看本地 Windows 应用程序和服务  事件日志和 Azure 信息保护  。 另外，此日志还会报告扫描程序完成扫描的时间，以及结果摘要。 请查看信息事件 ID 911  。

3. 查看存储在 %  localappdata%\Microsoft\MSIP\Scanner\Reports 中的报表。 .txt 摘要文件包括扫描所用的时间、扫描的文件数以及匹配信息类型的文件数量。 .csv 文件包含每个文件的更多详细信息。 此文件夹为每个扫描周期最多存储 60 个报表，并且压缩除最新报表之外的所有报表，以帮助最大程度地减少所需的磁盘空间。
    
    > [!NOTE]
    > 可以将  ReportLevel 参数和 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) 结合使用来更改日志记录级别，但不能更改报表文件夹位置或名称。 如果要将报表存储在其他卷或分区上，请考虑使用该文件夹的目录交叉点。
    >
    > 例如，使用 [Mklink](/windows-server/administration/windows-commands/mklink) 命令：`mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    使用“要发现的信息类型”  的“仅限策略”  的设置时，只有满足你为自动分类配置的条件的文件才会被包括在详细报表中。 如果看不到任何应用的标签，请检查标签配置是否包括自动分类而不是推荐分类。
    
    > [!TIP]
    > 扫描程序会每 5 分钟向 Azure 信息保护发送一次此信息，这样你就可以准实时地在 Azure 门户中查看结果。 有关详细信息，请参阅 [Azure 信息保护报表](reports-aip.md)。 
        
    如果结果与预期不符，则可能需要重新配置在 Azure 信息保护策略中为标签指定的条件。 如果是这种情况，请重复步骤 1 到 3，直到可更改配置以应用分类和保护（可选）。 

Azure 门户仅显示有关上次扫描的信息。 如果需要查看先前扫描的结果，请返回到扫描程序计算机上存储的报表，它位于 %localappdata  %\Microsoft\MSIP\Scanner\Reports 文件夹中。

如果已准备好对扫描程序发现的文件进行自动标记，请继续下一步。 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>将扫描程序配置为应用分类和保护

如果按照这些说明操作，扫描程序在仅报告模式下运行一次。 若要更改这些设置，请编辑扫描程序配置文件：

1. 重新**Azure 信息保护-配置文件**边栏选项卡中，选择要对其进行编辑的扫描程序配置文件。

2. 在 \<  配置文件名称 > 边栏选项卡上，更改以下两个设置，然后选择“保存”  ：
    
   - **计划**:更改为“始终” 
   - **强制执行**：选择“启用” 
    
     你可能还希望更改其他配置设置。 例如，文件属性是否更改，以及扫描程序是否可以重新标记文件。 使用信息弹出通知帮助了解有关每个配置设置的详细信息。

3. 请记下当前时间并从“Azure 信息保护 - 节点”  边栏选项卡再次启动扫描程序：
    
    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)
    
    或者，可以在 PowerShell 会话中运行以下命令：
    
        Start-AIPScan

4. 重新监视 911 信息类型的事件日志，并且时间戳要晚于上个步骤启动扫描时的时间。  
    
    然后查看报告，详细了解标记了哪些文件、向每个文件应用了什么分类，以及是否向它们应用了保护。 或者，使用 Azure 门户，更轻松地了解此信息。

因为我们将计划配置为持续运行，所以当扫描程序扫描完所有文件时，它将自动开始一个新周期，以便发现任何新文件和更改的文件。


## <a name="how-files-are-scanned"></a>如何扫描文件

扫描程序在扫描文件时运行以下过程。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1.确定要在扫描范围内加入或排除的文件 
扫描程序自动跳过[从分类和保护中排除](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)的文件，如可执行文件和系统文件。

可以定义要扫描或不要扫描的文件类型列表，从而更改此行为。 默认情况下，可以为扫描程序指定此列表以应用于所有数据存储库，并且可以为每个数据存储库指定一个列表。 若要指定此列表，请使用扫描程序配置文件中的“要扫描的文件类型”  设置：

![配置 Azure 信息保护扫描程序要扫描的文件类型](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2.检查文件并为其设置标签

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
>     要检查这是否是导致扫描程序停止的原因，请在 %localappdata%\Microsoft\MSIP\Logs\MSIPScanner.iplog（如有多个日志，则为压缩文件）中查看是否记录了扫描程序的以下错误消息：  无法连接到远程服务器 ---> System.Net.Sockets.SocketException:  每个套接字地址（协议/网络地址/端口）的唯一用法通常是 IP:port
>    
>     有关如何查看当前端口范围以及增加该范围的详细信息，请参阅[可通过修改设置来提高网络性能](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)。
> 
> - 对于大型 SharePoint 场，可能需要增加列表视图阈值（默认情况下为 5,000）。 有关详细信息，请参阅下列 SharePoint 文档：[管理 SharePoint 中的大型列表和库](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)。

### <a name="3-label-files-that-cant-be-inspected"></a>3.无法检查的标签文件
对于无法检查的文件类型，扫描程序应用 Azure 信息保护策略中的默认标签或为扫描程序配置的默认标签。

与上述步骤相同，在下列情况下，扫描程序无法为文件设置标签：

- 如果标签应用分类而不应用保护，并且文件类型不[只支持分类](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)。

- 如果标签应用分类和保护，但扫描程序不保护该文件类型。
    
    默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。 可通过[编辑注册表](#editing-the-registry-for-the-scanner)来保护其他文件类型，如下文所述。


### <a name="editing-the-registry-for-the-scanner"></a>编辑扫描程序的注册表

若要更改默认扫描程序行为以保护 Office 文件和 PDF 以外的文件类型，必须手动编辑注册表并指定想要保护的其他文件类型以及保护类型（本机或泛型）。 有关说明，请参阅开发人员指南中的[文件 API 配置](develop/file-api-configuration.md)。 对于本文档中的开发人员，常规保护被称为“PFile”。 此外，特定于扫描程序：

- 扫描程序具有自己的默认行为：默认情况下，只有 Office 文件格式和 PDF 文档受到保护。 如果未修改注册表，则扫描程序不会保护任何其他文件类型或为其设置标签。

- 如果您希望 Azure 信息保护客户端，其中所有文件均自动都保护与本机或常规保护的默认保护行为相同：指定`*`注册表项，作为通配符`Encryption`作为值 (REG_SZ) 和`Default`作为值数据。

编辑注册表时，如果 MSIPC  密钥和 FileProtection  密钥不存在，则手动创建这些密钥，并创建每个文件扩展名的密钥。

例如，除了 Office 文件和 PDF 之外，若要使扫描程序还保护 TIFF 图像，编辑后的注册表将与下图类似。 作为图像文件，TIFF 文件支持本机保护，且生成的文件扩展名为 .ptiff。

![编辑扫描程序的注册表以应用保护](./media/editregistry-scanner.png)

有关同样支持本机保护但必须在注册表中进行指定的文本和图像文件类型列表，请参阅管理员指南中的[分类和保护的支持文件类型](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection)。

对于不支持本机保护的文件，请将文件扩展名指定为新密钥，并为 PFile 获取常规保护  。 对于受保护的文件，生成的文件扩展名为 .pfile。


## <a name="when-files-are-rescanned"></a>重新扫描文件时的情况

在第一个扫描周期，扫描程序会检查所配置的数据存储中的所有文件，然后在后续扫描中仅检查新文件或修改后的文件。 

可以从 Azure 门户的  “Azure 信息保护 - 节点”边栏选项卡强制扫描程序再次检查所有文件。 从列表中选择扫描程序，然后选择“重新扫描所有文件”  选项：

![启动 Azure 信息保护扫描程序重新扫描](./media/scanner-rescan-files.png)

如果希望报告包含所有文件，再次检查所有文件非常有用；且当扫描程序在发现模式下运行时，通常会使用此配置选项。 完成全部扫描后，扫描类型自动更改为“增量”，以便后续扫描仅扫描新文件或修改后的文件。

此外，在扫描程序下载具有新条件或更改后的条件时，会检查所有文件。 扫描程序每小时刷新一次策略，当服务启动时以及策略执行一小时之后，也会刷新。  

> [!TIP]
> 如果需要早于此一小时间隔的时间刷新策略，例如，在测试期间：同时从 %LocalAppData%\Microsoft\MSIP\Policy.msip 和 %LocalAppData%\Microsoft\MSIP\Scanner 中手动删除策略文件 Policy.msip    。 然后重新启动 Azure 信息扫描程序服务。
> 
> 如果更改了此策略中的保护设置，请在保存保护设置后等待 15 分钟，再重新启动该服务。

如果扫描程序下载了未配置任何自动条件的策略，不会更新扫描程序文件夹中的策略文件副本。 在此方案中，必须从 **%LocalAppData%\Microsoft\MSIP\Policy.msip** 和 **%LocalAppData%\Microsoft\MSIP\Scanner** 中删除策略文件 **Policy.msip**，然后扫描程序才能够使用正确配置了自动条件标签的新下载的策略文件。

## <a name="editing-in-bulk-for-the-data-repository-settings"></a>批量编辑数据存储库设置

对于已添加到扫描程序配置文件的数据存储库，可以使用“导出”  和“导入”  选项快速更改设置。 例如，对于 SharePoint 数据存储库，你希望添加要从扫描中排除的新文件类型。

使用“存储库”  边栏选项卡中的“导出”  选项，而不是在 Azure 门户中编辑每个数据存储库：

![导出扫描程序的数据存储库设置](./media/export-scanner-repositories.png)

手动编辑文件以进行更改，然后使用同一边栏选项卡上的“导入”  选项。

## <a name="using-the-scanner-with-alternative-configurations"></a>使用具有备选配置的扫描程序

Azure 信息保护扫描程序支持两种备选方案，在任何一种方案中都无需配置标签： 

- 将默认标签应用于数据存储库中的所有文件。
    
    对于此配置，请将“默认标签”  设置为“自定义”  ，然后选择要使用的标签。
    
    不检查文件的内容，并根据为数据存储库或扫描程序配置文件指定的默认标签来标记数据存储库中的所有文件。
    

- 标识所有自定义条件和已知敏感信息类型。
    
    对于此配置，请将“要发现的信息类型”  设置为“全部”  。
    
    扫描程序使用为 Azure 信息保护策略中的标签指定的任何自定义条件以及可指定用于 Azure 信息保护策略中的标签的信息类型列表。 此设置有助于查找你可能没有意识到的敏感信息，但会降低扫描程序的扫描速率。
    
    以下针对扫描程序正式发布版本的快速入门使用此配置：[快速入门：查找具有的敏感信息](quickstart-findsensitiveinfo.md)。

## <a name="optimizing-the-performance-of-the-scanner"></a>优化扫描程序性能

使用以下指南有助于优化扫描程序的性能。 但是，如果优先级是扫描程序计算机而不是扫描程序的性能的响应能力，则可以使用[高级客户端设置](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner)来限制由扫描程序使用的线程数。

若要最大程度实现扫描程序的性能：

- **在扫描程序计算机和被扫描的数据存储之间建立高速可靠的网络连接**
    
    例如，将扫描程序计算机置于所扫描的数据存储所在的 LAN 或（首选）网络段中。
    
    网络连接的质量会影响扫描程序的性能，因为要检查文件，扫描程序需将文件内容传输到运行扫描程序服务的计算机中。 如果减少（或消除）此数据需传输的网络跃点数，网络上的负载随之减少。 

- **确保扫描程序计算机具有可用的处理器资源**
    
    检查文件内容以及进行文件加密和解密是处理器密集型操作。 请监视所指定的数据存储的典型扫描周期，以确定缺少处理器资源是否对扫描程序性能造成负面影响。
    
- **不扫描运行扫描程序服务的计算机上的本地文件夹**
    
    如果 Windows 服务器上具有要扫描的文件夹，请在其他计算机上安装扫描程序，并将这些文件夹配置为要扫描的网络共享。 将承载文件和扫描文件这两大功能分开，这意味着这些服务的计算资源不相互竞争。

如有必要，请安装扫描程序的多个实例。 指定扫描程序的自定义配置文件名称时，Azure 信息保护扫描程序支持同一 SQL Server 实例上的多个配置数据库。

影响扫描程序性能的其他因素：

- 包含要扫描的文件的数据存储的当前负载和响应时间

- 扫描程序是在发现模式还是强制模式下运行
    
    通常，发现模式的扫描速率比强制模式的高，因为发现操作需要单一文件读取操作，而强制模式需要读取和写入操作。

- 更改 Azure 信息保护中的条件
    
    在第一个扫描周期，扫描程序必须检查每个文件，而后续扫描周期默认仅检查新文件和更改的文件，因此第一个周期比后续周期耗时长。 但是，如果更改 Azure 信息保护中的条件，则重新扫描所有文件，如[上一部分](#when-files-are-rescanned)所述。

- 自定义条件的正则表达式构造
    
    为避免占用过多内存并存在超时风险（每个文件 15 分钟），请查看正则表达式了解有效的模式匹配。 例如：
    
    - 避免[贪婪限定符](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)
    
    - 使用 `(?:expression)` 等非捕获组，而不是 `(expression)`

- 所选的日志记录级别
    
    可对扫描程序报告选择“调试”、“信息”、“错误”或“关闭”     。 “关闭”可使性能最佳；“调试”会明显减低扫描程序的速度，应仅用于故障排除   。 有关详细信息，请参阅 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet 的 eportLevel 参数  。

- 文件自身：
    
    - Excel 文件，除了 Office 文件是更快地扫描比 PDF 文件。
    
    - 扫描未受保护的文件比扫描受保护的文件耗时更短。
    
    - 扫描大型文件明显比扫描小文件耗时更多。

- 此外：
    
    - 确认运行扫描程序的服务帐户仅具有[扫描程序先决条件](#prerequisites-for-the-azure-information-protection-scanner)部分中记录的权限，然后再将[高级客户端属性](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner)配置为禁用扫描程序的低完整性级别。
    
    - 在使用[备选配置](#using-the-scanner-with-alternative-configurations)将默认标签应用于所有文件时，扫描程序可以更快地运行，因为扫描程序不检查文件内容。
    
    - 如果你使用[替换配置](#using-the-scanner-with-alternative-configurations)标识所有自定义条件和已知敏感信息类型，扫描程序的运行速度会更慢。
    

## <a name="list-of-cmdlets-for-the-scanner"></a>适用于扫描程序的 cmdlet 列表

由于现在从 Azure 门户配置扫描程序，因此现已弃用配置的数据存储库的先前版本的 cmdlet 和扫描的文件类型列表。 

保留的 cmdlet 包括用于安装和升级扫描程序、更改扫描程序配置数据库和配置文件、更改本地报告级别以及导入已断开连接的计算机的配置设置的 cmdlet。 

扫描程序的当前版本支持的 cmdlet 的完整列表： 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>扫描程序的事件日志 ID 和说明

利用以下部分，确定扫描程序可能的事件 ID 和说明。 这些事件记录在扫描程序服务的服务器上、Windows 应用程序和服务事件日志和 Azure 信息保护中   。

-----

信息 910 

**扫描程序周期已开始。**

当扫描程序服务启动并开始扫描指定数据存储库中的文件时，会记录此事件。

----

信息 911 

**扫描程序周期已结束。**

扫描程序完成手动扫描，或完成连续计划的一个周期后，会记录此事件。

如果扫描程序配置为手动运行（而不是连续运行），要再次扫描文件，请在扫描程序配置文件中将“计划”  设置为“手动”  或“始终”  ，然后重启服务。

----

## <a name="next-steps"></a>后续步骤

想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读技术案例研究：[Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)（使用 Azure 信息保护扫描程序自动执行数据保护）。

你可能想知道：[Windows Server FCI 和 Azure 信息保护扫描程序有何区别？](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 要详细了解此方案及使用 PowerShell 的其他方案，请参阅[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。

