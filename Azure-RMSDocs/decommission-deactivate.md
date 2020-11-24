---
title: 解除授权和停用 Azure RMS
description: 有关决定不再使用 Azure 信息保护中基于云的保护服务的相关信息和说明。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f52bcf18c1348f4e4b6f4985c355ba227308cdc1
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "95566308"
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>解除 Azure 信息保护授权并停用对 Azure 信息保护的保护

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

可以通过使用 Azure 信息保护中的 Azure 权限管理服务，始终控制你组织是否保护内容。 如果你确定不再想要使用此信息保护服务，我们可以保证你仍可以访问以前保护的内容。

如果不需要继续访问之前受保护的内容，请停用该服务，让 Azure 信息保护订阅过期。 例如，这适用于完成测试 Azure 信息保护后再在生产环境中部署它的情况。

但是，如果已在生产和受保护的文档和电子邮件中部署了 Azure 信息保护，请确保在停用 Azure Rights Management 服务之前，你有 Azure 信息保护租户密钥副本和合适的可信发布域 (TPD) 。 请确保在订阅过期之前拥有密钥副本和 TPD，以确保你可以保留对该服务停用后由 Azure Rights Management 保护的内容的访问权限。 

如果你使用了可以在 HSM 中生成和管理自己的密钥的自带密钥 (BYOK) 解决方案，则你已经具有 Azure 信息保护租户密钥。 如果按照 [为未来云出口做好准备](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631)的说明进行操作，还会有合适的 TPD。 但是，如果你的租户密钥由 Microsoft 管理 (默认) ，请参阅 [Azure 信息保护租户密钥的操作](operations-tenant-key.md) 中有关导出租户密钥的说明文章。

> [!TIP]
> 即使在订阅到期后，Azure 信息保护租户仍可在延长期内用于使用内容。 但是，你将无法再导出租户密钥。

使用 Azure 信息保护租户密钥和 TPD 时，可以在本地部署 Rights Management (AD RMS) 并将租户密钥导入为受信任的发布域 (TPD) 。 然后，可以使用以下选项解除 Azure 信息保护部署的授权：

|如果这适用于你…|… 采取的措施：|
|----------------------------|--------------|
|你希望所有用户继续使用 Rights Management，但使用本地解决方案而不使用 Azure 信息保护    →|使用 Office 2016 或 Office 2013 的 **LicensingRedirection** 注册表项，将客户端重定向到本地部署。 有关说明，请参阅 RMS 客户端部署说明中的 [服务发现部分](./rms-client/client-deployment-notes.md) 。 对于 Office 2010，请使用 Office 2010 的 **LicenseServerRedirection** 注册表项，如 [office 注册表设置](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10))中所述。|
|你想要完全停止使用 Rights Management    →|赋予指定管理员[超级用户权限](configure-super-users.md)，并为此用户安装 [Azure 信息保护客户端](./rms-client/client-admin-guide-install.md)。<br /><br />然后，此管理员可以使用此客户端的 PowerShell 模块批量解密受 Azure 信息保护保护的文件夹中的文件。 文件还原到未受保护状态，因此可在不使用 Azure 信息保护或 AD RMS 等 Rights Management 技术的情况下进行读取。 由于此 PowerShell 模块可与 Azure 信息保护和 AD RMS 一起使用，因此你可以选择在停用 Azure 信息保护中的保护服务或组合之前或之后对文件进行解密。|
|无法识别所有受 Azure 信息保护保护的文件。 或者，你希望所有用户都可以自动读取任何丢失的受保护的文件    →|按照 RMS 客户端部署说明中的 [服务发现部分](./rms-client/client-deployment-notes.md)中所述，在所有客户端计算机上部署注册表设置，方法是使用 Office 2016 和 office 2013 的 **LicensingRedirection** 注册表项。 对于 Office 2010，请使用 **LicenseServerRedirection** 注册表项，如 [Office 注册表设置](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10))中所述。<br /><br />另外，部署其他注册表设置以防止用户保护新文件，方法是将 **DisableCreation** 设置为 **1**，如 [Office 注册表设置](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10))中所述。|
|你需要针对任何丢失文件的受控的手动恢复服务    →|赋予数据恢复组中的指定用户[超级用户权限](configure-super-users.md)，并为这些用户安装 [Azure 信息保护客户端](./rms-client/client-admin-guide-install.md)，以便在标准用户请求此操作时取消文件保护。<br /><br />在所有计算机上，部署注册表设置以防止用户通过将 **DisableCreation** 设置为 **1** 来保护新文件，如 [Office 注册表设置](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10))中所述。|

有关此表中的步骤的详细信息，请参阅以下资源：

- 有关 AD RMS 和部署引用的信息，请参阅 [Active Directory Rights Management Services 概述](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831364(v=ws.11))。

- 有关将 Azure 信息保护租户密钥导入为 TPD 文件的说明，请参阅 [添加可信发布域](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771460(v=ws.11))。

- 若要将 PowerShell 与 Azure 信息保护客户端配合使用，请参阅将 [PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。

准备好从 Azure 信息保护中停用保护服务时，请使用以下说明。

## <a name="deactivating-rights-management"></a>停用权限管理
使用以下过程之一来停用保护服务 Azure Rights Management。

> [!TIP]
> 你还可以使用 PowerShell cmdlet [AipService](/powershell/module/aipservice/disable-aipservice)来停用 Rights Management。

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>从 Microsoft 365 管理中心停用权限管理

1. 请参阅 Microsoft 365 管理员的 " [Rights Management" 页](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) 。
    
    如果系统提示你登录，请使用 Microsoft 365 的全局管理员帐户。

2. 在“权限管理”页中，单击“停用”。

3.  出现提示时 **，是否要停用 Rights Management？单击 "** **停用**"。

现在，应会显示“权限管理未激活”和用于激活的选项。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>从 Azure 门户停用 Rights Management

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到“Azure 信息保护”窗格。

    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。

2. 在初始 " **Azure 信息保护** " 窗格上，选择 " **保护激活**"。 

3.  在 " **Azure 信息保护-保护激活** " 窗格上，选择 " **停用**"。 选择“是”以确认你的选择。

信息栏会显示“停用已成功完成”且“停用”现在已替换为“激活”。