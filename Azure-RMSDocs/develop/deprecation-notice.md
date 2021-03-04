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
ms.openlocfilehash: dbf96e317f70e41e76223cf6512eaa32427ff4c9
ms.sourcegitcommit: 7420cf0200c90687996124424a254c289b11a26f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "101844296"
---
# <a name="rms-sdk-42-deprecation-notice"></a>RMS SDK 4.2 弃用通知 

*适用于4.2 年 3 2020 月之前的所有 RMS SDK 版本*

2020年3月3日，通过 Microsoft 下载中心发布了对适用于 Android、iOS 和 OSX 的 RMS SDK 4.2 的更新。 此更新对于目前使用这些 RMS SDK 平台的所有应用程序是必需的。  

截至2021年1月，年 3 2020 月之前发布的 RMS SDK 版本将无法连接到 Azure Rights Management 服务终结点。 尚未更新的应用程序将无法与 Azure Rights Management 服务建立 TLS 连接。 

## <a name="reason-for-change"></a>更改原因 

以前版本的 RMS SDK 使用证书固定来确保启用 RMS 的客户端与 RMS 服务进行通信，接收链接到特定的、预期的根 CA 的证书。  

新式浏览器使用证书透明度日志来验证是否已将证书颁发给合法的域所有者，以及这些证书是否由受信任的根证书颁发机构颁发。  

为了更好地支持新式浏览器，2020年12月1日，Microsoft 会将证书更新为 `https://api.aadrm.com` 由全局信任的根 CA 颁发的新证书，该证书将颁发的证书报告给新式浏览器信任的证书透明度日志。 完成此更改后，尝试对所需根证书执行证书固定的旧版本 RMS SDK 将无法找到该证书，因此将无法连接。  

## <a name="client-impact"></a>客户端影响 

以下 Microsoft 应用程序目前使用 RMS Sdk。 已对这些平台提供更新，设备应在12月截止时间之前更新。 

- 适用于 Mac 版本16.40 或更高版本的 Office Pro Plus/2019。
- 适用于 Mac 版本16.16.27 或更高版本的 Office 2016。
- 适用于 iOS 版本2.40.20071600 或更高版本的 Word、Excel 和 PowerPoint。
- 适用于 Android 版本16.0.12827.20140 或更高版本的 Word、Excel 和 PowerPoint。

资源 

- Android：https://www.microsoft.com/download/details.aspx?id=43673
- iOS：https://www.microsoft.com/download/details.aspx?id=43674 
- macOS：https://www.microsoft.com/download/details.aspx?id=43675 
- Linux：https://azuread.github.io/rms-sdk-for-cpp/annotated.html
