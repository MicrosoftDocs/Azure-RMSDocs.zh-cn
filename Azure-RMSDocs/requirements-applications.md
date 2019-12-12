---
title: 对 RMS 数据保护的应用程序支持 - AIP
description: 确定使用 RMS API 本机支持 Azure 信息保护中的 Azure Rights Management 服务的应用程序。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 81c95640f22e6234a3cc6d3487db6c12345a57b8
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73710235"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的应用程序

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)


使用以下信息来确定以本机方式支持 Azure Rights Management 服务（Azure RMS）的应用程序和解决方案，该服务提供 Azure 信息保护的数据保护。

对于这些应用程序和解决方案，Rights Management 支持通过使用 Rights Management Api 紧密集成，以支持[使用限制](configure-usage-rights.md)。 这些应用程序和解决方案也称为“启用 RMS 的”应用程序和解决方案。

除非另行说明，否则支持的功能同时适用于 Azure RMS 和 AD RMS。 此外，iOS、Android、macOS 和 Windows Phone 8.1 上的 AD RMS 支持需要 [Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))。

## <a name="rms-enlightened-applications"></a>启用 RMS 的应用程序

下表列出了 Microsoft 和软件供应商提供的启用 RMS 的客户端应用程序。 

有关查看受保护的 PDF 文档的信息，请参阅[适用于 Microsoft 信息保护的受保护的 PDF 阅读器](./rms-client/protected-pdf-readers.md)。

有关表列的信息：

-   **电子邮件：** 所列电子邮件客户端可以保护电子邮件本身，而电子邮件会自动保护任何不再受保护的附加 Office 文件。 在这种情况下，客户端的预览功能可以向授权收件人显示受保护的内容（邮件和附件）。 但是，如果未保护电子邮件本身，而保护了附件，则客户端的预览功能将无法向授权收件人显示受保护的附件。 
    
    提示：对于不支持保护电子邮件的电子邮件客户端，请考虑使用 [Exchange Online 邮件流规则来应用此保护](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)。

-   **其他文件类型**：文本和图像文件包括文件扩展名为 .txt、.xml、.jpg 和 .jpeg 之类的文件。 这些文件在接受 Rights Management 提供的本机保护以后，会更改其文件扩展名，变为只读文件。 不能进行本机保护的文件在接受 Rights Management 提供的常规保护以后，其文件扩展名为 .pfile。 有关详细信息，请参阅 Azure 信息保护客户端管理员指南中的[支持的文件类型](./rms-client/client-admin-guide-file-types.md)。


