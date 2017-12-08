---
title: "迁移 AD RMS-Azure 信息保护 - 第 2 阶段"
description: "从 AD RMS 迁移到 Azure 信息保护的第 2 阶段涉及从 AD RMS 迁移到 Azure 信息保护中的步骤 4 至 6。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/02/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0dff1b664cbac830dda2750cc6120ab4476c8183
ms.sourcegitcommit: c5408506170bdb00d9e677b02161b9f61d4d5d3c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2017
---
# <a name="migration-phase-2---server-side-configuration-for-ad-rms"></a>迁移第 2 阶段 - AD RMS 的服务器端配置

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*

使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的阶段 2。 这些过程涉及了[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)中的步骤 4-6。


## <a name="step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection"></a>步骤 4. 从 AD RMS 中导出配置数据并将其导入到 Azure 信息保护中
此步骤是一个分为两部分的过程：

1. 通过将受信任的发布域 (TPD) 导出到 .xml 文件，从 AD RMS 导出配置数据。 此过程对于所有迁移是相同的。

2. 将配置数据导入到 Azure 信息保护中。 此步骤具有不同处理，具体取决于你的当前 AD RMS 部署配置以及 Azure RMS 租户密钥的首选拓扑。

### <a name="export-the-configuration-data-from-ad-rms"></a>从 AD RMS 导出配置数据

在所有 AD RMS 群集中，针对已保护你组织内容的所有受信任的发布域执行以下过程。 无需在仅授权群集上运行此过程。

#### <a name="to-export-the-configuration-data-trusted-publishing-domain-information"></a>导出配置数据（受信任的发布域信息）

1. 以具有 AD RMS 管理权限的用户身份登录到 AD RMS 群集。

2. 从 AD RMS 管理控制台 (**Active Directory Rights Management Services**)，展开 AD RMS 群集名称，再展开“信任策略”，然后单击“受信任的发布域”。

3. 在结果窗格中，选择受信任的发布域，然后在操作窗格中单击“导出受信任的发布域” 。

4. 在“导出受信任的发布域”对话框中  ：

    - 单击“另存为”并将其保存到所选的路径和文件名  。 请确保指定 **.xml** 作为文件扩展名（此扩展名不会自动追加）。

    - 指定并确认一个强密码。 请记住此密码，因为稍后将配置数据导入到 Azure 信息保护中时，将需要此密码。

    - 不要选中将受信任的域文件保存在 RMS 版本 1.0 中的复选框。

当你已导出所有受信任的发布域后，便可以启动将此数据导入到 Azure 信息保护的过程了。

请注意，受信任的发布域包含之前用于解密受保护文件的服务器许可方证书 (SLC) 密钥，因此除了当前的活动域外，请务必导出所有受信任的发布域（并稍后导入到 Azure 中）。

例如，如果将 AD RMS 服务器从加密模式 1 升级到加密模式 2，则将拥有多个受信任的发布域。 如果没有导出受信任的发布域（这些域包含使用加密模式 1 的存档的密钥）并将其导入到 Azure 中，则在迁移结束时，用户将无法打开使用加密模式 1 密钥所保护的内容。


### <a name="import-the-configuration-data-to-azure-information-protection"></a>将配置数据导入到 Azure 信息保护
此步骤的确切过程取决于当前的 AD RMS 部署配置以及 Azure 信息保护租户密钥的首选拓扑。

当前 AD RMS 部署对服务器许可方证书 (SLC) 密钥使用以下配置之一：

- AD RMS 数据库中的密码保护。 这是默认设置。

- 通过使用 Thales 硬件安全模块 (HSM) 进行 HSM 保护。

- 通过使用 Thales 以外的供应商提供的硬件安全模块 (HSM) 进行 HSM 保护。

- 通过使用外部加密提供程序进行密码保护。

