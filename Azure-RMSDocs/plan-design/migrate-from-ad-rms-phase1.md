---
# required metadata

title: 从 AD RMS 迁移到 Azure Rights Management - 阶段 1 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 迁移阶段 1 - AD RMS 的服务器端配置
使用以下信息，完成从 AD RMS 迁移到 Azure Rights Management (Azure RMS) 的阶段 1。 这些过程涉及了[从 AD RMS 迁移到 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 中的步骤 1-4。


## 步骤 1：下载 Azure Rights Management 管理工具
转到 Microsoft 下载中心并下载 [Azure Rights Management 管理工具](http://go.microsoft.com/fwlink/?LinkId=257721)，其中包含 Windows PowerShell 的 Azure RMS 管理模块。

安装工具。 相关说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md)。

## 步骤 2。 从 AD RMS 中导出配置数据并将其导入到 Azure RMS 中
此步骤是一个分为两部分的过程：

1.  通过将受信任的发布域 (TPD) 导出到 .xml 文件，从 AD RMS 导出配置数据。 此过程对于所有迁移是相同的。

2.  将配置数据导入到 Azure RMS。 此步骤具有不同处理，具体取决于你的当前 AD RMS 部署配置以及 Azure RMS 租户密钥的首选拓扑。

### 从 AD RMS 导出配置数据
在所有 AD RMS 群集中，针对已保护你组织内容的所有受信任的发布域执行以下过程。 无需在仅授权群集上运行此过程。

> [!NOTE]
> 如果你使用的是 Windows Server 2003 Rights Management，请按照 [从 Windows RMS 迁移到不同基础结构中的 AD RMS](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) 文章中的[导出 SLC、TUD、TPD 和 RMS 私有密钥](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx)过程（而不是按上述说明）进行操作。

#### 导出配置数据（受信任的发布域信息）

1.  以具有 AD RMS 管理权限的用户身份登录到 AD RMS 群集。

2.  从 AD RMS 管理控制台 (**Active Directory Rights Management Services**)，展开 AD RMS 群集名称，再展开“信任策略”****，然后单击“受信任的发布域”****。

3.  在结果窗格中，选择受信任的发布域，然后在操作窗格中单击“导出受信任的发布域” ****。

4.  在“导出受信任的发布域”对话框中 **** ：

    -   单击“另存为”并将其保存到所选的路径和文件名 **** 。 请确保指定 **.xml** 作为文件扩展名（此扩展名不会自动追加）。

    -   指定并确认一个强密码。 请记住此密码，因为稍后在将配置数据导入到 Azure RMS 时，将需要此密码。

    -   不要选中将受信任的域文件保存在 RMS 版本 1.0 中的复选框。

当你已导出所有受信任的发布域后，便可启动将此数据从 Thales 导入 Azure RMS 硬件安全模块 (HSM) 的过程。 有关详细信息， 

### 将配置数据导入到 Azure RMS
此步骤的确切过程取决于你的当前 AD RMS 部署配置以及 Azure RMS 租户密钥的首选拓扑。

你的当前 AD RMS 部署将对服务器许可方证书 (SLC) 密钥使用以下配置之一：

-   AD RMS 数据库中的密码保护。 这是默认设置。

-   通过使用 Thales 硬件安全模块 (HSM) 进行 HSM 保护。

-   通过使用 Thales 以外的供应商提供的硬件安全模块 (HSM) 进行 HSM 保护。

-   通过使用外部加密提供程序进行密码保护。

> [!NOTE]
> 有关将硬件安全模块与 AD RMS 配合使用的详细信息，请参阅 [将 AD RMS 与硬件安全模块配合使用](http://technet.microsoft.com/library/jj651024.aspx)。

两个 Azure RMS 租户密钥拓扑选项包括：Microsoft 管理你的租户密钥（**由 Microsoft 管理**），或者你自行管理租户密钥（**由客户管理**）。 如果你自行管理 Azure RMS 租户密钥，则这有时也称为“自带密钥”(BYOK)，需要 Thales 提供的硬件安全模块 (HSM)。 有关详细信息，请参阅[计划并实施你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)文章。

> [!IMPORTANT]
> Exchange Online 当前与 Azure RMS BYOK 不兼容。  如果你想要在迁移后使用 BYOK 并打算使用 Exchange Online，请务必了解，这种配置会缩减 Exchange Online 的 IRM 功能。 请查看 [BYOK 定价和限制](byok-price-restrictions.md)中信息，以帮助选择最适合你的迁移防范的 Azure RMS 租户密钥拓扑。

使用下表来确定要使用哪个过程进行迁移。 不支持未列出的组合。

|当前的 AD RMS 部署|已选择 Azure RMS 租户密钥拓扑|迁移说明|
|-----------------------------|----------------------------------------|--------------------------|
|AD RMS 数据库中的密码保护|由 Microsoft 管理|请参阅此表后面的**软件保护密钥到软件保护密钥**的迁移过程。<br /><br />这是最简单的迁移路径，只需要将配置数据传输到 Azure RMS。|
|通过使用 Thales nShield 硬件安全模块 (HSM) 进行 HSM 保护|由客户管理 (BYOK)|请参阅此表后面的**HSM 保护密钥到 HSM 保护密钥**的迁移过程。<br /><br />这需要 BYOK 工具集和以下两组步骤：将密钥从本地 HSM 传输到 Azure RMS HSM，然后将配置数据传输到 Azure RMS。|
|AD RMS 数据库中的密码保护|由客户管理 (BYOK)|请参阅此表后面的**软件保护密钥到 HSM 保护密钥**的迁移过程。<br /><br />这需要 BYOK 工具集和以下三组步骤：首先提取软件密钥并将其导入到本地 HSM，然后将密钥从本地 HSM 传输到 Azure RMS HSM，最后将配置数据传输到 Azure RMS。|
|通过使用 Thales 以外的供应商提供的硬件安全模块 (HSM) 进行 HSM 保护|由客户管理 (BYOK)|与 HSM 供应商联系以获取有关如何将密钥从此 HSM 传输到 Thales nShield 硬件安全模块 (HSM) 的说明。 然后遵照此表后面的**HSM 保护密钥到 HSM 保护密钥**的迁移过程中的说明。|
|通过使用外部加密提供程序进行密码保护|由客户管理 (BYOK)|与加密提供程序的供应商联系以获取有关如何将密钥传输到 Thales nShield 硬件安全模块 (HSM) 的说明。 然后遵照此表后面的 **HSM 保护密钥到 HSM 保护密钥**的迁移过程中的说明。|
在开始这些过程之前，请确保你可以访问先前在导出受信任的发布域时创建的 .xml 文件。 例如，可以将这些文件保存到从 AD RMS 服务器移到接入 Internet 的工作站的 U 盘。

> [!NOTE]
> 但是，你将存储这些文件，请使用安全最佳做法来保护它们，因为此数据包含你的私钥。


若要完成步骤 2，请选择针对你的迁移路径的说明： 


- [软件密钥到软件密钥](migrate-softwarekey-to-softwarekey.md)
- [HSM 密钥到 HSM 密钥](migrate-hsmkey-to-hsmkey.md)
- [软件密钥到 HSM 密钥](migrate-softwarekey-to-hsmkey.md)


<<<<<<< HEAD
## 步骤 3. 激活 Azure RMS 租户
有关此步骤的完整说明，请参阅[激活 Azure Rights Management](../deploy-use/activate-azure-classic.md) 文章。
=======
## 步骤 3. 激活你的 RMS 租户
有关此步骤的完整说明，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md) 文章。
>>>>>>> 32b7eccb741760c33bf45a2ce253454827c6d6ba

> [!TIP]
> 如果你有 Office 365 订阅，则可以从 Office 365 管理中心或 Azure 经典门户激活 Azure RMS。 建议你使用 Azure 经典门户，因为你将使用该管理门户来完成下一步操作。

**如果 Azure RMS 租户已激活，会怎么样？** 如果已为你的组织激活了 Azure RMS 服务，则用户可能已使用 Azure RMS 和自动生成的租户密钥（及默认模板）而不是 AD RMS 中的现有密钥（和模板）来保护内容。 在 Intranet 中妥善管理的计算机上不太可能会发生这种情况，因为这些计算机会自动根据 AD RMS 基础结构进行配置。 但是，在工作组计算机或很少连接到 Intranet 的计算机上，可能会发生这种情况。 遗憾的是，这些计算机也很难识别，正因如此，我们建议在从 AD RMS 导入配置数据之前不要激活该服务。

如果你的 Azure RMS 租户已激活并且可以识别这些计算机，请确保根据步骤 5 中所述，在这些计算机上运行 CleanUpRMS_RUN_Elevated.cmd 脚本。 运行此脚本会强制这些计算机重新初始化用户环境，以便下载更新的租户密钥和导入的模板。

## 步骤 4. 配置导入的模板
由于所导入的模板具有“已存档”****的默认状态，如果你希望用户能够将这些模板用于 Azure RMS，必须将此状态更改为“已发布”****。

此外，如果 AD RMS 中的模板使用 **ANYONE** 组，则当你将这些模板导入 Azure RMS 时，系统会自动删除该组；你必须将相应的组/用户和相同的权限手动添加到已导入的模板中。 Azure RMS 的等效组名为 **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<tenant_name>.onmicrosoft.com**。 例如，此组可能看上去与用于 Contoso 的下例类似：**AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**。

如果你不确定 AD RMS 模板是否包括 ANYONE 组，可使用示例 Windows PowerShell 脚本来标识这些模板。 有关将 Windows PowerShell 用于 AD RMS 的详细信息，请参阅[使用 Windows PowerShell 管理 AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx)。

你可以看到组织自动创建的组，前提是将某个默认权限策略模板复制到 Azure 经典门户中，然后确定“权限”****页上的“用户名”****。 但是，你不能使用经典门户将该组添加到已手动创建或导入的模板中，而是必须使用以下 Azure RMS PowerShell 选项之一：

-   使用 [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) PowerShell cmdlet 将“AllStaff”组和权限定义为权限定义对象，然后除了 ANYONE 组外，还要再次对原始模板中已被授予权限的每个其他组或用户运行此命令。 然后，使用 [Set-AadrmTemplateProperty](https://msdn.microsoft.com/en-us/library/azure/dn727076.aspx) cmdlet 将所有这些权限定义对象添加到模板中。

-   使用 [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) cmdlet 将模板导出到 .XML 文件中，可通过编辑该文件将“AllStaff”组和权限添加到现有组和权限中，然后使用 [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) cmdlet 将所做的更改导回到 Azure RMS 中。

> [!NOTE]
> 这个相应的“AllStaff”组并非完全等同于 AD RMS 中的 ANYONE 组：“AllStaff”组包括你的 Azure 租户中的所有用户，而 ANYONE 组则包括所有经过身份验证的用户，这些用户可能不在你的组织中。
> 
> 由于这两个组存在这种差异，你可能还需要向“AllStaff”组添加外部用户。 目前不支持对组使用外部电子邮件地址。

你从 AD RMS 导入的模板的外观和行为就像你可以在 Azure 经典门户中创建的自定义模板一样。 若要将导入的模板更改为“已发布”，以便用户可以查看它们以及从应用程序中选择它们，或者要对模板进行其他更改，请参阅[为 Azure Rights Management 配置自定义模板](../deploy-use/configure-custom-templates.md)。

> [!TIP]
> 为了在迁移过程中向用户提供更一致的体验，请不要对导入的模板进行这两项更改以外的其他更改，请不要发布 Azure RMS 附带的两个默认模板，也不要在此时创建新模板。 请等到迁移过程完成并已解除 AD RMS 服务器的授权。

### 示例 Windows PowerShell 脚本，用于识别包括 ANYONE 组的 AD RMS 模板
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


## 后续步骤
转到“阶段 2 - 客户端配置”[](migrate-from-ad-rms-phase2.md)。



<!--HONumber=Apr16_HO3-->

