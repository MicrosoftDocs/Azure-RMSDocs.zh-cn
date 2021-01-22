---
title: 适用于 Azure 信息保护的 RMS 数据保护应用程序支持
description: 确定对 Azure Rights Management Service (Azure RMS) 提供内置支持的应用程序和解决方案。 Azure RMS 为 Azure 信息保护 (AIP) 提供数据保护。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 13454e0642cfaf60ed3bd742050cd3eb0d3a38dc
ms.sourcegitcommit: ee20112ada09165b185d9c0c9e7f1179fc39e7cf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2021
ms.locfileid: "98659130"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的应用程序

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>相关内容：*[AIP 统一标记客户端和 AIP 经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。


此页上列出的应用程序和解决方案对 Azure Rights Management Service（简称 Azure RMS，为 Azure 信息保护提供数据保护）服务提供内置支持。

这些应用程序和解决方案称为“启用 RMS”的应用程序和解决方案，通过使用 Rights Management API 将 Rights Management 和[使用情况限制](configure-usage-rights.md)紧密集成。

> [!NOTE]
> 除非另行说明，否则支持的功能同时适用于 Azure RMS 和 AD RMS。 
>
> iOS、Android、macOS 和 Windows Phone 8.1 上的 AD RMS 支持也需要 [Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))。
> 

