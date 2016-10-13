---
title: "开发人员指南和信息 | Azure RMS"
description: "本主题涵盖了几个重要开发方案的具体指南。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: d7e718c2e982702bef16c242370771d991b29db9


---

# 开发人员指南和信息

本部分介绍几个重要开发方案的特定指南，以及有关使用此 SDK 进行开发的常规信息。 本部分中的方案特定于此版本的 Rights Management Services SDK 2.1，在后续版本中可能会有所改动。
- [操作说明：使用 ADAL 身份验证](how-to-use-adal-authentication.md) - 使用 Azure Active Directory 身份验证库 (ADAL) 向 Azure RMS 验证应用身份。
- [操作说明：添加明确的所有者权限](add-explicit-owner-rights.md) - 应用程序在从头开始创建许可证 ([IpcCreateLicenseFromScratch](/information-protection/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)) 时，应显式添加&quot;所有者&quot;权限。
- [操作说明：调试启用权限的应用程序](debugging-applications-that-use-ad-rms.md) - 本主题演示如何调试应用程序和使用 Windows 事件日志。
- [操作说明：启用文档跟踪和撤销](tracking-content.md) - 本主题介绍用于实现文档内容跟踪和实现用于源数据更新和为应用创建**跟踪使用情况按钮**的示例代码的基本指导。
- [操作说明：启用电子邮件通知](how-to-enable-email-notification.md) - 电子邮件通知可以使受保护内容的所有者在其内容被访问时收到通知。
- [操作说明：使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md) - 本主题概述用于设置服务应用程序以使用 Azure Rights Management 的步骤。
- [操作说明：安装和配置 RMS 服务器](how-to-install-and-configure-an-rms-server.md) - 本主题介绍用于连接 RMS 服务器或 Azure RMS 以便测试启用权限的应用程序的步骤。
- [操作说明：设置 API 安全模式](setting-the-api-security-mode-api-mode.md) - 通过使用 [IpcSetGlobalProperty](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 函数，你可以选择文件 API 应用程序在哪种安全模式下运行。
- [操作说明：使用加密设置](working-with-encryption.md) - 本主题针对加密包，并显示其使用的一些代码片段。
- [应用程序类型](application-types.md) - 本主题介绍可以进行选择以作为启用权限形式而创建的应用程序类型。
- [文件 API 配置](file-api-configuration.md) - 可通过注册表中的设置来配置文件 API 的行为。
- [支持的文件格式](supported-file-formats.md) - 文件 API 支持本机和 Pfile 格式
- [支持的平台](supported-platforms.md)：本主题标识 RMS SDK 2.1 支持的客户端和服务器平台。
- [了解使用限制](understanding-usage-restrictions.md) - 所有启用 RMS 的应用程序都必须强制实施使用限制。
- [使用限制参考](usage-restriction-reference.md) - 使用限制由本主题中列出的常量定义。

 
## 相关主题 ##
* [概述](ad-rms-overview.md)
 

 



<!--HONumber=Oct16_HO1-->


