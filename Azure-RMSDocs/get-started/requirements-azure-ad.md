---
# required metadata

title: Azure RMS 要求&#58;Azure AD Directory | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure RMS 要求：Azure AD Directory

你必须拥有 Azure AD 目录才能使用 Azure Rights Management (Azure RMS)。 你可以使用此目录的组织帐户登录 Azure 经典门户，并在该门户中进行 Rights Management 模板的配置和管理之类的操作。

如果你还没有你组织的 Azure 订阅，则可以通过注册免费试用版来获取订阅：转到 [Azure 入门](https://account.windowsazure.com/organization)页并按照说明进行操作。

有关详细信息，请参阅 Azure Active Directory 文档中的以下资源：

-   [什么是 Azure AD Directory？](/active-directory/active-directory-whatis)

-   [Azure 订阅与 Azure Active Directory 的关联方式](/active-directory/active-directory-how-subscriptions-associated-directory)

如果要将 Azure AD 目录与本地 AD 林相集成，请参阅[将本地标识与 Azure Active Directory 集成](/active-directory/active-directory-aadconnect)。

> [!NOTE]
> 如果你的移动设备或 Mac 计算机使用 AD FS 或等效的身份验证提供程序进行本地身份验证，则：
> 
> -   你必须在最低服务器版的 **Windows Server 2012 R2** 上使用 AD FS，或者使用支持 OAuth 2.0 协议的备用身份验证提供程序。

## 多因素身份验证 (MFA) 和 Azure RMS
若要将多因素身份验证 (MFA) 和 Azure RMS 结合起来使用，至少需要以下条件之一：

-   Office 2013（最低版本）：

    -   如果你拥有 Office 2013，还需要安装[适用于 Office 2013 的 2015 年 6 月 9 日更新 (KB3054853)](https://support.microsoft.com/kb/3054853)。 有关此更新的详细信息以及现代身份验证如何将基于 Active Directory 身份验证库 (ADAL) 的登录加入到 Office 2013 中的详细信息，请参阅 Office 博客上的[已经公布的 Office 2013 现代身份验证公共预览版](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。

-   适用于 Windows 的权限管理共享应用程序：

    -   你需要安装最低版本的 1.0.1908.0，这可以通过使用“控制面板”、“程序”和“功能”来确认。 有关共享应用程序的详细信息，请参阅[适用于 Windows 的 Rights Management 共享应用程序](../rms-client/sharing-app-windows.md)。

-   适用于移动设备和 Mac 计算机的 Rights Management 共享应用：

    -   请确保你安装了最新版本。 MFA 支持已加入到 2015 年 9 月版的 RMS 共享应用。

然后，配置 MFA 解决方案：

-   对于 Microsoft 托管的租户（你拥有 Azure Active Directory 或 Office 365）：

    -   配置 Azure MFA 来为用户强制实施 MFA。 有关说明，请参阅多因素身份验证文档中的[在云中的 Azure 多因素身份验证入门](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)。

        有关 Azure MFA 的详细信息，请参阅[什么是 Azure 多因素身份验证？](/multi-factor-authentication/multi-factor-authentication)

-   对于联合租户（你在本地操作联合身份验证服务器）：

    -   为 Azure Active Directory 或 Office 365 配置联合身份验证服务器。 例如，如果你使用 AD FS，请参阅 TechNet 上的[为 AD FS 配置其他身份验证方法](https://technet.microsoft.com/library/dn758113.aspx)。

        有关此方案的详细信息，请参阅 Office 博客上的[使用 Office 365 – 标识程序现在已简化](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)。

## 后续步骤
若要查看其他要求，请参阅 [Azure Rights Management 的要求](requirements-azure-rms.md)。



<!--HONumber=Apr16_HO4-->

