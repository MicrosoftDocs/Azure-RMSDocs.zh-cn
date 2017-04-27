---
title: "对 RMS 数据保护的应用程序支持 - AIP"
description: "确定使用 RMS API 本机支持 Azure 信息保护中的 Azure Rights Management 服务的应用程序。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/20/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4ae74cd40811f7af1da0c7288f574617f6fdaefa
ms.sourcegitcommit: c7078f822cbcbb2bb33b841e8597c2a4163a54da
translationtype: HT
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的应用程序

>*适用于：Azure 信息保护、Office 365*


使用下表确定提供 Azure Rights Management Service（简称 Azure RMS，为 Azure 信息保护提供数据保护）本机支持的应用程序和解决方案。 

对于这些应用程序和解决方案，可以使用支持用法限制的 Rights Management API，从而紧密集成 Rights Management 支持。 这些应用程序和解决方案也称为“启用 RMS 的”应用程序和解决方案。

除非另行说明，否则支持的功能同时适用于 Azure RMS 和 AD RMS。 此外，iOS、Android、macOS 和 Windows Phone 8.1 上的 AD RMS 支持需要 [Active Directory Rights Management Services 移动设备扩展](https://technet.microsoft.com/library/dn673574.aspx)。

## <a name="rms-enlightened-applications"></a>启用 RMS 的应用程序

下表列出了 Microsoft 和软件供应商提供的启用 RMS 的客户端应用程序。

有关表列的信息：

-   **受保护的 PDF**：使用 RMS 共享应用程序通过电子邮件共享 Office 文件和 PDF 文件时自动创建的具有 .ppdf 文件扩展名的文件。 RMS 共享应用程序、适用于 iOS 和 Android 的 Azure 信息保护应用以及适用于 Window 的 Azure 信息保护客户端包括用于受保护 PDF 文件的阅读器。 以前，如果你创建的 PDF 文件是使用 Azure RMS 或 AD RMS 进行保护，则你可以继续使用 Foxit Reader 和 Nitro Pro 在 Windows、iOS 和 Android 设备上阅读这些文件。

-   **电子邮件：**所列电子邮件客户端可以保护电子邮件本身，而电子邮件则会自动保护任何附加的文件。 在这种情况下，客户端的预览功能可以向授权收件人显示受保护的内容（邮件和附件）。 但是，如果未保护电子邮件本身，而保护了附件，则客户端的预览功能将无法向授权收件人显示受保护的附件。

-   **其他文件类型**：文本和图像文件包括文件扩展名为 .txt、.xml、.jpg 和 .jpeg 之类的文件。 这些文件在接受 Rights Management 提供的本机保护以后，会更改其文件扩展名，变为只读文件。 不能进行本机保护的文件在接受 Rights Management 提供的常规保护以后，其文件扩展名为 .pfile。 有关详细信息，请参阅 Azure 信息保护客户端管理员指南中的[支持的文件类型](../rms-client/client-admin-guide-file-types.md)。


|**设备操作系统**|Word、Excel、PowerPoint|受保护的 PDF|Email|其他文件类型|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office Mobile 应用程序（仅适用于 Azure RMS）[[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|适用于 Windows 的 Azure 信息保护客户端 <br /><br />Gaaiho 文档<br /><br />适用于 Adobe 的 GigaTrust 桌面 PDF 客户端<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />RMS 共享应用程序|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|适用于 Windows 的 Azure 信息保护客户端：文本、图像、pfile<br /><br />适用于 Windows 的 RMS 共享应用程序：文本、图像、pfile<br /><br />适用于 AutoCAD 的 SealPath RMS 插件 [[8]](#footnote-8)：.dwg<br />|
|**iOS**|iPad 和 iPhone 版 Office [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS 文档|Azure 信息保护应用 [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />TITUS 文档|Azure 信息保护应用 [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />iPad 和 iPhone 版 Outlook [[4]](#footnote-4)<br /><br />OWA for iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Azure 信息保护应用 [[1]](#footnote-1)：文本、图像<br /><br />TITUS 文档：Pfile|
|**Android**|适用于 Android 的 GigaTrust 应用<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile [[1]](#footnote-1)|Azure 信息保护应用 [[1]](#footnote-1)<br /><br />适用于 Android 的 GigaTrust 应用<br /><br />Foxit Reader<br /><br />RMS 共享应用程序 [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />Azure 信息保护应用 [[1]](#footnote-1)<br /><br />适用于 Android 的 GigaTrust 应用程序 [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for Android [[4]](#footnote-4)<br /><br />OWA for Android [[3]](#footnote-3) 和 [[7]](#footnote-7)<br /><br />Samsung Email（S3 及更高版本）[[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Azure 信息保护应用 [[1]](#footnote-1)：文本、图像|
|**macOS**|Office 2011（仅适用于 AD RMS）<br /><br />Office 2016 for Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />RMS 共享应用程序 [[1]](#footnote-1)|Outlook 2011（仅适用于 AD RMS）<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共享应用程序 [[1]](#footnote-1)：文本、图像、pfile|
|**Windows 10 移动版**|Office Mobile 应用程序（仅适用于 Azure RMS）[[1]](#footnote-1)|不支持|Citrix WorxMail [[6]](#footnote-6)<br /><br />Outlook Mail|不支持|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|不支持|Outlook 2013 RT<br /><br />Windows 相关邮件应用程序<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go：JT 文件|
|**Windows Phone 8.1**|Office Mobile（仅适用于 AD RMS）|RMS 共享应用程序 [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|RMS 共享应用程序 [[1]](#footnote-1)：文本、图像、pfile|
|**Blackberry 10**|不支持|不支持|Blackberry 电子邮件 [[4]](#footnote-4)|不支持|


###### <a name="footnote-1"></a>脚注 1
支持查看受保护内容。

###### <a name="footnote-2"></a>脚注 2 
将未受保护的文档上传到 SharePoint Online 和 OneDrive for Business 中受保护的库中时，可查看受保护的文档。 

###### <a name="footnote-3"></a>脚注 3
如果收件人接收了受保护的电子邮件，且未将 Exchange 作为邮件服务器，或如果发送者属于另一组织，则只能在功能丰富的电子邮件客户端（如 Outlook）中打开此内容。 不能从 Outlook Web Access 打开此内容。

###### <a name="footnote-4"></a>脚注 4
使用 Exchange ActiveSync IRM，它必须由 Exchange 管理员启用。 用户可以查看受保护电子邮件并回复所有受保护电子邮件，但是他们自己不能保护新的电子邮件。

如果收件人接收了受保护的电子邮件，且未将 Exchange 作为邮件服务器，或如果发送者属于另一组织，则只能在功能丰富的电子邮件客户端（如 Outlook）中打开此内容。 无法从 Outlook Web Access 或使用 Exchange Active Sync IRM 的移动邮件客户端打开此内容。

###### <a name="footnote-5"></a>脚注 5
支持查看和编辑适用于 iOS 的受保护文档；支持查看适用于 Android 的受保护文档。 有关详细信息，请参阅 Office 博客上的以下帖子：[为 iPad 和 iPhone 版 Office 提供 Azure Rights Management 支持](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

###### <a name="footnote-6"></a>脚注 6
有关详细信息，请参阅 Citrix [product documentation for WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html)（Worxmail 的产品文档）。

###### <a name="footnote-7"></a>脚注 7
有关详细信息，请参阅 Office 博客上的以下帖子：[OWA for Android 现可在特定设备上使用](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

###### <a name="footnote-8"></a>脚注 8
有关详细信息，请参阅“企业和移动性”博客上的以下文章：[SealPath 向AutoCAD 引入 RMS 保护功能](https://blogs.technet.microsoft.com/enterprisemobility/2015/09/08/sealpath-brings-rms-protection-to-autocad/)


### <a name="more-information-about-azure-rms-support-for-office"></a>有关针对 Office 的 Azure RMS 支持的详细信息

Azure RMS 已紧密集成到 Word、Excel、PowerPoint 和 Outlook 应用中，在这些应用中，此功能通常称为信息权限管理 (IRM)。 以下 Office 客户端版本支持通过 Azure RMS 保护文件和电子邮件：

- Office 365 ProPlus：Office 2016 和 Office 2013

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

所有版本的 Office（不包括 Office 2007）都支持使用受保护的内容。

带 Office Professional Plus 2010 或 Office Professional 2010 的 Azure RMS：

- 需要适用于 Windows 的 Azure 信息保护客户端或适用于 Windows 的 Rights Management 共享应用程序

- 在 Windows 10 上不受支持

- 不支持联合用户帐户基于表单的身份验证。 这些帐户必须使用 Windows 集成身份验证。

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>有关适用于 iOS 和 Android 的 Azure 信息保护应用的详细信息

适用于 iOS 和 Android 的 Azure 信息保护应用将替换这些设备的 RMS 共享应用程序。 它提供相同的功能，此外，还支持受权限保护的电子邮件和 SharePoint Online 上受权限保护的 PDF 文件。

如果 iOS 和 Android 设备是通过 Microsoft Intune 注册的，则可以使用策略托管的应用部署和管理此应用。 更多详细信息，请参阅 Intune 文档中的[在 Microsoft Intune 控制台中配置和部署移动应用程序管理策略](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 对于此 Intune 文档中的步骤 2，使用说明来发布策略托管的应用。

有关详细信息，请参阅[适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题](../rms-client/mobile-app-faq.md)。


### <a name="more-information-about-the-azure-information-protection-client-for-windows"></a>有关适用于 Windows 的 Azure 信息保护客户端的详细信息

此客户端现替换了适用于 Windows 的 Rights Management 共享应用程序。 

有关详细信息，请参阅下列资源：

- [Azure 信息保护客户端管理员指南](../rms-client/client-admin-guide.md)

- [Azure 信息保护客户端用户指南](../rms-client/client-user-guide.md)

- [适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题解答](../rms-client/mobile-app-faq.md)

使用 [Microsoft Azure 信息保护页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用。

### <a name="more-information-about-the-rights-management-sharing-application"></a>有关 Rights Management 共享应用程序的详细信息

此应用程序现由 Azure 信息保护客户端替代。 它仍然是 Mac 计算机和 Windows Phone 移动设备所必需的应用程序。 

有关详细信息，请参阅下列资源：

-   [权限管理共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)

-   [权限管理共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)

-   [适用于移动平台的 Microsoft Rights Management 共享应用程序的常见问题解答](https://technet.microsoft.com/dn451248)

使用 [Microsoft Azure 信息保护页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载适用于 Mac 计算机和 Windows Phone 的应用。


### <a name="more-information-about-other-applications-that-support-azure-information-protection"></a>有关其他支持 Azure 信息保护的应用程序的详细信息

除了表中的应用程序，支持 Azure Rights Management 服务的 API 的任何应用程序都可与 Azure 信息保护集成，其中包括：

- 使用 RMS SDK 内部编写的业务线应用程序

- 使用 RMS SDK 编写，来自软件供应商的应用程序。

有关详细信息，请参阅 [Azure 信息保护开发人员指南](../develop/developers-guide.md)。

### <a name="applications-that-are-not-supported-by-azure-rms"></a>不受 Azure RMS 支持的应用程序

Azure RMS 当前不支持以下应用程序：

-   Microsoft Office for Mac 2011

-   Microsoft OneDrive for Business for SharePoint Server 2013

-   XPS 查看器
 
此外，RMS 共享应用程序和 Azure 信息保护客户端具有以下限制：

-   对于 Windows 计算机：要求最低版本为 Windows 7 Service Pack 1

## <a name="rms-enlightened-solutions"></a>启用 RMS 的解决方案

下表列出了软件供应商提供的启用 RMS 的解决方案。

如果你是软件供应商，且提供的解决方案此表未列出，请使用 Azure AD 注册你的应用程序。 有关详细信息，请参阅[如何使用 Azure AD 注册应用并为其启用 RMS](../develop/authentication-integration.md)。


|产品|供应商|说明|
|-------------------------------|---------------------------|-----------------|
|绝对|绝对|用于保护内容的数据丢失防护 (DLP)。|
|Content Locker|VMware|存储、使用并创建受保护的内容。|
|Controle|TakeControle|使用标记和保护功能进行电子数据展示。|
|Halocore|Secude|保护从 SAP 环境导出的文件。|
|MaaS 360|IBM|旨在使用和保护文档的集成。|
|Mobiliya|Mobiliya|保护 EMC Documentum 存储库中的文档。
|Ramessys|Ramessys|面向 Chemcart 和 Documentum 的集成。
|Sealpath|Sealpath Technologies|与 CAD 设计工具（如 AutoCAD 和 Siemens Jt2GO）集成。
|SecRMM|Sqaudra Technologies |为可移动媒体提供文档保护。
|Security Sheriff|CryptZone |SharePoint 上的访问管理，根据文档分类和访问权限来保护文档。
|Symantec DLP|Symantec |检测和监视受保护的文件。

## <a name="next-steps"></a>后续步骤
若要查看其他要求，请参阅 [Azure 信息保护的要求](requirements-azure-rms.md)。

有关最常用的应用程序如何支持 Azure RMS 的详细信息，请参阅[应用程序如何支持 Azure Rights Management 服务](../understand-explore/applications-support.md)。

有关如何为 Azure RMS 配置最常用的应用程序的信息，请参阅[为 Azure Rights Management 配置应用程序](../deploy-use/configure-applications.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]