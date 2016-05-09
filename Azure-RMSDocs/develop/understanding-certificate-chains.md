---
# required metadata

title: 了解证书链 | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 14694cb0-adc4-4c2f-aff5-22aa132777df

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# 了解证书链

开发启用权限的应用程序需要公钥对以及回溯到信任根处的 Microsoft 证书的证书链。

## 证书类型

每个 Rights Management Services (RMS) 环境中使用的许可证和证书包含回溯到 Microsoft 证书颁发机构 (CA) 证书的证书链。 Microsoft 提供了可以将许可证或证书嵌套在其中的两个链，即预生产证书链和生产链。 我们建议在开发应用程序时使用预生产层次结构，以便能够无需与 Microsoft 签订*生产许可协议*的情况下进行工作。 请注意，还必须为预生产配置 RMS 服务器。

必须在发布应用程序前切换到生产链。 预生产证书保护的内容的安全性要低于生产证书。

公钥和私钥以及预生产证书包含在位于 `%MsipcSDKDir%\Bin` 文件夹的以下文件中的 SDK 中。

- **ISVTier5AppSigningPrivKey.dat** 包含用于为在应用程序开发期间使用的清单签名的私钥。
- **ISVTier5AppSigningPubKey.dat** 包含登录到预生产证书层次结构中的公钥。
- **ISVTier5AppSignSDK_Client.xml** 包含用于生成在应用程序开发期间使用的清单的预生产证书。

 

使用证书和私钥来创建清单并对清单签名，该清单标识可以或必须加载到你的应用程序的进程空间中的文件以及禁止加载的文件。 之后平台将加载清单。

在应用程序开发期间无论是否已使用预生产证书，当准备好发布应用程序时，必须生成新密钥对、从 Microsoft 获取生产证书以及使用新的私钥和证书来创建应用程序清单并对其签名。

有关使用证书链和应用程序签名的详细信息，请参阅[切换到生产环境](switching-to-the-production-environment.md)。

### 相关主题

* [开发人员概念](ad-rms-concepts-nav.md)
* [切换到生产环境](switching-to-the-production-environment.md)
 

 


<!--HONumber=Apr16_HO3-->


