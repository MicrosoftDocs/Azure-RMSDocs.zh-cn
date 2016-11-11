---
title: "解除 Azure Rights Management 服务授权和停用 Azure Rights Management 服务 | Azure 信息保护"
description: "如果你决定不再想要使用 Azure 信息保护中的此信息保护服务，本文提供相关的信息和说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 865913eae3e0956c18d2caef4e68ab1dc07d74de


---

# <a name="decommissioning-and-deactivating-azure-rights-management"></a>解除 Azure Rights Management 授权和停用 Azure Rights Management

>*适用于：Azure 信息保护、Office 365*

通过使用 Azure 信息保护中的 Azure Rights Management 服务，你可以始终控制你的组织是否要保护内容；如果你决定不再想要使用此信息保护服务，我们可以保证你仍然可以访问之前受保护的内容。 如果你不需要继续访问之前受保护的内容，仅需停用该服务，让 Azure 信息保护订阅过期即可。 例如，这适用于完成测试 Azure 信息保护后再在生产环境中部署它的情况。

但是，如果你已经在生产、受保护的文档和电子邮件中部署了 Azure 信息保护，请确保你在停用 Azure Rights Management 服务之前具有 Azure 信息保护租户密钥的副本，并且要在订阅到期前执行此操作，因为这将确保你可以保留对该服务停用后由 Azure Rights Management 保护的内容的访问权限。 如果你使用了可以在 HSM 中生成和管理自己的密钥的自带密钥 (BYOK) 解决方案，则你已经具有 Azure 信息保护租户密钥。 但如果该密钥由 Microsoft 管理（默认），请参阅 [Azure Rights Management 租户密钥的操作](operations-tenant-key.md)文章中有关导出租户密钥的说明。

> [!TIP]
> 即使在订阅到期后，Azure 信息保护租户仍可在延长期内用于使用内容。 但是，你将无法再导出租户密钥。

如果具有 Azure 信息保护租户密钥，你可以本地部署 Rights Management (AD RMS)，并将租户密钥导入为可信发布域 (TPD)。 然后，可以使用以下选项解除 Azure 信息保护部署的授权：

|如果这适用于你…|… 采取的措施：|
|----------------------------|--------------|
|你希望所有用户继续使用 Rights Management，但使用本地解决方案而不使用 Azure 信息保护    →|当现有用户使用经过此更改之后受保护的内容时，请使用 [Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) cmdlet 将他们定向至本地部署。 用户将自动使用 AD RMS 安装以使用受保护内容。<br /><br />对于使用在此更改之前受保护的内容的用户，请将客户端重定向至本地部署，方法是使用 Office 2016 或 Office 2013 的 **LicensingRedirection** 注册表项（如在 RMS 客户端部署注释中的[服务发现部分](../rms-client/client-deployment-notes.md)所述）和 Office 2010 的 **LicenseServerRedirection** 注册表项（如 [Office 注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述）。|
|你想要完全停止使用 Rights Management    →|赋予指定管理员[超级用户权限](../deploy-use/configure-super-users.md)并给予此管理员 [RMS 保护工具](http://www.microsoft.com/en-us/download/details.aspx?id=47256)。<br /><br />随后，此管理员可使用该工具批量解密之前由 Azure Rights Management 服务保护的文件夹中的文件，以便将文件还原为不受保护状态，因此可以不借助 Rights Management 技术（如 Azure 信息保护或 AD RMS）进行读取。 此工具可以与 Azure 信息保护中的 Azure Rights Management 服务和 AD RMS 共同使用，因此你可以选择在停用 Azure Rights Management 服务之前或之后解密文件，或者将两者结合起来。|
|你无法标识所有由 Azure 信息保护中的 Azure Rights Management 服务保护的文件，或者你希望用户可以自动读取任何丢失的受保护文件    →|在所有客户端计算机上部署注册表设置，方法是使用 Office 2016 和 Office 2013 的 **LicensingRedirection** 注册表项（如在 RMS 客户端部署注释中的[服务发现部分](../rms-client/client-deployment-notes.md)中所述）和 Office 2010 的 **LicenseServerRedirection** 注册表项（如 [Office 注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述）。<br /><br />另外，部署其他注册表设置以防止用户保护新文件，方法是将 **DisableCreation** 设置为 **1**，如 [Office注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述。|
|你需要针对任何丢失文件的受控的手动恢复服务    →|赋予数据恢复组中的指定用户 [超级用户权限](../deploy-use/configure-super-users.md)，并给予他们 [RMS 保护工具](http://www.microsoft.com/en-us/download/details.aspx?id=47256)，以便在标准用户提出请求时取消文件保护。<br /><br />在所有计算机上部署注册表设置以防止用户保护新文件，方法是将 **DisableCreation** 设置为 **1**（如 [Office 注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述）。|
有关此表中的步骤的详细信息，请参阅以下资源：

-   有关 AD RMS 和部署引用的信息，请参阅 [Active Directory Rights Management Service 概述](https://technet.microsoft.com/library/hh831364.aspx)。

-   有关将 Azure 信息保护租户密钥导入为 TPD 文件的说明，请参阅 [添加可信发布域](https://technet.microsoft.com/library/cc771460.aspx)。

-   如果你需要安装适用于 Azure Rights Management 的 Windows PowerShell 模块以设置迁移 URL，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。

准备好为组织停用 Azure Rights Management 服务时，请使用以下说明。

## <a name="deactivating-rights-management"></a>停用权限管理
使用以下某个过程来停用[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]。

> [!TIP]
> 也可以使用 Windows PowerShell cmdlet [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) 来停用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]。

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>从 Office 365 管理中心停用权限管理

1.  使用你的工作或学校帐户（Office 365 部署的管理员）[登录到 Office 365](https://portal.office.com/) 。

2.  如果未自动显示 Office 365 管理中心，请选择左上方的“应用启动程序”图标，然后选择“管理”。 “管理”  磁贴只会向 Office 365 管理员显示。

    > [!TIP]
    > 有关管理中心的帮助，请参阅 [关于 Office 365 管理中心 - 管理员帮助](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)。

3.  在左窗格中，单击“服务设置” 。

4.  单击“权限管理” 。

5.  在 **“权限管理”** 页上，单击 **“管理”**。

6.  在“Rights Management”  页面中，单击“停用” 。

7.  当提示“是否要停用 Rights Management?”时，请单击“停用”。

现在，你应该会看到“Rights Management 未激活”  和用于激活的选项。

#### <a name="to-deactivate-rights-management-from-the-azure-classic-portal"></a>从 Azure 经典门户停用 Rights Management

1.  登录到 [Azure 经典门户](http://go.microsoft.com/fwlink/p/?LinkID=275081)。

2.  在左窗格中，单击“ACTIVE DIRECTORY” 。

3.  在 **“Active Directory”** 页中，单击 **“权限管理”**。

4.  为 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 选择要管理的目录，单击“停用”，然后确认你的操作。

“权限管理状态”现在应显示为“非活动”，而“停用”选项将替换为“激活”。






<!--HONumber=Nov16_HO2-->


