---
title: 测试 从 AD RMS 迁移到 Azure Rights Management
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: TEST
author: Cabailey
---
# 之前：从 AD RMS 迁移到 Azure Rights Management
使用下面的一组指令将 Active Directory 权限管理服务 (AD RMS) 部署迁移到 Azure Rights Management (Azure RMS)。 迁移之后，用户将仍然可以访问你的组织使用 AD RMS 来保护的文档和电子邮件，新保护的内容将使用 Azure RMS。

不确定这种 AD RMS 迁移是否适合你的组织？

-   有关 Azure RMS 的简介、它可以解决的业务问题、它对管理员和用户来说是什么样子，以及它是如何工作的，请参阅 [Azure Rights Management 是什么？](what-is-azure-rms.md)

-   有关 Azure RMS 与 AD RMS 的比较，请参阅[比较 Azure Rights Management 和 AD RMS](compare-azure-rms-ad-rms.md)。

## 将 AD RMS 迁移到 Azure RMS 的先决条件
在开始迁移到 Azure RMS 之前，请确保具备以下先决条件，并确保你了解所有限制。

|要求|更多信息|
|---------------|--------------------|
|支持的 RMS 部署|AD RMS 的所有版本（从 Windows Server 2008 到 Windows Server 2012 R2）均支持迁移到 Azure RMS：<br /><br />Windows Server 2008（x86 或 x64）<br /><br />Windows Server 2008 R2 (x64)<br /><br />Windows Server 2012 (x64)<br /><br />Windows Server 2012 R2 (x64)<br /><br />支持所有有效的 AD RMS 拓扑：<br /><br />单个林、单个 RMS 群集<br /><br />单个林、多个仅授权 RMS 群集<br /><br />多个林、多个 RMS 群集<br /><br />**注意**：默认情况下，多个 RMS 群集将迁移到单个 Azure RMS 租户。 如果你想要迁移到不同的 RMS 租户，必须将它们视为不同的迁移。 不能将一个 RMS 群集的密钥导入到多个 Azure RMS 租户。|
|运行 Azure RMS（包括 Azure RMS 租户（未激活））的所有要求|请参阅 [Azure Rights Management 的要求](requirements-azure-rms.md)。<br /><br />尽管在从 AD RMS 迁移之前你必须拥有 Azure RMS 租户，但我们建议在迁移之前不要激活 Rights Management 服务。 迁移过程包括此步骤，在从 AD RMS 导出密钥和模板并将其导入到 Azure RMS 之后执行此操作。 但是，如果 Azure RMS 已激活，你仍可以从 AD RMS 迁移。|
|为 Azure RMS 做准备：<br /><br />在本地目录和 Azure Active Directory 之间进行目录同步<br /><br />在 Azure Active Directory 中已启用邮件的组|请参阅[准备 Azure Rights Management](prepare.md)。|
|如果你已使用过 Exchange Server 的信息权限管理 (IRM) 功能（例如，传输规则和 Outlook Web Access）或带 AD RMS 的 SharePoint Server：<br /><br />为这些服务器上未提供 IRM 的较短期间拟定计划|在迁移后，你可以继续将这些服务器上的 IRM 与 Azure RMS 一起使用。 但是，其中一个迁移步骤是暂时禁用 IRM 服务、安装并配置连接器、重新配置服务器，然后重新启用 IRM。<br /><br />在迁移过程中，只有这一步会出现服务中断。|
限制：

