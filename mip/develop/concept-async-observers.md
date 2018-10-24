---
title: 概念 - MIP SDK 中的观察程序。
description: MIP SDK 几乎完全是异步的。 本文将帮助你了解如何针对异步操作实现和使用观察程序。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 99f68383a4e697f4f8f04c19523ccb0fb50fa3c0
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445543"
---
# <a name="microsoft-information-protection-sdk---observer-concepts"></a>Microsoft 信息保护 SDK - 观察程序概念

MIP SDK 几乎完全是异步的。 例如，导致网络或文件 IO 的任何操作都是异步执行的。 为了处理这些异步事件的事件通知，SDK 使用[观察程序模式](https://wikipedia.org/wiki/Observer_pattern)。 

## <a name="implementation-overview"></a>实现概述

构造将执行异步操作的对象时，必须实现 `Observer` 类。 观察程序将收到与 MIP SDK 中的各种异步操作相关的通知事件，并将结果提供给调用方。

每个 `Observer` 类中的函数都是虚拟的，并且会针对首选异步模式进行重写。 SDK 通过 `std::promise` 和 `std::future` 实现事件通知观察程序模式。

每个特定于类的观察程序都包含一组用于异步操作结果的 success 和 error/failure 函数。 *Success* 函数返回与操作关联的对象。 *Error*/*Failure* 函数返回一个异常，其中包含操作失败的详细原因。

例如，`FileProfile` 支持以下两项操作： 

- 它可以通过 `FileProfile::AddEngineAsync` 向配置文件添加新引擎。 
- 它可以通过 `FileProfile::UnloadEngineAsync` 从配置文件中卸载引擎。

由于每个异步操作实现两个 `Observer` 函数，因此可以假设有**四个** `Observer` 方法与 `FileProfile` 相关联： 

- `FileProfileObserver::OnAddEngineSuccess()`
- `FileProfileObserver::OnAddEngineError()`
- `FileProfileObserver::OnUnloadEngineSuccess`
- `FileProfileObserver::OnUnloadEngineError()`。 

## <a name="mip-sdk-observer-classes"></a>MIP SDK 观察程序类

MIP SDK 文件 API 包含两个观察程序：

* `mip::FileProfile::Observer`
* `mip::FileHandler::Observer`

MIP SDK 策略 API 只有一个观察程序：

* `mip::Profile::Observer`

MIP SDK 保护 API 具有三个观察程序：

* `mip::ProtectionProfile::Observer`
* `mip::ProtectionEngine::Observer`
* `mip::ProtectionHandler::Observer`

## <a name="next-steps"></a>后续步骤

详细了解如何通过各种 API 实现和使用观察程序：

* [文件 API 观察程序 (C++)](concept-async-observers-file-cpp.md)
* [策略 API 观察程序 (C++)](concept-async-observers-policy-cpp.md)
* [保护 API 观察程序 (C++)](concept-async-observers-protection-cpp.md)