## <a name="windows-rms-enlightened-applications"></a>Windows 上启用 RMS 的应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - [Microsoft 365 应用](#microsoft-365-app-support) <br />- Office 2010 <br />- Office 2013<br />- Office 2016 <br />- Office 2019 <br />- [Office 网页版（查看受保护的文档）](#viewing-protected-documents-in-office-for-the-web)<br />- [Web 浏览器](#web-browser-support)        |
|[电子邮件](#viewing-protected-content-in-email-clients)      |   - Outlook 2010<br />- Outlook 2013<br />- Outlook 2016 <br />- Outlook 2019 <br />- Microsoft 365 企业应用版中的 Outlook<br />- [Web 浏览器](#web-browser-support)<br />- [Windows 邮件](#email-clients-using-exchange-activesync-irm)|
|[**其他文件类型**](#supported-text-and-image-file-types)    |  - Microsoft 365 应用、Office 2019 和 Office 2016 中的 Visio：.vsdm、.vsdx、.vssm、.vstm、.vssx、.vstx      <br />- 适用于 Windows 的 Azure 信息保护客户端：文本、图像、pfile <br />- 适用于 AutoCAD 的 SealPath RMS 插件：.dwg       |
| | |

## <a name="macos-rms-enlightened-applications"></a>macOS 上启用 RMS 的应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    |  - Microsoft 365 应用，版本 16.40 或更高版本 <br />- Office 2019 for Mac，版本 16.40 或更高版本<br />- Office 2016 for Mac，版本 16.16.27 或更高版本<br />- [Office 网页版](#viewing-protected-documents-in-office-for-the-web)<br />- [Web 浏览器](#web-browser-support)    |
|[电子邮件](#viewing-protected-content-in-email-clients)   |   - Outlook 2019 for Mac，版本 16.40 或更高版本<br />- Outlook 2016 for Mac，版本 16.16.27 或更高版本<br />- [Web 浏览器](#web-browser-support)     |
|[**其他文件类型**](#supported-text-and-image-file-types)    | RMS 共享应用（查看受保护的文本、图像、常规受保护的文件）   |
| | |

## <a name="android-rms-enlightened-applications"></a>Android 上启用 RMS 的应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    |- 适用于 Android 的 GigaTrust 应用<br />- [Office 网页版](#viewing-protected-documents-in-office-for-the-web)<br />- Office Mobile（除非使用敏感度标签，否则仅限于查看和编辑受保护的文档） <br />- [Web 浏览器](#web-browser-support)      |
|[电子邮件](#viewing-protected-content-in-email-clients)     | - [9Folders](#email-clients-using-exchange-activesync-irm)<br />- Azure 信息保护应用（查看受保护的电子邮件）<br />- BlackBerry Work <br />- [适用于 Android 的 GigaTrust 应用](#email-clients-using-exchange-activesync-irm) <br />- Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook for Android](#email-clients-using-exchange-activesync-irm)<br />- [Samsung Email（S3 及更高版本）](#email-clients-using-exchange-activesync-irm)<br />- TITUS Classification for Mobile <br /><br />- [Web 浏览器](#web-browser-support)       |
|[**其他文件类型**](#supported-text-and-image-file-types)    |  Azure 信息保护应用（查看受保护的文本和图像）  |
| | |


## <a name="ios-rms-enlightened-applications"></a>iOS 上启用 RMS 的应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    |  - GigaTrust<br />- Office Mobile <br />- [Office 网页版](#viewing-protected-documents-in-office-for-the-web)<br />- TITUS Docs<br />- [Web 浏览器](#web-browser-support)    |
|[电子邮件](#viewing-protected-content-in-email-clients)     |   - Azure 信息保护应用（查看受保护的电子邮件）<br />- BlackBerry Work<br />- Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [iPad 和 iPhone 版 Outlook](#email-clients-using-exchange-activesync-irm)<br />- TITUS Mail <br />- [Web 浏览器](#web-browser-support)     |
|[**其他文件类型**](#supported-text-and-image-file-types)     | - Azure 信息保护应用（查看正在保护的文本和图像）<br />- TITUS Docs：Pfile  |
| | |

## <a name="windows-10-mobile-rms-enlightened-applications"></a>Windows 10 移动版上启用 RMS 的应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - Office Mobile 应用（查看使用 Azure RMS 的受保护文档） <br />- [Web 浏览器](#web-browser-support)    |
|[电子邮件](#viewing-protected-content-in-email-clients)    |  - Citrix WorxMail <br />- Outlook 邮件（查看受保护的电子邮件） <br />- [Web 浏览器](#web-browser-support)     |
|[**其他文件类型**](#supported-text-and-image-file-types)    | 不支持   |
| | |

## <a name="blackberry-10-rms-enlightened-applications"></a>Blackberry 10 上启用 RMS 的应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - [Web 浏览器](#web-browser-support)    |
|[电子邮件](#viewing-protected-content-in-email-clients)   | - [Blackberry 电子邮件](#email-clients-using-exchange-activesync-irm) <br />- [Web 浏览器](#web-browser-support)      |
|[**其他文件类型**](#supported-text-and-image-file-types)    | 不支持   |
| | |


## <a name="additional-details-about-rms-enlightened-applications"></a>有关启用 RMS 的应用程序的其他详细信息

有关上面列出的启用 RMS 的应用程序表的详细信息，请参阅：

- [查看电子邮件客户端中的受保护内容](#viewing-protected-content-in-email-clients)
- [受支持的文本和图像文件类型](#supported-text-and-image-file-types)
- [Microsoft 365 应用支持](#microsoft-365-app-support)
- [在 Office 网页版中查看受保护的文档](#viewing-protected-documents-in-office-for-the-web)
- [Web 浏览器支持](#web-browser-support)
- [使用 Exchange ActiveSync 信息权限管理 (IRM) 的电子邮件客户端](#email-clients-using-exchange-activesync-irm)

### <a name="viewing-protected-content-in-email-clients"></a>查看电子邮件客户端中的受保护内容

电子邮件客户端保护邮件时，附加到邮件且当前未受保护的所有 Office 文件将与电子邮件一起受到保护。 在这种情况下，电子邮件和附件只能由经过授权的收件人在电子邮件客户端中查看。

但是，如果只有附件受到保护，而不是电子邮件本身，将无法在电子邮件客户端中预览附件，即使是由经过授权的收件人操作也是如此。

> [!TIP]
> 对于不支持保护电子邮件的电子邮件客户端，请考虑使用 [Exchange Online 邮件流规则来应用此保护](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)。

### <a name="supported-text-and-image-file-types"></a>受支持的文本和图像文件类型

除了 Office 文件和电子邮件，文件类型还包括文本和图像文件类型，其扩展名有 .txt、.xml、.jpg 和 .jpeg 等   。 

这些文件在接受 Rights Management 提供的本机保护以后，会更改其文件扩展名，然后变为只读文件。 

不能进行本机保护的文件在接受 Rights Management 提供的常规保护以后，其文件扩展名为 .pfile。

有关详细信息，请参阅[受支持的文件类型](./rms-client/client-admin-guide-file-types.md)。

### <a name="microsoft-365-app-support"></a>Microsoft 365 应用支持

包括： 
- Office 应用，对于[各更新通道中受支持的 Microsoft 365 应用版本表](/officeupdates/update-history-microsoft365-apps-by-date)中列出的版本，从 Microsoft 365 商业应用版或 Microsoft 365 商业高级版，前提是已为用户分配了 Azure Rights Management（亦称为“适用于 Microsoft 365 的 Azure 信息保护”）许可证
- Microsoft 365 企业应用版

### <a name="viewing-protected-documents-in-office-for-the-web"></a>在 Office 网页版中查看受保护的文档

仅支持 Microsoft SharePoint 和 OneDrive，文档在上传到受保护的库之前不受支持。

### <a name="web-browser-support"></a>Web 浏览器支持

- 使用 [具有新功能的 Microsoft 365 邮件加密](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)保护 [Office 附件](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)时，Web 浏览器支持 **Word、Excel 和 PowerPoint文件**。

- 对于电子邮件，仅在以下情况下才支持 Web 浏览器：

    - 如果发件人和收件人均属于同一组织
    - 如果发件人或收件人使用的是 Exchange Online
    - 如果发件人使用的是混合配置中的本地 Exchange 

### <a name="email-clients-using-exchange-activesync-irm"></a>使用 Exchange ActiveSync IRM 的电子邮件客户端

以下电子邮件客户端使用 Exchange ActiveSync IRM，它必须由 Exchange 管理员启用：

- Windows Mail
- 9Folders
- 适用于 Android 的 GigaTrust 应用
- NitroDesk
- 适用于 Android 的 Outlook
- Samsung Email（S3 及更高版本）
- iPad 和 iPhone 版 Outlook
- Blackberry 电子邮件

用户可以查看并答复所有受保护的电子邮件，但是不能保护新的电子邮件。
 
如果电子邮件应用程序因 Exchange ActiveSync IRM 未启用而无法呈现邮件，当发件人使用混合配置中的 Exchange Online 或本地 Exchange 时，收件人可以在 Web 浏览器中查看电子邮件。 

## <a name="azure-rms-support-for-office"></a>Office 的 Azure RMS 支持

Azure RMS 已紧密集成到 Word、Excel、PowerPoint 和 Outlook 应用中，在这些应用中，此功能通常称为信息权限管理 (IRM)。 

- [用于信息权限管理 (IRM) 的 Windows 计算机](#windows-computers-for-information-rights-management-irm)
- [用于信息权限管理 (IRM) 的 Mac 计算机](#mac-computers-for-information-rights-management-irm)

另请参阅：[Office 应用程序服务说明](/office365/servicedescriptions/office-applications-service-description/office-applications-service-description)

### <a name="windows-computers-for-information-rights-management-irm"></a>用于信息权限管理 (IRM) 的 Windows 计算机

以下 Office 客户端套件支持使用 Azure Rights Management 服务保护 Windows 计算机上的文件和电子邮件：

- Office 应用，对于[各更新通道中受支持的 Microsoft 365 应用版本表](/officeupdates/update-history-microsoft365-apps-by-date)中列出的版本，从 Microsoft 365 商业应用版或 Microsoft 365 商业高级版，前提是已为用户分配了 Azure Rights Management（亦称为“适用于 Microsoft 365 的 Azure 信息保护”）许可证

- Microsoft 365 企业应用版

    包含 Azure 信息保护中数据保护的大多数订阅（并非所有）都附带这些版本的 Office。 检查你的订阅信息，确定是否包含适用于 Enterprise ProPlus 的 Microsoft 365 应用。 你还可以在 [Azure 信息保护数据表](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)中找到此信息。

- Office 专业增强版 2019

- Office 专业增强版 2016

- **Office 专业增强版 2013**

- Office 专业增强版 2010 Service Pack 2

所有版本的 Office（不包括 Office 2007）都支持使用受保护的内容。

#### <a name="azure-rights-management-service-with-office-professional-plus-2010-and-service-pack-2-or-office-professional-2010-with-service-pack-2"></a>带 Office 专业增强版 2010 的 Azure Rights Management 服务和 Service Pack 2 或带 Service Pack 2 的 Office Professional 2010

当你将 Azure Rights Management 服务与 Office Professional Plus 2010 和 Service Pack 2 或 Office Professional 2010 Service Pack 2 配合使用时，必须也具有适用于 Windows 的 AIP 客户端。

此外，此配置：

- 在 Windows 10 上不支持。
- 不支持联合用户帐户基于表单的身份验证。 这些帐户必须使用 Windows 集成身份验证。
- 不支持使用通过 AIP 客户端选择的自定义权限替代模板保护。 在此方案中，必须首先删除原始保护才能应用自定义权限。

### <a name="mac-computers-for-information-rights-management-irm"></a>用于信息权限管理 (IRM) 的 Mac 计算机

以下 Office 客户端套件支持使用 Azure RMS 保护 macOS 上的文件和电子邮件：

- Microsoft 365 企业应用版
- Office Standard 2019 for Mac
- Office Standard 2016 for Mac

所有版本的 Office for Mac 2019 和 Office for Mac 2016 都支持使用受保护的内容。

> [!TIP]
> 如果在 Mac 计算机上使用经典客户端，你可能会发现以下常见问题解答非常有用：[如何配置 Mac 计算机以保护和跟踪文档？](faqs-classic.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)
> 
## <a name="azure-information-protection-apps-for-ios-and-android"></a>适用于 iOS 和 Android 的 Azure 信息保护应用

当 iOS 和 Android 移动设备没有能够打开受保护电子邮件的电子邮件应用时，适用于 iOS 和 Android 的 Azure 信息保护应用将为受权限保护的电子邮件（.rpmsg 文件）提供查看器。 通过此应用还可以打开受权限保护的 PDF 文件、图片和文本文件。

如果已通过 Microsoft Intune 注册 iOS 和 Android 设备，用户可以从公司门户安装应用，你可以使用 Intune 的[应用保护策略](/intune/apps/app-protection-policies)来管理应用。

有关如何使用应用的详细信息，请参阅[适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题解答](./rms-client/mobile-app-faq.md)。

## <a name="the-azure-information-protection-client-for-windows"></a>适用于 Windows 的 Azure 信息保护客户端

若要使用 Azure 信息保护，必须在整个系统中部署 AIP 客户端。 

从 [Microsoft Azure 信息保护页面](https://go.microsoft.com/fwlink/?LinkId=303970)下载统一标记客户端安装。 

有关详细信息，请参阅：

- [Azure 信息保护的客户端](rms-client/use-client.md)
- [统一标记客户端管理员指南](./rms-client/clientv2-admin-guide.md)
- [统一标记客户端用户指南](./rms-client/clientv2-user-guide.md)

### <a name="aips-classic-client"></a>AIP 经典客户端

如果你尚未升级，则可能仍会部署旧版 [Azure 信息保护经典客户端](./rms-client/aip-client.md)。

有关部署和使用经典客户端的详细信息，请参阅：

- [AIP 经典客户端](./rms-client/aip-client.md)
- [经典客户端管理员指南](./rms-client/client-admin-guide.md)
- [经典客户端用户指南](./rms-client/client-user-guide.md)。

> [!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 
>
> 在此时间框架内，所有当前 Azure 信息保护客户都可以转换到 Microsoft 信息保护统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>
> 
>

## <a name="rights-management-sharing-app"></a>权限管理共享应用

对于 Mac 计算机，Rights Management 共享应用提供了一个查看器，可查看受保护的 PDF 文件 (.ppdf)、受保护的文本图像和受常规保护的文件。 它也可保护图像文件，但不能保护其他文件。 若要保护这些计算机上的 Office 文件，请使用 Office for Mac 或 Microsoft 365 企业应用版。 

有关详细信息，请参阅 [适用于移动平台的 Microsoft Rights Management 共享应用程序的常见问题解答](/previous-versions/msdn10/dn451248(v=msdn.10))

从 [Microsoft Azure 信息保护页](https://go.microsoft.com/fwlink/?LinkId=303970)上下载适用于 Mac 计算机的 Rights Management 共享应用。

## <a name="other-applications-that-support-azure-information-protection"></a>其他支持 Azure 信息保护的应用程序

除了上面列出的应用程序，支持 Azure Rights Management 服务的 API 的任何应用程序都可与 Azure 信息保护集成。 

示例可能包括内部编写的业务线应用程序或软件供应商的应用程序（使用 RSM SDK 编写）。

## <a name="applications-that-are-not-supported-by-azure-rms"></a>不受 Azure RMS 支持的应用程序

Azure RMS 当前不支持的应用程序包括：

- Microsoft OneDrive for SharePoint Server 2013
- XPS 查看器
- 在早于 Windows 7 和 Service Pack 1 的 Windows 版本上运行的应用程序


## <a name="next-steps"></a>后续步骤

另请参阅：

- [Azure 信息保护的要求](requirements.md)。
- [应用程序如何支持 Azure Rights Management 服务](./applications-support.md)。
- [为 Azure Rights Management 配置应用程序](configure-applications.md)。

有关支持 Azure Rights Management 服务和 Azure 信息保护的解决方案的最新信息，请参阅博客文章 [Microsoft Ignite 2019 - Microsoft 信息保护解决方案合作伙伴生态系统展示](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Microsoft-Ignite-2019-Microsoft-Information-Protection-solutions/ba-p/967024)。