---
title: 使用 PowerShell 管理 Azure 信息保护中的保护
description: 了解如何为 Azure 信息保护中保护服务中使用的 PowerShell 模块来管理此服务为你的租户。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a6aa0b8ecd01df9d012588f8e2b02d13f03cfff6
ms.sourcegitcommit: 6c6fda77e131e071c94c2a2fd7b27e4031266fa5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67544968"
---
# <a name="administering-protection-from-azure-information-protection-by-using-powershell"></a>使用 PowerShell 管理 Azure 信息保护中的保护

>适用对象：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

若要使用 PowerShell 管理 Azure 信息保护中保护服务需要吗？ 如果所有配置都可在 Azure 门户或 Microsoft 365 管理中心中完成，则可能不需要。 但是，需要使用 PowerShell 进行某些高级配置，并且可能还需使用 PowerShell 以进行更高效的命令行控制和脚本编写。

下一部分中的表格包括一些使用 PowerShell 的高级配置方案。 如果不使用 PowerShell 也可完成配置，则此信息也包括在表中。

此模块，详细了解每个可用的 cmdlet 的完整列表请参阅[AIPService](/powershell/module/aipservice/?view=azureipps#aipservice)。

> [!NOTE]
> 若要安装此 PowerShell 模块，请参阅[安装 AIPService PowerShell 模块](install-powershell.md)。

除了此服务端 PowerShell 模块，Azure 信息保护客户端还将安装一个补充 PowerShell 模块 **AzureInformationProtection**。 此客户端模块支持对多个文件进行分类和保护，这样可以方便某些操作，例如批量保护文件夹中的所有文件。 有关详细信息，请参阅管理员指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。

## <a name="cmdlets-grouped-by-administration-task"></a>按管理任务对 cmdlet 进行分组

|如果你需要…|…请使用以下 cmdlet|
|-------------------|------------------------------|
|从本地 Rights Management（AD RMS 或 Windows RMS）迁移到 Azure 信息保护。|[Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd)<br /><br />[Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)|
|连接到组织的 Rights Management 服务或断开与该服务的连接。|[Connect-AipService](/powershell/module/aipservice/connect-aipservice)<br /><br />[Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice)|
|生成和管理你自己的租户密钥 –“自带密钥”(BYOK) 方案。|[Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)<br /><br />[Use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey)<br /><br />[Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys)|
|激活或停用组织的 Rights Management 服务。<br /><br />还可以在管理门户中执行这些操作。 有关详细信息，请参阅[激活 Azure 信息保护的保护服务](activate-service.md)。|[Enable-AipService](/powershell/module/aipservice/enable-aipservice)<br /><br />[Disable-AipService](/powershell/module/aipservice/disable-aipservice)|
|管理适用于 Azure 信息保护的文档跟踪站点。|[Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature)<br /><br />[Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature)<br /><br />[Get-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature)<br /><br />[Set-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/set-aipservicedonottrackusergroup)<br /><br />[Clear-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Clear-AipServiceDoNotTrackUserGroup)<br /><br />[Get-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/get-AipServiceDoNotTrackUserGroup)<br /><br />[Get-AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)<br /><br />[Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)|
|为 Azure Rights Management 服务的分阶段部署配置内置控件。|[Get-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/get-aipserviceonboardingcontrolpolicy)<br /><br />[Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)|
|为你的组织创建和管理 Rights Management 模板。<br /><br />虽然 PowerShell 可提供更精密的控制，但也可以从 Azure 门户执行大多数操作。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)。|[Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)<br /><br />[Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)<br /><br />[Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)<br /><br />[Get-AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)<br /><br />[Import-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetemplate)<br /><br />[New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)<br /><br />[Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)<br /><br />[Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)|
|配置在没有 Internet 连接的情况下，可以访问你的组织保护的内容的最大天数（使用许可证有效期）。|[Get-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/get-aipservicemaxuselicensevaliditytime)<br /><br />[Set-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)|
|管理组织的 Rights Management 的超级用户功能。|[Enable-AipServiceSuperUserFeature](/powershell/module/aipservice/enable-aipservicesuperuserfeature)<br /><br />[Disable-AipServiceSuperUserFeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature)<br /><br />[Add-AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser)<br /><br />[Get-AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser)<br /><br />[Remove-AipServiceSuperUser](/powershell/module/aipservice/remove-aipservicesuperuser)<br /><br />[Set-AAipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup)<br /><br />[Get-AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup)<br /><br />[Clear-AipServiceSuperUserGroup](/powershell/module/aipservice/clear-aipservicesuperusergroup)|
|管理被授权管理组织的 Rights Management 服务的用户和组。|[Add-Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator)<br /><br />[Get-Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator)<br /><br />[Remove-Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/remove-aipservicerolebasedadministrator)|
|获取组织的 Rights Management 管理任务的日志。|[Get-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)|
|记录和分析 Rights Management 的使用情况日志记录。|[Get-AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog)|
|显示组织的当前 Rights Management 服务配置。|[Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)|
|将组织从 Azure 信息保护迁移到本地 AD RMS 部署。|[Set-AipServiceMigrationUrl](/powershell/module/aipservice/set-aipservicemigrationurl)<br /><br />[Get-AipServiceMigrationUrl](/powershell/module/aipservice/get-aipservicemigrationurl)|

