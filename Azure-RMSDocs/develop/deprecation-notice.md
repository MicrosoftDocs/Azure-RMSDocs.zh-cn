---
title: RMS SDK 4.2 弃用通知
description: RMS SDK 4.2 弃用通知
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
ms.date: 03/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 7a590457f04daf57bd8143883a6a29c9dd0e7219
ms.sourcegitcommit: e36c2dba68caac6e3d2b094bd38a67758665ca76
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2020
ms.locfileid: "78934433"
---
# <a name="rms-sdk-42-deprecation-notice"></a>RMS SDK 4.2 弃用通知 

*适用于4.2 年 3 2020 月之前的所有 RMS SDK 版本*

2020年3月3日，通过 Microsoft 下载中心发布了对适用于 Android、iOS 和 OSX 的 RMS SDK 4.2 的更新。 此更新对于目前使用这些 RMS SDK 平台的所有应用程序是必需的。  

2020年3月15日星期二，2020之前发布的 RMS SDK 版本将无法连接到 Azure Rights Management 服务终结点。 使用 RMS SDK 4.2 的应用程序必须在此日期之前更新。 

## <a name="reason-for-change"></a>更改原因 

以前版本的 RMS SDK 使用证书固定来确保启用 RMS 的客户端与 RMS 服务进行通信，接收链接到特定的、预期的根 CA 的证书。  

新式浏览器使用证书透明度日志来验证是否已将证书颁发给合法的域所有者，以及这些证书是否由受信任的根证书颁发机构颁发。  

为了更好地支持新式浏览器，2020年9月15日，Microsoft 将 https://api.aadrm.com 的证书更新到由全局信任的根 CA 颁发的新证书，该证书将颁发的证书报告给新式浏览器信任的证书透明度日志。 完成此更改后，尝试对所需根证书执行证书固定的旧版本 RMS SDK 将无法找到该证书，因此将无法连接。  

## <a name="client-impact"></a>客户端影响 

以下 Microsoft 应用程序目前使用 RMS Sdk。 将对这些平台提供更新，并且应在9月截止时间之前更新设备。 

- Office 2019 for Mac 
- Office 2016 for Mac 
- 适用于 iOS 的 Word、Excel 和 PowerPoint 
- 适用于 Android 的 Word、Excel 和 PowerPoint 

资源 

- Android： https://www.microsoft.com/en-us/download/details.aspx?id=43673
- iOS： https://www.microsoft.com/en-us/download/details.aspx?id=43674 
- MacOS： https://www.microsoft.com/en-us/download/details.aspx?id=43675 
- Linux： https://azuread.github.io/rms-sdk-for-cpp/annotated.html