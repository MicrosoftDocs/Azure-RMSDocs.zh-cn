---
title: 对 RMS 数据保护的应用程序支持 - AIP
description: 确定使用 RMS API 本机支持 Azure 信息保护中的 Azure Rights Management 服务的应用程序。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/13/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b632319b595c3745be576fa2d508ebcb089ec8aa
ms.sourcegitcommit: 1e6394044d646278ae582c7713cac8ffb9bf4c1e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "49170155"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的应用程序

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)


使用下表确定提供 Azure Rights Management Service（简称 Azure RMS，为 Azure 信息保护提供数据保护）本机支持的应用程序和解决方案。

对于这些应用程序和解决方案，可以使用支持用法限制的 Rights Management API，从而紧密集成 Rights Management 支持。 这些应用程序和解决方案也称为“启用 RMS 的”应用程序和解决方案。

除非另行说明，否则支持的功能同时适用于 Azure RMS 和 AD RMS。 此外，iOS、Android、macOS 和 Windows Phone 8.1 上的 AD RMS 支持需要 [Active Directory Rights Management Services 移动设备扩展](https://technet.microsoft.com/library/dn673574.aspx)。

## <a name="rms-enlightened-applications"></a>启用 RMS 的应用程序

下表列出了 Microsoft 和软件供应商提供的启用 RMS 的客户端应用程序。 

有关查看受保护的 PDF 文档的信息，请参阅[适用于 Microsoft 信息保护的受保护的 PDF 阅读器](./rms-client/protected-pdf-readers.md)。

有关表列的信息：

-   **电子邮件：** 所列电子邮件客户端可以保护电子邮件本身，而电子邮件会自动保护任何不再受保护的附加 Office 文件。 在这种情况下，客户端的预览功能可以向授权收件人显示受保护的内容（邮件和附件）。 但是，如果未保护电子邮件本身，而保护了附件，则客户端的预览功能将无法向授权收件人显示受保护的附件。 
    
    提示：对于不支持保护电子邮件的电子邮件客户端，请考虑使用 [Exchange Online 邮件流规则来应用此保护](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)。

-   **其他文件类型**：文本和图像文件包括文件扩展名为 .txt、.xml、.jpg 和 .jpeg 之类的文件。 这些文件在接受 Rights Management 提供的本机保护以后，会更改其文件扩展名，变为只读文件。 不能进行本机保护的文件在接受 Rights Management 提供的常规保护以后，其文件扩展名为 .pfile。 有关详细信息，请参阅 Azure 信息保护客户端管理员指南中的[支持的文件类型](./rms-client/client-admin-guide-file-types.md)。


|**设备操作系统**|Word、Excel、PowerPoint|Email|其他文件类型|
|---------------------------|-----------------------|-----------------|---------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office Online（查看受保护的文档）[[1]](#footnote-1)<br /><br />Web 浏览器 [[2]](#footnote-2)|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Web 浏览器 [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4) |适用于 Windows 的 Azure 信息保护客户端：文本、图像、pfile<br /><br />适用于 Windows 的 RMS 共享应用程序：文本、图像、pfile<br /><br />适用于 AutoCAD 的 SealPath RMS 插件：.dwg|
|**iOS**|GigaTrust<br /><br /> Office Mobile（查看和编辑受保护的文档）<br /><br />Office Online [[1]](#footnote-1)<br /><br />TITUS 文档<br /><br />Web 浏览器 [[2]](#footnote-2)|Azure 信息保护应用（查看受保护的电子邮件）<br /><br />BlackBerry Work<br /><br />Citrix WorxMail <br /><br />NitroDesk [[4]](#footnote-4)<br /><br />iPad 和 iPhone 版 Outlook [[4]](#footnote-4)<br /><br />TITUS Mail <br /><br />Web 浏览器 [[3]](#footnote-3)|Azure 信息保护应用（查看正在保护的文本和图像）<br /><br />TITUS 文档：Pfile|
|**Outlook Web Access (OWA)**|适用于 Android 的 GigaTrust 应用<br /><br />Office Online [[1]](#footnote-1)<br /><br />Office Mobile <br /><br />Web 浏览器 [[2]](#footnote-2)|9Folders [[4]](#footnote-4)<br /><br />Azure 信息保护应用（查看受保护的电子邮件）<br /><br />BlackBerry Work <br /><br />适用于 Android 的 GigaTrust 应用程序 [[4]](#footnote-4)<br /><br />Citrix WorxMail <br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for Android [[4]](#footnote-4)<br /><br />Samsung Email（S3 及更高版本）[[4]](#footnote-4)<br /><br />TITUS Classification for Mobile <br /><br />Web 浏览器 [[3]](#footnote-3)|Azure 信息保护应用（查看受保护的文本和图像）|
|**macOS**|Office 2016 for Mac<br /><br />Office Online [[1]](#footnote-1)<br /><br />Web 浏览器 [[2]](#footnote-2)|Outlook 2016 for Mac<br /><br />Web 浏览器 [[3]](#footnote-3)|RMS 共享应用（查看受保护的文本、图像、常规受保护的文件）|
|**Windows 10 移动版**|Office Mobile 应用（查看使用 Azure RMS 的受保护文档） <br /><br />Web 浏览器 [[2]](#footnote-2)|Citrix WorxMail <br /><br />Outlook 邮件（查看受保护的电子邮件） <br /><br />Web 浏览器 [[3]](#footnote-3)|不支持|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[1]](#footnote-1)<br /><br />Web 浏览器 [[2]](#footnote-2)|Outlook 2013 RT<br /><br />Windows 相关邮件应用程序<br /><br />Web 浏览器 [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go：JT 文件|
|**Windows Phone 8.1**|Office Mobile（仅适用于 AD RMS）<br /><br />Web 浏览器 [[2]](#footnote-2)|Outlook Mobile [[4]](#footnote-4) <br /><br />Web 浏览器 [[3]](#footnote-3)|RMS 共享应用（查看受保护的文本、图像、常规受保护的文件）|
|**Blackberry 10**|Web 浏览器 [[2]](#footnote-2)|Blackberry 电子邮件 [[4]](#footnote-4) <br /><br />Web 浏览器 [[3]](#footnote-3)|不支持|

###### <a name="footnote-1"></a>脚注 1
仅支持 SharePoint Online 和 OneDrive for Business，文档在上传到受保护的库之前不受支持。

###### <a name="footnote-2"></a>脚注 2
适用于通过使用[具有新功能的 Office 365邮件加密](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)保护的 [Office 附件](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)。

###### <a name="footnote-3"></a>脚注 3
如果发件人和收件人属于同一组织。 或者为以下任一种情况：

- 发件人或收件人使用的是 Exchange Online。

- 发件人使用混合配置中的本地 Exchange。 

###### <a name="footnote-4"></a>脚注 4
使用 Exchange ActiveSync IRM，它必须由 Exchange 管理员启用。 用户可以查看并答复所有受保护的电子邮件，但是他们不能保护新的电子邮件。
 
如果电子邮件应用程序因 Exchange ActiveSync IRM 未启用而无法呈现邮件，当发件人使用混合配置中的 Exchange Online 或本地 Exchange 时，收件人可以在 Web 浏览器中查看电子邮件。 



### <a name="more-information-about-azure-rms-support-for-office"></a>有关针对 Office 的 Azure RMS 支持的详细信息

Azure RMS 已紧密集成到 Word、Excel、PowerPoint 和 Outlook 应用中，在这些应用中，此功能通常称为信息权限管理 (IRM)。 

另请参阅：[Office 应用程序服务说明](https://technet.microsoft.com/library/office-applications-service-description.aspx)

#### <a name="windows-computers-for-information-rights-management-irm"></a>用于信息权限管理 (IRM) 的 Windows 计算机

以下 Office 客户端套件支持使用 Azure Rights Management 服务保护 Windows 计算机上的文件和电子邮件：

- 当为用户分配了 Azure Rights Management（也称为 Office 365 Azure 信息保护）许可证，可以使用含 Office 2016 应用的 Office 365（最低版本为 1805，生成号 9330.2078）

- Office 365 ProPlus：Office 2016 和 Office 2013
    
    包含 Azure 信息保护数据保护的大多数 Office 365 订阅（并非所有）都附带这些版本的 Office。 检查你的订阅信息，确定是否包含 Office 365 专业增强版。 你还可以在 [Azure 信息保护数据表](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)中找到此信息。

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010 Service Pack 2

所有版本的 Office（不包括 Office 2007）都支持使用受保护的内容。

当你将 Azure Rights Management 服务与 Office Professional Plus 2010 和 Service Pack 2 或 Office Professional 2010 Service Pack 2 配合使用：

- 需要适用于 Windows 的 Azure 信息保护客户端或适用于 Windows 的 Rights Management 共享应用程序。

- 在 Windows 10 上不受支持。

- 不支持联合用户帐户基于表单的身份验证。 这些帐户必须使用 Windows 集成身份验证。

- 不支持使用用户通过 Azure 信息保护客户端选择的自定义权限来替代模板保护。 在此方案中，必须首先删除原始保护才能应用自定义权限。

#### <a name="mac-computers-for-information-rights-management-irm"></a>用于信息权限管理 (IRM) 的 Mac 计算机

以下 Office 客户端套件支持使用 Azure RMS 保护 macOS 上的文件和电子邮件：

- Office 365 专业增强版：Office 2016

- Office Standard 2016 for Mac

提示：要开始使用 Office for Mac 保护文档，以下常见问题可能有用：[如何配置 Mac 计算机以保护和跟踪文档？](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>有关适用于 iOS 和 Android 的 Azure 信息保护应用的详细信息

适用于 iOS 和 Android 的 Azure 信息保护查看器应用将替换这些设备的 RMS 共享应用程序。 它提供相同的功能，此外，还支持受权限保护的电子邮件和 SharePoint Online 上受权限保护的 PDF 文件。

如果 iOS 和 Android 设备是通过 Microsoft Intune 注册的，则可以使用策略托管的应用部署和管理此应用。 更多详细信息，请参阅 Intune 文档中的[在 Microsoft Intune 控制台中配置和部署移动应用程序管理策略](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 对于此 Intune 文档中的步骤 2，使用说明来发布策略托管的应用。

有关详细信息，请参阅[适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题](./rms-client/mobile-app-faq.md)。


### <a name="more-information-about-the-azure-information-protection-client-for-windows"></a>有关适用于 Windows 的 Azure 信息保护客户端的详细信息

此客户端现替换了适用于 Windows 的 Rights Management 共享应用程序。

有关详细信息，请参阅下列资源：

- [Azure 信息保护客户端管理员指南](./rms-client/client-admin-guide.md)

- [Azure 信息保护客户端用户指南](./rms-client/client-user-guide.md)

- [适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题解答](./rms-client/mobile-app-faq.md)

使用 [Microsoft Azure 信息保护页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用。

### <a name="more-information-about-the-rights-management-sharing-application"></a>有关 Rights Management 共享应用程序的详细信息

此应用程序现由 Azure 信息保护客户端替代。 它仍然是使用 Windows Phone 移动设备查看受保护文件的必需应用程序。 

对于 Mac 计算机，它提供了一个查看器，可查看受保护的 PDF 文件 (.ppdf)、受保护的文本图像和受常规保护的文件。 适用于 Mac 的 RMS 共享应用也可保护图像文件，但不能保护其他文件。 要保护 Office 文件，请使用 Office for Mac。 

有关详细信息，请参阅下列资源：

-   [权限管理共享应用程序管理员指南](./rms-client/sharing-app-admin-guide.md)

-   [权限管理共享应用程序用户指南](./rms-client/sharing-app-user-guide.md)

-   [适用于移动平台的 Microsoft Rights Management 共享应用程序的常见问题解答](https://technet.microsoft.com/dn451248)

使用 [Microsoft Azure 信息保护页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载适用于 Mac 计算机和 Windows Phone 的查看器。


### <a name="more-information-about-other-applications-that-support-azure-information-protection"></a>有关其他支持 Azure 信息保护的应用程序的详细信息

除了表中的应用程序，支持 Azure Rights Management 服务的 API 的任何应用程序都可与 Azure 信息保护集成，其中包括：

- 使用 RMS SDK 内部编写的业务线应用程序

- 使用 RMS SDK 编写，来自软件供应商的应用程序。

有关详细信息，请参阅 [Azure 信息保护开发人员指南](./develop/developers-guide.md)。

### <a name="applications-that-are-not-supported-by-azure-rms"></a>不受 Azure RMS 支持的应用程序

Azure RMS 当前不支持以下应用程序：

-   Microsoft OneDrive for Business for SharePoint Server 2013

-   XPS 查看器

此外，RMS 共享应用程序和 Azure 信息保护客户端具有以下限制：

-   对于 Windows 计算机：要求最低版本为 Windows 7 Service Pack 1

## <a name="rms-enlightened-solutions"></a>启用 RMS 的解决方案

下表列出了软件供应商提供的启用 RMS 的解决方案。

如果你是软件供应商，且提供的解决方案此表未列出，请使用 Azure AD 注册你的应用程序。 有关详细信息，请参阅[如何使用 Azure AD 注册应用并为其启用 RMS](./develop/authentication-integration.md)。


|产品|供应商|描述|
|-------------------------------|---------------------------|-----------------|
|绝对|绝对|用于保护内容的数据丢失防护 (DLP)。|
|Content Locker|VMware|存储、使用并创建受保护的内容。|
|Controle|TakeControle|使用标记和保护功能进行电子数据展示。|
|Forcepoint|Forcepoint DLP|旨在强制实施组织数据安全策略的终结点数据丢失防护 (DLP) 解决方案。|
|Halocore|Secude|保护从 SAP 环境导出的文件。|
|MaaS 360|IBM|旨在使用和保护文档的集成。|
|Mobiliya|Mobiliya|保护 EMC Documentum 存储库中的文档。
|Ramessys|Ramessys|面向 Chemcart 和 Documentum 的集成。
|Sealpath|Sealpath Technologies|与 CAD 设计工具（如 AutoCAD 和 Siemens Jt2GO）集成。
|SecRMM|Sqaudra Technologies |为可移动媒体提供文档保护。
|Security Sheriff|CryptZone |SharePoint 上的访问管理，根据文档分类和访问权限来保护文档。
|Symantec DLP|Symantec |检测和监视受保护的文件。

## <a name="next-steps"></a>后续步骤
若要查看其他要求，请参阅 [Azure 信息保护的要求](requirements.md)。

有关最常用的应用程序如何支持 Azure RMS 的详细信息，请参阅[应用程序如何支持 Azure Rights Management 服务](./applications-support.md)。

有关如何为 Azure RMS 配置最常用的应用程序的信息，请参阅[为 Azure Rights Management 配置应用程序](configure-applications.md)。

