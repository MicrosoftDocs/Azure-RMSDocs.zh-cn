---
title: 概念-MIP SDK 中的核心概念-MipContext
description: 本文将帮助你了解称为 MipContext 的核心 SDK 概念，这些概念将驱动应用程序初始化。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 97b6720a4501ab389099b7c2d49fa7cfbf81e00b
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555664"
---
# <a name="microsoft-information-protection-sdk---mipcontext-object-concepts"></a>Microsoft 信息保护 SDK-MipContext 对象概念

## <a name="mipcontext"></a>MipContext

`MipContext` 是 SDK 中最高级别的对象。 它负责管理可作为应用程序或服务的一部分创建的所有配置文件的状态。 此外，在销毁 MipContext 对象后，它将处理释放 MIP SDK 资源。

具体而言，`MipContext` 设置以下各项：

- 跨 SDK `mip::ApplicationInfo`，用于应用程序 ID、版本和应用程序名称。
- 应存储 MIP 状态信息的路径（如果已启用）。
- 日志记录级别。
- 自定义记录器委托（如果需要）。
- 遥测配置重写。
- 启用 SDK 中位于功能标志后面的预览功能。

创建 `mip::MipContext` 的对象后，可以使用 `MipContext` 对象创建 `mip::FileProfile` 对象（或 `PolicyProfile`/`ProtectionProfile`）。

### <a name="mipcontext-functions"></a>MipContext 函数

`mip::MipContext` 公开了三个用于创建和销毁 `MipContext` 对象的重要静态函数。

#### `mip::MipContext::Create()`

创建要在初始化配置文件时使用的新的 MipContext 实例。 此函数接受：

- `mip::ApplicationInfo`
- MIP 存储缓存的路径。
- `mip::LogLevel`
- （可选）`mip::LoggerDelegate`
- （可选）`mip::TelemetryConfiguration`

#### `mip::MipContext::CreateWithCustomFeatureSettings()`

创建一个新的 MipContext 实例，以便在初始化配置文件时使用，并启用自定义功能设置。

- `mip::ApplicationInfo`
- MIP 存储缓存的路径。
- `mip::LogLevel`
- （可选）`mip::LoggerDelegate`
- （可选）`mip::TelemetryConfiguration`
- `mip::FlightingFeature`

#### `mip::mipContext::Shutdown()`

释放所有 MIP 资源。 在应用程序关闭之前应调用。 销毁 `MipContext` 对象时，`MipContext` 析构函数也会调用此。

## <a name="next-steps"></a>后续步骤

- 接下来，详细了解[身份验证概念](concept-authentication-cpp.md)和[观察程序](concept-async-observers.md)。 MIP 提供可扩展的身份验证模型，而观察程序用于为异步事件提供事件通知。 两者都必不可少，适用于所有 MIP API 集。
- 然后学习文件 API、策略 API 和保护 API 的配置文件和引擎概念
  - [文件 API 配置文件概念](concept-profile-engine-file-profile-cpp.md)
  - [文件 API 引擎概念](concept-profile-engine-file-engine-cpp.md)
  - [策略 API 配置文件概念](concept-profile-engine-file-profile-cpp.md)
  - [策略 API 引擎概念](concept-profile-engine-file-engine-cpp.md)
  - [保护 API 配置文件概念](concept-profile-engine-file-profile-cpp.md)
  - [保护 API 引擎概念](concept-profile-engine-file-engine-cpp.md)
