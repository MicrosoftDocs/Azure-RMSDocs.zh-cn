---
title: 为 Azure Rights Management 配置超级用户 - AIP
description: 了解并实现 Azure 信息保护中 Azure Rights Management 服务的超级用户功能，以便已获授权的人员和服务始终可以读取和检查 ( "原因" ) 组织的受保护数据。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bf7b4d46c2dd63c87f48c244f38a515c7376fc1a
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "95566309"
---
# <a name="configuring-super-users-for-azure-information-protection-and-discovery-services-or-data-recovery"></a>为 Azure 信息保护和发现服务或数据恢复配置超级用户

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

Azure 信息保护中的 Azure Rights Management 服务的超级用户功能可以确保经授权的人员和服务始终可以阅读和检查 Azure Rights Management 为你的组织保护的数据。 如有必要，可以删除或更改保护。

超级用户对由你的组织的 Azure 信息保护租户保护的文档和电子邮件始终具有 Rights Management 完全控制[使用权限](configure-usage-rights.md)。 这种功能有时称为“数据推理”，是保持对组织数据进行控制的关键所在。 例如，你将为以下任何方案使用此功能：

- 员工离职，你需要阅读其保护的文件。

- IT 管理员需要删除已经为文件配置的当前保护策略并应用新的保护策略。

- Exchange Server 需要为邮箱编制索引以便执行搜索操作。

- 你拥有用于提供数据丢失防护 (DLP) 解决方案的现有 IT 服务、内容加密网关 (CEG) 和反恶意软件产品，它们需要检查已受保护的文件。

- 出于审核、法律或其他符合性原因，你需要对文件进行解密。

## <a name="configuration-for-the-super-user-feature"></a>超级用户功能的配置

默认情况下，超级用户功能未启用，并且不会为任何用户分配此角色。 如果为 Exchange 配置了 Rights Management 连接器，则会自动启用此功能; 对于在 Microsoft 365 中运行 Exchange Online、Microsoft Sharepoint Server 或 SharePoint 的标准服务，它不是必需的。

如果需要手动启用超级用户功能，请使用 PowerShell cmdlet [AipServiceSuperUserFeature](/powershell/module/aipservice/enable-aipservicesuperuserfeature)，然后根据需要使用 [AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser) cmdlet 或 [AipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup) cmdlet 向用户分配 (或服务帐户) ，并根据需要向此组添加 (或其他组) 。 

