---
# required metadata

title: 此 SDK 好在何处 | Azure RMS
description: 本主题介绍 RMS SDK 2.1 相对于原始 Active Directory Rights Management Services SDK 的重大进步。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 622D5C6E-07D5-4C71-A99D-9823C1FE6936
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 此 SDK 内容不是最新的。 在短时间内，请在 MSDN 上找到[最新版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)的文档。 **
# 此 SDK 好在何处
本主题介绍 Rights Management Services SDK 2.1 相对于原始 [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379) 在创建启用了权限的应用程序所需的开发人员工作量方面的重大进步。

**API 图面** - 通过抽象显著减少了 API 图面，将你从后端实现的很多细节中解放出来。 在 RMS SDK 的 84 个函数的 API 图面中，RMS SDK 2.1 只包括 20 个 API 函数。 大多数应用程序将仅需使用此 API 图面的一小部分。

**加速时间** - 使用 RMS SDK 2.1，你将能够按照分步指南确定应用程序的哪些资源是敏感的以及如何保护它们。 这与 RMS SDK不同，使用它你需要具有证书、格式和拓扑的详细知识，并为多线程处理编写复杂代码。

**多拓扑支持** - RMS SDK 2.1 有助于最大程度减少代码重写；你的应用程序应与所有拓扑配合使用，因为我们简化了开发人员面临的拓扑复杂性。 使用 RMS SDK，你需要了解所有受支持的拓扑，然后为每一个拓扑编写并测试特定的代码。

**不会过时** - RMS SDK 2.1 可帮助你最大程度减少重写启用了权限的代码；你的应用程序应在任何 RMS 环境中运行并在发布更新的核心 RMS 功能后自动利用新功能。 这与 AD RMS SDK 不同，在 AD RMS SDK 中，你需要更新应用程序以显式利用任何新功能。

**重要声明**  
MSDN 库中的所有原始 [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379) 相关主题现在以以下支持语句开头：

AD RMS SDK 利用客户端在 Msdrm.dll 中公开的功能，可用于 Windows Server 2008、Windows Vista、Windows Server 2008 R2、Windows 7、Windows Server 2012 和 Windows 8。 它可能在后续版本中变更或不可用。 请改用 [Active Directory Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md)（它利用客户端在 *Msipc.dll* 中公开的功能）。

 

## 相关主题 ##
* [概述](ad-rms-overview.md)
* [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379)
* [Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md)
 

 


<!--HONumber=Jun16_HO1-->


