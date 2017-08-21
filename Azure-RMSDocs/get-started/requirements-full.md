---
title: "Azure 信息保护的要求 - 全文"
description: "确定为组织部署 Azure 信息保护的必备条件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 10cf9371-a61b-495f-9d42-898448806994
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2a5791dfd571091e8c9e510447b0a5b36818a8df
ms.sourcegitcommit: 17f593b099dddcbb1cf0422353d594ab964b2736
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2017
---
# <a name="requirements-for-azure-information-protection"></a>Azure 信息保护的要求

>*适用于：Azure 信息保护、Office 365*


为组织部署 Azure 信息保护之前，请确保具备以下必备条件。 

|要求|更多信息|
|---------------|--------------------|
|Azure 信息保护的订阅|查看 Azure 信息保护网站上的[订阅信息](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)和[功能列表](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)，以确保组织的订阅具有想要使用的 Azure 信息保护功能。|
|Azure Active Directory|你的组织必须具有 Azure Active Directory (Azure AD)，以此支持 Azure 信息保护的用户身份验证。 此外，如果你希望使用本地目录 (AD DS) 中的用户帐户，则还必须配置目录集成。<br /><br />如果你的帐户已联合（例如，使用 AD FS），则帐户必须使用 Windows 集成身份验证。 Azure 信息保护不支持基于窗体的身份验证。<br /><br />具有所需客户端软件并正确配置 MFA 支持基础结构后，Azure 信息保护将支持多重身份验证 (MFA)。<br /><br />有关详细信息，请参阅 [Azure 信息保护的 Azure Active Directory 要求](requirements-azure-ad.md)。|
|客户端设备|用户必须拥有运行支持 Azure 信息保护的操作系统的客户端设备（计算机或移动设备）。<br /><br />以下设备支持 Azure 信息保护客户端，它可使用户分类并标记其 Office 文档和电子邮件：<br /><br />- Windows 10（x86、x64）<br /><br />- Windows 8.1（x86、x64）<br /><br />- Windows 8（x86、x64）<br /><br />- Windows 7 Service Pack 1（x86、x64）<br /><br />当此客户端可以通过使用 Azure Rights Management 服务保护数据时，支持 Azure Rights Management 服务的同一设备（Windows、Mac、iOS、Android）可以使用它。 <br /><br />有关支持 Azure Rights Management 服务的设备的详细信息，请参阅[支持 Azure Rights Management 数据保护的客户端设备](../get-started/requirements-client-devices.md)。|
|应用程序|Azure 信息保护客户端支持对使用以下 Office 套件中的 **Word**、**Excel**、**PowerPoint** 和 **Outlook** 等 Office 应用创建的文件和电子邮件设置标签和进行保护：<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />有关支持 Azure Rights Management 服务的应用程序的信息，请参阅[支持 Azure Rights Management 数据保护的应用程序](requirements-applications.md)。|
|支持连接到 Internet 及所依赖的云服务的基础结构|如果你有必须配置为允许特定连接的防火墙或类似中介网络设备，请参阅以下 Office 文章的 [Office 365 portal and shared](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)（Office 365 门户和共享）部分的有关 **Azure 权限管理 (RMS)** 的信息：[《Office 365 URLs and IP address ranges》](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)（Office 365 URL 和 IP 地址范围）。<br /><br />使用此 Office 文章中的说明通过订阅 RSS 源来跟踪本信息的最新更改。<br /><br />除了 Office 文章中特定于 Azure 信息保护的信息外：<br /><br />- 允许 TCP 443 上的 HTTPS 流量流入 **api.informationprotection.azure.com**。<br /><br />- 不要终止 TLS 客户端到服务连接（例如，为了执行数据包级别检查）。 这样做会中断 RMS 客户端用于 Microsoft 托管的 CA 以帮助确保其与 Azure RMS 的通信安全的证书锁定。<br /><br />- 如果使用要求进行身份验证的 Web 代理，则必须将其配置为将集成 Windows 身份验证与用户的 Active Directory 登录凭据配合使用。|

如果想要将 Azure 信息保护中的 Azure Rights Management 服务与本地服务器配合使用，则支持以下产品：

-   Exchange Server

-   SharePoint Server

-   支持文件分类基础结构的 Windows Server 文件服务器

有关此方案的其他要求的信息，请参阅[支持 Azure Rights Management 数据保护的本地服务器](requirements-servers.md)。

