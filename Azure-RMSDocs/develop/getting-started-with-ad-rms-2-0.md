---
title: "入门 | Azure RMS"
description: "借助 RMS SDK 2.1 平台，开发人员可构建利用 RMS 信息保护的应用程序。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 728113C9-FCF9-4280-BE1D-6AF5C15E449E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 2987c6a8c93ee586ac2f1a05918212f95e67fe3c
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="getting-started"></a>开始使用

Rights Management Services SDK 2.1 平台使开发人员可以通过 RMS 服务器或 Azure RMS 构建利用 RMS 信息保护的应用程序。 该平台可处理复杂的安全实践（如密钥管理、加密和解密处理），并提供简化 API 以便轻松开发应用程序。

## <a name="get-started-with-rms-sdk-21"></a>RMS SDK 2.1 入门

本主题将指导你完成设置过程以及在测试环境中运行启用权限的应用程序的过程。 以下主题讨论如何设置开发环境，其列出方式表示执行任务时可以使用的建议顺序。

## <a name="in-this-sections"></a>本部分内容

| 主题 | 描述 |
|-------|-------------|
| [发行说明](release-notes-rtm.md) | 本主题包含有关此版本和以前版本的 RMS SDK 2.1 的重要信息。|
| [安装 SDK](install-the-rms-sdk.md) | 本主题指导你完成安装开发人员工具的过程。|
| [配置 Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md) | 本主题包含有关如何配置 Visual Studio 项目以使用 RMS SDK 2.1 的说明。|
| [开发应用程序](developing-your-application.md) | 本主题包含启用了 RMS 的应用程序的核心层面的基本指南，可作为应用程序开发的基础。|
| [测试应用程序](how-to-set-up-your-test-environment.md) |本主题包含有关如何为应用程序测试进行设置的说明。|
| [部署到生产](deploying-your-application.md) |本主题将引导你完成启用权限的应用程序的部署选项。|


遵循以下这些主题中的指导原则来尝试使用 RMS SDK 2.1：

- [安装 SDK](install-the-rms-sdk.md)
- [配置 Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)
- [开发应用程序](developing-your-application.md)
- [测试应用程序](how-to-set-up-your-test-environment.md)
- [部署到生产](deploying-your-application.md)

### <a name="why-use-rms-sdk-21-for-protecting-your-content"></a>为什么使用 RMS SDK 2.1 保护你的内容

对于要向其新的和现有应用程序添加 RMS 支持的开发人员，RMS SDK 2.1 可帮助使以下工作更容易：

-   创建可管理、符合标准且强健的感知 RMS 的应用程序。
-   持久加密用户数据。 数据保持加密状态，不考虑环境、设备或操作系统。
-   强制实施一组丰富的使用限制，如阻止对敏感数据的屏幕捕获。
-   支持企业管理的保护策略。
-   随着新身份验证机制和加密算法可用而支持它们。

RMS SDK 2.1 支持一系列重要的客户端和服务器平台。 有关详细信息，请参阅 [支持的平台](supported-platforms.md)。

## <a name="core-principles"></a>核心原则

**简单易用**— 有关 AD RMS SDK 1.0 的反馈和使用模式进行了分析，该数据过去常常用于简化或自动处理最困难的编程任务。 使用 RMS SDK 2.1 创作的 RMS 应用程序需要的 RMS 代码通常比使用 AD RMS SDK 1.0 编写的 RMS 应用程序少 5–10 倍。
**编写一次**— RMS SDK 2.1 应用程序不需要代码更改或重新编译即可使用最新 RMS 功能。 新 RMS 功能会随着添加到 RMS 服务器，而在现有应用程序中可用。
**一致性**— RMS SDK 2.1 可帮助轻松地编写以一致方式采用不同 RMS 配置的应用程序。 它还显著降低了你作为应用程序开发人员而需要创作的 RMS 用户界面量，从而鼓励采用一致的外观并减少用户培训需求。

## <a name="related-topics"></a>相关主题

* [RMS 开发人员指南](developers-guide.md)
* [AD RMS 开发人员活动角](http://blogs.msdn.com/b/rms/)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]