---
title: "使用 Windows PowerShell 管理 Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: bf1f684bc394ec3a1025f8c9ed3e57d07c598125


---

# 使用 Windows PowerShell 管理 Azure 权限管理

*适用于：Azure Rights Management、Office 365*

虽然你可以使用 [!INCLUDE[o365_2](../includes/o365_2_md.md)] 管理中心或 Azure 经典门户来激活 Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS)，但也可以使用适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (AADRM) 的 Windows PowerShell 模块来执行此操作。

在你激活[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]之后，可能不再需要对服务进行更多管理。 但是，有些高级配置方案可能要求你使用适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]的 Windows PowerShell 模块。 下表列出了一些使用 Windows PowerShell 的高级配置方案。 有关可用 cmdlet 的完整列表，以及关于每个 cmdlet 的详细信息，请参阅 [Azure Rights Management Cmdlet](http://msdn.microsoft.com/library/azure/dn629398.aspx)。

> [!NOTE]
> 如果你需要安装适用于 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的 Windows PowerShell 模块，请参阅 [安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。

此外还有一个补充的 Windows PowerShell 模块 **RMSProtection**，它支持 Azure RMS 和 AD RMS。 此模块支持保护或删除多个文件中的保护，以便你可以大量保护文件夹中的所有文件。 有关详细信息，请参阅 [为 Azure Rights Management 和发现服务或数据恢复配置超级用户](configure-super-users.md) 一文中的 [超级用户的脚本选项](configure-super-users.md#scripting-options-for-super-users) 部分。

|如果你需要…|…请使用以下 cmdlet|
|-------------------|------------------------------|
|从本地权限管理（AD RMS 或 Windows RMS）迁移到 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]。|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|连接到组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务或断开与该服务的连接。|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|生成和管理你自己的租户密钥 –“自带密钥”(BYOK) 方案。|[Add-AadrmKey](http://msdn.microsoft.com/library/azure/dn629418.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|激活或停用组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务。|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|禁用或启用适用于 Azure Rights Management 的文档跟踪站点。|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|为 Azure Rights Management 的分阶段部署配置内置控件。|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|为你的组织创建和管理权限策略模板。|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Export-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Import-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|配置在没有 Internet 连接的情况下，可以访问你的组织保护的内容的最大天数（使用许可证有效期）。|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|管理组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]的超级用户功能。|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|管理被授权管理组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务的用户和组。|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|获取组织的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]管理任务的日志。|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|记录和分析[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]的使用日志记录。|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|显示组织的当前[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务配置。|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|将组织从 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]迁移到本地 AD RMS 部署。|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|






<!--HONumber=Jun16_HO4-->