> [!IMPORTANT]
> 不支持以下部署方案，除非将 AD RMS 保护与 Azure 信息保护配合使用（“自留密钥”或 HYOK 配置）：
> 
> -   在同一个组织中并行运行 AD RMS 和 Azure RMS，除非是在迁移过程中，如[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)所述。
> 
> 支持[从 AD RMS 到 Azure 信息保护](http://technet.microsoft.com/library/Dn858447.aspx)和[从 Azure 信息保护到 AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx) 的迁移路径。 如果你部署 Azure 信息保护，然后决定不再想要使用此云服务，请参阅[解除 Azure 信息保护授权和停用 Azure 信息保护](../deploy-use/decommission-deactivate.md)。

## <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Azure 信息保护的 Azure Active Directory 要求

必须拥有 Azure AD 目录才能使用 Azure 信息保护。 你可以使用此目录的组织帐户登录 Azure 经典门户，并在该门户中进行 Rights Management 模板的配置和管理之类的操作。

如果你还没有你组织的 Azure 订阅，则可以通过注册免费试用版来获取订阅：转到 [Azure 入门](https://account.windowsazure.com/organization)页并按照说明进行操作。

有关详细信息，请参阅 Azure Active Directory 文档中的以下资源：

-   [什么是 Azure AD Directory？](/active-directory/active-directory-whatis)

-   [Azure 订阅与 Azure Active Directory 的关联方式](/active-directory/active-directory-how-subscriptions-associated-directory)

如果要将 Azure AD 目录与本地 AD 林相集成，请参阅[将本地标识与 Azure Active Directory 集成](/active-directory/active-directory-aadconnect)。

> [!NOTE]
> 如果你的移动设备或 Mac 计算机使用 AD FS 或等效的身份验证提供程序进行本地身份验证，则：
> 
> -   你必须在最低服务器版的 **Windows Server 2012 R2** 上使用 AD FS，或者使用支持 OAuth 2.0 协议的备用身份验证提供程序。

### <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>多重身份验证 (MFA) 和 Azure 信息保护
若要将多因素身份验证 (MFA) 和 Azure 信息保护结合起来使用，至少需要以下条件之一：

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

## <a name="client-devices-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的客户端设备

使用下列部分来确定哪些设备支持 Azure Rights Management 服务，它提供了 Azure 信息保护的数据保护。

### <a name="computers"></a>计算机
以下计算机操作系统支持 Azure Rights Management 服务：

-   **Windows 7** (x86, x64)

-   **Windows 8** (x86, x64)

-   **Windows 8.1** (x86, x64)

-   **Windows 10** (x86, x64)

-   **Mac OS X**：最低版本的 Mac OS X 10.8 (Mountain Lion)

### <a name="mobile-devices"></a>移动设备
以下移动设备操作系统支持 Azure Rights Management 服务：

-   **Windows Phone**：Windows Phone 8.1

-   **Android 手机和平板电脑**：最低版本的 Android 4.0.3

-   **iPhone 和 iPad**：最低版本的 iOS 7.0

-   **Windows 平板电脑**：Windows 10 Mobile 和 Windows 8.1 RT

## <a name="applications-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的应用程序

使用下表确定本机支持 Azure Rights Management 服务 (Azure RMS) 的应用程序，它为 Azure 信息保护提供了数据保护。 

对于这些应用程序，通过使用 Rights Management API 来实现 Rights Management 支持的紧密集成，以支持使用限制。 这些应用程序也称为“启用 RMS 型”应用程序。

除非另行说明，否则支持的功能同时适用于 Azure RMS 和 AD RMS。 此外，iOS、Android、OS X 和 Windows Phone 8.1 上的 AD RMS 支持需要 [Active Directory Rights Management 服务移动设备扩展](https://technet.microsoft.com/library/dn673574.aspx)。

有关表列的信息：

-   **受保护的 PDF**：使用 RMS 共享应用程序通过电子邮件共享 Office 文件和 PDF 文件时自动创建的具有 .ppdf 文件扩展名的文件。 RMS 共享应用程序和适用于 iOS 和 Android 的 Azure 信息保护应用包括用于受保护 PDF 文件的阅读器。 以前，如果你创建的 PDF 文件是使用 Azure RMS 或 AD RMS 进行保护，则你可以继续使用 Foxit Reader 和 Nitro Pro 在 Windows、iOS 和 Android 设备上阅读这些文件。

-   **电子邮件：**所列电子邮件客户端可以保护电子邮件本身，而电子邮件则会自动保护任何附加的文件。 在这种情况下，客户端的预览功能可以向授权收件人显示受保护的内容（邮件和附件）。 但是，如果未保护电子邮件本身，而保护了附件，则客户端的预览功能将无法向授权收件人显示受保护的附件。

-   **其他文件类型**：文本和图像文件包括文件扩展名为 .txt、.xml、.jpg 和 .jpeg 之类的文件。 这些文件在接受 Rights Management 提供的本机保护以后，会更改其文件扩展名，变为只读文件。 不能进行本机保护的文件在接受 Rights Management 提供的常规保护以后，其文件扩展名为 .pfile。 有关详细信息，请参阅 [Rights Management 共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)。


|**设备操作系统**|Word、Excel、PowerPoint|受保护的 PDF|Email|其他文件类型|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office Mobile 应用程序（仅适用于 Azure RMS）[[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho 文档<br /><br />适用于 Adobe 的 GigaTrust 桌面 PDF 客户端<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />RMS 共享应用程序|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|适用于 Windows 的 RMS 共享应用程序：文本、图像、pfile<br /><br />Siemens JT2Go：JT 文件（仅适用于 Windows 10）|
|**iOS**|iPad 和 iPhone 版 Office [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS 文档|Azure 信息保护应用 [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />TITUS 文档|Azure 信息保护应用 [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />iPad 和 iPhone 版 Outlook [[4]](#footnote-4)<br /><br />OWA for iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Azure 信息保护应用 [[1]](#footnote-1)：文本、图像<br /><br />TITUS 文档：Pfile|
|**Android**|适用于 Android 的 GigaTrust 应用<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile（仅适用于 Azure RMS）[[1]](#footnote-1)|Azure 信息保护应用 [[1]](#footnote-1)<br /><br />适用于 Android 的 GigaTrust 应用<br /><br />Foxit Reader<br /><br />RMS 共享应用程序 [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />Azure 信息保护应用 [[1]](#footnote-1)<br /><br />适用于 Android 的 GigaTrust 应用程序 [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for Android [[4]](#footnote-4)<br /><br />OWA for Android [[3]](#footnote-3) 和 [[7]](#footnote-7)<br /><br />Samsung Email（S3 及更高版本）[[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Azure 信息保护应用 [[1]](#footnote-1)：文本、图像|
|**OS X**|Office 2011（仅适用于 AD RMS）<br /><br />Office 2016 for Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />RMS 共享应用程序 [[1]](#footnote-1)|Outlook 2011（仅适用于 AD RMS）<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共享应用程序 [[1]](#footnote-1)：文本、图像、pfile|
|**Windows 10 移动版**|Office Mobile 应用程序（仅适用于 Azure RMS）[[1]](#footnote-1)|不支持|Citrix WorxMail [[6]](#footnote-6)<br /><br />Outlook Mail|不支持|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|不支持|Outlook 2013 RT<br /><br />Windows 相关邮件应用程序<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go：JT 文件|
|**Windows Phone 8.1**|Office Mobile（仅适用于 AD RMS）|RMS 共享应用程序 [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|RMS 共享应用程序 [[1]](#footnote-1)：文本、图像、pfile|
|**Blackberry 10**|不支持|不支持|Blackberry 电子邮件 [[4]](#footnote-4)|不支持|


##### <a name="footnote-1"></a>脚注 1
支持查看受保护内容。

##### <a name="footnote-2"></a>脚注 2 
将未受保护的文档上传到 SharePoint Online 和 OneDrive for Business 中受保护的库中时，可查看受保护的文档。 

##### <a name="footnote-3"></a>脚注 3
如果收件人接收了受保护的电子邮件，且未将 Exchange 作为邮件服务器，或如果发送者属于另一组织，则只能在功能丰富的电子邮件客户端（如 Outlook）中打开此内容。 不能从 Outlook Web Access 打开此内容。

##### <a name="footnote-4"></a>脚注 4
使用 Exchange ActiveSync IRM，它必须由 Exchange 管理员启用。 用户可以查看受保护电子邮件并回复所有受保护电子邮件，但是他们自己不能保护新的电子邮件。

如果收件人接收了受保护的电子邮件，且未将 Exchange 作为邮件服务器，或如果发送者属于另一组织，则只能在功能丰富的电子邮件客户端（如 Outlook）中打开此内容。 无法从 Outlook Web Access 或使用 Exchange Active Sync IRM 的移动邮件客户端打开此内容。

##### <a name="footnote-5"></a>脚注 5
支持查看和编辑受保护文档。 有关详细信息，请参阅 Office 博客上的以下帖子：[为 iPad 和 iPhone 版 Office 提供 Azure Rights Management 支持](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

##### <a name="footnote-6"></a>脚注 6
有关详细信息，请参阅 Citrix [product documentation for WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html)（Worxmail 的产品文档）。

##### <a name="footnote-7"></a>脚注 7
有关详细信息，请参阅 Office 博客上的以下帖子：[OWA for Android 现可在特定设备上使用](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## <a name="more-information-about-azure-rms-support-for-office"></a>有关针对 Office 的 Azure RMS 支持的详细信息

Azure RMS 已紧密集成到 Word、Excel、PowerPoint 和 Outlook 应用中，在这些应用中，此功能通常称为信息权限管理 (IRM)。 以下 Office 客户端版本支持通过 Azure RMS 保护文件和电子邮件：

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

所有版本的 Office（不包括 Office 2007）都支持使用受保护的内容。

带 Office Professional Plus 2010 或 Office Professional 2010 的 Azure RMS：

- 需要适用于 Windows 的 Rights Management 共享应用程序

- 在 Windows 10 上不受支持

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>有关适用于 iOS 和 Android 的 Azure 信息保护应用的详细信息

适用于 iOS 和 Android 的 Azure 信息保护应用将替换这些设备的 RMS 共享应用程序。 它提供相同的功能，此外，还支持受权限保护的电子邮件和 SharePoint Online 上受权限保护的 PDF 文件。

如果 iOS 和 Android 设备是通过 Microsoft Intune 注册的，则可以使用策略托管的应用部署和管理此应用。 更多详细信息，请参阅 Intune 文档中的[在 Microsoft Intune 控制台中配置和部署移动应用程序管理策略](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 对于此 Intune 文档中的步骤 2，使用说明来发布策略托管的应用。

有关详细信息，请参阅[适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题](../rms-client/mobile-app-faq.md)。


### <a name="more-information-about-the-rights-management-sharing-application"></a>有关 Rights Management 共享应用程序的详细信息

有关适用于 Windows 的权限管理共享应用程序的详细信息，请参阅以下资源：

-   [权限管理共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)

-   [权限管理共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)

有关适用于移动平台的权限管理共享应用程序的详细信息，请参阅以下资源：

-   使用 [Microsoft Rights Management 页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用程序

-   [适用于移动平台的 Microsoft Rights Management 共享应用程序的常见问题解答](https://technet.microsoft.com/dn451248)

> [!NOTE]
> 适用于 iOS 和 Android 的 RMS 共享应用程序现已替换为 Azure 信息保护应用。

### <a name="more-information-about-other-applications-that-support-azure-rms"></a>有关其他支持 Azure RMS 的应用程序的详细信息

除了表中的应用程序，任何支持 RMS API 的应用程序都可以与 Azure RMS 集成，包括：

- 使用 RMS SDK 内部编写的业务线应用程序

- 来自软件供应商、使用 RMS SDK 编写的应用程序。

有关 SDK 的详细信息，请参阅 [Microsoft Rights Management SDK](../develop/developers-guide.md)。

### <a name="applications-that-are-not-supported-by-azure-rms"></a>不受 Azure RMS 支持的应用程序

Azure RMS 当前不支持以下应用程序：

-   Microsoft Office for Mac 2011

-   Microsoft OneDrive for Business for SharePoint Server 2013

-   XPS 查看器
 
此外，RMS 共享应用程序具有以下限制：

-   对于 Windows 计算机：要求最低版本为 Windows 7 Service Pack 1

## <a name="on-premises-servers-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的本地服务器

使用 Azure Rights Management 连接器时 Azure 信息保护支持以下本地服务器产品。 该连接器充当本地服务器和 Azure Rights Management 服务（Azure 信息保护使用该服务保护 Office 文档和电子邮件）之间的通信接口（中继）。 

若要使用该连接器，必须配置 Active Directory 林和 Azure Active Directory 之间的目录同步。

-   **Exchange Server**：

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**：

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器**：

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > 由于运行 Windows Server 2008 R2 的文件服务器未使用内置文件管理任务操作来应用 Rights Management 保护，在这种情况下，不能使用 Rights Management 连接器。 但是，如果你配置自定义文件管理任务以运行可通过使用 Azure RMS 来保护文件的可执行文件或脚本，则可以在这些操作系统上使用文件分类基础结构和 Azure RMS。 例如，使用 [RMS 保护 cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx) 的 Windows PowerShell 脚本。
    > 
    > 你也可以在运行更高版本的 Windows Server 的服务器上使用这些 cmdlet，好处是这些 cmdlet 可以保护所有文件类型。 RMS 连接器仅保护 Office 文件。 有关操作说明，请参阅[使用 Windows Server 文件分类基础结构 &#40;FCI&#41; 的 RMS 保护](../rms-client/configure-fci.md)。

Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 支持 Rights Management 连接器。

有关如何为这些本地服务器配置 Rights Management 连接器的详细信息，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
