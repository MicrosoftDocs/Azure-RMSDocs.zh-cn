---
title: "条款 | Azure RMS"
description: "特定于 Rights Management Services 的术语定义的集合。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 99390fb78a9da3bef8a67c8595770a84fb9bb89a
ms.openlocfilehash: a32bfc59dd72efbcb239845ddabfa9bd3a969127


---

# 条款

特定于 Rights Management Services 的术语定义的集合。

**弃用的算法**  
实现较旧内容保护方案的模式设置，特指电子密码本密码模式 (ECB)。 在此 SDK 中，该设置使你可以生成与 [AD Rights Management Services SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx) 所使用的 MSDRM 库相兼容的许可证。

此设置可能会导致你的应用程序以不符合你客户的内容保护标准的方式来保护内容。

此设置将阻止应用程序从任何添加到 Microsoft Rights Management SDK 3.0 或更高版本的加密增强功能获益。

**Microsoft 受保护的文件格式**

也称为 PFile 格式，它是支持 RMS 的应用程序中用于 AD RMS 和函数的标准默认文件格式。

PFile 格式对于应用程序开发人员是透明的，因为它是按设计 Microsoft Rights Management SDK 4.2 的方式嵌入的。

 

 






<!--HONumber=Sep16_HO1-->


