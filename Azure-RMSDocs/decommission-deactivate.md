---
title: 解除授权和停用 Azure RMS
description: 有关决定不再使用 Azure 信息保护中基于云的保护服务的相关信息和说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 683434b4094ca694539613279d0fae74bdde7be1
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520554"
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>解除 Azure 信息保护授权并停用对 Azure 信息保护的保护

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

可以通过使用 Azure 信息保护中的 Azure 权限管理服务，始终控制你组织是否保护内容。 如果你确定不再想要使用此信息保护服务，我们可以保证你仍可以访问以前保护的内容。

如果不需要继续访问之前受保护的内容，请停用该服务，让 Azure 信息保护订阅过期。 例如，这适用于完成测试 Azure 信息保护后再在生产环境中部署它的情况。

但是，如果已在生产中部署 Azure 信息保护并保护文档和电子邮件，请确保在停用 Azure 权限管理服务前，拥有 Azure 信息保护租户密钥的副本。 请确保在订阅过期前拥有密钥副本，以确保在停用服务后，可以保留对由 Azure 权限管理保护的内容的访问权限。 如果你使用了可以在 HSM 中生成和管理自己的密钥的自带密钥 (BYOK) 解决方案，则你已经具有 Azure 信息保护租户密钥。 不过，如果密钥是由 Microsoft 管理（默认情况），请参阅 [Azure 信息保护租户密钥操作](operations-tenant-key.md)一文，了解如何导出租户密钥。

> [!TIP]
> 即使在订阅到期后，Azure 信息保护租户仍可在延长期内用于使用内容。 但是，你将无法再导出租户密钥。

如果具有 Azure 信息保护租户密钥，你可以本地部署 Rights Management (AD RMS)，并将租户密钥导入为可信发布域 (TPD)。 然后，可以使用以下选项解除 Azure 信息保护部署的授权：

|如果这适用于你…|… 采取的措施：|
|----------------------------|--------------|
|你希望所有用户继续使用 Rights Management，但使用本地解决方案而不使用 Azure 信息保护    →|将你的客户端重定向到的本地部署，通过使用**LicensingRedirection** Office 2016 或 Office 2013 的注册表项。 有关说明，请参阅[服务发现部分](./rms-client/client-deployment-notes.md)在 RMS 客户端部署说明。 对于 Office 2010，请使用**LicenseServerRedirection**注册表项中所述的 Office 2010 [Office 注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)。|
|你想要完全停止使用 Rights Management    →|赋予指定管理员[超级用户权限](configure-super-users.md)，并为此用户安装 [Azure 信息保护客户端](./rms-client/client-admin-guide-install.md)。<br /><br />然后，此管理员可以使用此客户端的 PowerShell 模块批量解密受保护的 Azure 信息保护的文件夹中的文件。 文件还原到未受保护状态，因此可在不使用 Azure 信息保护或 AD RMS 等 Rights Management 技术的情况下进行读取。 由于此 PowerShell 模块可以使用 Azure 信息保护和 AD RMS，必须选择解密文件之前或之后停用 Azure 信息保护或组合的保护服务。|
|不能用于标识所有受保护的 Azure 信息保护的文件。 或者，你希望所有用户都可以自动读取任何丢失的受保护的文件    →|使用部署所有客户端计算机上的注册表设置**LicensingRedirection** Office 2016 和 Office 2013，如中所述的注册表项[服务发现部分](./rms-client/client-deployment-notes.md)在 RMS 客户端部署说明。 对于 Office 2010，请使用**LicenseServerRedirection**注册表项，如中所述[Office 注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)。<br /><br />另外，部署其他注册表设置以防止用户保护新文件，方法是将 **DisableCreation** 设置为 **1**，如 [Office注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述。|
|你需要针对任何丢失文件的受控的手动恢复服务    →|赋予数据恢复组中的指定用户[超级用户权限](configure-super-users.md)，并为这些用户安装 [Azure 信息保护客户端](./rms-client/client-admin-guide-install.md)，以便在标准用户请求此操作时取消文件保护。<br /><br />在所有计算机上部署注册表设置以防止用户保护新文件，方法是将 **DisableCreation** 设置为 **1**（如 [Office 注册表设置](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述）。|

有关此表中的步骤的详细信息，请参阅以下资源：

- 有关 AD RMS 和部署引用的信息，请参阅 [Active Directory Rights Management Service 概述](https://technet.microsoft.com/library/hh831364.aspx)。

- 有关将 Azure 信息保护租户密钥导入为 TPD 文件的说明，请参阅 [添加可信发布域](https://technet.microsoft.com/library/cc771460.aspx)。

- 若要将 PowerShell 与 Azure 信息保护客户端配合使用，请参阅将 [PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。

若要停用 Azure 信息保护中的保护服务准备就绪后，请按照以下说明。

## <a name="deactivating-rights-management"></a>停用权限管理
使用以下过程之一来停用保护服务，Azure Rights Management。

> [!TIP]
> 此外可以使用 PowerShell cmdlet[禁用 AipService](/powershell/module/aipservice/disable-aipservice)来停用 Rights Management。

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>从 Microsoft 365 管理中心停用权限管理

1. 转到 Office 365 管理员的 [Rights Management 页](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)。
    
    如果系统提示登录，请使用 Office 365 的全局管理员帐户。

2. 在“Rights Management”  页面中，单击“停用”  。

3.  当提示“是否要停用 Rights Management?”  时，请单击“停用”  。

现在，你应该会看到“Rights Management 未激活”  和用于激活的选项。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>从 Azure 门户停用 Rights Management

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”  边栏选项卡。

    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”   。 选择“Azure 信息保护”。 

2. 在初始“Azure 信息保护”边栏选项卡上，选择“保护激活”   。 

3.  在“Azure 信息保护” -“保护激活”边栏选项卡上，选择“停用”   。 选择“是”  以确认你的选择。

信息栏会显示“停用已成功完成”  且“停用”  现在已替换为“激活”  。 
