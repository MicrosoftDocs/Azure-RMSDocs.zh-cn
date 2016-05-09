---
# required metadata

title: 条款 | Azure RMS
description: 特定于 Rights Management Services 的术语定义的集合。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6f53c7e5-bbe2-4619-83b0-cdc620b3af14

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 条款

特定于 Rights Management Services 的术语定义的集合。

**弃用的算法**  
实现较旧的内容保护方案的模式设置，特指电子食谱密码模式 (ECB)。 在此 SDK 中，设置使你可以生成与 [AD Rights Management Services SDK](https://msdn.microsoft.com/en-us/library/windows/desktop/cc530379.aspx) 所使用的 MSDRM 库相兼容的许可证。

此设置可能会导致你的应用程序以不符合你客户的内容保护标准的方式来保护内容。

此设置将阻止应用程序从任何添加到 Microsoft Rights Management SDK 3.0 或更高版本的加密增强功能获益。

**Microsoft 受保护的文件格式**

也称为 PFile 格式，它是支持 RMS 的应用程序中用于 AD RMS 和函数的标准默认文件格式。

PFile 格式对于应用程序开发人员是透明的，因为它是按设计 Microsoft Rights Management SDK 4.2 的方式嵌入的。

 

 





<!--HONumber=Apr16_HO3-->


