---
title: 为 Azure Rights Management 配置超级用户 - AIP
description: 了解并实施 Azure 信息保护中的 Azure Rights Management 服务超级用户功能，以便已获授权的用户与服务始终可以阅读和检查 Azure Rights Management 为你的组织保护的数据。 这种功能有时称为“数据推理”，是保持对组织数据进行控制的关键所在。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/31/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7d52bd4547b24acad3e9b2db8c8ade8b632d517d
ms.sourcegitcommit: 6cbd03b28873b192dc730556c6dd5a7da6e705df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39411336"
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>为 Azure Rights Management 和发现服务或数据恢复配置超级用户

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

Azure 信息保护中的 Azure Rights Management 服务超级用户功能可确保已获授权的用户与服务始终可以阅读和检查 Azure Rights Management 为你的组织保护的数据。 如有需要，超级用户可以删除保护，或者更改以前应用的保护。 

对于受你的组织 Azure 信息保护租户保护的文档和电子邮件，超级用户始终具有权限管理完全控制[使用权](configure-usage-rights.md)。 这种功能有时称为“数据推理”，是保持对组织数据进行控制的关键所在。 例如，对于以下任何情况，你可以使用此功能：

- 某位员工离职，你需要阅读其保护的文件。

- IT 管理员需要删除当前针对文件配置的保护策略，并应用新的保护策略。

- Exchange Server 需要为邮箱编制索引以执行搜索操作。

- 数据丢失防护 (DLP) 解决方案、内容加密网关 (CEG) 和反恶意软件产品的现有 IT 服务需要检查已受保护的文件。

- 出于审核、法律或其他合规性原因，你需要批量解密文件。

## <a name="configuration-for-the-super-user-feature"></a>超级用户功能的配置

默认情况下，超级用户功能未启用，并且没有向任何用户分配此角色。 如果你为 Exchange 配置了 Rights Management 连接器，则会自动启用超级用户功能，对于运行 Exchange Online、SharePoint Online 或 SharePoint Server 的标准服务，不需要该功能。

如果需要手动启用超级用户功能，请使用 PowerShell cmdlet [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature)，然后根据需要使用 [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) cmdlet 或 [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup) cmdlet 分配用户（或服务帐户），并根据需要向此组添加用户（或其他组）。 

尽管为超级用户使用组更易管理，但请注意，出于性能原因，Azure 权限管理[缓存组成员身份](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection)。 因此，如果需要将新用户分配为超级用户以立即解密内容，请通过使用 Add-AadrmSuperUser 添加用户，而不要将用户添加到已使用 Set-AadrmSuperUserGroup 配置的现有组。

> [!NOTE]
> 如果尚未安装适用于 Azure Rights Management 的 Windows PowerShell 模块，请参阅[安装 AADRM PowerShell 模块](install-powershell.md)。

启用超级用户功能或将用户添加为超级用户的时间并不重要。 例如，如果在星期四启用该功能，然后在星期五添加了一名用户，则这位用户在这周一开始即可立即打开受保护的内容。

## <a name="security-best-practices-for-the-super-user-feature"></a>超级用户功能的最佳安全做法

- 使用 [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) cmdlet 限制和监视分配为 Office 365 或 Azure 信息保护租户全局管理员或获得了 GlobalAdministrator 角色的管理员。 这些用户可以启用超级用户功能并将用户（包括其自己）分配为超级用户，并且可能解密组织保护的所有文件。

- 若要确定已将哪些用户和服务帐户单独分配为超级用户，请使用 [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser) cmdlet。 若要确定是否配置了超级用户组，请使用 [Get-AadrmSuperUserGroup](/powershell/module/aadrm/get-aadrmsuperusergroup) cmdlet 和标准用户管理工具，以确认哪些用户是此组的成员。 与所有管理操作一样，对于启用或禁用超级功能，以及添加或删除超级用户操作，将会加以记录，并且可使用 [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) 进行审核。 有关示例，请参阅下一部分。 超级用户解密文件时，会记录此操作，并且可使用[使用情况日志记录](log-analyze-usage.md)进行审核。

- 如果你不需要日常服务的超级用户功能，仅在需要时启用该功能，并使用 [Disable-AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature) cmdlet 再次禁用。

### <a name="example-auditing-for-the-super-user-feature"></a>超级用户功能的审核示例

下面的日志提取显示了使用 [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) cmdlet 的一些示例条目。 

在此示例中，Contoso Ltd 的管理员确认已禁用超级用户功能、将 Richard Simone 添加为超级用户、检查是否将 Richard 配置为 Azure Rights Management 服务唯一的超级用户，然后启用超级用户功能，以便 Richard 可以解密已离开公司的员工保护的某些文件。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>超级用户的脚本选项
通常，具有 Azure Rights Management 超级用户身份的用户需要删除对位于多个位置的多个文件的保护。 尽管可以手动执行此操作，但使用脚本会提高效率（并且通常更可靠）。 为此，请根据需要使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet 和 [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) cmdlet。 

如果使用分类和保护，也可以使用 [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) 应用未应用保护的新标签，或删除已应用保护的标签。 

有关这些 cmdlet 的详细信息，请参阅 Azure 信息保护客户端管理员指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](../rms-client/client-admin-guide-powershell.md)。

> [!NOTE]
> AzureInformationProtection 模块将替换随 RMS 保护工具一起安装的 RMS 保护 PowerShell 模块。 这两种模块不同于[适用于 Azure 权限管理的 PowerShell 模块](administer-powershell.md)，并且对该模块提供了补充。 AzureInformationProtection 模块支持 Azure 信息保护、适用于 Azure 信息保护的 Azure Rights Management 服务 (Azure RMS) 和 Active Directory Rights Management Services (AD RMS)。


