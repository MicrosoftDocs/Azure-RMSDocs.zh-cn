---
title: "Azure 信息保护的要求 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: aa4353e5-c5b0-47f6-a6f9-87d13e8f075f
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fe19726959bc16384120b610183c392031519813
ms.openlocfilehash: ff322e4ff0914ca29c7fe937a41936cb15d9a913


---

# Azure 信息保护的要求

>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

若要评估 Azure 信息保护的预览版本，请确保具备以下先决条件。 

|要求|更多信息|
|---------------|--------------------|
|包括 Azure RMS 的云订阅|你的组织必须具有支持 Rights Management 的云订阅。<br /><br />有关详细信息和免费试用版的链接，请参阅[《Cloud subscriptions that support Azure RMS》](../get-started/requirements-subscriptions.md)（支持 Azure RMS 的云订阅）。|
|Azure AD 目录|你的组织必须具有 Azure AD 目录，以支持 Azure RMS 和 Azure 信息保护的用户身份验证。 此外，如果你希望使用本地目录 (AD DS) 中的用户帐户，则还必须配置目录集成。<br /><br />具有了所需客户端软件并正确配置了 MFA 支持基础结构后，Azure RMS 将支持多因素身份验证 (MFA)。<br /><br />有关详细信息，请参阅[《Azure AD directory》](../get-started/requirements-azure-ad.md)（Azure AD 目录），其中的 Azure RMS 的信息也适用于 Azure 信息保护。|
|客户端设备|此预览版支持以下客户端设备：<br /><br />- Windows 10（x86、x64）<br /><br />- Windows 8.1（x86、x64）<br /><br />- Windows 8（x86、x64）<br /><br />- Windows 7 Service Pack 1（x86、x64）<br /><br />当你保护数据时，支持 Azure 权限管理的同一设备（Windows、Mac、iOS、Android）可以使用它。 有关这些设备和支持的版本的详细信息，请参阅[《Azure RMS requirements: Client devices that support Azure RMS》](../get-started/requirements-client-devices.md)（Azure RMS 要求：支持 Azure RMS 的客户端设备）。|
|应用程序|对于预览版和正式发布版 (GA)，Azure 信息保护支持对使用以下 Office 套件中的 **Word**、**Excel**、**PowerPoint** 和 **Outlook** 等 Office 应用创建的文件和电子邮件设置标签和进行保护：<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />在正式发布之后，在[企业移动性和安全性博客](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)上查找有关 Azure 信息保护何时支持其他文件类型（例如 PDF、音频、视频和图像文件）的公告。|
|支持连接到 Internet 及所依赖的云服务的基础结构|如果你有必须配置为允许特定连接的防火墙或类似中介网络设备，请参阅以下 Office 文章的 [Office 365 portal and shared](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)（Office 365 门户和共享）部分的有关 **Azure 权限管理 (RMS)** 的信息：[《Office 365 URLs and IP address ranges》](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)（Office 365 URL 和 IP 地址范围）。<br /><br />此外：<br /><br />- 允许 TCP 443 上的到 **rmsibizaapiprod.cloudapp.net** 的 HTTPS 通信。<br /><br />- 不要终止 TLS 客户端到服务连接（例如，为了执行数据包级别检查）。 <br /><br />- 如果你使用的 Web 代理要求身份验证，你必须将其配置为将集成 Windows 身份验证与用户的 Active Directory 登录凭据配合使用。|

## 后续步骤

如果满足这些要求，请尝试我们的自导式演示教程来亲自配置并体验 Azure 信息保护：[《Quick start tutorial for Azure Information Protection》](infoprotect-quick-start-tutorial.md)（Azure 信息保护的快速入门教程）。




<!--HONumber=Jul16_HO5-->


