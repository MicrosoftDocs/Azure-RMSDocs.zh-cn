---
title: 为 Azure Rights Management 配置超级用户 - AIP
description: 了解并实现 Azure 信息保护中 Azure Rights Management 服务的超级用户功能, 以便已获授权的人员和服务始终可以阅读和检查 ("原因") 组织的受保护数据。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 23cb44d9b4101c4e73aeed27142be50c79a70cfb
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68789048"
---
# <a name="configuring-super-users-for-azure-information-protection-and-discovery-services-or-data-recovery"></a>为 Azure 信息保护和发现服务或数据恢复配置超级用户

>适用对象：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

Azure 信息保护中的 Azure Rights Management 服务超级用户功能可确保已获授权的用户与服务始终可以阅读和检查 Azure Rights Management 为你的组织保护的数据。 如有必要，可以删除或更改保护。

对于受你的组织 Azure 信息保护租户保护的文档和电子邮件，超级用户始终具有权限管理完全控制[使用权](configure-usage-rights.md)。 这种功能有时称为“数据推理”，是保持对组织数据进行控制的关键所在。 例如，对于以下任何情况，你可以使用此功能：

- 某位员工离职，你需要阅读其保护的文件。

- IT 管理员需要删除当前针对文件配置的保护策略，并应用新的保护策略。

- Exchange Server 需要为邮箱编制索引以执行搜索操作。

- 数据丢失防护 (DLP) 解决方案、内容加密网关 (CEG) 和反恶意软件产品的现有 IT 服务需要检查已受保护的文件。

- 出于审核、法律或其他法规遵从原因，你需要批量解密文件。

## <a name="configuration-for-the-super-user-feature"></a>超级用户功能的配置

默认情况下，超级用户功能未启用，并且没有向任何用户分配此角色。 如果你为 Exchange 配置了 Rights Management 连接器，则会自动启用超级用户功能，对于运行 Exchange Online、SharePoint Online 或 SharePoint Server 的标准服务，不需要该功能。

如果需要手动启用超级用户功能, 请使用 PowerShell cmdlet [AipServiceSuperUserFeature](/powershell/module/aipservice/enable-aipservicesuperuserfeature), 然后根据需要使用[AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser) cmdlet[分配用户 (或服务帐户)。AipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup) cmdlet, 并根据需要向此组添加用户 (或其他组)。 

尽管为超级用户使用组更易管理，但请注意，出于性能原因，Azure 权限管理[缓存组成员身份](prepare.md#group-membership-caching-by-azure-information-protection)。 因此, 如果需要将新用户分配为超级用户来立即解密内容, 请使用 AipServiceSuperUser 添加该用户, 而不是将该用户添加到使用 AipServiceSuperUserGroup 配置的现有组。

> [!NOTE]
> 如果尚未安装适用于 Azure Rights Management 的 Windows PowerShell 模块, 请参阅[安装 AIPService PowerShell 模块](install-powershell.md)。

启用超级用户功能或将用户添加为超级用户的时间并不重要。 例如，如果在星期四启用该功能，然后在星期五添加了一名用户，则这位用户在这周一开始即可立即打开受保护的内容。

## <a name="security-best-practices-for-the-super-user-feature"></a>超级用户功能的最佳安全做法

- 限制和监视为 Office 365 或 Azure 信息保护租户分配了全局管理员的管理员, 或使用[AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator) cmdlet 分配了 GlobalAdministrator 角色的管理员。 这些用户可以启用超级用户功能并将用户（包括其自己）分配为超级用户，并且可能解密组织保护的所有文件。

- 若要查看已将哪些用户和服务帐户单独分配为超级用户, 请使用[AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser) cmdlet。 若要查看超级用户组是否已配置, 请使用[AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup) cmdlet 和标准用户管理工具检查哪些用户是该组的成员。 与所有管理操作一样, 启用或禁用超级功能, 以及添加或删除超级用户, 并可通过使用[AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)命令进行审核。 有关示例，请参阅下一部分。 超级用户解密文件时，会记录此操作，并且可使用[使用情况日志记录](log-analyze-usage.md)进行审核。

- 如果你不需要针对日常服务的超级用户功能, 请仅在需要时启用该功能, 并使用[AipServiceSuperUserFeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature) cmdlet 再次禁用它。

### <a name="example-auditing-for-the-super-user-feature"></a>超级用户功能的审核示例

下面的日志提取显示了使用[AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog) cmdlet 的一些示例条目。 

在此示例中，Contoso Ltd 的管理员确认已禁用超级用户功能、将 Richard Simone 添加为超级用户、检查是否将 Richard 配置为 Azure Rights Management 服务唯一的超级用户，然后启用超级用户功能，以便 Richard 可以解密已离开公司的员工保护的某些文件。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>超级用户的脚本选项
通常，具有 Azure Rights Management 超级用户身份的用户需要删除对位于多个位置的多个文件的保护。 尽管可以手动执行此操作，但使用脚本会提高效率（并且通常更可靠）。 为此，请根据需要使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet 和 [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) cmdlet。 

如果使用分类和保护，也可以使用 [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) 应用未应用保护的新标签，或删除已应用保护的标签。 

有关这些 cmdlet 的详细信息，请参阅 Azure 信息保护客户端管理员指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。

> [!NOTE]
> AzureInformationProtection 模块不同于并补充了用于管理 azure 信息保护的 Azure Rights Management 服务的[AIPService PowerShell 模块](administer-powershell.md)。

### <a name="guidance-for-using-unprotect-rmsfile-for-ediscovery"></a>使用 Unprotect-RMSFile 进行电子数据展示的指南

虽然可以使用 Unprotect-RMSFile cmdlet 解密 PST 文件中的受保护内容，但请策略性地将此 cmdlet 用作电子数据展示过程的一部分。 在计算机上的大型文件上运行 Unprotect-RMSFile 是资源密集型的（内存和磁盘空间），而此 cmdlet 支持的最大文件大小为 5 GB。

理想情况下，使用 [Office 365 电子数据展示](/office365/securitycompliance/ediscovery)在电子邮件中搜索和提取受保护的电子邮件和受保护的附件。 超级用户功能自动与 Exchange Online 集成，以便 Office 365 安全与合规中心或 Microsoft 365 合规中心中的电子数据展示可以在导出之前搜索加密项目，或在导出时解密加密电子邮件。

如果无法使用 Office 365 电子数据展示，则可能有另一个与 Azure Rights Management 服务集成的电子数据展示解决方案，对数据进行类似推理。 或者，如果你的电子数据展示解决方案无法自动读取和解密受保护的内容，则仍然可以在多步骤过程中使用此解决方案，以便更有效地运行 Unprotect-RMSFile：

1. 将有问题的电子邮件从 Exchange Online 或 Exchange 服务器中导出为 PST 文件，或从用户存储其电子邮件的工作站导出。

2. 将 PST 文件导入电子数据展示工具。 由于该工具无法读取受保护的内容，因此预计这些项会产生错误。

3. 从该工具无法打开的所有项目中，生成此次新的 PST 文件，仅包含受保护的项目。 第二个 PST 文件可能比原始 PST 文件小得多。

4. 在第二个 PST 文件上运行 Unprotect-RMSFile 来解密这个小得多的文件的内容。 在输出中，将现已解密的 PST 文件导入发现工具中。

有关跨邮箱和 PST 文件执行电子数据展示的更多详细信息和指南，请参阅以下博客文章：[Azure 信息保护和电子数据展示流程](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-and-eDiscovery-Processes/ba-p/270216)。

