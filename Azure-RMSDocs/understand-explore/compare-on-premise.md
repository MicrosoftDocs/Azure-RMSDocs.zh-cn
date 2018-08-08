---
title: 比较 Azure 信息保护和 AD RMS
description: 如果你了解或以前部署过 Active Directory Rights Management Services (AD RMS)，你可能想知道 Azure 信息保护在功能和要求方面与它相比有何差别。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: fcf31485505b1daff3571c33e5262fd6f7586b77
ms.sourcegitcommit: 6cbd03b28873b192dc730556c6dd5a7da6e705df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39410996"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>比较 Azure 信息保护与 AD RMS

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

如果你了解或以前部署过 Active Directory Rights Management Services (AD RMS)，你可能想知道 Azure 信息保护作为信息保护解决方案在功能和要求方面与它相比有何差别。

Azure 信息保护的一些主要差异：

- **无需服务器基础结构**：Azure 信息保护不需要 AD RMS 所需的额外服务器和 PKI 证书，因为 Microsoft Azure 将处理那些内容。 因而这一云解决方案可以更快部署且更易维护。

- **基于云的身份验证**：对于内部用户和来自其他组织的用户，Azure 信息保护都使用 Azure AD 进行身份验证。 这意味着即使移动用户未连接到你的内部网络，也可对其进行身份验证，并且你可以更轻松地与来自其他组织的用户共享受保护的内容。 许多组织由于运行 Azure 服务或使用 Office 365，因而在 Azure AD 中已拥有用户帐户。 但是如果没有，个人的 RMS 可以让用户创建一个免费帐户，或者 Microsoft 帐户可以用于[支持此 Azure 信息保护身份验证的应用程序](../get-started/secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)。 若要与其他组织共享受 AD RMS 保护的内容，则需要对每个组织配置显式信任。

- **对移动设备的内置支持**：无需进行部署更改，Azure RMS 即可支持移动设备和 Mac 计算机。 若要使 AD RMS 支持这些设备，必须安装移动设备扩展、配置 AD FS 以便进行联合身份验证，并为公共 DNS 服务创建其他记录。

- **默认模板**：激活 Azure 信息保护后，该保护服务将创建两个默认模板，让你可以轻松地立即开始保护重要数据。 AD RMS 无默认模板。

- **部门模板**：Azure 信息保护支持部门模板，它是你所创建额外模板的一项配置设置。 通过此配置，可指定部分用户在其客户端应用程序中看到特定模板。 通过限制用户可查看的模板数量，使他们更容易选择你为不同用户组定义的正确策略。 AD RMS 不支持部门模板。

- **文档跟踪和吊销**：Azure 信息保护通过 Azure信息保护客户端支持这些功能，而 AD RMS 不支持。

- **分类和标记**： Azure 信息保护通过与 Office 应用程序和文件资源浏览器集成的 Azure 信息保护客户端支持这些功能，而 AD RMS 不支持。


此外，由于 Azure 信息保护是一项云服务，因此与基于本地服务器的解决方案相比，它可以更快交付新功能和修补程序。 Windows Server 2016 中未为 AD RMS 规划新功能。

