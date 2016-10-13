---
title: "Windows 和移动平台的 RMS 共享应用程序 | Azure 信息保护"
description: "RMS 共享应用程序如何作为支持 Office 2010 所必需的免费可下载应用程序来支持 Azure RMS，但我们也建议将其用于 Windows 计算机、Mac 计算机和移动设备。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1da6e372-2b3f-4af7-80f7-6b9073dff7f5
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 55fd22b60ad87dadce0ffb89bb658e949670f728
ms.openlocfilehash: e4b9a13ba29820cd7a19e0b8509966f5d8195353


---


# Windows 和移动平台的 RMS 共享应用程序

>*适用于：Azure 信息保护、Office 365*

RMS 共享应用程序是支持 Office 2010 所必需的免费可下载应用程序，但我们也建议将其用于 Windows 计算机、Mac 计算机和移动设备。 它的一大优点是能够为无法以本机方式支持 Azure Rights Management 服务的应用程序和文件提供通用保护，这意味着所有文件都能得到保护。 有关不同保护级别的详细信息，请参阅 [Rights Management 共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)中的[保护级别 – 本机和常规](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)部分。

当用户通过使用 RMS 共享应用程序保护其文件时，他们还可以跟踪他们保护的文档，如有必要，撤消对这些文档的访问权限。 他们通过使用 [文档跟踪站点](http://go.microsoft.com/fwlink/?LinkId=529562)来执行此操作。

对于 Windows 计算机，RMS 共享应用程序可与用户已在使用的应用程序轻松集成，并且增强这些应用程序的功能：

-   安装 Word、Excel、PowerPoint 和 Outlook 的 Office 加载项。 这样可在功能区上为用户提供“共享保护项”按钮，该按钮可以调用一个易于使用的对话框，其中包含用于保护要通过电子邮件发送的文件的最常用设置。 此按钮还提供了用于访问文档跟踪站点的快捷方式。

-   文件资源管理器的全新右键单击选项。 它可在功能区上为用户提供“就地保护”选项，该选项可以调用一个易于使用的对话框，其中包含用于保护存储在磁盘上的文件的最常用设置。

-   用于打开受 Azure Rights Management 服务保护的文件的查看器。 当没有其他已安装的应用程序可以打开受保护文件时，将自动调用此查看器。

-   Office 2010 的后端配置，让此套件的 Word、Excel、PowerPoint 和 Outlook 能够与 Azure Rights Management 服务无缝集成。

虽然可通过使用 [Microsoft Rights Management 页](http://go.microsoft.com/fwlink/?LinkId=303970)为单台计算机下载和安装适用于 Windows 的 RMS 共享应用程序，但它也支持企业部署的静默安装和自定义配置。 有关详细信息，请参阅下列资源：

-   [保护级别 – 本机和常规](../rms-client/sharing-app-admin-guide.md)

-   [权限管理共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)

适用于移动设备的 RMS 共享应用程序支持最常用的移动设备，例如 iPad 和 iPhone、Android、Windows Phone 和 Windows RT。 用户可以从相关应用商店下载此应用， [Microsoft 权限管理页](http://go.microsoft.com/fwlink/?LinkId=303970)提供这些应用商店的链接。

**如果你有 Microsoft Intune**：因为 RMS 共享应用包括了 Microsoft Intune 应用软件开发工具包，所以你可以使用以下选项：

-   为通过 Intune 注册的 iOS 和 Android 设备部署和管理该应用。

-   管理未通过 Intune 注册的 Android 设备的应用。


## 后续步骤
若要查看其他应用程序和服务如何支持 Azure 信息保护中的 Azure Rights Management 服务，请参阅[应用程序如何支持 Azure Rights Management 服务](applications-support.md)。




<!--HONumber=Sep16_HO4-->


