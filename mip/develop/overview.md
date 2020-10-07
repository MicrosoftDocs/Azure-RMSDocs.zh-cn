---
title: 概述 - Microsoft 信息保护 SDK。
description: Microsoft 信息保护 (MIP) 将 Microsoft 的分类、标记和保护服务统一到一个管理体验和软件开发工具包 (SDK) 中。
author: msmbaldwin
ms.service: information-protection
ms.topic: overview
ms.date: 01/18/2019
ms.author: mbaldwin
ms.openlocfilehash: 32f2895d8b52a5fd63d5c764eebb78736b1917a9
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91588319"
---
# <a name="overview"></a>概述

## <a name="microsoft-information-protection"></a>Microsoft 信息保护

Microsoft 信息保护 (MIP) 统一了 Microsoft 的分类、标记与保护服务：

- 它跨 Microsoft 365、Azure 信息保护、Windows 信息保护和其他 Microsoft 服务提供统一管理。 
- 第三方可以通过 MIP SDK 使用标准一致的数据标记架构和保护服务与应用程序集成。

* [什么是 Office 365 安全与合规中心？](/office365/securitycompliance/)
* [什么是 Azure 信息保护？](/azure/information-protection/understand-explore/what-is-information-protection)
* [如何使用 Azure 信息保护进行保护？](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="microsoft-information-protection-sdk"></a>Microsoft 信息保护 SDK

MIP SDK 将 Office 365 安全与合规中心的标记和保护服务公开给第三方应用程序和服务。 开发人员可以使用 SDK 生成本机支持，以便为文件应用标签和保护。 开发人员可以推断在检测到特定标签时应执行哪些操作，并推断 MIP 加密信息。 

应用于 Microsoft 服务套件中的信息的标签和保护是**一致**的。 一致性允许支持 MIP 的应用程序和服务以可预测的通用方式读取和写入标签。

高级 MIP SDK 用例包括：

* 向正在导出的文件应用分类标签的业务线应用程序。
* CAD/CAM 设计应用程序为 Microsoft 信息保护标记提供本机支持。
* 云访问安全代理或数据丢失防护解决方案推断使用 Azure 信息保护加密的数据。

有关更详尽的列表，请查看 [API 概念](concept-apis-use-cases.md)。

以下平台支持 MIP SDK：

[!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

## <a name="next-steps"></a>后续步骤

现在你已准备好开始使用该 SDK。 首先需要[完成 MIP SDK 安装和配置步骤](setup-configure-mip.md)。 这些步骤可确保正确设置 Microsoft 365 订阅和客户端计算机。