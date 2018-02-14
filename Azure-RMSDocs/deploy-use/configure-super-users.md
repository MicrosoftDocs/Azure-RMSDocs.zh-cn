---
title: "为 Azure Rights Management 配置超级用户 - AIP"
description: "了解并实现 Azure 信息保护中的 Azure Rights Management 服务的超级用户功能，以便经授权的人员和服务始终可以读取和检查 Azure Rights Management 为你的组织保护的数据。 此功能有时称为“对数据的推理”，并且在保持对你的组织数据的控制权时起着关键作用。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a134d6619f67bfc3d26cb1726fe07e8ffca403cd
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2018
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>为 Azure Rights Management 和发现服务或数据恢复配置超级用户

>*适用于：Azure 信息保护、Office 365*

Azure 信息保护中的 Azure Rights Management 服务的超级用户功能可以确保经授权的人员和服务始终可以阅读和检查 Azure Rights Management 为你的组织保护的数据。 并且，如果有必要，可以删除保护或者更改以前应用的保护。 

超级用户对由你的组织的 Azure 信息保护租户保护的文档和电子邮件始终具有 Rights Management 完全控制[使用权限](configure-usage-rights.md)。 此功能有时称为“对数据的推理”，并且在保持对你的组织数据的控制权时起着关键作用。 例如，你将为以下任何方案使用此功能：

- 员工离职，你需要阅读其保护的文件。

- IT 管理员需要删除已经为文件配置的当前保护策略并应用新的保护策略。

- Exchange Server 需要为邮箱编制索引以便执行搜索操作。

- 你拥有用于提供数据丢失防护 (DLP) 解决方案的现有 IT 服务、内容加密网关 (CEG) 和反恶意软件产品，它们需要检查已受保护的文件。

- 出于审核、法律或其他符合性原因，你需要对文件进行解密。

默认情况下，超级用户功能未启用，并且不会为任何用户分配此角色。 如果为 Exchange 配置了 Rights Management 连接器，则会自动启用此功能，对于运行 Exchange Online、SharePoint Online 或 SharePoint Server 的标准服务，此功能不是必需的。

如果需要手动启用超级用户功能，请使用 PowerShell cmdlet [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature)，然后根据需要使用 [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) cmdlet 或 [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup) cmdlet 分配用户（或服务帐户）并根据需要向此组添加用户（或其他组）。 

虽然为超级用户使用组更容易管理，但请注意，出于性能原因，Azure Rights Management [会缓存组成员关系](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection)。 因此，如果需要将新用户分配为超级用户来立即对内容进行解密，请使用 Add-AadrmSuperUser 添加该用户，而不是将用户添加到已使用 Set-AadrmSuperUserGroup 配置的现有组。

> [!NOTE]
> 如果尚未安装适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 模块，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。

适用于超级用户功能的安全最佳做法：

- 限制并监视被分配为 Office 365 或 Azure 信息保护租户全局管理员的管理员，或者通过使用 [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) cmdlet 分配为 GlobalAdministrator 角色的管理员。 这些用户可以启用超级用户功能并将用户（及其自己）分配为超级用户，并且可能会对你的组织保护的所有文件进行解密。

- 若要查看哪些用户和服务帐户被单独分配为超级用户，请使用 [Get-AadrmSuperUser cmdlet](/powershell/module/aadrm/get-aadrmsuperuser)。 若要查看是否配置了某个超级用户组，请使用 [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperusergroup) cmdlet 和标准用户管理工具来检查哪些用户是此组的成员。 与所有管理操作一样，启用或禁用超级用户功能以及添加或删除超级用户这类操作会记录到日志中，并且可以使用 [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) 命令进行审核。 当超级用户对文件进行解密时，此操作会记录到日志中并且可以通过[使用情况日志记录](log-analyze-usage.md)对其进行审核。

- 如果不需要将超级用户功能用于日常服务，可以仅在需要此功能时启用它，然后使用 [Disable-AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature) cmdlet 将其重新禁用。

下面的日志摘录显示了使用 Get-AadrmAdminLog cmdlet 时的一些示例条目。 在此示例中，Contoso Ltd 的管理员确认禁用超级用户功能，将 Richard Simone 添加为超级用户，检查 Richard 是为 Azure Rights Management 服务配置的唯一超级用户，然后启用超级用户功能以使 Richard 能够对目前已从公司离职的员工保护的一些文件进行解密。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>超级用户的脚本选项
通常，被分配为 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的超级用户的某人将需要从多个位置中的多个文件删除保护。 虽然可以手动执行此操作，但是通过脚本执行此操作更为高效（并且通常更为可靠）。 为此，可以根据需要使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet 和 [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) cmdlet。 

如果你使用分类和保护，还可以使用 [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) 来应用一个不应用保护的新标签，或者删除已应用了保护的标签。 

有关这些 cmdlet 的详细信息，请参阅 Azure 信息保护客户端管理指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](../rms-client/client-admin-guide-powershell.md)。

> [!NOTE]
> AzureInformationProtection 模块替代了随 RMS Protection Tool 安装的 RMS 保护 PowerShell 模块。 这两个模块都不同于主要的[适用于 Azure Rights Management 的 Windows PowerShell 模块](administer-powershell.md)并且对其进行了补充。 AzureInformationProtection 模块支持 Azure 信息保护，用于 Azure 信息保护的 Azure Rights Management 服务 (Azure RMS) 以及 Active Directory Rights Management Services (AD RMS)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

