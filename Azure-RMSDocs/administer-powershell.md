---
title: 使用 PowerShell 管理 Azure 信息保护的保护
description: 了解如何使用 Azure 信息保护中的保护服务的 PowerShell 模块为租户管理此服务。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 04/28/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8ae0df982453206ec1069767dc0c25e74a996c1d
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384111"
---
# <a name="administering-protection-from-azure-information-protection-by-using-powershell"></a>使用 PowerShell 管理 Azure 信息保护的保护

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月31日** 被 **弃用**。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

是否需要使用 PowerShell 来管理 Azure 信息保护中的保护服务？ 如果所有配置都可在 Azure 门户或 Microsoft 365 管理中心中完成，则可能不需要。 但是，需要使用 PowerShell 进行某些高级配置，并且可能还需使用 PowerShell 以进行更高效的命令行控制和脚本编写。

下一部分中的表格包括一些使用 PowerShell 的高级配置方案。 如果不使用 PowerShell 也可完成配置，则此信息也包括在表中。

有关此模块的可用 cmdlet 的完整列表，以及每个 cmdlet 的详细信息，请参阅 [AIPService](/powershell/module/aipservice/#aipservice)。

若要安装此 PowerShell 模块，请参阅 [安装 AIPService PowerShell 模块](install-powershell.md)。

> [!TIP]
> 除了此服务端 PowerShell 模块，Azure 信息保护客户端还将安装一个补充 PowerShell 模块 **AzureInformationProtection**。 
>
> 此客户端模块支持对多个文件进行分类和保护，这样可以方便某些操作，例如批量保护文件夹中的所有文件。 有关详细信息，请参阅管理员指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/clientv2-admin-guide-powershell.md)。

## <a name="cmdlets-grouped-by-administration-task"></a>按管理任务对 cmdlet 进行分组

|如果你需要…|…请使用以下 cmdlet|
|-------------------|------------------------------|
|从本地权限管理（AD RMS 或 Windows RMS）迁移到 Azure 信息保护。|[导入-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd)<br /><br />[AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)|
|连接到组织的 Rights Management 服务或断开与该服务的连接。|[连接-AipService](/powershell/module/aipservice/connect-aipservice)<br /><br />[断开-AipServiceService](/powershell/module/aipservice/disconnect-aipservice)|
|生成和管理你自己的租户密钥 –“自带密钥”(BYOK) 方案。|[AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)<br /><br />[使用-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey)<br /><br />[AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys)|
|激活或停用组织的 Rights Management 服务。<br /><br />还可以在管理门户中执行这些操作。 有关详细信息，请参阅[激活 Azure 信息保护的保护服务](activate-service.md)。|[AipService](/powershell/module/aipservice/enable-aipservice)<br /><br />[AipService](/powershell/module/aipservice/disable-aipservice)|
|为 Azure Rights Management 服务的分阶段部署配置内置控件。|[AipServiceOnboardingControlPolicy](/powershell/module/aipservice/get-aipserviceonboardingcontrolpolicy)<br /><br />[AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)|
|为你的组织创建和管理 Rights Management 模板。<br /><br />虽然 PowerShell 可提供更精密的控制，但也可以从 Azure 门户执行大多数操作。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)。|[AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)<br /><br />[导出-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)<br /><br />[AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)<br /><br />[AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)<br /><br />[导入-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetemplate)<br /><br />[新-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)<br /><br />[AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)<br /><br />[AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)|
|配置在没有 internet 连接的情况下，可以访问你的组织保护的内容的最大天数 (使用许可证有效期) 。|[AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/get-aipservicemaxuselicensevaliditytime)<br /><br />[AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)|
|管理组织的 Rights Management 的超级用户功能。|[AipServiceSuperUserFeature](/powershell/module/aipservice/enable-aipservicesuperuserfeature)<br /><br />[AipServiceSuperUserFeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature)<br /><br />[AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser)<br /><br />[AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser)<br /><br />[AipServiceSuperUser](/powershell/module/aipservice/remove-aipservicesuperuser)<br /><br />[AAipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup)<br /><br />[AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup)<br /><br />[AipServiceSuperUserGroup](/powershell/module/aipservice/clear-aipservicesuperusergroup)|
|管理被授权管理组织的 Rights Management 服务的用户和组。|[Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator)<br /><br />[Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator)<br /><br />[Aip-ServiceRoleBasedAdministrator](/powershell/module/aipservice/remove-aipservicerolebasedadministrator)|
|获取组织的 Rights Management 管理任务的日志。|[AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)|
|记录和分析 Rights Management 的使用情况日志记录。|[AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog)|
|显示组织的当前 Rights Management 服务配置。|[AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)|
|将组织从 Azure 信息保护迁移到本地 AD RMS 部署。|[AipServiceMigrationUrl](/powershell/module/aipservice/set-aipservicemigrationurl)<br /><br />[AipServiceMigrationUrl](/powershell/module/aipservice/get-aipservicemigrationurl)|
|管理适用于 Azure 信息保护的文档跟踪站点。<br><br>仅 **适用于**：经典客户端|[AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature)<br /><br />[AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature)<br /><br />[AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature)<br /><br />[AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/set-aipservicedonottrackusergroup)<br /><br />[AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Clear-AipServiceDoNotTrackUserGroup)<br /><br />[AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/get-AipServiceDoNotTrackUserGroup)<br /><br />[AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)<br /><br />[AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)|
| | |
