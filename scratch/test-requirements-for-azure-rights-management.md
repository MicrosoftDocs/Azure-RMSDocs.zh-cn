---
title: 测试 Azure Rights Management 要求
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: TEST
author: Cabailey
---
# 以前为：Azure Rights Management 要求
若要在你的组织中部署 Microsoft Azure Rights Management (Azure RMS)，请确保你具备以下先决条件。 然后，可以使用 [Azure Rights Management 部署路线图](deployment-roadmap.md)为你所在组织部署 Rights Management。

|要求|更多信息|
|---------------|--------------------|
|用于 RMS 的云订阅|你的组织必须具有支持 RMS 的云订阅。<br /><br />有关许可信息，请参阅本主题中的[支持 Azure RMS 的云订阅](requirements-azure-rms.md#BKMK_SupportedSubscriptions)部分。|
|Azure AD 目录|你的组织必须具有 Azure AD 目录，以支持 RMS 的用户身份验证。 此外，如果你希望使用本地目录 (AD DS) 中的用户帐户，则还必须配置目录集成。<br /><br />如果你具有所需的客户端软件并正确配置了 MFA 支持基础结构，Azure RMS 将支持多因素身份验证 (MFA)。<br /><br />有关详细信息，请参阅本主题中的 [Azure AD 目录](requirements-azure-rms.md#BKMK_AzureADTenant)部分。|
|客户端设备|用户必须拥有运行支持 RMS 的操作系统的客户端设备（计算机或移动设备）。<br /><br />有关详细信息，请参阅本主题中的[支持 Azure RMS 的客户端设备](requirements-azure-rms.md#BKMK_SupportedDevices)部分。|
|应用程序|用户必须运行支持 RMS 的应用程序。<br /><br />有关详细信息，请参阅本主题中的[支持 Azure RMS 的应用程序](requirements-azure-rms.md#BKMK_SupportedApplications)部分。|
|支持连接到 Internet 及所依赖的云服务的基础结构|如果你有防火墙或必须配置为允许特定连接的类似中间网络设备，请参阅 [Office 365 URL 和 IP 地址范围](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)。<br /><br />**Office 365 门户和标识**部分中的 URL 和 IP 地址列表适用于 Office 365 门户、Azure Active Directory 资源和 Azure Rights Management。 使用本文中的说明通过订阅 RSS 源来跟踪本信息的最新更改。<br /><br />除了 Office 文章中特定于 Azure RMS 的信息外：<br /><br />不要终止 TLS 客户端到服务连接（例如，为了执行数据包级别检查）。 这样做会中断 RMS 客户端用于 Microsoft 托管的 CA 以帮助确保其与 Azure RMS 的通信安全的证书锁定。<br /><br />不要使用代表用户进行身份验证的 Web 代理配置。|

如果你希望将 Azure RMS 用于本地服务器，则支持以下产品：

-   Exchange Server

-   SharePoint Server

-   支持文件分类基础结构的 Windows Server 文件服务器

有关此方案的其他 Azure RMS 要求的信息，请参阅本主题中的[支持 Azure RMS 的本地服务器](requirements-azure-rms.md#BKMK_SupportedServers)部分。

> [!IMPORTANT]
> 不支持以下部署方案：
> 
> -   在同一个组织中并行运行 AD RMS 和 Azure RMS，除非是在迁移过程中，如[从 AD RMS 迁移到 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 所述。
> 
> 支持的迁移路径有：[从 AD RMS 到 Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) 以及从[ Azure RMS 到 AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx)。 如果你部署 Azure RMS，然后决定不再想要使用此云服务，请参阅[解除 Azure Rights Management 授权和停用 Azure Rights Management](decommission-deactivate.md)。

使用以下部分可以了解有关 Azure RMS 要求的详细信息。

## <a name="BKMK_SupportedSubscriptions"></a>支持 Azure RMS 的云订阅
若要使用 Azure RMS，你的组织必须至少具有下列其中一个订阅，这些订阅可提供足够数目的用户和服务许可证来保护文件与电子邮件。 如果你的某个服务要为用户（文件或电子邮件的所有者）应用保护，则这些用户需要这些许可证之一。 只需使用（例如，阅读和编辑）此类受保护数据的用户不需要许可证。

-   Office 365

-   Azure Rights Management 高级版（以前称为 Azure RMS 独立版）

-   公司移动套件

-   个人 RMS

使用以下部分了解更多信息和注册选项。

有关付费订阅的 Azure RMS 功能的许可比较，请参阅 [Rights Management 服务 (RMS) 产品比较](http://technet.microsoft.com/dn858608)。

是否有关于 Azure RMS 许可的其他问题？ 从 [Azure Rights Management 购买](https://www.microsoft.com/en-us/server-cloud/products/azure-rights-management/Purchasing.aspx)页下载 **Azure Rights Management 许可常见问题**。 

### Office 365 订阅
[免费 30 天试用版：企业版 E3](http://go.microsoft.com/fwlink/p/?LinkID=403802)

此订阅的适用对象是希望使用 Office 联机服务并使用信息权限管理功能（此功能使用了 Azure RMS）的组织。 但是，并非所有 Office 365 订阅都包括 Azure RMS。

|许可选项|Office 365 商业协作版|Office 365 商业高级版|Office 365 企业版 E1<br /><br />Office 365 教育版 A1|Office 365 企业版 E3<br /><br />Office 365 教育版 A3<br /><br />Office 365 政府版 G3|Office 365 企业版 E4<br /><br />Office 365 教育版 A4<br /><br />Office 365 政府版 G4|Office 365 企业版 E5<br /><br />Office 365 教育版 A5<br /><br />Office 365 政府版 G5|Office 365 企业版 K1|SharePoint 计划 1<br />SharePoint 计划 2|Exchange Online 计划 1<br />Exchange Online 计划 2|
|--------------------|----------------------------------|-------------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|信息权限管理 (IRM)|否|否|否|是|是|是|否|否|否|

### Azure Rights Management 高级版订阅
[免费 30 天试用版](https://portal.microsoftonline.com/Signup/MainSignUp15.aspx?&amp;OfferId=A43415D3-404C-4df3-B31B-AAD28118A778&amp;dl=RIGHTSMANAGEMENT&amp;ali=1)

此订阅以前称为 Azure RMS 独立版，它的适用对象是想要使用 Azure RMS 但不包括 Azure RMS 的订阅的组织。 例如，如果你有 Office 365 商业协作版或 Office 365 企业版 E1 的订阅，则这些订阅不包含 Azure RMS（请参阅前一节中的表）。 若要使用 Azure RMS，你可以购买 Azure Rights Management 高级版订阅（或者购买包括 Azure RMS 的其他订阅，例如 Office 365 企业版 E4）。

有关详细信息，请参阅 [Microsoft Azure Rights Management](http://products.office.com/business/microsoft-azure-rights-management)。

此订阅还为你提供试用期，允许 25 名用户试用 Azure RMS，不收取任何费用。 如果此订阅在你购买替代订阅之前过期，请参阅以下部分：“试用订阅到期时会发生什么情况？”

|许可选项|Office 365 商业协作版|Office 365 商业高级版|Office 365 企业版 E1<br /><br />Office 365 教育版 A1|Office 365 企业版 E3<br /><br />Office 365 教育版 A3<br /><br />Office 365 政府版 G3|Office 365 企业版 E4<br /><br />Office 365 教育版 A4<br /><br />Office 365 政府版 G4|Office 365 企业版 E5<br /><br />Office 365 教育版 A5<br /><br />Office 365 政府版 G5|Office 365 企业版 K1|SharePoint 计划 1<br />SharePoint 计划 2|Exchange Online 计划 1<br />Exchange Online 计划 2|
|--------------------|----------------------------------|-------------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|信息权限管理 (IRM)|是|是 [脚注 1]|是|是|是|是|是|是|是|
脚注 1：对于商业高级版，存在一些客户端限制。你可以配合使用 Outlook Web App 和 RMS 共享应用程序，以此保护内容和使用受保护的内容与 RMS。 你可以通过使用包括 Office Online 和适用于 Office 365 商业高级版的客户端应用程序的所有其他 Office 应用程序来使用受保护的内容。

#### <a name="BKMK_TrialExpiryBehavior"></a>试用订阅到期时会发生什么情况？
如果试用订阅到期，你将失去使用 Azure RMS 试用订阅保护的内容的访问权限。 但是，如果你随后购买支持 Azure RMS 的订阅，则访问权限将自动恢复。

在过期之后会失去访问权限，但也有一种例外情况：在获得试用订阅之前，你的组织通过个人 RMS 订阅来使用 Azure RMS。 那么，即便在试用订阅过期之后，你仍然具有对以前受保护内容的访问权限。

### 公司移动套件订阅
[免费 30 天试用版](http://go.microsoft.com/fwlink/?LinkId=615385)

此订阅的适用对象是希望结合使用 Azure Active Directory 高级版、Windows Intune 和 Azure Rights Management 的组织。 有关更多信息，请参阅 [Microsoft 企业移动概述](http://go.microsoft.com/fwlink/?LinkId=615386)。

|许可选项|Office 365 商业协作版|Office 365 商业高级版|Office 365 企业版 E1<br /><br />Office 365 教育版 A1|Office 365 企业版 E3<br /><br />Office 365 教育版 A3<br /><br />Office 365 政府版 G3|Office 365 企业版 E4<br /><br />Office 365 教育版 A4<br /><br />Office 365 政府版 G4|Office 365 企业版 E5<br /><br />Office 365 教育版 A5<br /><br />Office 365 政府版 G5|Office 365 企业版 K1|SharePoint 计划 1<br />SharePoint 计划 2|Exchange Online 计划 1<br />Exchange Online 计划 2|
|--------------------|----------------------------------|-------------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|信息权限管理 (IRM)|是|是 [脚注 1]|是|是|是|是|是|是|是|
脚注 1：对于商业高级版，存在一些客户端限制。你可以配合使用 Outlook Web App 和 RMS 共享应用程序，以此保护内容和使用受保护的内容与 RMS。 你可以通过使用包括 Office Online 和适用于 Office 365 商业高级版的客户端应用程序的所有其他 Office 应用程序来使用受保护的内容。

### 个人 RMS 订阅
此订阅的适用对象是没有部署 Azure RMS 或 AD RMS 的组织中的个人。 它让这些用户能够读取组织使用 Azure RMS 保护的内容，也能够保护他们自己的内容。

有关详细信息，请参阅[个人 RMS 和 Azure Rights Management](rms-for-individuals.md)。

## <a name="BKMK_AzureADTenant"></a>Azure AD 目录
你必须拥有 Azure AD 目录才能使用 Azure RMS。 你可以使用此目录的组织帐户登录 Azure 经典门户，并在该门户中进行 Rights Management 模板的配置和管理之类的操作。

如果你还没有你组织的 Azure 订阅，则可以通过注册免费试用版来获取订阅：转到 [Azure 入门](https://account.windowsazure.com/organization)页并按照说明进行操作。

有关详细信息，请参阅 Azure Active Directory 文档中的以下资源：

-   [什么是 Azure AD 目录？](http://msdn.microsoft.com/library/185da266-58a9-43e6-9c66-2c8f702545c6)

-   [Azure 订阅与 Azure AD 的关联方式](http://msdn.microsoft.com/library/edf05c2e-944a-4da5-a330-dc9dc479f127)

如果你希望将 Azure AD 目录与本地 AD 林相集成，请参阅[目录集成](http://msdn.microsoft.com/library/bf82bdff-2467-403b-8c1a-0e9eebcf31e8)。

> [!NOTE]
> 如果你的移动设备或 Mac 计算机使用 AD FS 或等效的身份验证提供程序进行本地身份验证，则：
> 
> -   你必须在最低服务器版的 **Windows Server 2012 R2** 上使用 AD FS，或者使用支持 OAuth 2.0 协议的备用身份验证提供程序。

### <a name="BKMK_MFA"></a>多因素身份验证 (MFA) 和 Azure RMS
若要将多因素身份验证 (MFA) 和 Azure RMS 结合起来使用，至少需要以下条件之一：

-   Office 2013（最低版本）：

    -   如果你拥有 Office 2013，还需要安装[适用于 Office 2013 的 2015 年 6 月 9 日更新 (KB3054853)](https://support.microsoft.com/kb/3054853)。 有关此更新的详细信息以及现代身份验证如何将基于 Active Directory 身份验证库 (ADAL) 的登录加入到 Office 2013 中的详细信息，请参阅 Office 博客上的 [Office 2013 modern authentication public preview announced（已经宣布的 Office 2013 新式身份验证公共预览版）](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。

-   适用于 Windows 的权限管理共享应用程序：

    -   你需要安装最低版本的 1.0.1908.0，这可以通过使用“控制面板”、“程序”和“功能”来确认。 有关共享应用程序的详细信息，请参阅[适用于 Windows 的 Rights Management 共享应用程序](sharing-app-windows.md)。

-   适用于移动设备和 Mac 计算机的 Rights Management 共享应用：

    -   请确保你安装了最新版本。 MFA 支持已加入到 2015 年 9 月版的 RMS 共享应用。

然后，配置 MFA 解决方案：

-   对于 Microsoft 托管的租户（你拥有 Azure Active Directory 或 Office 365）：

    -   配置 Azure MFA 来为用户强制实施 MFA。 有关说明，请参阅 Azure 身份验证中的 [Getting started with Azure Multi-Factor Authentication in the cloud（开始使用云中的 Azure Multi-Factor Authentication）](https://azure.microsoft.com/documentation/articles/multi-factor-authentication-get-started-cloud/)。

        有关 Azure MFA 的详细信息，请参阅[什么是 Azure 多因素身份验证？](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)

-   对于联合租户（你在本地操作联合身份验证服务器）：

    -   为 Azure Active Directory 或 Office 365 配置联合身份验证服务器。 例如，如果你使用 AD FS，请参阅 TechNet 上的[为 AD FS 配置其他身份验证方法](https://technet.microsoft.com/library/dn758113.aspx)。

        有关此方案的详细信息，请参阅 Office 博客上的[使用 Office 365 – 标识程序现在已简化](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)。

## <a name="BKMK_SupportedDevices"></a>支持 Azure RMS 的客户端设备
使用以下部分确定哪些设备支持 Azure 权限管理 (RMS)，以及这些设备支持哪些 RMS 功能：

-   [计算机](requirements-azure-rms.md#BKMK_RMSSupportedComputers)

-   [移动设备](requirements-azure-rms.md#BKMK_RMSSupportedMobileDevices)

-   [客户端设备功能](requirements-azure-rms.md#BKMK_ClientCapabilities)

### <a name="BKMK_RMSSupportedComputers"></a>计算机
以下计算机操作系统支持 Azure Rights Management：

-   **Windows 7** (x86, x64)

-   **Windows 8** (x86, x64)

-   **Windows 8.1** (x86, x64)

-   **Windows 10** (x86, x64)

-   **Mac OS X**：最低版本的 Mac OS X 10.8 (Mountain Lion)

### <a name="BKMK_RMSSupportedMobileDevices"></a>移动设备
以下移动设备操作系统支持 Azure Rights Management：

-   **Windows Phone**：Windows Phone 8.1

-   **Android 手机和平板电脑**：最低版本的 Android 4.0.3

-   **iPhone 和 iPad**：最低版本的 iOS 7.0

-   **Windows RT 平板电脑**：Windows 8.1 RT

### <a name="BKMK_ClientCapabilities"></a>客户端设备功能
并非所有受支持客户端设备当前都支持全部 RMS 功能。 使用下表可确定哪些应用程序支持 RMS 功能以及例外情况。

除非另行说明，否则支持的功能同时适用于 Azure RMS 和 AD RMS。 此外，iOS、Android、OS X 和 Windows Phone 8.1 上的 AD RMS 支持需要 [Active Directory Rights Management 服务移动设备扩展](http://technet.microsoft.com/library/a69ead9d-7dd3-4b38-9830-4728e9757341)。

有关表列的信息：

-   **受保护的 PDF**：使用 RMS 共享应用程序通过电子邮件共享 Office 文件和 PDF 文件时自动创建的具有 .ppdf 文件扩展名的文件。 RMS 共享应用程序包括用于受保护的 PDF 文件的阅读器。 以前，如果你创建的 PDF 文件是使用 Azure RMS 或 AD RMS 进行保护，则你可以继续使用 Foxit Reader 和 Nitro Pro 在 Windows、iOS 和 Android 设备上阅读这些文件。

-   **电子邮件：**所列电子邮件客户端可以保护电子邮件本身，而电子邮件则会自动保护任何附加的文件。 在这种情况下，客户端的预览功能可以向授权收件人显示受保护的内容（邮件和附件）。 但是，如果未保护电子邮件本身，而保护了附件，则客户端的预览功能将无法向授权收件人显示受保护的附件。

-   **其他文件类型**：文本和图像文件包括文件扩展名为 .txt、.xml、.jpg 和 .jpeg 之类的文件。 这些文件在接受 RMS 提供的本机保护以后，会更改其文件扩展名，变为只读文件。 不能进行本机保护的文件在接受 RMS 提供的常规保护以后，其文件扩展名为 .pfile。 有关详细信息，请参阅[权限管理共享应用程序管理员指南](http://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)中的[保护级别 – 本机和常规](https://technet.microsoft.com/library/dn339003.aspx)和[支持的文件类型和文件扩展名](https://technet.microsoft.com/library/dn339003.aspx)部分。

|**设备操作系统**|Word、Excel、PowerPoint|受保护的 PDF|Email|其他文件类型|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 移动应用（仅适用于 Azure RMS）[脚注 1]<br /><br />Office Online [脚注 2]|Gaaiho 文档<br /><br />适用于 Adobe 的 GigaTrust 桌面 PDF 客户端<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />RMS 共享应用程序|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook Web App (OWA) [脚注 3]<br /><br />Windows Mail [脚注 4]|适用于 Windows 的 RMS 共享应用程序：文本、图像、pfile<br /><br />Siemens JT2Go：JT 文件（仅适用于 Windows 10）|
|**iOS**|iPad 和 iPhone 版 Office [脚注 5]<br /><br />Office Online [脚注 2]<br /><br />TITUS 文档|Foxit Reader<br /><br />RMS 共享应用 [脚注 1]<br /><br />TITUS 文档|NitroDesk [脚注 4]<br /><br />iPad 和 iPhone 版 Outlook [脚注 4]<br /><br />OWA for iOS [脚注 3]<br /><br />TITUS Mail|RMS 共享应用 [脚注 1]：文本、图像、pfile<br /><br />TITUS 文档：Pfile|
|**Android**|适用于 Android 的 GigaTrust 应用<br /><br />Office Online [脚注 2]|适用于 Android 的 GigaTrust 应用<br /><br />Foxit Reader<br /><br />RMS 共享应用 [脚注 1]|9Folders [脚注 4]<br /><br />适用于 Android 的 GigaTrust 应用程序 [脚注 4]<br /><br />NitroDesk [脚注 4]<br /><br />OWA for Android [脚注 3 和 6]<br /><br />Samsung Email（S3 及更高版本）[脚注 6]<br /><br />TITUS Classification for Mobile|RMS 共享应用 [脚注 1]：文本、图像、pfile|
|**OS X**|Office 2011（仅适用于 AD RMS）<br /><br />Office 2016 for Mac<br /><br />Office Online [脚注 2]|Foxit Reader<br /><br />RMS 共享应用 [脚注 1]|Outlook 2011（仅适用于 AD RMS）<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共享应用 [脚注 1]：文本、图像、pfile|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [脚注 2]|不支持|Outlook 2013 RT<br /><br />Windows 相关邮件应用程序<br /><br />Windows Mail [脚注 4]|Siemens JT2Go：JT 文件|
|**Windows Phone 8.1**|Office Mobile（仅适用于 AD RMS）|RMS 共享应用 [脚注 1]|Outlook Mobile [脚注 4]|RMS 共享应用 [脚注 1]：文本、图像、pfile|
|**Blackberry 10**|不支持|不支持|Blackberry 电子邮件 [脚注 4]|不支持|
[脚注 1]：支持查看受保护内容。

[脚注 2]：支持查看 SharePoint Online、OneDrive for Business 和 Outlook Web Access 中的受保护内容。

[脚注 3]：如果收件人在本地 Exchange 中有邮箱，并且收到受保护的电子邮件，则只能在功能丰富的电子邮件客户端（如 Outlook）中打开此内容。  不能从 Outlook Web Access 打开此内容。

[脚注 4]：使用 Exchange ActiveSync IRM，它必须由 Exchange 管理员启用。 用户可以查看受保护电子邮件并回复所有受保护电子邮件，但是他们自己不能保护新的电子邮件。

如果收件人在本地 Exchange 中有邮箱，并且收到其他组织中使用 Exchange 的用户发来的受保护电子邮件，则只能在功能丰富的电子邮件客户端（如 Outlook）中打开此内容。  不能从使用 Exchange Active Sync IRM 的设备打开此内容。

[脚注 5]：支持查看和编辑受保护文档。 有关详细信息，请参阅 Office 博客上的以下帖子：[为 iPad 和 iPhone 版 Office 提供 Azure Rights Management 支持](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

[脚注 6]：有关详细信息，请参阅 Office 博客上的以下帖子：[OWA for Android now available on select devices（OWA for Android 当前在某些设备上可用）](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

> [!TIP]
> 有关 Office 中即将针对不同平台推出的 RMS 支持的详细信息，请参阅 Office 博客中的以下帖子：[Office everywhere, encryption everywhere（办公无处不在，加密无处不在）](http://blogs.office.com/2015/02/18/office-everywhere-encryption-everywhere/)

## <a name="BKMK_SupportedApplications"></a>支持 Azure RMS 的应用程序
以下应用程序以本机方式支持 Azure RMS，这意味着 RMS 通过使用 RMS API 紧密集成到这些应用程序中，以支持使用限制。 我们将它们称为“启用 RMS 型”应用程序：

-   来自以下套件的 **Microsoft Office 应用程序**（Word、Excel、PowerPoint 和 Outlook）可以使用 Azure RMS 保护内容：

    -   Office 365 ProPlus

    -   Office 365 企业版 E3

    -   Office 365 企业版 E4

    -   Office 365 企业版 E5

    -   Office Professional Plus 2016

    -   Office Professional Plus 2013

    -   Office Professional Plus 2010

    其他版本的 Office（不包括 Office 2007）可以使用受保护的内容。

    > [!NOTE]
    > 带 Office Professional Plus 2010 或 Office Professional 2010 的 Azure RMS：
    > 
    > -   需要适用于 Windows 的 Rights Management 共享应用程序
    > -   在 Windows 10 上不受支持

-   **适用于 Windows 的权限管理共享应用程序**

    有关适用于 Windows 的权限管理共享应用程序的详细信息，请参阅以下资源：

    -   [权限管理共享应用程序管理员指南](http://technet.microsoft.com/library/dn339003.aspx)

    -   [权限管理共享应用程序用户指南](http://technet.microsoft.com/library/dn339006.aspx)

-   **适用于移动平台的权限管理共享应用程序**

    有关适用于移动平台的权限管理共享应用程序的详细信息，请参阅以下资源：

    -   使用 [Microsoft Rights Management 页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用程序
 
    -   [适用于移动平台的 Microsoft 权限管理共享应用程序的常见问题](http://technet.microsoft.com/dn451248)

-   **支持 RMS API 的其他应用程序**：

    -   使用 RMS SDK 内部编写的业务线应用程序

    -   来自软件供应商的使用 RMS SDK 编写的应用程序

    有关 SDK 的详细信息，请参阅 [Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx)。

> [!IMPORTANT]
> 以下应用程序当前不受 Azure RMS 支持：
> 
> -   Microsoft Office for Mac 2011
> -   Microsoft OneDrive for Business for SharePoint Server 2013
> -   XPS 查看器
> 
> 此外，RMS 共享应用程序具有以下限制：
> 
> -   对于 Windows 计算机：要求最低版本为 Windows 7 Service Pack 1

有关这些应用程序如何支持 Azure RMS 的详细信息，请参阅[应用程序如何支持 Azure Rights Management](applications-support.md)。

有关如何配置这些应用程序的信息，请参阅[为 Azure Rights Management 配置应用程序](configure-applications.md)。

## <a name="BKMK_SupportedServers"></a>支持 Azure RMS 的本地服务器
当你使用 Azure RMS 连接器时，它将充当本地服务器和 Azure RMS 之间的通信接口（一种中继），让 Azure RMS 能够支持以下本地服务器产品。 此外，这种配置要求你配置 Active Directory 林和 Azure Active Directory 之间的目录同步。

-   **Exchange Server**：

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**：

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器**：

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > 由于运行 Windows Server 2008 R2 的文件服务器未使用内置文件管理任务操作来应用 RMS 保护，在这种情况下，你不能使用 RMS 连接器。 但是，如果你配置自定义文件管理任务以运行可通过使用 Azure RMS 来保护文件的可执行文件或脚本，则可以在这些操作系统上使用文件分类基础结构和 Azure RMS。 例如，使用 [RMS 保护 cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx) 的 Windows PowerShell 脚本。
    > 
    > 你也可以在运行更高版本的 Windows Server 的服务器上使用这些 cmdlet，好处是这些 cmdlet 可以保护所有文件类型。 RMS 连接器仅保护 Office 文件。 有关操作说明，请参阅[使用 Windows Server 文件分类基础结构 &#40;FCI&#41; 的 RMS 保护](configure-fci.md)。

Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 支持 RMS 连接器。

有关如何为这些本地服务器配置 RMS 连接器的详细信息，请参阅[部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

## 另请参阅
[Azure 权限管理入门](getting-started-with-azure-rights-management.md)



<!--HONumber=Apr16_HO3-->


