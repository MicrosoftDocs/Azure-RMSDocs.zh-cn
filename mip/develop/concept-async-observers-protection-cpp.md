---
title: 概念 - MIP SDK 中的保护 API 观察程序。
description: MIP SDK 几乎完全是异步的。 本文将帮助你了解如何针对异步操作实现和使用保护 API 观察程序。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 559e6088edc4bab51867ac379451ae3feef5acd6
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555919"
---
# <a name="microsoft-information-protection-sdk---protection-api-observers"></a>Microsoft 信息保护 SDK - 保护 API 观察程序

保护 API 包含三个观察程序类。 观察程序成员是虚拟的，可重写以处理异步操作的回叫。

- [保护配置文件：`mip::ProtectionProfile::Observer`](reference/class_mip_ProtectionProfile_observer.md)
- [保护引擎：`mip::ProtectionEngine::Observer`](reference/class_mip_ProtectionEngine_observer.md)
- [保护处理程序：`mip::ProtectionHandler::Observer`](reference/class_mip_Protectionhandler_observer.md)

异步操作完成后，将调用与结果对应的 `OnXxx()` 成员函数。 示例包括 `mip::ProtectionProfile::Observer` 的 `OnLoadSuccess()`、`OnLoadFailure()` 和 `OnAddEngineSuccess()`。

下面的示例演示了 SDK 样例所使用的 promise/future 模式，可扩展该模式以实现所需的回叫行为。 

## <a name="protectionprofile-observer-implementation"></a>ProtectionProfile 观察程序实现

在以下示例中，我们创建了一个派生自 `mip::ProtectionProfile::Observer` 的 `ProtectionProfileObserverImpl` 类。 已重写成员函数以使用整个示例中使用的 promise/future 模式。

### <a name="protectionprofileobserverimpl-class-declaration"></a>ProtectionProfileObserverImpl 类声明

在标头中，定义派生自 `mip::ProtectionProfile::Observer` 的 `ProtectionProfileObserverImpl`，然后替代每个成员函数。

```cpp
//ProtectionProfileObserverImpl.h
class ProtectionProfileObserverImpl final : public mip::ProtectionProfile::Observer {
public:
  ProtectionProfileObserverImpl() { }
  void OnLoadSuccess(const shared_ptr<mip::ProtectionProfile>& profile, const shared_ptr<void>& context) override;
  void OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) override;
  void OnAddEngineSuccess(const shared_ptr<mip::ProtectionEngine>& engine, const shared_ptr<void>& context) override;
  void OnAddEngineError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionprofileobserverimpl-implementation"></a>ProtectionProfileObserverImpl 实现

在实现中，我们定义了要为每个观察程序成员函数采取的操作。

每个成员都接受两个参数。 第一个是指向我们在函数中处理的类的共享指针。 `ProtectionObserver::OnLoadSuccess` 预计会收到 `mip::ProtectionProtection`，`ProtectionObserver::OnAddEngineSuccess` 预计会收到 `mip::ProtectionEngine`。

第二个是指向*上下文*的共享指针。 在实现中，上下文是对 `std::promise` 的引用，作为 `shared_ptr<void>` 传入。 函数的第一行将其强制转换为 `std::promise`，然后存储在名为 `promise` 的对象中。

最后，通过设置 `promise->set_value()` 并传入 `mip::ProtectionProtection` 对象，future 模式即准备就绪。

```cpp
//protection_observers.cpp

void ProtectionProfileObserverImpl::OnLoadSuccess(
  const shared_ptr<mip::ProtectionProfile>& profile,
  const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_value(profile);
};

void ProtectionProfileObserverImpl::OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_exception(error);
};

void ProtectionProfileObserverImpl::OnAddEngineSuccess(
  const shared_ptr<mip::ProtectionEngine>& engine,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_value(engine);
};

void ProtectionProfileObserverImpl::OnAddEngineError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_exception(error);
};
```

当实例化任何 SDK 类或使用执行异步操作的函数时，将观察程序实现传递给设置构造函数或异步函数本身。 当实例化 `mip::ProtectionProfile::Settings` 对象时，构造函数接受 `mip::ProtectionProfile::Observer` 作为参数之一。 以下示例展示了在 `mip::ProtectionProfile::Settings` 构造函数中使用的自定义 `ProtectionProfileObserverImpl`。

## <a name="protectionhandler-observer-implementation"></a>ProtectionHandler 观察程序实现

与保护观察程序类似，`mip::ProtectionHandler` 实现 `mip::ProtectionHandler::Observer` 类，用于在保护操作期间处理异步事件通知。 该实现类似于上面详述的实现。 `ProtectionHandlerObserverImpl` 的部分定义如下。 完整的实现可在我们的 [GitHub 示例存储库](https://azure.microsoft.com/resources/samples/?sort=0&term=mip+sdk)中找到。

### <a name="protectionhandlerobserverimpl-class-declaration"></a>ProtectionHandlerObserverImpl 类声明

```cpp
//protection_observers.h

class ProtectionHandlerObserverImpl final : public mip::ProtectionHandler::Observer {
public:
  ProtectionHandlerObserverImpl() { }
  void OnCreateProtectionHandlerSuccess(const shared_ptr<mip::ProtectionHandler>& protectionHandler, const shared_ptr<void>& context) override;
  void OnCreateProtectionHandlerError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionhandlerobserverimpl-partial-implementation"></a>ProtectionHandlerObserverImpl 部分实现

此示例只是前两个函数，但其​​余函数使用与这些函数以及 `ProtectionObserver` 类似的模式。

```cpp
//protection_observers.cpp

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerSuccess(
  const shared_ptr<mip::ProtectionHandler>& protectionHandler,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_value(protectionHandler);
};

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_exception(error);
};
```

