---
title: "Azure 信息保护 SDK 2.1 开发人员指南 | Microsoft Docs"
description: "使用 AIP SDK 2.1 进行开发的操作指南主题的集合"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: a6953bb33c5cff99b7ac034a035a85363c3b4065
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="developer-guidance"></a>开发人员指南

本部分介绍几个重要开发方案的特定指南，以及有关使用此 SDK 进行开发的常规信息。 本部分中的方案特定于此版本的 Rights Management Services SDK 2.1，在后续版本中可能会有所改动。
- [操作说明：使用 ADAL 身份验证](how-to-use-adal-authentication.md) - 使用 Azure Active Directory 身份验证库 (ADAL) 向 Azure RMS 验证应用身份。
- [操作说明：添加显式所有者权限](add-explicit-owner-rights.md) - 应用程序在从头开始创建许可证 ([IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)) 时，应显式添加“所有者”权限。
- [操作说明：调试启用权限的应用程序](debugging-applications-that-use-ad-rms.md) - 本主题演示如何调试应用程序和使用 Windows 事件日志。
- [如何：将应用部署到客户的租户中](how-to-deploy-app.md) - 概述将应用从其开发 Azure AD 租户部署到生产 Azure AD 租户的步骤。
- [操作说明：启用文档跟踪和撤销](tracking-content.md) - 本主题介绍用于实现文档内容跟踪和实现用于源数据更新和为应用创建**跟踪使用情况按钮**的示例代码的基本指导。
- [操作说明：启用电子邮件通知](how-to-enable-email-notification.md) - 电子邮件通知可以使受保护内容的所有者在其内容被访问时收到通知。
- [操作说明：使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md) - 本主题概述用于设置服务应用程序以使用 Azure Rights Management 的步骤。
- [操作说明：安装和配置 RMS 服务器](how-to-install-and-configure-an-rms-server.md) - 本主题介绍用于连接 RMS 服务器或 Azure RMS 以便测试启用权限的应用程序的步骤。
- [操作说明：设置 API 安全模式](setting-the-api-security-mode-api-mode.md) - 通过使用 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 函数，你可以选择文件 API 应用程序在哪种安全模式下运行。
- [操作说明：使用加密设置](working-with-encryption.md) - 本主题针对加密包，并显示其使用的一些代码片段。
- [应用程序类型](application-types.md) - 本主题介绍可以进行选择以作为启用权限形式而创建的应用程序类型。
- [文件 API 配置](file-api-configuration.md) - 可通过注册表中的设置来配置文件 API 的行为。
- [安全准则](security-guidelines.md) - 为应用程序开发人员提供方向和指导，使他们能在 AIP 生态系统中更好地工作。
- [支持的文件格式](supported-file-formats.md) - 文件 API 支持本机和 Pfile 格式
- [支持的平台](supported-platforms.md)：本主题标识 RMS SDK 2.1 支持的客户端和服务器平台。
- [了解使用限制](understanding-usage-restrictions.md) - 所有启用 RMS 的应用程序都必须强制实施由本主题中列出的常量所定义的使用限制。

 
## <a name="related-topics"></a>相关主题
* [概述](ad-rms-overview.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]