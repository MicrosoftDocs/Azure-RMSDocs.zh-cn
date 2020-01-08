---
title: 概念 - MIP SDK 中的策略 API 观察程序。
description: MIP SDK 几乎完全是异步的。 本文将帮助你了解如何针对异步操作实现和使用策略 API 观察程序。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: db2926809ccd7d29628a2b729ce59879e6e513fd
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555885"
---
# <a name="microsoft-information-protection-sdk---policy-api-observers"></a>Microsoft 信息保护 SDK - 策略 API 观察程序

策略 API SDK 包含一个观察程序类。 观察程序成员是虚拟的，应被覆盖以处理对异步操作的回叫。

- [`mip::PolicyProfile::Observer`](reference/class_mip_policyprofile_observer.md)

异步操作完成后，将调用与结果对应的 `OnXxx()` 成员函数。 示例包括 `mip::Profile::Observer` 的 `OnLoadSuccess()`、`OnLoadFailure()` 和 `OnAddEngineSuccess()`。

下面的示例演示了 SDK 样例所使用的 promise/future 模式，可扩展该模式以实现所需的回叫行为。 

## <a name="profile-observer-implementation"></a>配置文件观察程序实现

在以下示例中，我们创建了一个派生自 `mip::Profile::Observer` 的 `ProfileObserver` 类。 已重写成员函数以使用整个示例中使用的 future/promise 模式。

**注意**：以下示例仅部分实现，不包括 `mip::ProfileEngine` 相关观察程序的替代。

### <a name="profile_observerh"></a>profile_observer.h

在标头中，定义派生自 `mip::Profile::Observer` 的 `ProfileObserver`，然后替代每个成员函数。

```cpp
class ProfileObserver final : public mip::Profile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement remaining members
};
```

### <a name="profile_observercpp"></a>profile_observer.cpp

在实现中，我们定义了要为每个观察程序成员函数采取的操作。

每个成员都接受两个参数。 第一个是指向函数处理的类的共享指针。 `ProfileObserver::OnLoadSuccess` 预计会收到 `mip::Profile`。 `ProfileObserver::OnAddEngineSuccess` 预计会收到 `mip::ProfileEngine`。

第二个是指向*上下文*的共享指针。 在实现中，上下文是对 `std::promise` 的引用，作为 `shared_ptr<void>` 传入。 函数的第一行将其强制转换为 `std::promise`，然后存储在名为 `promise` 的对象中。

最后，通过设置 `promise->set_value()` 并传入 `mip::Profile` 对象，future 模式即准备就绪。

```cpp
#include "profile_observer.h"
#include <future>

//Called when Profile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when Profile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement remaining observer members
```

执行任何异步操作时，观察程序实现将传递给 settings 构造函数或异步函数本身。 

