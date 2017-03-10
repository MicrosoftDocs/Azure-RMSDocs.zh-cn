---
title: "使用 PowerShell 管理 Azure Rights Management - AIP"
description: "了解如何使用适用于 Azure 信息保护的 Azure 权限管理服务的 PowerShell 模块 (AADRM) 为组织管理此服务。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 1e2ca63ef811ca6fbce01e79846f18d2fd93d833
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="administering-the-azure-rights-management-service-by-using-windows-powershell"></a>使用 Windows PowerShell 管理 Azure Rights Management 服务

>*适用于：Azure 信息保护、Office 365*

是否需要使用 PowerShell 管理适用于 Azure 信息保护的 Azure 权限管理服务？ 如果你是全局管理员，则不需要。此服务需要的唯一配置是将其激活（或停用），然后配置 Rights Management 模板。

但是，对于更高级的配置则需要使用 PowerShell，并且如果你不是全局管理员，但全局管理员已向你授予管理此服务的权限，也需要使用 PowerShell。 如果想要让命令行控制和脚本编写更高效，也请使用 PowerShell。

下一部分中的表格包括一些使用 PowerShell 的高级配置方案。 如果不使用 PowerShell 也可完成配置，则此信息也包括在表中。

有关可用 cmdlet 的完整列表，以及关于每个 cmdlet 的详细信息，请参阅 [Azure Rights Management Cmdlet](http://msdn.microsoft.com/library/azure/dn629398.aspx)。

> [!NOTE]
> 若要安装此 PowerShell 模块，请参阅[安装适用于 Azure 权限管理的 Windows PowerShell](install-powershell.md)。

除了此服务端 PowerShell 模块，Azure 信息保护客户端还将安装一个补充 PowerShell 模块 **AzureInformationProtection**。 此客户端模块支持对多个文件进行分类和保护，这样可以方便某些操作，例如批量保护文件夹中的所有文件。 有关详细信息，请参阅管理员指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](../rms-client/client-admin-guide-powershell.md)。

## <a name="cmdlets-grouped-by-administration-task"></a>按管理任务对 cmdlet 进行分组

|如果你需要…|…请使用以下 cmdlet|
|-------------------|------------------------------|
|从本地权限管理（AD RMS 或 Windows RMS）迁移到 Azure 信息保护。|[Import-AadrmTpd](/powershell/aadrm/vlatest//import-aadrmtpd)|
|连接到组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务或断开与该服务的连接。|[Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice)<br /><br />[Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice)|
|生成和管理你自己的租户密钥 –“自带密钥”(BYOK) 方案。|[Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey)<br /><br />[Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys)|
|激活或停用组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务。<br /><br />还可以在管理门户中执行这些操作。 有关详细信息，请参阅[激活 Azure 权限管理服务](activate-service.md)。|[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm)<br /><br />[Disable-Aadrm](/powershell/aadrm/vlatest/disable-aadrm)|
|禁用或启用适用于 Azure 信息保护的文档跟踪站点。|[Disable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/disable-aadrmdocumenttrackingfeature)<br /><br />[Enable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/enable-aadrmdocumenttrackingfeature)<br /><br />[Get-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/get-aadrmdocumenttrackingfeature)|
|为 Azure Rights Management 服务的分阶段部署配置内置控件。|[Get-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/get-aadrmonboardingcontrolpolicy)<br /><br />[Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy)|
|为你的组织创建和管理 Rights Management 模板。<br /><br />虽然 PowerShell 可提供更精密的控制，但你也可以从 Azure 经典门户执行大多数操作。 有关详细信息，请参阅[为 Azure Rights Management 服务配置自定义模板](configure-custom-templates.md)。|[Add-AadrmTemplate](/powershell/aadrm/vlatest/add-aadrmtemplate)<br /><br />[Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate)<br /><br />[Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate)<br /><br />[Get-AadrmTemplateProperty](/powershell/aadrm/vlatest/get-aadrmtemplateproperty)<br /><br />[Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate)<br /><br />[New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition)<br /><br />[Remove-AadrmTemplate](/powershell/aadrm/vlatest/remove-aadrmtemplate)<br /><br />[Set-AadrmTemplateProperty](/powershell/aadrm/vlatest/set-aadrmtemplateproperty)|
|配置在没有 Internet 连接的情况下，可以访问你的组织保护的内容的最大天数（使用许可证有效期）。|[Get-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/get-aadrmmaxuselicensevaliditytime)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime)|
|管理组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]的超级用户功能。|[Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature)<br /><br />[Disable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/disable-aadrmsuperuserfeature)<br /><br />[Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser)<br /><br />[Get-AadrmSuperUser](/powershell/aadrm/vlatest/get-aadrmsuperuser)<br /><br />[Remove-AadrmSuperUser](/powershell/aadrm/vlatest/remove-aadrmsuperuser)<br /><br />[Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup)<br /><br />[Get-AadrmSuperUserGroup](/powershell/aadrm/vlatest/get-aadrmsuperusergroup)<br /><br />[Clear-AadrmSuperUserGroup](/powershell/aadrm/vlatest/clear-aadrmsuperusergroup)|
|管理被授权管理组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务的用户和组。|[Add-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/add-aadrmrolebasedadministrator)<br /><br />[Get-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/get-aadrmrolebasedadministrator)<br /><br />[Remove-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/remove-aadrmrolebasedadministrator)|
|获取组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]管理任务的日志。|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|记录和分析[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]的使用日志记录。|[Get-AadrmUserLog](/powershell/aadrm/vlatest/get-aadrmuserlog)|
|显示组织的当前[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务配置。|[Get-AadrmConfiguration](/powershell/aadrm/vlatest/get-aadrmconfiguration)|
|将组织从 Azure 信息保护迁移到本地 AD RMS 部署。|[Set-AadrmMigrationUrl](/powershell/aadrm/vlatest/set-aadrmmigrationurl)<br /><br />[Get-AadrmMigrationUrl](/powershell/aadrm/vlatest/get-aadrmmigrationurl)|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
