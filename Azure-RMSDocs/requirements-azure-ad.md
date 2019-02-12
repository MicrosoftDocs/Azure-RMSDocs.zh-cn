---
title: Azure 信息保护的 Azure AD 要求 - AIP
description: 确定使用 Azure 信息保护的 Azure AD 要求，以便用户可以成功进行身份验证。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/05/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.suite: ems
ms.openlocfilehash: b2ca14d6dcff00009b6e032d5ca17f5e466d69ea
ms.sourcegitcommit: 1cd3a3bc19cd973f81a62419c946bfaf2796dfb2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2019
ms.locfileid: "55760763"
---
# <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Azure 信息保护的 Azure Active Directory 要求

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

必须拥有 Azure AD 目录才能使用 Azure 信息保护。 可以使用此目录中的帐户登录 Azure 门户，并且可以在该门户中进行 Azure 信息保护标签和 Azure Rights Management 模板的配置和管理等操作。

如果拥有包含 Azure 信息保护或 Azure Rights Management 的订阅，你的 Azure AD 目录则将自动为你创建（如有需要）。  

有关 Azure AD 的详细信息，请参阅[什么是 Azure AD Directory？](/azure/active-directory/fundamentals/active-directory-whatis)

若要将 Azure AD 目录与本地 AD 林相集成，请参阅[将本地 Active Directory 域与 Azure Active Directory 集成](/azure/architecture/reference-architectures/identity/azure-ad)。

### <a name="scenarios-that-have-specific-requirements"></a>具有特定要求的方案 

运行 Office 2010 的计算机： 

- 这些计算机需要 [Azure 信息保护客户端](./rms-client/aip-client.md)来对 Azure 信息保护及其数据保护服务 Azure Rights Management 进行身份验证。

- 如果你的用户帐户已联合（例如，使用 AD FS），则帐户必须使用 Windows 集成身份验证。 在此方案中，基于表单的身份验证无法对 Azure 信息保护的用户进行身份验证。

支持基于证书的身份验证 (CBA)：

- 适用于 iOS 和 Android 的 Azure 信息保护应用支持基于证书的身份验证。 有关配置基于证书的身份验证的说明，请参阅 [Azure Active Directory 中的基于证书的身份验证入门](/azure/active-directory/active-directory-certificate-based-authentication-get-started)。

用户的 UPN 值与其电子邮件地址不匹配：

- 这不是推荐的配置。 如果无法更改 UPN 值，请为用户配置备用登录 ID，并指导他们使用此备用登录方式登录 Office。 有关详细信息，请参阅[配置备用登录 ID](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) 和 [Office 应用程序定期提示输入 SharePoint Online、OneDrive 和 Lync Online 的凭据](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)。
    
    如果 UPN 值中的域名已针对你的租户进行验证，请将用户的 UPN 值作为另一个电子邮件地址添加到 Azure AD proxyAddresses 属性。 如果在授予使用权限时指定了用户的 UPN 值，则可以对用户进行 Azure 权限管理授权。 有关这一点及如何对用户帐户授权的详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

使用 AD FS 或等效的身份验证提供程序进行本地身份验证的移动设备或 Mac 计算机：

- 必须在最低服务器版的 Windows Server 2012 R2 上使用 AD FS，或者使用支持 OAuth 2.0 协议的备用身份验证提供程序。

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>多重身份验证 (MFA) 和 Azure 信息保护
若要将多因素身份验证 (MFA) 和 Azure 信息保护结合起来使用，至少需要以下条件之一：

-   Office 2013（最低版本）：

    -   如果具有 Office 2013，可能需要安装其他更新以支持 Active Directory 身份验证库 (ADAL)。 例如， [2015 年 6 月 9 日发布的 Office 2013 更新 (KB3054853)](https://support.microsoft.com/kb/3054853)。 有关此更新的详细信息以及现代身份验证如何将基于 Active Directory 身份验证库 (ADAL) 的登录加入到 Office 2013 中的详细信息，请参阅 Office 博客上的[已经公布的 Office 2013 现代身份验证公共预览版](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。

- Azure 信息保护客户端：

    - 适用于 Windows 的 [Azure 信息保护客户端](./rms-client/aip-client.md)和适用于 iOS 和 Android 的查看器应用始终支持 MFA，且无最低版本要求。 

-   适用于 Mac 计算机的 Rights Management 共享应用：

    -   MFA 支持已加入到 2015 年 9 月版的 RMS 共享应用。

然后，配置 MFA 解决方案：

-   对于 Microsoft 托管的租户（你拥有 Azure Active Directory 或 Office 365）：

    - 配置 Azure MFA 来为用户强制实施 MFA。 有关说明，请参阅多因素身份验证文档中的[在云中的 Azure 多因素身份验证入门](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)。

        有关 Azure MFA 的详细信息，请参阅[什么是 Azure 多因素身份验证？](/multi-factor-authentication/multi-factor-authentication)

- 对于联合租户（你在本地操作联合身份验证服务器）：

    - 为 Azure Active Directory 或 Office 365 配置联合身份验证服务器。 例如，如果你使用 AD FS，请参阅 TechNet 上的[为 AD FS 配置其他身份验证方法](https://technet.microsoft.com/library/dn758113.aspx)。

        有关此方案的详细信息，请参阅 Office 博客上的[使用 Office 365 – 标识程序现在已简化](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)。

Rights Management 连接器和 Azure 信息保护扫描程序不支持 MFA。 如果部署连接器或扫描程序，以下帐户不得要求执行 MFA：

- 安装和配置连接器的帐户。

- 连接器在 Azure AD 中创建的服务主体帐户 Aadrm_S-1-7-0。
 
- 运行扫描程序的服务帐户。

## <a name="next-steps"></a>后续步骤
若要查看其他要求，请参阅 [Azure 信息保护的要求](requirements.md)。

