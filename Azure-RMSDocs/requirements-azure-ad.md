---
title: Azure 信息保护的其他 Azure AD 先决条件
description: 了解 Azure 信息保护在特定方案中的其他 Azure AD 先决条件，例如多重身份验证或基于证书的身份验证，或使用 Office 2010 的计算机等。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/22/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.subservice: prereqs
ms.suite: ems
ms.custom: admin, has-adal-ref
ms.openlocfilehash: 858a2ebb1bbc5040d564d9df05943c10a3f58a4a
ms.sourcegitcommit: 24c97b58849af4322d3211b8d3165734d5ad6c88
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91428349"
---
# <a name="additional-azure-ad-requirements-for-azure-information-protection"></a>Azure 信息保护的其他 Azure AD 要求

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

使用 Azure 信息保护时，[Azure AD 目录是需要满足的一项要求](requirements.md#azure-active-directory)。 使用 Azure AD 目录中的帐户登录到 Azure 门户，在门户中可以配置 Azure 信息保护设置。

如果拥有包含 Azure 信息保护或 Azure Rights Management 的订阅，你的 Azure AD 目录则将自动为你创建（如有需要）。

以下部分列出了特定方案中的其他 AIP 和 Azure AD 要求。 

## <a name="computers-running-office-2010"></a>运行 Office 2010 的计算机

除了 Azure AD 帐户，运行 Microsoft Office 2010 的计算机还需要使用 [Azure 信息保护统一标签客户端](./rms-client/aip-clientv2.md)或 [Azure 信息保护经典客户端](./rms-client/aip-client.md) 对 Azure 信息保护及其数据保护服务 Azure Rights Management 进行身份验证。

如果你的用户帐户已联合（例如，使用 AD FS），这些计算机必须使用 Windows 集成身份验证。 在此方案中，基于表单的身份验证无法对 Azure 信息保护的用户进行身份验证。

## <a name="support-for-certificate-based-authentication-cba"></a>支持基于证书的身份验证 (CBA)

适用于 iOS 和 Android 的 Azure 信息保护应用支持基于证书的身份验证。 

有关详细信息，请参阅 [Azure Active Directory 中基于证书的身份验证入门](/azure/active-directory/active-directory-certificate-based-authentication-get-started)。

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>多重身份验证 (MFA) 和 Azure 信息保护

若要将多因素身份验证 (MFA) 和 Azure 信息保护结合起来使用，至少需要安装以下内容之一：

- **Microsoft Office，** 版本 2013 或更高版本
- **AIP 客户端**。 没有最低版本要求。 适用于 Windows 的 AIP 客户端以及适用于 iOS 和 Android 的查看器应用均支持 MFA。
- **适用于 Mac 计算机的 Rights Management 共享应用**。 自 2015 年 9 月版起，RMS 共享应用已支持 MFA。

> [!NOTE]
> 如果使用 Office 2013，可能还需要安装一个更新来支持 Active Directory 身份验证库 (ADAL)，如 [2015 年 6 月 9 日发布的 Office 2013 更新 (KB3054853)](https://support.microsoft.com/kb/3054853)。 
>
> 有关详细信息，请参阅 Office 博客上的 [Office 2013 现代身份验证公共预览版发布声明](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。       

确认这些先决条件后，请根据你的租户配置执行以下操作之一：

- **Microsoft 托管的租户，配置了 Azure AD 或 Microsoft 365**。 配置 Azure MFA 来为用户强制实施 MFA。 

    有关详细信息，请参阅： 
    - [云中的 Azure 多重身份验证入门](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)
    - [什么是 Azure 多重身份验证？](/multi-factor-authentication/multi-factor-authentication)

- **联合租户，其中联合身份验证服务器在本地运行**。 为 Azure Active Directory 或 Microsoft 365 配置联合身份验证服务器。 例如，如果你使用 AD FS，请参阅[为 AD FS 配置其他身份验证方法](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)。 

    有关此方案的详细信息，请参阅 Office 博客上的[使用 Microsoft 365 - 标识程序现在已简化](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)。 

## <a name="rights-management-connector--aip-scanner-requirements"></a>Rights Management 连接器 / AIP 扫描器要求

Rights Management 连接器和 Azure 信息保护扫描程序不支持 MFA。 

如果部署连接器或扫描程序，以下帐户不得要求执行 MFA：

- 安装和配置连接器的帐户。
- 连接器在 Azure AD 中创建的服务主体帐户 Aadrm_S-1-7-0****。
- 运行扫描程序的服务帐户。

## <a name="user-upn-values-dont-match-their-email-addresses"></a>用户 UPN 值与其电子邮件地址不匹配

不建议使用用户 UPN 值与其电子邮件地址不匹配的配置，且这种配置不支持 Azure 信息保护的单一登录。

如果无法更改 UPN 值，请为相关用户配置备用登录 ID，并指导他们使用此备用 ID 登录 Office。 

有关详细信息，请参阅：

- [配置备用登录 ID](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)
- [Office 应用程序会定期提示输入 SharePoint、OneDrive 和 Lync Online 的凭据](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)。

> [!TIP]
> 如果 UPN 值中的域名已针对你的租户进行验证，请将用户的 UPN 值作为另一个电子邮件地址添加到 Azure AD proxyAddresses 属性。 如果在授予使用权限时指定了用户的 UPN 值，则可以对用户进行 Azure Rights Management 授权。 

有关详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

## <a name="authenticating-on-premises-using-adfs-or-another-authentication-provider"></a>使用 AD FS 或其他身份验证提供程序在本地进行身份验证

如果使用的移动设备或 Mac 计算机使用 AD FS 或等效的身份验证提供程序在本地进行身份验证，则需要在以下配置之一中使用 AD FS：

- 服务器版本不得低于 **Windows Server 2012 R2**
- 支持 OAuth 2.0 协议的备用身份验证提供程序

## <a name="next-steps"></a>后续步骤
若要查看其他要求，请参阅 [Azure 信息保护的要求](requirements.md)。
