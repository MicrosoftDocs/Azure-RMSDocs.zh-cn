---
title: "使用 Windows PowerShell 管理 Azure Rights Management 服务 | Azure 信息保护"
description: "了解如何使用适用于 Azure 信息保护的 Azure 权限管理服务的 PowerShell 模块 (AADRM) 为组织管理此服务。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/14/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 16d6a8a00db28c23fd650a1b8beba00333ba6ea4
ms.openlocfilehash: f9aa0d5910ba4868878ae54c446793bfc031d3c2


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
|从本地权限管理（AD RMS 或 Windows RMS）迁移到 Azure 信息保护。|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|连接到组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务或断开与该服务的连接。|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|生成和管理你自己的租户密钥 –“自带密钥”(BYOK) 方案。|[Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|激活或停用组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务。<br /><br />还可以在管理门户中执行这些操作。 有关详细信息，请参阅[激活 Azure 权限管理服务](activate-service.md)。|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|禁用或启用适用于 Azure 信息保护的文档跟踪站点。|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|为 Azure Rights Management 服务的分阶段部署配置内置控件。|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|为你的组织创建和管理 Rights Management 模板。<br /><br />虽然 PowerShell 可提供更精密的控制，但你也可以从 Azure 经典门户执行大多数操作。 有关详细信息，请参阅[为 Azure Rights Management 服务配置自定义模板](configure-custom-templates.md)。|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Export-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Import-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|配置在没有 Internet 连接的情况下，可以访问你的组织保护的内容的最大天数（使用许可证有效期）。|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|管理组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]的超级用户功能。|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|管理被授权管理组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务的用户和组。|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|获取组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]管理任务的日志。|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|记录和分析[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]的使用日志记录。|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|显示组织的当前[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务配置。|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|将组织从 Azure 信息保护迁移到本地 AD RMS 部署。|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Feb17_HO2-->