有关详细信息和其他差别，请使用以下表格并排比较 Azure 信息保护和 AD RMS 的功能和优势。 如果你有安全方面的比较问题，请参阅本文中的[签名和加密的加密控制](#cryptographic-controls-for-signing-and-encryption)。

> [!NOTE]
> 为了简化这种比较，本文重复了 [Azure 信息保护的要求](../get-started/requirements-azure-rms.md)中的一些信息。 使用该资源了解有关 Azure Rights Management 的更具体的支持和版本信息。

|Azure Information Protection|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|支持 Microsoft Online Services（例如  Exchange Online 和 SharePoint Online 以及 Office 365）中的信息权限管理 (IRM) 功能。<br /><br />还支持本地 Microsoft 服务器产品，例如 Exchange Server、SharePoint Server 以及运行 Windows Server 和文件分类基础结构 (FCI) 的文件服务器。|支持本地 Microsoft 服务器产品，例如 Exchange Server、SharePoint Server 以及运行 Windows Server 和文件分类基础结构 (FCI) 的文件服务器。|
|与任何也使用 Azure AD 进行身份验证的组织自动实现文档的安全协作。 这意味着组织可以保护其与外部或其他组织共享的文档。|在组织外部实现文档的安全协作要求在两个组织之间以直接点对点的关系显式定义身份验证信任。 必须配置受信任的用户域 (TUD) 或使用 Active Directory 联合身份验证服务 (AD FS) 创建的联合信任。|
|如果不存在任何身份验证信任关系，则向用户发送受保护的电子邮件（可选择附加自动受到保护的 Office 文档附件）。 使用联合与社交提供程序或一次性密码和 Web 浏览器进行查看时可能需要采取这种操作。|如果不存在任何身份验证信任关系，则不支持发送受保护的电子邮件。|
|提供两个默认权限策略模板，将内容的访问权限仅限于自己的组织范围内；一个模板提供受保护内容的只读查看，另一个模板提供受保护内容的写入或修改权限。<br /><br />还可创建自己的自定义模板，其中包括只对用户的子集可见的部门模板。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](../deploy-use/configure-policy-templates.md)。<br /><br />此外，如果模板不能满足需求，用户可以定义自己的一组权限。|没有默认模板；必须创建这些模板，然后分发自己的模板。 有关详细信息，请参阅 [AD RMS 策略模板注意事项](http://go.microsoft.com/fwlink/?LinkId=154765)。<br /><br />此外，如果模板不能满足需求，用户可以定义自己的一组权限。|
|支持的 Microsoft Office 最低版本为 Office 2010，它需要 [Azure 信息保护客户端](../rms-client/aip-client.md)或 RMS 共享应用程序。<br /><br />Microsoft Office for Mac：<br /><br />- Microsoft Office for Mac 2016：受支持<br /><br />- Microsoft Office for Mac 2011：不受支持|支持的 Microsoft Office 最低版本为 Office 2007。<br /><br />Microsoft Office for Mac：<br /><br />- Microsoft Office for Mac 2016：受支持<br /><br />- Microsoft Office for Mac 2011：受支持|
|支持适用于 Windows、iOS 和 Android 的 [Azure 信息保护客户端](../rms-client/aip-client.md)。 RMS 共享应用继续支持 Mac 计算机和 Windows Phone。<br /><br />此外，Azure 信息保护客户端支持以下各项：<br /><br />- 与其他组织的用户共享。<br /><br />- 适用于用户的文档跟踪站点，包括撤消文档的功能。|支持适用于 Windows、iOS 和 Android 的 [Azure 信息保护客户端](../rms-client/aip-client.md)。 RMS 共享应用继续支持 Mac 计算机和 Windows Phone。 但是，共享不支持与其他组织的用户共享或文档跟踪站点以及用户撤销文档的功能。|
|使用 Azure 信息保护客户端时，可以对大多数[文件类型](../rms-client/client-admin-guide-file-types.md)进行分类和保护。<br /><br />对于其他应用程序，检查[支持 Azure Rights Management 数据保护的应用程序](../get-started/requirements-applications.md)中的表。|使用 Azure 信息保护客户端时，可以对大多数[文件类型](../rms-client/client-admin-guide-file-types.md)进行保护。<br /><br />对于其他应用程序，检查[支持 Azure Rights Management 数据保护的应用程序](../get-started/requirements-applications.md)中的表。|
|支持的 Windows 客户端最低版本为 Windows 7 SP1。|支持的 Windows 客户端最低版本为 Windows 7 SP1。|
|移动设备支持包括 Windows Phone、Android、iOS 和 Windows RT。<br /><br />在支持 Exchange ActiveSync IRM 协议的所有移动设备平台上，也支持使用该协议管理电子邮件。|移动设备支持包括 Windows Phone、Android、iOS 和 Windows RT，并需要 [Active Directory Rights Management 服务移动设备扩展](http://technet.microsoft.com/library/dn673574.aspx)。<br /><br />在支持 Exchange ActiveSync IRM 协议的所有移动设备平台上，支持使用 Exchange ActiveSync IRM 管理电子邮件。|
|支持适用于计算机和移动设备的多因素身份验证 (MFA)。<br /><br />有关详细信息，请参阅[多重身份验证 (MFA) 和 Azure 信息保护](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection)。|如果将 IIS 配置为请求证书，将支持智能卡身份验证。|
|支持加密模式 2，而无需额外配置，该模式针对各种密钥长度和加密算法提供更强大的安全性。<br /><br />有关详细信息，请参阅本文中的[对签名和加密的加密控制](#cryptographic-controls-for-signing-and-encryption)部分以及 [AD RMS 加密模式](http://go.microsoft.com/fwlink/?LinkId=266659)。|默认情况下支持加密模式 1，需要额外配置才能支持加密算法 2，以提供更强大的安全性。<br /><br />有关详细信息，请参阅本文中的[对签名和加密的加密控制](#cryptographic-controls-for-signing-and-encryption)部分以及 [AD RMS 加密模式](http://go.microsoft.com/fwlink/?LinkId=266659)。|
|支持从 AD RMS 迁移，如果需要，支持迁移到 AD RMS：<br /><br />- [从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [解除 Azure 信息保护授权并停用 Azure 信息保护](../deploy-use/decommission-deactivate.md)|支持从 Azure 信息保护迁移以及迁移到 Azure 信息保护：<br /><br />- [解除 Azure 权限管理授权并停用 Azure 权限管理](../deploy-use/decommission-deactivate.md)<br /><br />- [从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)|
|需要 Office 365 的 Azure 信息保护许可证或 Azure 权限管理许可证才能保护内容。 无需许可证即可使用已受 Azure 信息保护（包括另一个组织的用户）保护的内容。<br /><br />有关详细信息，请参阅 Azure 信息保护网站上的[功能列表](https://www.microsoft.com/cloud-platform/azure-information-protection-features)。|需要 RMS 许可证才能保护内容，以及使用已受 AD RMS 保护的内容。<br /><br />有关 AD RMS 授权的详细信息，如果是一般信息，请参阅 [客户端访问许可证和管理许可证](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) ，如果是特定信息，请联系 Microsoft 合作伙伴或 Microsoft 代表。|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>对签名和加密的加密控制
默认情况下，Azure 信息保护将 RSA 2048 用于所有公钥加密，将 SHA 256 用于签名操作。 相比之下，AD RMS 支持 RSA 1024 和 RSA 2048，还将 SHA 1 或 SHA 256 用于签名操作。

Azure 信息保护和 AD RMS 都将 AES 128 用于对称加密。

租户密钥大小为 2048 位时，Azure 信息保护符合 FIPS 140-2，这是激活 Azure Rights Management 服务时的默认设置。 

有关加密控制的详细信息，请参阅 [Azure RMS 使用的加密控制：算法和密钥长度](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)。


## <a name="next-steps"></a>后续步骤
如果希望从 AD RMS 迁移到 Azure 信息保护，请参阅[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)