-   虽然迁移过程支持将服务器授权证书 (SLC) 密钥迁移到 Azure RMS 的硬件安全模块 (HSM)，但 Exchange Online 目前不支持此配置。 如果你希望在迁移到 Azure RMS 之后获得 Exchange Online 的完整 IRM 功能，必须[由 Microsoft 管理](http://technet.microsoft.com/library/dn440580.aspx)你的 Azure RMS 租户密钥。 你也可以自行管理 Azure RMS 租户 (BYOK)，在这种情况下，Exchange Online 的 IRM 功能将会受限。 有关将 Exchange Online 与 Azure RMS 配合使用的详细信息，请参阅[步骤 6。为 Exchange Online 配置 IRM 集成](#BKMK_Step6Migration)。

-   如果你的软件和客户端不受 Azure RMS 支持，则它们将不能保护或使用受 Azure RMS 保护的内容。 请务必查看 [Azure Rights Management 的要求](requirements-azure-rms.md)主题中的“支持的应用程序和客户端”部分。

-   如果你将本地密钥作为存档导入 Azure RMS（在导入过程中未将 TPD 设置为活动）并在分阶段迁移过程中分批迁移用户，则 AD RMS 中保留的用户将无法访问已迁移用户最近保护的内容。 在这种情况下，请尽量缩短迁移持续时间，并以逻辑批的形式迁移用户，以便在用户相互协作的情况下会一起迁移。

    如果你在导入过程中将 TPD 设置为活动，则不存在这种限制，因为所有用户将使用同一密钥保护内容。 我们建议采用这种配置，因为这样你就可以根据自己的步调单独迁移所有用户。

-   如果你与外部合作伙伴协作（例如，通过使用受信任的用户域或联合），则在你迁移的同时或之后尽早的时间，这些合作伙伴也必须迁移到 Azure RMS。 若要继续访问你的组织以前使用 AD RMS 保护的内容，这些合作伙伴必须进行与你进行的更改（在本文档中提供了这些更改）类似的客户端配置更改。

    由于你的合作伙伴进行的配置可能有所变动，确切说明此重新配置已超出了本文档的范围。 有关帮助，请与 Microsoft 客户支持服务 (CSS) 联系。

## 将 AD RMS 迁移到 Azure RMS 的步骤

|迁移步骤|更多信息|
|------------------|--------------------|
|**1.下载“Azure RMS 管理”管理工具**|有关说明，请参阅 [步骤 1：下载“Azure Rights Management”管理工具](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step1Migration)。|
|**2.从 AD RMS 中导出配置数据并将其导入到 Azure RMS 中**|将 AD RMS 中的配置数据（密钥、模板、URL）导出到 XML 文件，然后使用 Import-AadrmTpd Windows PowerShell cmdlet 将该文件上载到 Azure RMS。 可能需要其他步骤，具体取决于你的 AD RMS 密钥配置：<br /><br />**软件保护密钥到软件保护密钥的迁移**：集中管理的基于密码的密钥迁移到由 Microsoft 管理的 Azure RMS 租户密钥。 这是最简单的迁移路径，并且无需执行任何附加步骤。<br /><br />**HSM 保护密钥到 HSM 保护密钥的迁移**：将 HSM 存储的 AD RMS 密钥迁移到客户管理的 Azure RMS 租户密钥（“自带密钥”方案，简称 BYOK）。 这需要执行附加步骤，以将密钥从本地 Thales HSM 传输到 Azure RMS HSM。 现有的 HSM 保护密钥必须受模块保护；BYOK 工具集不支持 OCS 保护密钥。<br /><br />**软件保护密钥到 HSM 保护密钥的迁移**：AD RMS 中集中管理的基于密码的密钥迁移到由客户管理的 Azure RMS 租户密钥（“携带你自己的密钥”或 BYOK 方案）。 这需要的配置最多，因为你必须先提取软件密钥并将其导入到本地 HSM 中，然后再执行附加步骤以将该密钥从本地 Thales HSM 传输到 Azure RMS HSM。<br /><br />有关说明，请参阅[步骤 2：从 AD RMS 中导出配置数据并将其导入到 Azure RMS 中](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step2Migration)。|
|**3.激活你的 RMS 租户**|如果可能，请在执行导入过程之后而不是之前执行此步骤。<br /><br />有关详细信息和说明，请参阅[步骤 3：激活你的 RMS 租户](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration)。|
|**4.配置导入的模板**|当你导入权限策略模板时，系统会将其状态存档。 如果你希望用户能够查看并使用这些模板，则必须在 Azure 经典门户中将模板状态更改为“已发布”。<br /><br />有关说明，请参阅[步骤 4：配置导入的模板](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step4Migration)。|
|**5.将客户端重新配置为使用 Azure RMS**|必须将现有 Windows 计算机重新配置为使用 Azure RMS 服务而不是 AD RMS。 此步骤适用于你组织中的计算机以及合作伙伴组织(如果你在运行 AD RMS 时已与其协作)中的计算机。<br /><br />此外，如果你部署了 [移动设备扩展](http://technet.microsoft.com/library/dn673574.aspx) 以支持移动设备（如 iOS 手机和 iPad、Android 手机和平板电脑、Windows phone 以及 Mac 计算机），你必须删除 DNS 中重定向这些客户端的 SRV 记录以使用 AD RMS。<br /><br />有关说明，请参阅[步骤 5：将客户端重新配置为使用 Azure RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step5Migration)。|
|**6.配置 IRM 与 Exchange Online 的集成**|如果要将 Exchange Online 与 Azure RMS 配合使用，则必须执行此步骤。<br /><br />有关说明，请参阅[步骤 6：为 Exchange Online 配置 IRM 集成](#BKMK_Step6Migration)。|
|**7.部署 RMS 连接器**|如果要将以下任何本地服务与 Azure RMS 配合使用，此步骤是必需的：<br /><br />Exchange Server（例如，传输规则和 Outlook Web Access）<br /><br />SharePoint Server<br /><br />运行文件分类基础结构的 Windows Server<br /><br />有关说明，请参阅[步骤 7：部署 RMS 连接器](#BKMK_Step7Migration)。|
|**8.解除 AD RMS 的授权**|当你已确认所有客户端均使用 Azure RMS 而不再访问 AD RMS 服务器，你可以解除 AD RMS 部署的授权。<br /><br />有关说明，请参阅[步骤 8：解除 AD RMS 的授权](#BKMK_Step8Migration)。|
|**9.重新键入你的 Azure RMS 租户密钥**|如果在迁移前未运行加密模式 2，此步骤是必需的；对于所有迁移来说，此步骤是可选的但建议执行，以帮助保护 Azure RMS 租户密钥的安全性。<br /><br />有关说明，请参阅[步骤 9：重新键入你的 Azure RMS 租户密钥](#BKMK_Step9Migration)。|

### <a name="BKMK_Step1Migration"></a>步骤 1：下载 Azure Rights Management 管理工具
转到 Microsoft 下载中心并下载 [Azure Rights Management 管理工具](http://go.microsoft.com/fwlink/?LinkId=257721)，其中包含 Windows PowerShell 的 Azure RMS 管理模块。

### <a name="BKMK_Step2Migration"></a>步骤 2。 从 AD RMS 中导出配置数据并将其导入到 Azure RMS 中
此步骤是一个分为两部分的过程：

1.  通过将受信任的发布域 (TPD) 导出到 .xml 文件，从 AD RMS 导出配置数据。 此过程对于所有迁移是相同的。

2.  将配置数据导入到 Azure RMS。 此步骤具有不同处理，具体取决于你的当前 AD RMS 部署配置以及 Azure RMS 租户密钥的首选拓扑。

#### 从 AD RMS 导出配置数据
在所有 AD RMS 群集中，针对已保护你组织内容的所有受信任的发布域执行以下过程。 无需在仅授权群集上运行此过程。

> [!NOTE]
> 如果你使用的是 Windows Server 2003 Rights Management，请按照 [从 Windows RMS 迁移到不同基础结构中的 AD RMS](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) 主题中的过程 [导出 SLC、TUD、TPD 和 RMS 私钥](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx)（而不是按上述说明）进行操作。

###### 导出配置数据（受信任的发布域信息）

1.  以具有 AD RMS 管理权限的用户身份登录到 AD RMS 群集。

2.  从 AD RMS 管理控制台 (**Active Directory Rights Management Services**)，展开 AD RMS 群集名称，再展开“信任策略”****，然后单击“受信任的发布域”****。

3.  在结果窗格中，选择受信任的发布域，然后在操作窗格中单击“导出受信任的发布域” ****。

4.  在“导出受信任的发布域”对话框中 **** ：

    -   单击“另存为”并将其保存到所选的路径和文件名 **** 。 请确保指定 **.xml** 作为文件扩展名（此扩展名不会自动追加）。

    -   指定并确认一个强密码。 请记住此密码，因为稍后在将配置数据导入到 Azure RMS 时，将需要此密码。

    -   不要选中将受信任的域文件保存在 RMS 版本 1.0 中的复选框。

当你已导出所有受信任的发布域后，便可以启动将此数据导入到 Azure RMS 的过程了。

#### 将配置数据导入到 Azure RMS
此步骤的确切过程取决于你的当前 AD RMS 部署配置以及 Azure RMS 租户密钥的首选拓扑。

你的当前 AD RMS 部署将对服务器许可方证书 (SLC) 密钥使用以下配置之一：

-   AD RMS 数据库中的密码保护。 这是默认设置。

-   通过使用 Thales 硬件安全模块 (HSM) 进行 HSM 保护。

-   通过使用 Thales 以外的供应商提供的硬件安全模块 (HSM) 进行 HSM 保护。

-   通过使用外部加密提供程序进行密码保护。

> [!NOTE]
> 有关将硬件安全模块与 AD RMS 配合使用的详细信息，请参阅 [将 AD RMS 与硬件安全模块配合使用](http://technet.microsoft.com/library/jj651024.aspx)。

两个 Azure RMS 租户密钥拓扑选项包括：Microsoft 管理你的租户密钥（**由 Microsoft 管理**），或者你自行管理租户密钥（**由客户管理**）。 如果你自行管理 Azure RMS 租户密钥，则这有时也称为“自带密钥”(BYOK)，需要 Thales 提供的硬件安全模块 (HSM)。 有关详细信息，请参阅[计划和实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)主题中的[选择你的租户密钥拓扑：由 Microsoft 管理（默认设置）或由你管理 (BYOK)](plan-implement-tenant-key.md#BKMK_ChooseTenantKey) 部分。

> [!IMPORTANT]
> Exchange Online 当前与 Azure RMS BYOK 不兼容。  如果你想要在迁移后使用 BYOK 并打算使用 Exchange Online，请务必了解，这种配置会缩减 Exchange Online 的 IRM 功能。 请查看[计划和实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)主题中的 [BYOK 定价和限制](plan-implement-tenant-key.md#BKMK_Pricing)部分，以帮助选择最适合你的迁移方案的 Azure RMS 租户密钥拓扑。

使用下表来确定要使用哪个过程进行迁移。 不支持未列出的组合。

|当前的 AD RMS 部署|已选择 Azure RMS 租户密钥拓扑|迁移说明|
|-----------------------------|----------------------------------------|--------------------------|
|AD RMS 数据库中的密码保护|由 Microsoft 管理|请参阅此表后面的**软件保护密钥到软件保护密钥的迁移**过程。<br /><br />这是最简单的迁移路径，只需要将配置数据传输到 Azure RMS。|
|通过使用 Thales nShield 硬件安全模块 (HSM) 进行 HSM 保护|由客户管理 (BYOK)|请参阅此表后面的 **HSM 保护密钥到 HSM 保护密钥的迁移**过程。<br /><br />这需要 BYOK 工具集和以下两组步骤：将密钥从本地 HSM 传输到 Azure RMS HSM，然后将配置数据传输到 Azure RMS。|
|AD RMS 数据库中的密码保护|由客户管理 (BYOK)|请参阅此表后面的**软件保护密钥到 HSM 保护密钥的迁移**过程。<br /><br />这需要 BYOK 工具集和以下三组步骤：首先提取软件密钥并将其导入到本地 HSM，然后将密钥从本地 HSM 传输到 Azure RMS HSM，最后将配置数据传输到 Azure RMS。|
|通过使用 Thales 以外的供应商提供的硬件安全模块 (HSM) 进行 HSM 保护|由客户管理 (BYOK)|与 HSM 供应商联系以获取有关如何将密钥从此 HSM 传输到 Thales nShield 硬件安全模块 (HSM) 的说明。 然后遵照此表后面的 **HSM 保护密钥到 HSM 保护密钥的迁移**过程中的说明。|
|通过使用外部加密提供程序进行密码保护|由客户管理 (BYOK)|与加密提供程序的供应商联系以获取有关如何将密钥传输到 Thales nShield 硬件安全模块 (HSM) 的说明。 然后遵照此表后面的 **HSM 保护密钥到 HSM 保护密钥的迁移**过程中的说明。|
在开始这些过程之前，请确保你可以访问先前在导出受信任的发布域时创建的 .xml 文件。 例如，可以将这些文件保存到从 AD RMS 服务器移到接入 Internet 的工作站的 U 盘。

> [!NOTE]
> 但是，你将存储这些文件，请使用安全最佳做法来保护它们，因为此数据包含你的私钥。

##### 软件保护密钥到软件保护密钥的迁移
使用此过程将 AD RMS 配置导入到 Azure RMS，以生成由 Microsoft 管理的 Azure RMS 租户密钥。

###### 将配置数据导入到 Azure RMS

1.  在连接 Internet 的工作站上，下载并安装用于 Azure RMS 的 Windows PowerShell 模块（最低版本 2.1.0.0），其中包括 [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet。

    > [!TIP]
    > 如果你以前已下载并安装过该模块，请通过运行以下命令检查版本号： `(Get-Module aadrm -ListAvailable).Version`

    有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。

2.  使用“以管理员身份运行” **** 选项启动 Windows PowerShell，然后使用 [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) cmdlet 连接到 Azure RMS 服务：

    ```
    Connect-AadrmService
    ```
    出现提示时，输入 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 租户管理员凭据（通常，将使用作为 Azure Active Directory 或 Office 365 的全局管理员的帐户）。

3.  使用 [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet 上载首先导出的受信任发布域 (.xml) 文件。 如果你有多个 .xml 文件（因为有多个受信任发布域），请选择包含已导出受信任发布域的文件，你要在 Azure RMS 中使用该文件来在迁移后保护内容。 使用以下命令：

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    例如：**Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    出现提示时，输入你先前指定的密码，并确认要执行此操作。

4.  该命令完成后，请对你通过导出受信任发布域创建的每个剩余 .xml 文件重复执行步骤 3。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。 例如：**Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) cmdlet 断开与 Azure RMS 服务的连接：

    ```
    Disconnect-AadrmService
    ```

现在可以转到[步骤 3。激活你的 RMS 租户](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration)。

##### HSM 保护密钥到 HSM 保护密钥的迁移

> [!NOTE]
> 这些说明假定你的 AD RMS 密钥受模块保护。 这是常见的情况。 如果你的 AD RMS 密钥受 OCS 保护，请在按这些说明操作之前联系 [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key)。

此过程分为两部分，可将 HSM 密钥和 AD RMS 配置导入到 Azure RMS，以生成由你管理的 Azure RMS 租户密钥 (BYOK)。

你必须先打包 HSM 密钥以便随时可将其传输到 Azure RMS，然后再将其连同配置数据一起导入。

###### 第 1 部分：打包 HSM 密钥以便随时可将其传输到 Azure RMS

1.  使用过程**生成并传输租户密钥 - 通过 Internet**，并按照[计划和实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)中的“实现自带密钥 (BYOK)”[](plan-implement-tenant-key.md#BKMK_ImplementBYOK)部分中的步骤进行操作，但以下情况例外：

    -   不要遵循 **生成你的租户密钥**中的步骤，因为你已从 AD RMS 部署获得等效物。 你必须标识 AD RMS 服务器使用的从 Thales 安装获得的密钥，并在迁移期间使用此密钥。 Thales 加密的密钥文件通常在本地服务器上名为 **key_(keyAppName)_(keyIdentifier)**。

    -   不要遵循**将你的租户密钥传送到 Azure RMS** 中的步骤，因为此操作使用 Add-AadrmKey 命令。  你应该在上载所导出的受信任发布域时，使用 Import-AadrmTpd 命令传输你准备好的 HSM 密钥。

2.  在已连接 Internet 的工作站上，通过 Windows PowerShell 会话重新连接到 Azure RMS 服务。

现在，你已经为 Azure RMS 准备好了 HSM 密钥，接下来可以导入 HSM 密钥文件和 AD RMS 配置数据。

###### 第 2 部分：将 HSM 密钥和配置数据导入到 Azure RMS

1.  仍在连接 Internet 的工作站上的 Windows PowerShell 会话中，上载首先导出的受信任发布域 (.xml) 文件。 如果你有多个 .xml 文件（因为有多个受信任发布域），请选择包含与 HSM 密钥对应的已导出受信任发布域的文件，你要在 Azure RMS 中使用该文件来在迁移后保护内容。 使用以下命令：

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    例如：**Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    出现提示时，输入你先前指定的密码，并确认要执行此操作。

2.  该命令完成后，请对你通过导出受信任发布域创建的每个剩余 .xml 文件重复执行步骤 1。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。  例如：**Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet 断开与 Azure RMS 服务的连接：

    ```
    Disconnect-AadrmService
    ```

现在可以转到[步骤 3。激活你的 RMS 租户](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration)。

##### 软件保护密钥到 HSM 保护密钥的迁移
此过程分为三部分，用于将 AD RMS 配置导入到 Azure RMS，以生成由你管理的 Azure RMS 租户密钥 (BYOK)。

必须首先从配置数据中提取服务器许可方证书 (SLC) 密钥并将该密钥传输到本地 Thales HSM，然后打包 HSM 密钥并将其传输到 Azure RMS，最后导入配置数据。

###### 第 1 部分：从配置数据中提取 SLC，并将密钥导入到本地 HSM

1.  按照[计划和实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)主题中的“实现自带密钥 (BYOK)”[](plan-implement-tenant-key.md#BKMK_ImplementBYOK)部分中的以下步骤进行操作：

    -   **生成和传送租户密钥 – 通过 Internet**：**准备连接你的 Internet 的工作站**

    -   **生成和传送租户密钥 – 通过 Internet**： **准备你的未连接工作站**

    不用按照这些步骤生成租户密钥，因为你在导出的配置数据 (.xml) 文件中已有等效项。 你将改为运行命令以从该文件中提取此密钥并将其导入到本地 HSM。

2.  在断开连接的工作站上，运行以下命令：

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    例如，对于北美地区：**KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    其他信息:

    -   ImportRmsCentrallyManagedKey 参数指示该操作是导入 SLC 密钥。

    -   如果你未在命令中指定密码，则将提示你指定它。

    -   KeyIdentifier 参数指定用于创建密钥文件名的密钥友好名称。 你必须使用仅小写的 ASCII 字符。

    -   ExchangeKeyPackage 参数指定特定于区域的密钥交换密钥 (KEK) 软件包，该软件包的名称以“BYOK-KEK-pkg-”开头。

    -   NewSecurityWorldPackage 参数指定特定于区域的安全体系包，该包的名称以“BYOK-SecurityWorld-pkg-”开头。

    此命令将生成以下项：

    -   HSM 密钥文件：%NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   已删除 SLC 的 RMS 配置数据文件：%NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  如果你有多个 RMS 配置数据文件，请对这些文件的其余部分重复执行步骤 2。

现在，你已提取 SLC 使其成为基于 HSM 的密钥，你已可以将其打包并传输到 Azure RMS 了。

###### 第 2 部分：打包 HSM 密钥并将其传输到 Azure RMS

1.  按照[计划和实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)中的[实现自带密钥 (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) 部分中的以下步骤进行操作：

    -   **生成和传送租户密钥 – 通过 Internet**： **准备要传送的租户密钥**

    -   **生成和传送租户密钥 – 通过 Internet**： **将你的租户密钥传送到 Azure RMS**

现在，你已将 HSM 密钥传输到 Azure RMS，已可以导入 AD RMS 配置数据（其中只包含指向新传输的租户密钥的指针）了。

###### 第 3 部分：将配置数据导入到 Azure RMS

1.  仍在连接 Internet 的工作站上的 Windows PowerShell 会话中，从断开连接的工作站复制删除了 SLC 的 RMS 配置文件 (%NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  上载第一个文件。 如果你有多个 .xml 文件（因为有多个受信任发布域），请选择包含与 HSM 密钥对应的已导出受信任发布域的文件，你要在 Azure RMS 中使用该文件来在迁移后保护内容。 使用以下命令：

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    例如：**Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    出现提示时，输入你先前指定的密码，并确认要执行此操作。

3.  该命令完成后，请对你通过导出受信任发布域创建的每个剩余 .xml 文件重复执行步骤 2。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。 例如：**Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet 断开与 Azure RMS 服务的连接：

    ```
    Disconnect-AadrmService
    ```

现在可以转到[步骤 3。激活你的 RMS 租户](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration)。

### <a name="BKMK_Step3Migration"></a>步骤 3. 激活你的 RMS 租户
[激活 Azure Rights Management](activate-service.md) 主题中全面说明了此步骤。

> [!TIP]
> 如果你有 Office 365 订阅，则可以从 Office 365 管理中心或 Azure 经典门户激活 Azure RMS。 建议你使用 Azure 经典门户，因为你将使用该管理门户来完成下一步操作。

**如果 Azure RMS 租户已激活，会怎么样？** 如果已为你的组织激活了 Azure RMS 服务，则用户可能已使用 Azure RMS 和自动生成的租户密钥（及默认模板）而不是 AD RMS 中的现有密钥（和模板）来保护内容。 在 Intranet 中妥善管理的计算机上不太可能会发生这种情况，因为这些计算机会自动根据 AD RMS 基础结构进行配置。 但是，在工作组计算机或很少连接到 Intranet 的计算机上，可能会发生这种情况。 遗憾的是，这些计算机也很难识别，正因如此，我们建议在从 AD RMS 导入配置数据之前不要激活该服务。

如果你的 Azure RMS 租户已激活并且可以识别这些计算机，请确保根据步骤 5 中所述，在这些计算机上运行 CleanUpRMS_RUN_Elevated.cmd 脚本。 运行此脚本会强制这些计算机重新初始化用户环境，以便下载更新的租户密钥和导入的模板。

### <a name="BKMK_Step4Migration"></a>步骤 4. 配置导入的模板
由于所导入的模板具有“已存档”****的默认状态，如果你希望用户能够将这些模板用于 Azure RMS，必须将此状态更改为“已发布”****。

此外，如果 AD RMS 中的模板使用 **ANYONE** 组，则当你将这些模板导入 Azure RMS 时，系统会自动删除该组；你必须将相应的组/用户和相同的权限手动添加到已导入的模板中。 Azure RMS 的等效组名为 **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<tenant_name>.onmicrosoft.com**。 例如，此组可能看上去与用于 Contoso 的下例类似：**AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**。

如果你不确定你的 AD RMS 模板是否包括 ANYONE 组，请在此步骤中展开[示例 Windows PowerShell 脚本，用于识别包括 ANYONE 组的 AD RMS 模板](#BKMK_ScriptForANYONE)部分以复制并使用示例 PowerShell 脚本来标识这些模板。 有关将 Windows PowerShell 用于 AD RMS 的详细信息，请参阅[使用 Windows PowerShell 管理 AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx)。

你可以看到组织自动创建的组，前提是将某个默认权限策略模板复制到 Azure 经典门户中，然后确定“权限”****页上的“用户名”****。 但是，你不能使用经典门户将该组添加到已手动创建或导入的模板中，而是必须使用以下 Azure RMS PowerShell 选项之一：

-   使用 [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) PowerShell cmdlet 将“AllStaff”组和权限定义为权限定义对象，然后除了 ANYONE 组外，还要再次对原始模板中已被授予权限的每个其他组或用户运行此命令。 然后，使用 [Set-AadrmTemplateProperty](https://msdn.microsoft.com/en-us/library/azure/dn727076.aspx) cmdlet 将所有这些权限定义对象添加到模板中。

-   使用 [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) cmdlet 将模板导出到 .XML 文件中，可通过编辑该文件将“AllStaff”组和权限添加到现有组和权限中，然后使用 [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) cmdlet 将所做的更改导回到 Azure RMS 中。

> [!NOTE]
> 这个相应的“AllStaff”组并非完全等同于 AD RMS 中的 ANYONE 组：“AllStaff”组包括你的 Azure 租户中的所有用户，而 ANYONE 组则包括所有经过身份验证的用户，这些用户可能不在你的组织中。
> 
> 由于这两个组存在这种差异，你可能还需要向“AllStaff”组添加外部用户。 目前不支持对组使用外部电子邮件地址。

你从 AD RMS 导入的模板的外观和行为就像你可以在 Azure 经典门户中创建的自定义模板一样。 若要将导入的模板更改为“已发布”，以便用户可以查看它们以及从应用程序中选择它们，或者要对模板进行其他更改，请参阅[为 Azure Rights Management 配置自定义模板](configure-custom-templates.md)。

> [!TIP]
> 为了在迁移过程中向用户提供更一致的体验，请不要对导入的模板进行这两项更改以外的其他更改，请不要发布 Azure RMS 附带的两个默认模板，也不要在此时创建新模板。 请等到迁移过程完成并已解除 AD RMS 服务器的授权。

#### <a name="BKMK_ScriptForANYONE"></a>示例 Windows PowerShell 脚本，用于识别包括 ANYONE 组的 AD RMS 模板
本节包含示例脚本，用于帮助你确定定义有 ANYONE 组的 AD RMS 模板，如前一节所述。

**免责声明：**此示例脚本在任何 Microsoft 标准支持计划或服务下均不受支持。 此示例脚本按原样提供，不提供任何形式的保证。*

```
import-module adrmsadmin 

New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force 

$ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate

foreach($Template in $ListofTemplates) 
{ 
                $templateID=$Template.id

                $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright

     $templateName=$Template.DefaultDisplayName 

        if ($rights.usergroupname -eq "anyone")

                         {
                           $templateName = $Template.defaultdisplayname

                           write-host "Template " -NoNewline

                           write-host -NoNewline $templateName -ForegroundColor Red

                           write-host " contains rights for " -NoNewline

                           write-host ANYONE  -ForegroundColor Red
                         }
 } 
Remove-PSDrive MyRmsAdmin -force
```

### <a name="BKMK_Step5Migration"></a>步骤 5. 将客户端重新配置为使用 Azure RMS
对于 Windows 客户端：

1.  [下载迁移脚本](http://go.microsoft.com/fwlink/?LinkId=524619)：

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    这些脚本将重置 Windows 计算机上的配置，以使其将使用 Azure RMS 服务而不是 AD RMS。

2.  按照重定向脚本 (Redirect_OnPrem.cmd) 中的说明修改脚本，使其指向新的 Azure RMS 租户。

3.  在 Windows 计算机上，使用提升的特权，在用户的上下文中运行这些脚本。

对于移动设备客户端和 Mac 计算机：

-   删除在部署 [AD RMS 移动设备扩展](http://technet.microsoft.com/library/dn673574.aspx)时创建的 DNS SRV 记录。

#### 由迁移脚本进行的更改
本节介绍迁移脚本进行的更改。 你只能将此信息出于参考目的，或用于故障排除，或者用于你想要自己进行这些更改的场合。

CleanUpRMS_RUN_Elevated.cmd：

-   删除 %userprofile%\AppData\Local\Microsoft\DRM 和 %userprofile%\AppData\Local\Microsoft\MSIPC 文件夹的内容，包括任何子文件夹以及具有长文件名的任何文件。

-   删除以下注册表项的内容：

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   删除以下注册表值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd：

-   为以下每个位置下作为参数提供的每个 URL 创建以下注册表值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    每一项均具有 REG_SZ 值 **https://OldRMSserverURL/_wmcs/licensing**，其数据采用以下格式：**https://&lt;YourTenantURL&gt;/_wmcs/licensing**。

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* 采用以下格式：**{GUID}.rms.[Region].aadrm.com**。
    > 
    > 例如：5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > 在对 Azure RMS 运行 **Get-AadrmConfiguration** cmdlet 时，可以通过标识 [RightsManagementServiceId](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) 值找到此值。

### <a name="BKMK_Step6Migration"></a>步骤 6. 为 Exchange Online 配置 IRM 集成
如果以前已将 TDP 从 AD RMS 导入 Exchange Online，则必须删除此 TDP，以避免在迁移到 Azure RMS 后发生模板和策略冲突。 为此，请在 Exchange Online 中使用 [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) cmdlet。

如果你选择了 **Microsoft 管理**的 Azure RMS 租户密钥拓扑：

-   查看[为 Azure Rights Management 配置应用程序](configure-applications.md)主题中的 [Exchange Online: IRM 配置](configure-applications.md#BKMK_ExchangeOnline)部分。 此部分介绍了一些典型的命令，运行这些命令可以连接到 Exchange Online 服务、从 Azure RMS 导入租户密钥，以及为 Exchange Online 启用 IRM 功能。 完成这些步骤后，你将获得 Exchange Online 的完整 RMS 功能。

如果你选择了**客户管理 (BYOK)** 的 Azure RMS 租户密钥拓扑：

-   Exchange Online 的 RMS 功能将有所削减，如[计划和实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)主题中的 [BYOK 定价和限制](plan-implement-tenant-key.md#BKMK_Pricing)部分所述。

### <a name="BKMK_Step7Migration"></a>步骤 7. 部署 RMS 连接器
如果你已将 Exchange Server 或 SharePoint Server 的信息权限管理 (IRM) 功能与 AD RMS 一起使用，则必须先在这些服务器上禁用 IRM 并删除 AD RMS 配置。 然后，部署 Rights Management (RMS) 连接器，该连接器将充当本地服务器和 Azure RMS 之间的通信接口（中继）。

此步骤的最后一步，如果你已将多个用于保护电子邮件的 TPD 导入到 Azure RMS ，则必须手动编辑 Exchange Server 计算机上的注册表，将所有 TPD URL 重定向到 RMS 连接器。

> [!NOTE]
> 在开始之前，请在 [Azure Rights Management 要求](requirements-azure-rms.md)主题中的[支持 Azure RMS 的应用程序](requirements-azure-rms.md#BKMK_SupportedApplications)部分的“支持 Azure RMS 的本地服务器”中，核实 RMS 连接器支持的本地服务器的受支持版本。

##### 在 Exchange 服务器上禁用 IRM 并删除 AD RMS 配置

1.  在每个 Exchange 服务器上，找到以下文件夹，并删除该文件夹中的所有条目：\ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  在任一 Exchange 服务器上，使用 Exchange [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) cmdlet，先对向内部收件人发送的消息禁用 IRM 功能：

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  然后使用同一 cmdlet 对向外部收件人发送的消息禁用 IRM 功能：

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  接下来，使用同一 cmdlet 在 Microsoft Office Outlook Web App 和 Microsoft Exchange ActiveSync 中禁用 IRM：

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  最后，使用同一 cmdlet 清除所有缓存的证书：

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  现在，在每个 Exchange Server 上重置 IIS，例如通过以管理员身份运行命令提示符并键入 **iisreset**。

##### 在 SharePoint 服务器上禁用 IRM 并删除 AD RMS 配置

1.  请确保没有文档从 RMS 保护的库中签出。 如果有，这些文档将在此过程结束时变为不可访问。

2.  在 SharePoint 管理中心网站的“快速启动”****部分中，单击“安全性”****。

3.  在“安全性”****页的“信息策略”****部分中，单击“配置信息权限管理”****。

4.  在“信息权限管理”****页的“信息权限管理”****部分中，选择“不在此服务器上使用 IRM”****，然后单击“确定”****。

5.  在每台 SharePoint Server 计算机上，删除文件夹 \ProgramData\Microsoft\MSIPC\Server\*&lt;SID of the account running SharePoint Server&gt;* 的内容。

##### 安装并配置 RMS 连接器

-   使用[部署 Azure Rights Management 连接器](deploy-rms-connector.md)主题中的说明。

##### 对于仅 Exchange 和多个 TPD：编辑注册表

-   在每个 Exchange 服务器上，手动为每个已导入的附加 TPD 添加以下注册表项，将 TPD URL 重定向到 RMS 连接器。 这些注册表项特定于迁移，并且不是通过 Microsoft RMS 连接器的服务器配置工具添加的。

    进行这些注册表编辑时，请使用以下说明：

    -   将 *ConnectorFQDN* 替换为你在 DNS 中为连接器定义的名称。 例如 **rmsconnector.contoso.com**。

    -   对连接器 URL 使用 HTTP 或 HTTPS 前缀，具体取决于你已将连接器配置为使用 HTTP 还是使用 HTTPS 与本地服务器通信。

    **对于 Exchange 2013：**

    |注册表路径|类型|值|数据|
    |-----------------|--------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS Intranet Licensing URL&gt;/_wmcs/licensing|以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：<br /><br />http://&lt;connectorFQDN&gt;/_wmcs/licensing<br /><br />https://&lt;connectorName&gt;/_wmcs/licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS Extranet Licensing URL&gt;/_wmcs/licensing|以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：<br /><br />http://&lt;connectorFQDN&gt;/_wmcs/licensing<br /><br />https://&lt;connectorFQDN&gt;/_wmcs/licensing|
    **对于 Exchange Server 2010：**

    |注册表路径|类型|值|数据|
    |-----------------|--------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS Intranet Licensing URL&gt;/_wmcs/licensing|以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：<br /><br />http://&lt;connectorName&gt;/_wmcs/licensing<br /><br />https://&lt;connectorName&gt;/_wmcs/licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;AD RMS Extranet Licensing URL&gt;/_wmcs/licensing|以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：<br /><br />http://&lt;connectorName&gt;/_wmcs/licensing<br /><br />https://&lt;connectorName&gt;/_wmcs/licensing|

完成这些过程之后，请务必阅读[部署 Azure Rights Management 连接器](deploy-rms-connector.md)主题中的“后续步骤”****部分。

### <a name="BKMK_Step8Migration"></a>步骤 8. 解除 AD RMS 的授权
可选：从 Active Directory 中删除服务连接点 (SCP) 以防止计算机发现你的本地权限管理基础结构。 由于你在注册表中配置的重定向（例如，通过运行迁移脚本），此步骤是可选的。 若要删除服务连接点，请使用 [Rights Management Services 管理工具包](http://www.microsoft.com/download/details.aspx?id=1479)中的 AD SCP 注册工具。

监视 AD RMS 服务器的活动，例如，通过检查[系统运行状况报告中的请求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest 表](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)，或者[审核用户对受保护内容的访问权限](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)。 当你确认 RMS 客户端将不再与这些服务器进行通信，并且客户端成功使用 Azure RMS 时，你可以从这些服务器中删除 AD RMS 服务器角色。 当你调查为什么客户端未使用 Azure RMS 时，如果你使用的是专用服务器，你可能希望采取警告步骤，即先关闭服务器一段时间，以确保没有报告可能需要重新启动这些服务器以确保服务连续性的问题。

解除 AD RMS 服务器的授权后，你可能想要利用此机会来查看你在 Azure 经典门户中的模板并将其合并以使用户有较少的选项，或重新配置它们，或者甚至添加新模板。 这还将是发布默认模板的好时机。 有关详细信息，请参阅[为 Azure Rights Management 配置自定义模板](configure-custom-templates.md)。

### <a name="BKMK_Step9Migration"></a>步骤 9. 重新键入你的 Azure RMS 租户密钥
迁移完成时，如果 AD RMS 部署使用的是 RMS 加密模式 1，则此步骤是必需的，因为重新键入将创建使用 RMS 加密模式 2 的新租户密钥。 将 Azure RMS 与加密模式 1 配合使用仅在迁移过程中受支持。

迁移完成时，此步骤是可选的但建议使用（即使你已以 RMS 加密模式 2 运行），因为它可帮助保护你的 Azure RMS 租户密钥，使 AD RMS 密钥免遭潜在的安全漏洞的威胁。 当你重新键入 Azure RMS 租户密钥（也称为“滚动密钥”）时，将创建新的密钥，并将原始密钥存档。 但是，由于从一个密钥移到另一个密钥并不会立即发生，而是经过几周才会发生，请不要等到你怀疑原始密钥受到破坏再进行，而应在迁移完成时，立即重新键入你的 RMS 租户密钥。

若要重新键入你的 Azure RMS 租户密钥，请执行以下操作：

-   如果你的 RMS 租户密钥由 Microsoft 管理：致电 Microsoft 客户支持服务 (CSS)，并证明你是 RMS 租户管理员。

-   如果你的 RMS 租户密钥由你管理 (BYOK)：重复执行 BYOK 过程以通过 Internet 或亲自生成并创建新的密钥。

有关管理 RMS 租户密钥的详细信息，请参阅[你的 Azure Rights Management 租户密钥的操作](operations-tenant-key.md)。

## 另请参阅
[配置 Azure 权限管理](configuring-azure-rights-management.md)



<!--HONumber=Apr16_HO3-->


