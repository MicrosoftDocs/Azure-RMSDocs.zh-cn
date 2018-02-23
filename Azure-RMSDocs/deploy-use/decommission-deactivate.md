---
title: "解除授权和停用 Azure RMS"
description: "有关决定不再使用 Azure 信息保护中基于云的保护服务的相关信息和说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 14887bb14599b24d95a19ee111ec3ab30ea95612
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>解除 Azure 信息保护授权并停用对 Azure 信息保护的保护

>*适用于：Azure 信息保护、Office 365*

可以通过使用 Azure 信息保护中的 Azure 权限管理服务，始终控制你组织是否保护内容。 如果你确定不再想要使用此信息保护服务，我们可以保证你仍可以访问以前保护的内容。

如果不需要继续访问之前受保护的内容，请停用该服务，让 Azure 信息保护订阅过期。 例如，这适用于完成测试 Azure 信息保护后再在生产环境中部署它的情况。

但是，如果已在生产中部署 Azure 信息保护并保护文档和电子邮件，请确保在停用 Azure 权限管理服务前，拥有 Azure 信息保护租户密钥的副本。 请确保在订阅过期前拥有密钥副本，以确保在停用服务后，可以保留对由 Azure 权限管理保护的内容的访问权限。 如果你使用了可以在 HSM 中生成和管理自己的密钥的自带密钥 (BYOK) 解决方案，则你已经具有 Azure 信息保护租户密钥。 但如果该密钥由 Microsoft 管理（默认），请参阅 [Azure Rights Management 租户密钥的操作](operations-tenant-key.md)文章中有关导出租户密钥的说明。

> [!TIP]
> 即使在订阅到期后，Azure 信息保护租户仍可在延长期内用于使用内容。 但是，你将无法再导出租户密钥。

如果具有 Azure 信息保护租户密钥，你可以本地部署 Rights Management (AD RMS)，并将租户密钥导入为可信发布域 (TPD)。 然后，可以使用以下选项解除 Azure 信息保护部署的授权：

|如果这适用于你…|… 采取的措施：|
|----------------------------|--------------|
|你希望所有用户继续使用 Rights Management，但使用本地解决方案而不使用 Azure 信息保护    →|当现有用户使用经过此更改之后受保护的内容时，请使用 [Set-AadrmMigrationUrl](/powershell/module/aadrm/Set-AadrmMigrationUrl) cmdlet 将他们定向至本地部署。 用户将自动使用 AD RMS 安装以使用受保护内容。<br /><br />对于要使用此更改之前受保护内容的用户，可使用 Office 2016 或 Office 2013 的“LicensingRedirection”注册表项将客户端重定向到本地部署。 有关说明，请参阅 RMS 客户端部署说明中的[服务发现部分](../rms-client/client-deployment-notes.md)，以及 Office 2010 的 LicenseServerRedirection 注册表项，如 [Office Registry Settings](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)（Office 注册表设置）中所述。|
|你想要完全停止使用 Rights Management    →|赋予指定管理员[超级用户权限](../deploy-use/configure-super-users.md)，并为此用户安装 [Azure 信息保护客户端](../rms-client/client-admin-guide-install.md)。<br /><br />然后，此管理员可以使用此客户端的 PowerShell 模块批量解密受 Azure 权限管理服务保护的文件夹中的文件。 文件还原到未受保护状态，因此可在不使用 Azure 信息保护或 AD RMS 等 Rights Management 技术的情况下进行读取。 因为此 PowerShell 模块可以与 Azure 信息保护中的 Azure 权限管理服务和 AD RMS 共同使用，因此可以选择在停用 Azure 权限管理服务之前或之后解密文件，或者将两者结合起来。|
|无法标识所有由 Azure 信息保护中的 Azure 权限管理服务保护的文件。 或者，你希望所有用户都可以自动读取任何丢失的受保护的文件   →|在所有客户端计算机上部署注册表设置，方法是使用 Office 2016 和 Office 2013 的 **LicensingRedirection** 注册表项（如在 RMS 客户端部署注释中的[服务发现部分](../rms-client/client-deployment-notes.md)中所述）和 Office 2010 的 **LicenseServerRedirection** 注册表项（如 [Office 注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述）。<br /><br />另外，部署其他注册表设置以防止用户保护新文件，方法是将 **DisableCreation** 设置为 **1**，如 [Office注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述。|
|你需要针对任何丢失文件的受控的手动恢复服务    →|赋予数据恢复组中的指定用户[超级用户权限](../deploy-use/configure-super-users.md)，并为这些用户安装 [Azure 信息保护客户端](../rms-client/client-admin-guide-install.md)，以便在标准用户请求此操作时取消文件保护。<br /><br />在所有计算机上部署注册表设置以防止用户保护新文件，方法是将 **DisableCreation** 设置为 **1**（如 [Office 注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述）。|
有关此表中的步骤的详细信息，请参阅以下资源：

- 有关 AD RMS 和部署引用的信息，请参阅 [Active Directory Rights Management Service 概述](https://technet.microsoft.com/library/hh831364.aspx)。

- 有关将 Azure 信息保护租户密钥导入为 TPD 文件的说明，请参阅 [添加可信发布域](https://technet.microsoft.com/library/cc771460.aspx)。

- 如果你需要安装适用于 Azure Rights Management 的 Windows PowerShell 模块以设置迁移 URL，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。

- 若要将 PowerShell 与 Azure 信息保护客户端配合使用，请参阅将 [PowerShell 与 Azure 信息保护客户端配合使用](../rms-client/client-admin-guide-powershell.md)。

准备好为组织停用 Azure Rights Management 服务时，请使用以下说明。

## <a name="deactivating-rights-management"></a>停用权限管理
使用以下某个过程来停用[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]。

> [!TIP]
> 也可以使用 Windows PowerShell cmdlet [Disable-Aadrm](/powershell/module/aadrm/disable-aadrm) 来停用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]。

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>从 Office 365 管理中心停用权限管理

1. 转到 Office 365 管理员的 [Rights Management 页](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)。
    
    如果系统提示登录，请使用 Office 365 的全局管理员帐户。    

2. 在“Rights Management”  页面中，单击“停用” 。

3.  当提示“是否要停用 Rights Management?”时，请单击“停用”。

现在，你应该会看到“Rights Management 未激活”  和用于激活的选项。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>从 Azure 门户停用 Rights Management

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“更多服务”，然后在“筛选”框中开始键入**信息**。 选择“Azure 信息保护”。

2. 在初始“Azure 信息保护”边栏选项卡上，选择“保护激活”。 

3.  在“Azure 信息保护” -“保护激活”边栏选项卡上，选择“停用”。 选择“是”以确认你的选择。

信息栏会显示“停用已成功完成”且“停用”现在已替换为“激活”。 


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


