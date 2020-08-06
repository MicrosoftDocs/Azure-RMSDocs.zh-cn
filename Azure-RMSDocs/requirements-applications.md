---
title: 适用于 Azure 信息保护的 RMS 数据保护的应用程序支持
description: 确定对 Azure Rights Management (Azure RMS) 服务的本机支持的应用程序和解决方案。 Azure RMS 为 Azure 信息保护提供数据保护 (AIP) 。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 37cb3b1f3c3eb60459cabe813f0cb00fb69b7d5b
ms.sourcegitcommit: dec5df81b569283a72f0a983d3f53b82cbbc562c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2020
ms.locfileid: "87802158"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的应用程序

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

此页上列出的应用程序和解决方案对 Azure Rights Management (提供对 Azure 信息保护的数据保护的 Azure) Azure RMS 的本机支持。

这些应用程序和解决方案称为 "enlighted"，并使用 Rights Management Api 紧密集成 Rights Management 和[使用限制](configure-usage-rights.md)。

> [!NOTE]
> 除非另行说明，否则支持的功能同时适用于 Azure RMS 和 AD RMS。 
>
> IOS、Android、macOS 和 Windows Phone 8.1 上的 AD RMS 支持还需要[Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))。
> 

## <a name="windows-rms-enlightened-applications"></a>Windows RMS-启用应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - [Office 365 应用](#office-365-app-support) <br />- Office 2010 <br />-Office 2013<br />- Office 2016 <br />-Office 2019 <br />- [Office for web (查看受保护的文档) ](#viewing-protected-documents-in-office-for-the-web)<br />- [Web 浏览器](#web-browser-support)        |
|[**电子邮件**](#viewing-protected-content-in-email-clients)      |   -Outlook 2010<br />-Outlook 2013<br />-Outlook 2016 <br />-Outlook 2019 <br />-Office 365 ProPlus 中的 Outlook<br />- [Web 浏览器](#web-browser-support)<br />- [Windows Mail](#email-clients-using-exchange-activesync-irm)|
|[**其他文件类型**](#supported-text-and-image-file-types)    |  -Office 365 应用、Office 2019 和 Office 2016： **. .vsdm、** **.vsdx、** **. .vssm**、 **.vstm**、 **.vssx**、 **.vstx** <br />-适用于 Windows 的 Azure 信息保护客户端：文本、图像、 **.pfile** <br />-用于 AutoCAD 的 SealPath RMS 插件： **。 dwg**       |
| | |

## <a name="macos-rms-enlightened-applications"></a>macOS RMS-启用应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    |  -Office 365 应用<br />-Office 2019 for Mac<br />-Office 2016 for Mac<br />- [适用于 web 的 Office](#viewing-protected-documents-in-office-for-the-web)<br />- [Web 浏览器](#web-browser-support)    |
|[**电子邮件**](#viewing-protected-content-in-email-clients)   |   -适用于 Mac 的 Outlook 2019<br />-适用于 Mac 的 Outlook 2016<br />- [Web 浏览器](#web-browser-support)     |
|[**其他文件类型**](#supported-text-and-image-file-types)    | RMS 共享应用（查看受保护的文本、图像、常规受保护的文件）   |
| | |

## <a name="android-rms-enlightened-applications"></a>Android RMS-启用应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    |-适用于 Android 的 GigaTrust 应用<br />- [适用于 web 的 Office](#viewing-protected-documents-in-office-for-the-web)<br />-Office Mobile (，除非使用敏感度标签，仅限于查看和编辑受保护的文档)  <br />- [Web 浏览器](#web-browser-support)      |
|[**电子邮件**](#viewing-protected-content-in-email-clients)     | - [9Folders](#email-clients-using-exchange-activesync-irm)<br />-Azure 信息保护应用 (查看受保护的电子邮件) <br />-BlackBerry 工作 <br />- [适用于 Android 的 GigaTrust 应用](#email-clients-using-exchange-activesync-irm) <br />-Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [适用于 Android 的 Outlook](#email-clients-using-exchange-activesync-irm)<br />- [Samsung Email (S3 及更高版本) ](#email-clients-using-exchange-activesync-irm)<br />-移动的 TITUS 分类 <br /><br />- [Web 浏览器](#web-browser-support)       |
|[**其他文件类型**](#supported-text-and-image-file-types)    |  Azure 信息保护应用（查看受保护的文本和图像）  |
| | |


## <a name="ios-rms-enlightened-applications"></a>iOS RMS-启用应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    |  -GigaTrust<br />-Office Mobile <br />- [适用于 web 的 Office](#viewing-protected-documents-in-office-for-the-web)<br />-TITUS 文档<br />- [Web 浏览器](#web-browser-support)    |
|[**电子邮件**](#viewing-protected-content-in-email-clients)     |   -Azure 信息保护应用 (查看受保护的电子邮件) <br />-BlackBerry 工作<br />-Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [适用于 iPad 和 iPhone 的 Outlook](#email-clients-using-exchange-activesync-irm)<br />-TITUS Mail <br />- [Web 浏览器](#web-browser-support)     |
|[**其他文件类型**](#supported-text-and-image-file-types)     | -Azure 信息保护应用 (查看保护文本和图像) <br />-TITUS 文档： **.pfile**  |
| | |

## <a name="windows-10-mobile-rms-enlightened-applications"></a>Windows 10 移动版 RMS-启用应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    | -Office 移动应用 (使用 Azure RMS) 查看受保护的文档 <br />- [Web 浏览器](#web-browser-support)    |
|[**电子邮件**](#viewing-protected-content-in-email-clients)    |  -Citrix WorxMail <br />-Outlook Mail (查看受保护的电子邮件)  <br />- [Web 浏览器](#web-browser-support)     |
|[**其他文件类型**](#supported-text-and-image-file-types)    | 不支持   |
| | |

## <a name="blackberry-10-rms-enlightened-applications"></a>Blackberry 10 RMS-启用应用程序

|类型  |支持的应用程序   |
|---------|---------|
|**Word、Excel、PowerPoint**    | - [Web 浏览器](#web-browser-support)    |
|[**电子邮件**](#viewing-protected-content-in-email-clients)   | - [Blackberry 电子邮件](#email-clients-using-exchange-activesync-irm) <br />- [Web 浏览器](#web-browser-support)      |
|[**其他文件类型**](#supported-text-and-image-file-types)    | 不支持   |
| | |


## <a name="additional-details-about-rms-enlightened-applications"></a>有关 RMS 启用应用程序的其他详细信息

有关上面列出的启用应用程序表的详细信息，请参阅：

- [查看电子邮件客户端中的受保护内容](#viewing-protected-content-in-email-clients)
- [支持的文本和图像文件类型](#supported-text-and-image-file-types)
- [Office 365 应用支持](#office-365-app-support)
- [在 Office for web 中查看受保护的文档](#viewing-protected-documents-in-office-for-the-web)
- [Web 浏览器支持](#web-browser-support)
- [使用 Exchange ActiveSync 信息 Rights Management (IRM) 的电子邮件客户端](#email-clients-using-exchange-activesync-irm)

### <a name="viewing-protected-content-in-email-clients"></a>查看电子邮件客户端中的受保护内容

电子邮件客户端保护邮件时，附加到邮件并当前未受保护的任何 Office 文件将与电子邮件一起受到保护。 在这种情况下，电子邮件和附件只能由授权收件人在电子邮件客户端中查看。

但是，如果只有附件受到保护，而不是电子邮件本身，电子邮件客户端将无法预览附件，即使是由授权的收件人。

> [!TIP]
> 对于不支持保护电子邮件的电子邮件客户端，请考虑使用 [Exchange Online 邮件流规则来应用此保护](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)。

### <a name="supported-text-and-image-file-types"></a>支持的文本和图像文件类型

Office 文件和电子邮件消息以外的文件类型包括文本和图像文件类型，扩展名为 **.txt、** **.xml、** **.jpg**和**jpeg。** 

这些文件在由 Rights Management 本地保护后会更改其文件扩展名，然后变为只读。 

如果文件受到 Rights Management 的常规保护，则无法以本机方式保护的文件具有 .pfile 文件扩展名 **。**

有关详细信息，请参阅[支持的文件类型](./rms-client/client-admin-guide-file-types.md)。

### <a name="office-365-app-support"></a>Office 365 应用支持

包括： 
- Office 应用最小版本1805，从 Office 365 Business 或 Microsoft 365 商业版生成9330.2078。 仅在向用户分配 Azure Rights Management 的许可证时才受支持 (也称为 Azure 信息保护 "Office 365) "。
- Office 365 ProPlus 应用。

### <a name="viewing-protected-documents-in-office-for-the-web"></a>在 Office for web 中查看受保护的文档

仅在 Microsoft SharePoint 和 OneDrive 中受支持，并且在将文档上传到受保护的库之前不会对其进行保护。

### <a name="web-browser-support"></a>Web 浏览器支持

- 当使用[带有新功能的 office 365 消息加密](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)保护[office 附件](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)时， **Word、Excel 和 PowerPoint**文件支持 Web 浏览器。

- 对于**电子邮件，** 仅在以下情况下支持 web 浏览器：

    - 如果发送方和接收方都属于同一组织
    - 如果发件人或收件人正在使用 Exchange Online
    - 如果发送方在混合配置中使用本地 Exchange， 

### <a name="email-clients-using-exchange-activesync-irm"></a>使用 Exchange ActiveSync IRM 的电子邮件客户端

下面的电子邮件客户端使用 Exchange ActiveSync IRM，它必须由 Exchange 管理员启用：

- Windows Mail
- 9Folders
- 适用于 Android 的 GigaTrust 应用
- NitroDesk
- 适用于 Android 的 Outlook
- Samsung Email（S3 及更高版本）
- iPad 和 iPhone 版 Outlook
- Blackberry 电子邮件

用户可以查看、答复和回复受保护的电子邮件，但无法保护新的电子邮件。
 
如果电子邮件应用程序因 Exchange ActiveSync IRM 未启用而无法呈现邮件，当发件人使用混合配置中的 Exchange Online 或本地 Exchange 时，收件人可以在 Web 浏览器中查看电子邮件。 

## <a name="azure-rms-support-for-office"></a>Office Azure RMS 支持

Azure RMS 已紧密集成到 Word、Excel、PowerPoint 和 Outlook 应用中，在这些应用中，此功能通常称为信息权限管理 (IRM)。 

- [用于信息权限管理 (IRM) 的 Windows 计算机](#windows-computers-for-information-rights-management-irm)
- [用于信息权限管理 (IRM) 的 Mac 计算机](#mac-computers-for-information-rights-management-irm)

另请参阅：[Office 应用程序服务说明](https://technet.microsoft.com/library/office-applications-service-description.aspx)

### <a name="windows-computers-for-information-rights-management-irm"></a>用于信息权限管理 (IRM) 的 Windows 计算机

以下 Office 客户端套件支持使用 Azure Rights Management 服务保护 Windows 计算机上的文件和电子邮件：

- **Office 应用最小版本1805，在向用户分配 azure Rights Management 许可证时，从 office 365 Business 或 Microsoft 365 商业版生成 9330.2078**)  (也称为 azure 信息365保护

- **Office 365 ProPlus**

    包含 Azure 信息保护数据保护的大多数 Office 365 订阅（并非所有）都附带这些版本的 Office。 检查你的订阅信息，确定是否包含 Office 365 专业增强版。 你还可以在 [Azure 信息保护数据表](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)中找到此信息。

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013**

- **带有 Service Pack 2 的 Office Professional Plus 2010**

所有版本的 Office（不包括 Office 2007）都支持使用受保护的内容。

#### <a name="azure-rights-management-service-with-office-professional-plus-2010-and-service-pack-2-or-office-professional-2010-with-service-pack-2"></a>Azure Rights Management 服务，其中包含 Office Professional Plus 2010 和 Service Pack 2 或带有 Service Pack 2 的 Office Professional 2010

将 Azure Rights Management 服务与 Office Professional Plus 2010 和 Service Pack 2 或 Office Professional 2010 service Pack 2 一起使用时，你还必须具有适用于 Windows 的 AIP 客户端。

此外，此配置：

- 在 Windows 10 上不受支持。
- 不支持联合用户帐户基于表单的身份验证。 这些帐户必须使用 Windows 集成的身份验证。
- 不支持使用通过 AIP 客户端选择的自定义权限替代模板保护的功能。 在此方案中，必须首先删除原始保护才能应用自定义权限。

### <a name="mac-computers-for-information-rights-management-irm"></a>用于信息权限管理 (IRM) 的 Mac 计算机

以下 Office 客户端套件支持使用 Azure RMS 保护 macOS 上的文件和电子邮件：

- Office 365 ProPlus
- Office Standard 2019 for Mac
- Office Standard 2016 for Mac

所有版本的 Office for Mac 2019 和 Office for Mac 2016 都支持使用受保护的内容。

> [!TIP]
> 若要开始使用 Office for Mac 保护文档，你可能会发现以下常见问题很有用：[如何实现配置 Mac 计算机以保护和跟踪文档？](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)
> 
## <a name="azure-information-protection-apps-for-ios-and-android"></a>适用于 iOS 和 Android 的 Azure 信息保护应用

适用于 iOS 和 Android 的 Azure 信息保护应用会在这些移动设备没有可打开受保护电子邮件的电子邮件应用时，为受权限保护的电子邮件 ( 提供查看器) **。** 通过此应用还可以打开受权限保护的 PDF 文件、图片和文本文件。

如果已通过 Microsoft Intune 注册 iOS 和 Android 设备，用户可以从公司门户安装应用，你可以使用 Intune 的[应用保护策略](/intune/app-protection-policies)来管理应用。

有关如何使用应用的详细信息，请参阅[适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题解答](./rms-client/mobile-app-faq.md)。

## <a name="the-azure-information-protection-client-for-windows"></a>适用于 Windows 的 Azure 信息保护客户端

Azure 信息保护 (AIP) 客户端包括两个版本，每个版本有管理员和用户指南：

- **统一标签客户端**：
    - [管理员指南](./rms-client/clientv2-admin-guide.md)
    - [用户指南](./rms-client/clientv2-user-guide.md)

- **经典客户端**：
    - [管理员指南](./rms-client/client-admin-guide.md)
    - [用户指南](./rms-client/client-user-guide.md)

从 " [Microsoft Azure 信息保护" 页](https://go.microsoft.com/fwlink/?LinkId=303970)下载相关应用。

> [!NOTE]
> 不确定这两个版本之间的差异吗？ 请参阅相关[常见问题解答](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。
> 
## <a name="rights-management-sharing-app"></a>权限管理共享应用

对于 Mac 计算机，Rights Management 共享应用为受保护的 PDF 文件提供了一个查看器** () 、** 受保护的文本图像以及一般受保护的文件。 它也可保护图像文件，但不能保护其他文件。 若要保护这些计算机上的 Office 文件，请使用 Office for Mac 或 Office 365 专业增强版。 

有关详细信息，请参阅适用[于移动平台的 Microsoft Rights Management 共享应用程序的常见问题](https://technet.microsoft.com/dn451248)

从 " [Microsoft Azure 信息保护" 页](https://go.microsoft.com/fwlink/?LinkId=303970)下载适用于 Mac 计算机的 Rights Management 共享应用。

## <a name="other-applications-that-support-azure-information-protection"></a>支持 Azure 信息保护的其他应用程序

除了上面列出的应用程序，支持 Azure Rights Management 服务 Api 的任何应用程序都可与 Azure 信息保护集成。 

示例可能包括内部编写的业务线应用程序或软件供应商的应用程序（使用 RSM Sdk 编写）。

有关详细信息，请参阅 [Azure 信息保护开发人员指南](./develop/developers-guide.md)。

## <a name="applications-that-are-not-supported-by-azure-rms"></a>不受 Azure RMS 支持的应用程序

Azure RMS 当前不支持的应用程序包括：

- Microsoft OneDrive for SharePoint Server 2013
- XPS 查看器
- Windows 7 之前的 Windows 版本上运行的应用程序，Service Pack 1


## <a name="next-steps"></a>后续步骤

另请参阅：

- [Azure 信息保护的要求](requirements.md)。
- [应用程序如何支持 Azure Rights Management 服务](./applications-support.md)。
- [配置 Azure Rights Management 的应用程序](configure-applications.md)。

有关支持 Azure Rights Management 服务和 Azure 信息保护的解决方案的最新信息，请参阅博客文章[Microsoft Ignite 2019 – Microsoft Information Protection 解决方案合作伙伴生态系统展示](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Microsoft-Ignite-2019-Microsoft-Information-Protection-solutions/ba-p/967024)。