> [!NOTE]
> 有关将硬件安全模块与 AD RMS 配合使用的详细信息，请参阅 [将 AD RMS 与硬件安全模块配合使用](http://technet.microsoft.com/library/jj651024.aspx)。

两个 Azure 信息保护租户密钥拓扑选项包括：Microsoft 管理你的租户密钥（**由 Microsoft 管理**），或者你在 Azure 密钥保管库中自行管理租户密钥（**由客户管理**）。 如果你自行管理 Azure 信息保护租户密钥，这有时也称为“创建自己的密钥”(BYOK)。 有关详细信息，请参阅[计划和实施你的 Azure 信息保护租户密钥](plan-implement-tenant-key.md)文章。

使用下表来确定要使用哪个过程进行迁移。 

|当前的 AD RMS 部署|选择的 Azure 信息保护租户密钥拓扑|迁移说明|
|-----------------------------|----------------------------------------|--------------------------|
|AD RMS 数据库中的密码保护|由 Microsoft 管理|请参阅此表后面的 **软件保护密钥到软件保护密钥**的迁移过程。<br /><br />这是最简单的迁移路径，只需要将配置数据传送到 Azure 信息保护。|
|通过使用 Thales nShield 硬件安全模块 (HSM) 进行 HSM 保护 |由客户管理 (BYOK)|请参阅此表后面的**HSM 保护密钥到 HSM 保护密钥**的迁移过程。<br /><br />这需要 Azure Key Vault BYOK 工具集和以下三组步骤：首先将密钥从本地 HSM 传输到 Azure Key Vault HSM，然后授权 Azure 信息保护中的 Azure Rights Management 服务使用租户密钥，最后将配置数据传输到 Azure 信息保护。|
|AD RMS 数据库中的密码保护|由客户管理 (BYOK)|请参阅此表后面的**软件保护密钥到 HSM 保护密钥**的迁移过程。<br /><br />这需要 Azure 密钥保管库 BYOK 工具集和以下四组步骤：首先提取软件密钥并将其导入到本地 HSM，然后将密钥从本地 HSM 传送到 Azure 信息保护 HSM，之后将密钥保管库数据传送到 Azure 信息保护，最后将配置数据传送到 Azure 信息保护。|
|通过使用 Thales 以外的供应商提供的硬件安全模块 (HSM) 进行 HSM 保护 |由客户管理 (BYOK)|与 HSM 供应商联系，获取有关如何将密钥从此 HSM 传输到 Thales nShield 硬件安全模块 (HSM) 的说明。 然后遵照此表后面的 **HSM 保护密钥到 HSM 保护密钥**的迁移过程中的说明。|
|通过使用外部加密提供程序进行密码保护|由客户管理 (BYOK)|与加密提供程序的供应商联系以获取有关如何将密钥传输到 Thales nShield 硬件安全模块 (HSM) 的说明。 然后遵照此表后面的 **HSM 保护密钥到 HSM 保护密钥**的迁移过程中的说明。|

如果拥有无法导出的 HSM 保护密钥，仍可通过将 AD RMS 群集配置为只读模式来迁移到 Azure 信息保护。 在只读模式下，仍可打开之前受保护的内容，但新的受保护内容使用由你 (BYOK) 或 Microsoft 管理的新租户密钥。 有关详细信息，请参阅[可更新 Office 以支持从 AD RMS 到 Azure RMS 的迁移](https://support.microsoft.com/help/4023955/an-update-is-available-for-office-to-support-migrations-from-ad-rms-to)。

在开始这些密钥迁移过程之前，请确保可以访问先前在导出受信任的发布域时创建的 .xml 文件。 例如，可以将这些文件保存到从 AD RMS 服务器移到接入 Internet 的工作站的 U 盘。

> [!NOTE]
> 但是，你将存储这些文件，请使用安全最佳做法来保护它们，因为此数据包含你的私钥。

若要完成步骤 4，请选择针对你的迁移路径的说明： 

- [软件保护密钥到软件保护密钥](migrate-softwarekey-to-softwarekey.md)
- [HSM 保护密钥到 HSM 保护密钥](migrate-hsmkey-to-hsmkey.md)
- [软件保护密钥到 HSM 保护密钥](migrate-softwarekey-to-hsmkey.md)

## <a name="step-5-activate-the-azure-rights-management-service"></a>步骤 5. 激活 Azure Rights Management 服务

打开 PowerShell 会话并运行下列命令：

1. 连接到 Azure Rights Management 服务，并在出现提示时，指定全局管理员凭据：
    
        Connect-Aadrmservice

2. 激活 Azure Rights Management 服务：
    
        Enable-Aadrm

**如果 Azure 信息保护租户已激活，会怎么样？** 如果已为组织激活 Azure Rights Management 服务，并且已创建想要在迁移后使用的自定义模板，则必须导出和导入这些模板。 下一步中介绍了此过程。 

## <a name="step-6-configure-imported-templates"></a>步骤 6. 配置导入的模板

由于所导入的模板具有“已存档”的默认状态，如果你希望用户能够将这些模板用于 Azure Rights Management 服务，必须将此状态更改为“已发布”。

从 AD RMS 导入的模板的外观和行为就像可以在 Azure 门户中创建的自定义模板一样。 若要将导入的模板更改为“已发布”，以便用户可以查看它们以及从应用程序中选择它们，请参阅[配置和管理 Azure 信息保护的模板](../deploy-use/configure-policy-templates.md)。

除了发布新导入的模板，可能还需要对模板进行两项重要更改，才能继续迁移。 为了在迁移过程中向用户提供更一致的体验，请不要对导入的模板进行额外的更改，也不要发布 Azure 信息保护附带的两个默认模板，或在此时创建新模板。 相反，请等到迁移过程完成并已取消预配 AD RMS 服务器。

你可能需要在此步骤中进行以下模板更改：

- 如果在迁移前创建了 Azure 信息保护自定义模板，则必须手动导出并导入它们。

- 如果 AD RMS 中的模板使用 ANYONE 组，可能需要从组织外部添加用户或组。 
    
    在 AD RMS 中，ANYONE 组向所有经过身份验证的用户授予了权限。 此组将自动转换为 Azure AD 租户中的所有用户。 如果不需要向任何额外用户授予权限，则无需进一步操作。 但如果使用 ANYONE 组来包括外部用户，必须手动添加这些用户以及要向他们授予的权限。

### <a name="procedure-if-you-created-custom-templates-before-the-migration"></a>在迁移前创建了自定义模板时需执行的过程

如果在迁移前创建了自定义模板（无论是在激活 Azure Rights Management 服务之前或之后），那么在迁移后，用户将无法使用这些模板，即使模板设置为“已发布”也是如此。 若要使其可供用户使用，必须先执行以下操作： 

1. 通过运行 [Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate) 标识这些模板并记下其模板 ID。 

2. 通过使用 Azure RMS PowerShell cmdlet [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate) 导出模板。

3. 通过使用 Azure RMS PowerShell cmdlet [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate) 导入模板。

然后可以发布或存档这些模板，就像迁移后创建的任何其他模板一样。

### <a name="procedure-if-your-templates-in-ad-rms-used-the-anyone-group"></a>AD RMS 中的模板使用 **ANYONE** 组时需执行的过程

如果 AD RMS 中的模板使用 ANYONE 组，此组将自动转换为使用名为 AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@\<tenant_name>.onmicrosoft.com 的组。例如，如果公司为 Contoso，则该组可能会如下所示：**AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**。此组包含 Azure AD 租户中的所有用户。

如果在 Azure 门户中管理模板和标签，此组将显示为 Azure AD 中的租户域名。 例如，如果公司为 Contoso，此组可能类似于：contoso.onmicrosoft.com。要添加此组，选项将显示“添加 \<组织名称> - 所有成员”。

如果不确定 AD RMS 模板是否包括 ANYONE 组，可使用以下 Windows PowerShell 示例脚本来标识这些模板。 有关将 Windows PowerShell 用于 AD RMS 的详细信息，请参阅[使用 Windows PowerShell 管理 AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx)。

如果在 Azure 门户中将模板转换为标签，可以轻松将外部用户添加到这些模板。 然后，在“添加权限”边栏选项卡上，选择“输入详细信息”，手动为这些用户指定电子邮件地址。 

有关此配置的详细信息，请参阅[如何配置标签以进行 Rights Management 保护](../deploy-use/configure-policy-protection.md)。

#### <a name="sample-windows-powershell-script-to-identify-ad-rms-templates-that-include-the-anyone-group"></a>示例 Windows PowerShell 脚本，用于识别包括 ANYONE 组的 AD RMS 模板
本节包含示例脚本，可帮助你确定任何定义了 ANYONE 组的 AD RMS 模板，如前一节所述。

**免责声明：**此示例脚本在任何 Microsoft 标准支持计划或服务下均不受支持。 此示例脚本按原样提供，不提供任何形式的保证。

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


## <a name="next-steps"></a>后续步骤
转到[第 3 阶段 - 客户端配置](migrate-from-ad-rms-phase3.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]