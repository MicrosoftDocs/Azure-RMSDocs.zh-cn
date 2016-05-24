---
# required metadata

title: 开发人员说明 | Azure RMS
description: 本主题涵盖了几个重要开发方案的具体指南。 
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 开发人员说明

本部分涵盖了几个重要开发方案的具体指南。 本部分中的方案特定于此版本的 Rights Management Services SDK 2.1，在后续版本中可能会有所改动。

- [添加明确的所有者权限](add-explicit-owner-rights.md) - 在从头开始创建许可证时，你的应用程序应显示添加“所有者”权限 ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch))。
- [常见的错误情形和解决方案](common-error-conditions-and-solutions.md) - 在使用 RMS SDK 2.1 开发人员工具时可能遇到的最常见的错误信息。
- [启用电子邮件通知](how-to-enable-email-notification.md) - 电子邮件通知可以使受保护内容的所有者在其内容被访问时收到通知。
- [文件 API 配置](file-api-configuration.md) - 可通过注册表中的设置来配置文件 API 的行为。
- [IPCHelloWorld - 示例应用程序](how-to-build-your-first-application.md) - 本主题包含创建启用权限的应用程序示例的说明。
- [设置 API 安全模式](setting-the-api-security-mode-api-mode.md) - 通过使用 [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 函数，你可以选择文件 API 应用程序在哪种安全模式下运行。
- [支持的文件格式](supported-file-formats.md) - 文件 API 支持本机和 Pfile 格式。
- [跟踪内容](tracking-content.md) - 本主题涵盖了用于实现跟踪受 RMS SDK 2.1 保护内容的文档的基本指南。
- [使用加密](working-with-encryption.md) - 本主题针对加密包，并显示其使用的一些代码片段。

 

## 相关主题 ##
* [概述](ad-rms-overview.md)
* [使用方法](how-to-use-msipc.md)
 

 


<!--HONumber=Apr16_HO4-->


