---
title: 概念-MIP SDK-代理支持中的核心概念
description: 本文将帮助你了解 MIP SDK 中的代理支持。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/29/2020
ms.author: tommos
ms.openlocfilehash: fdbcf9d618612021a971af34380b65dc062c2802
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "95566096"
---
# <a name="microsoft-information-protection-sdk---proxy-support"></a>Microsoft 信息保护 SDK-代理支持

## <a name="proxies-and-the-mip-sdk"></a>代理和 MIP SDK

目前，在 MIP SDK 中，仅在 Windows 上支持非透明代理。

* **透明代理** 是指任何不需要客户端配置的代理类型，包括显式或 autodiscovered 设置。
* **经过身份验证的代理** 引用需要对调用方进行身份验证的任何类型的代理。
* **代理自动发现** 是指通过 web 代理自动发现 (WPAD) 找到的代理或设置。
* **显式代理** 指直接向操作系统或应用程序提供的代理。
  
| 平台        | 透明代理 | 经过身份验证的代理 | 代理自动发现 | 显式代理 |
| --------------- | ----------------- | --------------------- | -------------------- | -------------- |
| **Windows**     | 支持         | 不支持         | 支持            | 支持      |
| **Linux (所有)** | 支持         | 不支持         | 不支持        | 不支持  |
| ****       | 支持         | 不支持         | 不支持        | 不支持  |
| **Android**     | 支持         | 不支持         | 不支持        | 不支持  |
| **iOS**         | 支持         | 不支持         | 不支持        | 不支持  |

## <a name="proxies-on-windows"></a>Windows 上的代理

在 Windows 上运行的 MIP SDK 应用程序将使用 WinHTTP 来访问网络。 WinHTTP 配置设置独立于 Windows Internet (WinINet) Internet 浏览代理设置，只能通过使用以下发现方法来发现代理服务器：

* 自动发现方法：
  * 透明代理
  * Web 代理自动发现协议 (WPAD) 
* 手动静态代理配置：
  * 使用 netsh 命令配置的 WinHTTP

有关配置 WinHTTP 的详细信息，请参阅 [winhttp 文档](/windows/win32/winhttp/winhttp-start-page)。

## <a name="proxies-on-other-platforms"></a>其他平台上的代理

MIP SDK 不支持非 Windows 平台上的任何类型的所有透明代理。 如果需要此功能，请查看自定义 HTTP 委托和解决方法部分了解更多详细信息。

## <a name="custom-http-delegate"></a>自定义 HTTP 委托

Microsoft 信息保护 SDK 支持实现自定义 HTTP 委托，该委托可替代 SDK 的默认 HTTP 堆栈。 如果有功能不存在，或者需要特定的 HTTP 实现，则可以通过添加继承的新类来实现此委托 [`mip::HttpDelegate`](./reference/class_mip_httpdelegate.md) 。

此 `mip::HttpDelegate` 派生类通过以下方式设置 `mip::FileProfile::Settings` ：

```cpp
std::shared_ptr<MyHttpDelegate> httpDelegate = std::make_shared<MyHttpDelegate>();
            
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDisk,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());

profileSettings.SetHttpDelegate(httpDelegate);
```

## <a name="other-workarounds"></a>其他解决方法

当自定义 HTTP 委托不是一个选项时，将要求你绕过代理，并为 MIP 标签和保护终结点启用直接网络连接，并 Azure Active Directory。 如果需要 [审核日志记录](/azure/information-protection/reports-aip) ，则还需要审核日志记录终结点。

| 终结点           | 主机名                                                                                                                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 保护服务 | https://api.aadrm.com                                                                                                                                                   |
| 策略             | https:// \* . protection.outlook.com                                                                                                                                       |
| 审核日志      | https:// \* events.data.microsoft.com、https:// \* (仅)                                                                                           |
| 身份验证     | [查看 Azure AD 文档](/azure/active-directory/develop/authentication-national-cloud#azure-ad-authentication-endpoints) |