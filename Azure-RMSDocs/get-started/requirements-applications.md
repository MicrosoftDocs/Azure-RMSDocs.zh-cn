---
title: "Azure RMS 要求&#58;应用程序 | Azure RMS"
description: "使用下表确定以本机方式支持 Azure RMS 的应用程序，这意味着 RMS 通过使用 RMS API 紧密集成到这些应用程序中以支持使用限制。 这些应用程序也称为“启用 RMS 型”应用程序。"
author: cabailey
manager: mbaldwin
ms.date: 08/19/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: d3408f954381978287852dd74a38c5903f583dda


---


# Azure RMS 要求：应用程序

>*适用于：Azure Rights Management、Office 365*


使用下表确定以本机方式支持 Azure RMS 的应用程序，这意味着 RMS 通过使用 RMS API 紧密集成到这些应用程序中以支持使用限制。 这些应用程序也称为“启用 RMS 型”应用程序。

除非另行说明，否则支持的功能同时适用于 Azure RMS 和 AD RMS。 此外，iOS、Android、OS X 和 Windows Phone 8.1 上的 AD RMS 支持需要 [Active Directory Rights Management 服务移动设备扩展](https://technet.microsoft.com/library/dn673574.aspx)。

有关表列的信息：

-   **受保护的 PDF**：使用 RMS 共享应用程序通过电子邮件共享 Office 文件和 PDF 文件时自动创建的具有 .ppdf 文件扩展名的文件。 RMS 共享应用程序包括用于受保护的 PDF 文件的阅读器。 以前，如果你创建的 PDF 文件是使用 Azure RMS 或 AD RMS 进行保护，则你可以继续使用 Foxit Reader 和 Nitro Pro 在 Windows、iOS 和 Android 设备上阅读这些文件。

-   **电子邮件：**所列电子邮件客户端可以保护电子邮件本身，而电子邮件则会自动保护任何附加的文件。 在这种情况下，客户端的预览功能可以向授权收件人显示受保护的内容（邮件和附件）。 但是，如果未保护电子邮件本身，而保护了附件，则客户端的预览功能将无法向授权收件人显示受保护的附件。

-   **其他文件类型**：文本和图像文件包括文件扩展名为 .txt、.xml、.jpg 和 .jpeg 之类的文件。 这些文件在接受 RMS 提供的本机保护以后，会更改其文件扩展名，变为只读文件。 不能进行本机保护的文件在接受 RMS 提供的常规保护以后，其文件扩展名为 .pfile。 有关详细信息，请参阅 [Rights Management 共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)。


|**设备操作系统**|Word、Excel、PowerPoint|受保护的 PDF|Email|其他文件类型|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office Mobile 应用程序（仅适用于 Azure RMS）[[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho 文档<br /><br />适用于 Adobe 的 GigaTrust 桌面 PDF 客户端<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />RMS 共享应用程序|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|适用于 Windows 的 RMS 共享应用程序：文本、图像、pfile<br /><br />Siemens JT2Go：JT 文件（仅适用于 Windows 10）|
|**iOS**|iPad 和 iPhone 版 Office [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS 文档|Foxit Reader<br /><br />RMS 共享应用程序 [[1]](#footnote-1)<br /><br />TITUS 文档|Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />iPad 和 iPhone 版 Outlook [[4]](#footnote-4)<br /><br />OWA for iOS [[3]](#footnote-3)<br /><br />TITUS Mail|RMS 共享应用程序 [[1]](#footnote-1)：文本、图像、pfile<br /><br />TITUS 文档：Pfile|
|**Android**|适用于 Android 的 GigaTrust 应用<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile（仅适用于 Azure RMS）[[1]](#footnote-1)|适用于 Android 的 GigaTrust 应用<br /><br />Foxit Reader<br /><br />RMS 共享应用程序 [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />适用于 Android 的 GigaTrust 应用程序 [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for Android [[4]](#footnote-4)<br /><br />OWA for Android [[3]](#footnote-3) 和 [[7]](#footnote-7)<br /><br />Samsung Email（S3 及更高版本）[[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|RMS 共享应用程序 [[1]](#footnote-1)：文本、图像、pfile|
|**OS X**|Office 2011（仅适用于 AD RMS）<br /><br />Office 2016 for Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />RMS 共享应用程序 [[1]](#footnote-1)|Outlook 2011（仅适用于 AD RMS）<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共享应用程序 [[1]](#footnote-1)：文本、图像、pfile|
|**Windows 10 移动版**|Office Mobile 应用程序（仅适用于 Azure RMS）[[1]](#footnote-1)|不支持|Citrix WorxMail [[6]](#footnote-6)<br /><br />Outlook Mail|不支持|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|不支持|Outlook 2013 RT<br /><br />Windows 相关邮件应用程序<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go：JT 文件|
|**Windows Phone 8.1**|Office Mobile（仅适用于 AD RMS）|RMS 共享应用程序 [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|RMS 共享应用程序 [[1]](#footnote-1)：文本、图像、pfile|
|**Blackberry 10**|不支持|不支持|Blackberry 电子邮件 [[4]](#footnote-4)|不支持|


###### 脚注 1
支持查看受保护内容。

###### 脚注 2 
支持查看 SharePoint Online、OneDrive for Business 和 Outlook Web Access 中的受保护内容。

###### 脚注 3
如果收件人在本地 Exchange 中有邮箱，并且收到受保护的电子邮件，则只能在功能丰富的电子邮件客户端（如 Outlook）中打开此内容。  不能从 Outlook Web Access 打开此内容。

###### 脚注 4
使用 Exchange ActiveSync IRM，它必须由 Exchange 管理员启用。 用户可以查看受保护电子邮件并回复所有受保护电子邮件，但是他们自己不能保护新的电子邮件。

如果收件人在本地 Exchange 中有邮箱，并且收到其他组织中使用 Exchange 的用户发来的受保护电子邮件，则只能在功能丰富的电子邮件客户端（如 Outlook）中打开此内容。  不能从使用 Exchange Active Sync IRM 的设备打开此内容。

###### 脚注 5
支持查看和编辑受保护文档。 有关详细信息，请参阅 Office 博客上的以下帖子：[为 iPad 和 iPhone 版 Office 提供 Azure Rights Management 支持](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

###### 脚注 6
有关详细信息，请参阅 Citrix [product documentation for WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html)（Worxmail 的产品文档）。

###### 脚注 7
有关详细信息，请参阅 Office 博客上的以下帖子：[OWA for Android 现可在特定设备上使用](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## 有关针对 Office 的 Azure RMS 支持的详细信息

Azure RMS 已紧密集成到 Word、Excel、PowerPoint 和 Outlook 应用中，在这些应用中，此功能通常称为信息权限管理 (IRM)。 以下 Office 客户端版本支持通过 Azure RMS 保护文件和电子邮件：

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

所有版本的 Office（不包括 Office 2007）都支持使用受保护的内容。

带 Office Professional Plus 2010 或 Office Professional 2010 的 Azure RMS：

- 需要适用于 Windows 的 Rights Management 共享应用程序

- 在 Windows 10 上不受支持


## 有关 Rights Management 共享应用程序的详细信息

有关适用于 Windows 的权限管理共享应用程序的详细信息，请参阅以下资源：

-   [权限管理共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)

-   [权限管理共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)

有关适用于移动平台的权限管理共享应用程序的详细信息，请参阅以下资源：

-   使用 [Microsoft Rights Management 页](http://go.microsoft.com/fwlink/?LinkId=303970)上的链接下载相关应用程序

-   如果你有 Microsoft Intune，则可以通过使用策略托管应用来部署和管理应用程序： 

    -   对于由 Intune 注册的 iOS 和 Android 设备：[在 Microsoft Intune 控制台中配置和部署移动应用程序管理策略](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)

    -   对于不是由 Intune 注册的 Android 设备：[使用 Microsoft Intune 控制台创建和部署移动应用程序管理策略](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune)

-   [适用于移动平台的 Microsoft 权限管理共享应用程序的常见问题](https://technet.microsoft.com/dn451248)



## 有关其他支持 Azure RMS 的应用程序的详细信息

除了表中的应用程序，任何支持 RMS API 的应用程序都可以与 Azure RMS 集成，包括：

- 使用 RMS SDK 内部编写的业务线应用程序

- 来自软件供应商、使用 RMS SDK 编写的应用程序。

有关 SDK 的详细信息，请参阅 [Microsoft Rights Management SDK](../develop/developers-guide.md)。

## 不受 Azure RMS 支持的应用程序

Azure RMS 当前不支持以下应用程序：

-   Microsoft Office for Mac 2011

-   Microsoft OneDrive for Business for SharePoint Server 2013

-   XPS 查看器
 
此外，RMS 共享应用程序具有以下限制：

-   对于 Windows 计算机：要求最低版本为 Windows 7 Service Pack 1



## 后续步骤
若要查看其他要求，请参阅 [Azure Rights Management 的要求](requirements-azure-rms.md)。

有关最常用的应用程序如何支持 Azure RMS 的详细信息，请参阅[应用程序如何支持 Azure Rights Management](../understand-explore/applications-support.md)。

有关如何为 Azure RMS 配置最常用的应用程序的信息，请参阅[为 Azure Rights Management 配置应用程序](../deploy-use/configure-applications.md)。


<!--HONumber=Aug16_HO4-->


