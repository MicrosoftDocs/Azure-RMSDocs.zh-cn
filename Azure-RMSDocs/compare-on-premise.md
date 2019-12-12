---
title: 比较 Azure 信息保护和 AD RMS - AIP
description: 如果你了解或以前部署过 Active Directory Rights Management Services (AD RMS)，你可能想知道 Azure 信息保护在功能和要求方面与它相比有何差别。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d0cd811adcd773446c60a3442bb5687210931ed0
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73444823"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>比较 Azure 信息保护与 AD RMS

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

如果你了解或以前部署过 Active Directory Rights Management Services (AD RMS)，你可能想知道 Azure 信息保护作为信息保护解决方案在功能和要求方面与它相比有何差别。

Azure 信息保护的一些主要差异：

- **无需服务器基础结构**：Azure 信息保护不需要 AD RMS 所需的额外服务器和 PKI 证书，因为 Microsoft Azure 将处理那些内容。 因而这一云解决方案可以更快部署且更易维护。

- **基于云的身份验证**：对于内部用户和来自其他组织的用户，Azure 信息保护都使用 Azure AD 进行身份验证。 这意味着，即使用户未连接到内部网络，也可以对其进行身份验证，并且可以更轻松地与其他组织的用户共享受保护的内容。 许多组织由于运行 Azure 服务或使用 Office 365，因而在 Azure AD 中已拥有用户帐户。 但是如果没有，个人的 RMS 可以让用户创建一个免费帐户，或者 Microsoft 帐户可以用于[支持此 Azure 信息保护身份验证的应用程序](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)。 相比之下，若要与另一个组织共享 AD RMS 受保护的内容，你必须为每个组织配置显式信任关系。

- **对移动设备的内置支持**： Azure 信息保护不需要进行任何部署更改即可支持移动设备和 Mac 计算机。 若要使 AD RMS 支持这些设备，必须安装移动设备扩展、配置 AD FS 以便进行联合身份验证，并为公共 DNS 服务创建其他记录。

- **默认模板**： Azure 信息保护会自动创建默认模板，用于将内容访问限制到你自己的组织。 这些模板使你可以轻松地立即开始保护敏感数据。 AD RMS 无默认模板。

- **部门模板**：也称为作用域模板。 Azure 信息保护支持将部门模板用于用户创建的额外模板。 通过此配置，可指定部分用户在其客户端应用程序中看到特定模板。 通过限制用户可查看的模板数量，使他们更容易选择你为不同用户组定义的正确策略。 AD RMS 不支持部门模板。

- **文档跟踪和吊销**： Azure 信息保护通过 Azure 信息保护客户端（经典）支持这些功能，而 AD RMS 不支持。

- **分类和标记**： Azure 信息保护支持应用分类和保护（可选）的标签。 [Azure 信息保护客户端（经典）和 Azure 信息保护统一标签客户端](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers)随附了这些功能。 使用这些客户端，可以将分类和标签与 Office 应用程序、文件资源管理器、PowerShell 以及本地数据存储的扫描程序集成。 AD RMS 不支持这些分类和标签功能。

此外，由于 Azure 信息保护是一项云服务，因此与基于本地服务器的解决方案相比，它可以更快交付新功能和修补程序。 Windows Server 中没有为 AD RMS 规划的新功能。

对于其他差异，请使用下表进行并行比较。 如果你有安全方面的比较问题，请参阅本文中的[签名和加密的加密控制](#cryptographic-controls-for-signing-and-encryption)。

|Azure Information Protection|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|支持 Microsoft Online services 和本地 Microsoft 服务器产品中的信息权限管理（IRM）功能。|支持本地 Microsoft 服务器产品和 Exchange Online 的信息权限管理（IRM）功能。|
|与任何也使用 Azure AD 进行身份验证的组织自动实现文档的安全协作。|在组织外部实现文档的安全协作要求在两个组织之间以直接点对点的关系显式定义身份验证信任。 必须配置受信任的用户域 (TUD) 或使用 Active Directory 联合身份验证服务 (AD FS) 创建的联合信任。|
|如果不存在任何身份验证信任关系，则向用户发送受保护的电子邮件（可选择附加自动受到保护的 Office 文档附件）。 使用联合与社交提供程序或一次性密码和 Web 浏览器进行查看时可能需要采取这种操作。|如果不存在任何身份验证信任关系，则不支持发送受保护的电子邮件。|
|支持 Azure 信息保护客户端（经典）和 Azure 信息保护统一标签客户端，同时提供保护和消耗活动。|支持用于保护和消耗活动的 Azure 信息保护客户端（经典）。 <br /><br />仅支持 Azure 信息保护统一标签客户端以供使用，并且必须安装[Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))。
|支持适用于计算机和移动设备的多因素身份验证 (MFA)。<br /><br />有关详细信息，请参阅[多重身份验证 (MFA) 和 Azure 信息保护](./requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection)。|如果将 IIS 配置为请求证书，将支持智能卡身份验证。|
|默认情况下支持加密模式2，以便为密钥长度和加密算法提供推荐的安全级别。|默认情况下支持加密模式1，需要额外配置才能支持加密模式2，以获得推荐的安全级别。<br /><br />有关详细信息，请参阅[AD RMS 加密模式](https://go.microsoft.com/fwlink/?LinkId=266659)。|
|要求使用 Azure 信息保护许可证或具有 Office 365 的 Azure Rights Management 许可证来保护内容。 <br /><br />无需许可证即可使用已受 Azure 信息保护（包括另一个组织的用户）保护的内容。<br /><br />有关授权的详细信息，包括 P1 和 P2 许可证之间的差异，请参阅 Azure 信息保护站点中的[功能列表](https://www.microsoft.com/cloud-platform/azure-information-protection-features)。|需要 RMS 许可证才能保护内容，以及使用已受 AD RMS 保护的内容。<br /><br />有关授权的详细信息，请参阅[客户端访问许可证和管理许可证](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx)获取一般信息，但请联系 microsoft 合作伙伴或 microsoft 代表了解特定信息。|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>对签名和加密的加密控制
默认情况下，Azure 信息保护将 RSA 2048 用于所有公钥加密，将 SHA 256 用于签名操作。 相比之下，AD RMS 支持 RSA 1024 和 RSA 2048，还将 SHA 1 或 SHA 256 用于签名操作。

Azure 信息保护和 AD RMS 都将 AES 128 用于对称加密。

租户密钥大小为 2048 位时，Azure 信息保护符合 FIPS 140-2，这是激活 Azure Rights Management 服务时的默认设置。 

有关加密控制的详细信息，请参阅 [Azure RMS 使用的加密控制：算法和密钥长度](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)。


## <a name="next-steps"></a>后续步骤
若要详细了解如何使用 Azure 信息保护，例如设备支持和最低版本，请参阅[Azure 信息保护的要求](requirements.md)。

如果希望从 AD RMS 迁移到 Azure 信息保护，请参阅[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)。

你可能对以下 Faq 感兴趣：
- [Azure 信息保护和 Microsoft 信息保护之间的区别是什么？](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)
- [Azure 信息保护与 Azure Rights Management 之间有何区别？](faqs.md#whats-the-difference-between-azure-information-protection-and-azure-rights-management)

