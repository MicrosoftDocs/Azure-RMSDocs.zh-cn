---
title: "Azure Rights Management 的要求 | Azure RMS"
description: "确定在组织中部署 Microsoft Azure Rights Management (Azure RMS) 的先决条件。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 81426cf43f31625c6e83d443fa925f6426eb89da
ms.openlocfilehash: 9bd75b44541f51b39315a898417ebe5d3b562cf9


---

# Azure 权限管理要求

>*适用于：Azure Rights Management、Office 365*


若要在你的组织中部署 Microsoft Azure Rights Management (Azure RMS)，请确保你具备以下先决条件。 然后，可以使用 [Azure Rights Management 部署路线图](../plan-design/deployment-roadmap.md)为你所在组织部署 Rights Management。

|要求|更多信息|
|---------------|--------------------|
|用于 RMS 的云订阅|你的组织必须具有支持 RMS 的云订阅。<br /><br />有关许可信息，请参阅 [支持 Azure RMS 的云订阅](requirements-subscriptions.md)。|
|Azure AD 目录|你的组织必须具有 Azure AD 目录，以支持 RMS 的用户身份验证。 此外，如果你希望使用本地目录 (AD DS) 中的用户帐户，则还必须配置目录集成。<br /><br />具有了所需客户端软件并正确配置了 MFA 支持基础结构后，Azure RMS 将支持多因素身份验证 (MFA)。<br /><br />有关详细信息，请参阅 [Azure AD 目录](requirements-azure-ad.md)。|
|客户端设备|用户必须拥有运行支持 RMS 的操作系统的客户端设备（计算机或移动设备）。<br /><br />有关详细信息，请参阅[支持 Azure RMS 的客户端设备](requirements-client-devices.md)。|
|应用程序|用户必须运行支持 RMS 的应用程序。<br /><br />有关详细信息，请参阅[支持 Azure RMS 的应用程序](requirements-applications.md)。|
|支持连接到 Internet 及所依赖的云服务的基础结构|如果你有必须配置为允许特定连接的防火墙或类似中介网络设备，请参阅以下 Office 文章的 [Office 365 portal and shared](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)（Office 365 门户和共享）部分的有关 **Azure 权限管理 (RMS)** 的信息：[《Office 365 URLs and IP address ranges》](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)（Office 365 URL 和 IP 地址范围）。<br /><br />使用此 Office 文章中的说明通过订阅 RSS 源来跟踪本信息的最新更改。<br /><br />除了 Office 文章中特定于 Azure RMS 的信息外：<br /><br />- 不要终止 TLS 客户端到服务连接（例如，为了执行数据包级别检查）。 这样做会中断 RMS 客户端用于 Microsoft 托管的 CA 以帮助确保其与 Azure RMS 的通信安全的证书锁定。<br /><br />- 如果你使用的 Web 代理要求身份验证，你必须将其配置为将集成 Windows 身份验证与用户的 Active Directory 登录凭据配合使用。|

如果你希望将 Azure RMS 用于本地服务器，则支持以下产品：

-   Exchange Server

-   SharePoint Server

-   支持文件分类基础结构的 Windows Server 文件服务器

有关此方案的其他 Azure RMS 要求的信息，请参阅[支持 Azure RMS 的本地服务器](requirements-servers.md)。

> [!IMPORTANT]
> 不支持以下部署方案：
> 
> -   在同一个组织中并行运行 AD RMS 和 Azure RMS，除非是在迁移过程中，如[从 AD RMS 迁移到 Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md) 所述。
> 
> 支持的迁移路径有：[从 AD RMS 到 Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) 以及从[ Azure RMS 到 AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx)。 如果你部署 Azure RMS，然后决定不再想要使用此云服务，请参阅[解除 Azure Rights Management 授权和停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)。






<!--HONumber=Aug16_HO4-->