虽然为超级用户使用组更容易管理，但请注意，出于性能原因，Azure Rights Management [会缓存组成员关系](prepare.md#group-membership-caching-by-azure-information-protection)。 因此，如果需要将新用户分配为超级用户来立即解密内容，请使用 AipServiceSuperUser 添加该用户，而不是将该用户添加到使用 AipServiceSuperUserGroup 配置的现有组。

> [!NOTE]
> 如果尚未安装适用于 Azure Rights Management 的 Windows PowerShell 模块，请参阅 [安装 AIPService PowerShell 模块](install-powershell.md)。

启用超级用户功能或将用户添加为超级用户的时间并不重要。 例如，如果在星期四启用该功能，然后在星期五添加了一名用户，则这位用户在这周一开始即可立即打开受保护的内容。

## <a name="security-best-practices-for-the-super-user-feature"></a>超级用户功能的最佳安全做法

- 限制和监视为你的 Microsoft 365 或 Azure 信息保护租户分配全局管理员的管理员，或者通过使用 [AipServiceRoleBasedAdministrator Cmdlet 向](/powershell/module/aipservice/add-aipservicerolebasedadministrator) 其分配 GlobalAdministrator 角色的管理员。 这些用户可以启用超级用户功能并将用户（及其自己）分配为超级用户，并且可能会对你的组织保护的所有文件进行解密。

- 若要查看已将哪些用户和服务帐户单独分配为超级用户，请使用 [AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser) cmdlet。 

- 若要查看超级用户组是否已配置，请使用 [AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup) cmdlet 和标准用户管理工具检查哪些用户是该组的成员。 

- 与所有管理操作一样，启用或禁用超级功能，以及添加或删除超级用户，并可通过使用 [AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog) 命令进行审核。 有关示例，请参阅 [超级用户功能的示例审核](#example-auditing-for-the-super-user-feature)。

- 当超级用户对文件进行解密时，此操作会记录到日志中并且可以通过[使用情况日志记录](log-analyze-usage.md)对其进行审核。

    > [!NOTE]
    > 尽管日志包含有关解密的详细信息（包括解密该文件的用户），但当用户是超级用户时，它们不会注意到。 将日志与上面列出的 cmdlet 一起使用，以首先收集你可以在日志中识别的超级用户的列表。
    >

- 如果你不需要针对日常服务的超级用户功能，请仅在需要时启用该功能，并使用 [AipServiceSuperUserFeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature) cmdlet 再次禁用它。

### <a name="example-auditing-for-the-super-user-feature"></a>超级用户功能的审核示例

下面的日志提取显示了使用 [AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog) cmdlet 的一些示例条目。 

在此示例中，Contoso Ltd 的管理员确认禁用超级用户功能，将 Richard Simone 添加为超级用户，检查 Richard 是为 Azure Rights Management 服务配置的唯一超级用户，然后启用超级用户功能以使 Richard 能够对目前已从公司离职的员工保护的一些文件进行解密。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>超级用户的脚本选项
通常，具有 Azure Rights Management 超级用户身份的用户需要删除对位于多个位置的多个文件的保护。 虽然可以手动执行此操作，但是通过脚本执行此操作更为高效（并且通常更为可靠）。 为此，可以根据需要使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet 和 [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) cmdlet。 

如果你使用分类和保护，还可以使用 [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) 来应用一个不应用保护的新标签，或者删除已应用了保护的标签。 

有关这些 cmdlet 的详细信息，请参阅 Azure 信息保护客户端管理指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。

> [!NOTE]
> AzureInformationProtection 模块不同于并补充了用于管理 azure 信息保护的 Azure Rights Management 服务的 [AIPService PowerShell 模块](administer-powershell.md) 。

### <a name="guidance-for-using-unprotect-rmsfile-for-ediscovery"></a>使用 Unprotect-RMSFile 进行电子数据展示的指南

虽然可以使用 Unprotect-RMSFile cmdlet 解密 PST 文件中的受保护内容，但请策略性地将此 cmdlet 用作电子数据展示过程的一部分。 在计算机上的大型文件上运行 Unprotect-RMSFile 是资源密集型的（内存和磁盘空间），而此 cmdlet 支持的最大文件大小为 5 GB。

理想情况下， [在 Microsoft 365 中使用电子数据展示](/microsoft-365/compliance/ediscovery) 搜索和提取电子邮件中受保护的电子邮件和受保护的附件 超级用户功能自动与 Exchange Online 集成，以便 Office 365 安全与合规中心或 Microsoft 365 合规中心中的电子数据展示可以在导出之前搜索加密项目，或在导出时解密加密电子邮件。

如果无法使用 Microsoft 365 电子数据展示，则可能会有另一个与 Azure Rights Management 服务集成的电子数据展示解决方案，以类似于数据的原因。 或者，如果你的电子数据展示解决方案无法自动读取和解密受保护的内容，则仍然可以在多步骤过程中使用此解决方案，以便更有效地运行 Unprotect-RMSFile：

1. 将有问题的电子邮件从 Exchange Online 或 Exchange 服务器中导出为 PST 文件，或从用户存储其电子邮件的工作站导出。

2. 将 PST 文件导入电子数据展示工具。 由于该工具无法读取受保护的内容，因此预计这些项会产生错误。

3. 从该工具无法打开的所有项目中，生成此次新的 PST 文件，仅包含受保护的项目。 第二个 PST 文件可能比原始 PST 文件小得多。

4. 在第二个 PST 文件上运行 Unprotect-RMSFile 来解密这个小得多的文件的内容。 在输出中，将现已解密的 PST 文件导入发现工具中。

有关跨邮箱和 PST 文件执行电子数据展示的更多详细信息和指南，请参阅以下博客文章：[Azure 信息保护和电子数据展示流程](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-and-eDiscovery-Processes/ba-p/270216)。