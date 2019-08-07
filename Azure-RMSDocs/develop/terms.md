---
title: AIP 开发人员术语 | Microsoft Docs
description: 特定于 Rights Management Services 的开发人员术语定义的集合。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 01/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 87aa190a87426e61d919b8781444239c4ce5d3c7
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68790764"
---
# <a name="terms"></a>条款

特定于 Azure 信息保护的开发人员术语定义的集合。

**弃用的算法**  
实现较旧内容保护方案的模式设置，特指电子密码本密码模式 (ECB)。 在此 SDK 中，该设置使你可以生成与 [AD Rights Management Services SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx) 所使用的 MSDRM 库相兼容的许可证。

此设置可能会导致你的应用程序以不符合你客户的内容保护标准的方式来保护内容。

此设置将阻止应用程序从任何添加到 Microsoft Rights Management SDK 3.0 或更高版本的加密增强功能获益。

**Microsoft 受保护的文件格式**

也称为 PFile 格式，它是支持 RMS 的应用程序中用于 AD RMS 和函数的标准默认文件格式。

PFile 格式对于应用程序开发人员是透明的，因为它是按设计 Microsoft Rights Management SDK 4.2 的方式嵌入的。

