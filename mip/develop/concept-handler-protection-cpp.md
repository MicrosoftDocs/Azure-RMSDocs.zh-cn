---
title: 概念 - MIP SDK 中的保护处理程序。
description: 本文将帮助你了解如何创建保护 API 处理程序并将其用于调用操作。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 892e492351d3779667629ff4522891bb527fd782
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556157"
---
# <a name="microsoft-information-protection-sdk---protection-handler-concepts"></a>Microsoft 信息保护 SDK - 保护处理程序概念

在 MIP SDK 保护 API 中，`mip::ProtectionHandler` 公开了用于加密和解密受保护的流和缓冲区、执行访问检查、获取发布许可证以及从受保护信息中获取属性的功能。

## <a name="requirements"></a>惠?

创建 `ProtectionHandler` 用于处理特定文件需要使用以下对象：

- `mip::MipContext`
- `mip::ProtectionProfile`
- 已添加到 `ProtectionProfile` 的 `mip::ProtectionEngine`
- 继承 `mip::ProtectionHandler::Observer`的类。
- `mip::ProtectionDescriptor` 或发布许可证

## <a name="create-a-protection-handler"></a>创建保护处理程序

通过向两个 `ProtectionEngine` 函数中的一个提供 `ProtectionDescriptor` 或序列化发布许可证来构造 `mip::ProtectionHandler` 对象。 必须生成保护描述符以保护尚无发布许可证的明文信息。 解密已受保护的内容或保护已构建许可证的内容时，将使用发布许可证。 如果没有关联的发布许可证，则无法解密受保护的内容。

`mip::ProtectionEngine` 公开两个用于创建 `ProtectionHandler` 的函数。 参数是相同的，但作为第一个参数的处理程序或发布许可证除外。

- `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync`
  - 需要 `ProtectionDescriptor` 作为第一个参数。
- `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync`
  - 需要一个序列化的发布许可证，存储在 `std::vector<unint8_t>` 中作为第一个参数。

### <a name="create-from-descriptor"></a>从描述符创建

如果保护尚未受到保护的内容，或者对内容应用新保护（这意味着它已被解密），则必须构建 `mip::ProtectionDescriptor`。 构造后，会将其传递给 `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync()`，并通过 `mip::ProtectionHandler::Observer` 返回结果。

```cpp
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();
auto observer = std::make_shared<ProtectionHandlerObserverImpl>();

//Refer to ProtectionDescriptor docs for details on creating the descriptor
auto descriptor = CreateProtectionDescriptor(); //Stub function

mEngine->CreateProtectionHandlerFromDescriptorAsync(
    descriptor,
    mip::ProtectionHandlerCreationOptions::None,
    observer,
    handlerPromise);

auto handler = handlerFuture.get();
```

成功创建 `ProtectionHandler` 对象后，可以执行文件操作（获取/设置/删除/提交）。

### <a name="create-from-publishing-license"></a>从发布许可证创建

此示例假定已从某个源读取发布许可证并将其存储在 `std::vector<uint8_t> serializedPublishingLicense` 中。

```cpp

//TODO: Implement GetPublishingLicense()
//Snip implies that function reads PL from source file, database, stream, etc.
std::vector<uint8_t> serializedPublishingLicense = GetPublishingLicense(filePath);

auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();

shared_ptr<ProtectionHandlerObserverImpl> handleObserver =
    std::make_shared<ProtectionHandlerObserverImpl>();

mEngine->CreateProtectionHandlerFromPublishingLicenseAsync(
    serializedPublishingLicense,
    mip::ProtectionHandlerCreationOptions::None,
    handleObserver,
    handlerPromise);

auto handler = handlerFuture.get();
```