|**设备操作系统**|Word、Excel、PowerPoint|电子邮件|其他文件类型|
|---------------------------|-----------------------|-----------------|---------|
|**Windows**|Office 365 应用 [[1]](#footnote-1)<br /><br />Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office 2019 <br /><br />Office for web （查看受保护的文档） [[2]](#footnote-2)<br /><br />Web 浏览器 [[3]](#footnote-3)|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook 2016 <br /><br />Outlook 2019 <br /><br />Office 365 ProPlus 中的 Outlook<br /><br />Web 浏览器 [[4]](#footnote-4)<br /><br />Windows 邮件 [[5]](#footnote-5) |Office 365 应用、Office 2019 和 Office 2016：. .vsdm、.vsdx、. .vssm、.vstm、.vssx、.vstx 中的 Visio <br /><br />适用于 Windows 的 Azure 信息保护客户端：文本、图像、pfile<br /><br />适用于 AutoCAD 的 SealPath RMS 插件：.dwg|
|**Android**|GigaTrust<br /><br /> Office Mobile <br /><br />用于 web 的 Office [[2]](#footnote-2)<br /><br />TITUS 文档<br /><br />Web 浏览器 [[3]](#footnote-3)|Azure 信息保护应用（查看受保护的电子邮件）<br /><br />BlackBerry Work<br /><br />Citrix WorxMail <br /><br />NitroDesk [[5]](#footnote-5)<br /><br />iPad 和 iPhone 版 Outlook [[5]](#footnote-5)<br /><br />TITUS Mail <br /><br />Web 浏览器 [[4]](#footnote-4)|Azure 信息保护应用（查看正在保护的文本和图像）<br /><br />TITUS 文档：Pfile|
|**Android
**|适用于 Android 的 GigaTrust 应用程序<br /><br />用于 web 的 Office [[2]](#footnote-2)<br /><br />Office Mobile （除非使用敏感度标签，仅限于查看和编辑受保护的文档） <br /><br />Web 浏览器 [[3]](#footnote-3)|9Folders [[5]](#footnote-5)<br /><br />Azure 信息保护应用（查看受保护的电子邮件）<br /><br />BlackBerry Work <br /><br />适用于 Android 的 GigaTrust 应用 [[5]](#footnote-5)<br /><br />Citrix WorxMail <br /><br />NitroDesk [[5]](#footnote-5)<br /><br />Outlook for Android [[5]](#footnote-5)<br /><br />Samsung Email（S3 及更高版本）[[5]](#footnote-5)<br /><br />TITUS Classification for Mobile <br /><br />Web 浏览器 [[4]](#footnote-4)|Azure 信息保护应用（查看受保护的文本和图像）|
|**macOS**|Office 365 应用<br /><br />Office 2019 for Mac<br /><br />Office 2016 for Mac<br /><br />用于 web 的 Office [[2]](#footnote-2)<br /><br />Web 浏览器 [[3]](#footnote-3)|Outlook 2019 for Mac<br /><br /> Outlook 2016 for Mac<br /><br />Web 浏览器 [[4]](#footnote-4)|RMS 共享应用（查看受保护的文本、图像、常规受保护的文件）|
|**Windows 10 移动版**|Office Mobile 应用（查看使用 Azure RMS 的受保护文档） <br /><br />Web 浏览器 [[3]](#footnote-3)|Citrix WorxMail <br /><br />Outlook 邮件（查看受保护的电子邮件） <br /><br />Web 浏览器 [[4]](#footnote-4)|不支持|
|**Blackberry 10**|Web 浏览器 [[3]](#footnote-3)|Blackberry 电子邮件 [[5]](#footnote-5) <br /><br />Web 浏览器 [[4]](#footnote-4)|不支持|

###### <a name="footnote-1"></a>脚注 1
包括： 
- Office 应用最低版本 1805，Office 365 商业版或 Microsoft 365 商业版中的内部版本 9330.2078，前提是已为用户分配了 Azure Rights Management（亦称为“适用于 Office 365 的 Azure 信息保护”）许可证
- Office 365 专业增强版应用

###### <a name="footnote-2"></a>脚注 2
仅支持 SharePoint Online 和 OneDrive for Business，文档在上传到受保护的库之前不受支持。

###### <a name="footnote-3"></a>脚注 3
适用于通过使用[具有新功能的 Office 365邮件加密](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)保护的 [Office 附件](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)。

###### <a name="footnote-4"></a>脚注 4
如果发件人和收件人属于同一组织。 或者为以下任一种情况：
- 发件人或收件人使用的是 Exchange Online。
- 发件人使用混合配置中的本地 Exchange。 

###### <a name="footnote-5"></a>脚注 5
使用 Exchange ActiveSync IRM，它必须由 Exchange 管理员启用。 用户可以查看并答复所有受保护的电子邮件，但是他们不能保护新的电子邮件。
 
如果电子邮件应用程序因 Exchange ActiveSync IRM 未启用而无法呈现邮件，当发件人使用混合配置中的 Exchange Online 或本地 Exchange 时，收件人可以在 Web 浏览器中查看电子邮件。 

### <a name="more-information-about-azure-rms-support-for-office"></a>有关针对 Office 的 Azure RMS 支持的详细信息

Azure RMS 已紧密集成到 Word、Excel、PowerPoint 和 Outlook 应用中，在这些应用中，此功能通常称为信息权限管理 (IRM)。 

另请参阅：[Office 应用程序服务说明](https://technet.microsoft.com/library/office-applications-service-description.aspx)

#### <a name="windows-computers-for-information-rights-management-irm"></a>用于信息权限管理 (IRM) 的 Windows 计算机

以下 Office 客户端套件支持使用 Azure Rights Management 服务保护 Windows 计算机上的文件和电子邮件：

- Office 应用最低版本 1805，Office 365 商业版或 Microsoft 365 商业版中的内部版本 9330.2078，前提是已为用户分配了 Azure Rights Management（亦称为“适用于 Office 365 的 Azure 信息保护”）许可证

- Office 365 ProPlus
    
    包含 Azure 信息保护数据保护的大多数 Office 365 订阅（并非所有）都附带这些版本的 Office。 检查你的订阅信息，确定是否包含 Office 365 专业增强版。 你还可以在 [Azure 信息保护数据表](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)中找到此信息。

- Office 专业增强版 2019

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010 Service Pack 2

所有版本的 Office（不包括 Office 2007）都支持使用受保护的内容。

当你将 Azure Rights Management 服务与 Office Professional Plus 2010 和 Service Pack 2 或 Office Professional 2010 Service Pack 2 配合使用：

- 需要适用于 Windows 的 Azure 信息保护客户端。

- 在 Windows 10 上不受支持。

- 不支持联合用户帐户基于表单的身份验证。 这些帐户必须使用 Windows 集成身份验证。

- 不支持使用用户通过 Azure 信息保护客户端选择的自定义权限来替代模板保护。 在此方案中，必须首先删除原始保护才能应用自定义权限。

#### <a name="mac-computers-for-information-rights-management-irm"></a>用于信息权限管理 (IRM) 的 Mac 计算机

以下 Office 客户端套件支持使用 Azure RMS 保护 macOS 上的文件和电子邮件：

- Office 365 ProPlus

- Office Standard 2019 for Mac

- Office Standard 2016 for Mac

所有版本的 Office for Mac 2019 和 Office for Mac 2016 都支持使用受保护的内容。

提示：要开始使用 Office for Mac 保护文档，以下常见问题可能有用：[如何配置 Mac 计算机以保护和跟踪文档？](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>有关适用于 iOS 和 Android 的 Azure 信息保护应用的详细信息

当 iOS 和 Android 移动设备没有能够打开受保护电子邮件的电子邮件应用时，适用于 iOS 和 Android 的 Azure 信息保护应用将为受权限保护的电子邮件（.rpmsg 文件）提供查看器。 通过此应用还可以打开受权限保护的 PDF 文件、图片和文本文件。

如果已通过 Microsoft Intune 注册 iOS 和 Android 设备，用户可以从公司门户安装应用，你可以使用 Intune 的[应用保护策略](/intune/app-protection-policies)来管理应用。

有关如何使用应用的详细信息，请参阅[适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题解答](./rms-client/mobile-app-faq.md)。


### <a name="more-information-about-the-azure-information-protection-client-for-windows"></a>有关适用于 Windows 的 Azure 信息保护客户端的详细信息

有关详情，请参阅以下资源：

- Azure 信息保护客户端管理员指南：
    - [统一标签客户端](./rms-client/clientv2-admin-guide.md)
    - [经典客户端](./rms-client/client-admin-guide.md)

- Azure 信息保护客户端用户指南：
    - [统一标签客户端](./rms-client/clientv2-user-guide.md)
    - [经典客户端](./rms-client/client-user-guide.md)

- [适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题解答](./rms-client/mobile-app-faq.md)

使用 [Microsoft Azure 信息保护页](https://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用。

### <a name="more-information-about-the-rights-management-sharing-app"></a>有关 Rights Management 共享应用的详细信息

对于 Mac 计算机，Rights Management 共享应用提供了一个查看器，可查看受保护的 PDF 文件 (.ppdf)、受保护的文本图像和受常规保护的文件。 它也可保护图像文件，但不能保护其他文件。 若要保护这些计算机上的 Office 文件，请使用 Office for Mac 或 Office 365 专业增强版。 

有关详情，请参阅以下资源：

-   [适用于移动平台的 Microsoft Rights Management 共享应用程序的常见问题解答](https://technet.microsoft.com/dn451248)

使用 [Microsoft Azure 信息保护页](https://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载适用于 Mac 计算机的 Rights Management 共享应用。


### <a name="more-information-about-other-applications-that-support-azure-information-protection"></a>有关其他支持 Azure 信息保护的应用程序的详细信息

除了表中的应用程序，支持 Azure Rights Management 服务的 API 的任何应用程序都可与 Azure 信息保护集成，其中包括：

- 使用 RMS SDK 内部编写的业务线应用程序

- 使用 RMS SDK 编写，来自软件供应商的应用程序。

有关详细信息，请参阅 [Azure 信息保护开发人员指南](./develop/developers-guide.md)。

### <a name="applications-that-are-not-supported-by-azure-rms"></a>不受 Azure RMS 支持的应用程序

Azure RMS 当前不支持以下应用程序：

- Microsoft OneDrive for Business for SharePoint Server 2013

- XPS 查看器

此外，Azure 信息保护客户端具有以下限制：

- 对于 Windows 计算机：要求最低版本为 Windows 7 Service Pack 1

## <a name="rms-enlightened-solutions"></a>启用 RMS 的解决方案

有关支持 Azure Rights Management 服务和 Azure 信息保护的解决方案的最新信息，请参阅博客文章[Microsoft Ignite 2019 – Microsoft Information Protection 解决方案合作伙伴生态系统展示](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Microsoft-Ignite-2019-Microsoft-Information-Protection-solutions/ba-p/967024)。

## <a name="next-steps"></a>后续步骤
若要查看其他要求，请参阅 [Azure 信息保护的要求](requirements.md)。

有关最常用的应用程序如何支持 Azure Rights Management 服务的详细信息，请参阅[应用程序如何支持 azure Rights Management 服务](./applications-support.md)。

有关如何为 Azure Rights Management 服务配置最常使用的应用程序的信息，请参阅为[azure Rights Management 配置应用程序](configure-applications.md)。

