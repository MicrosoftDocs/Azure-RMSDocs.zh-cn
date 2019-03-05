---
title: 概念 - MIP SDK 中的文件 API 观察程序。
description: MIP SDK 几乎完全是异步的。 本文将帮助你了解如何针对异步操作实现和使用文件 API 观察程序。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: baa62e34e10de3fb4cacc3eb7cb21c0b3e2ebf75
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329948"
---
# <a name="microsoft-information-protection-sdk---file-api-observers"></a>Microsoft 信息保护 SDK - 文件 API 观察程序

文件 API 包含两个观察程序类。 观察程序成员是虚拟的，可重写以处理事件回叫。

- [`mip::FileProfile::Observer`](reference/class_mip_fileprofile_observer.md)
- [`mip::FileHandler::Observer`](reference/class_mip_filehandler_observer.md)

异步操作完成后，将调用与结果对应的 `OnXxx()` 成员函数。 示例包括 `mip::FileProfile::Observer` 的 `OnLoadSuccess()`、`OnLoadFailure()` 和 `OnAddEngineSuccess()`。

下面的示例演示了 SDK 样例所使用的 promise/future 模式，可扩展该模式以实现所需的回叫行为。 

## <a name="file-profile-observer-implementation"></a>文件配置文件观察程序实现

在以下示例中，我们创建了一个派生自 `mip::FileProfile::Observer` 的 `ProfileObserver` 类。 已重写成员函数以使用整个示例中使用的 future/promise 模式。

**请注意**:以下示例仅部分实现，但不包括替代`mip::FileEngine`相关观察者。

### <a name="profileobserverh"></a>profile_observer.h

在标头中，定义派生自 `mip::FileProfile::Observer` 的 `ProfileObserver`，然后替代每个成员函数。

```cpp
class ProfileObserver final : public mip::FileProfile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement mip::FileEngine related observers.
};
```

### <a name="profileobservercpp"></a>profile_observer.cpp

在实现中，我们定义了要为每个观察程序成员函数采取的操作。

每个成员都接受两个参数。 第一个是指向我们在函数中处理的类的共享指针。 `ProfileObserver::OnLoadSuccess` 预计会收到 `mip::FileProfile`。 `ProfileObserver::OnAddEngineSuccess` 预计会收到 `mip::FileEngine`。

第二个是指向*上下文*的共享指针。 在实现中，上下文是对 `std::promise` 的引用，通过引用作为 `std::shared_ptr<void>` 传递。 函数的第一行将其强制转换为 `std::promise`，然后存储在名为 `promise` 的对象中。

最后，通过设置 `promise->set_value()` 并传入 `mip::FileProfile` 对象，future 模式即准备就绪。

```cpp
#include "profile_observer.h"
#include <future>

//Called when FileProfile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = 
  std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when FileProfile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement mip::FileEngine related observers.
```

当实例化任何 SDK 类或使用执行异步操作的函数时，将观察程序实现传递给设置构造函数或异步函数本身。 当实例化 `mip::FileProfile::Settings` 对象时，构造函数接受 `mip::FileProfile::Observer` 作为参数之一。 以下示例展示了在 `mip::FileProfile::Settings` 构造函数中使用的自定义 `ProfileObserver`。

## <a name="filehandler-observer-implementation"></a>FileHandler 观察程序实现

与配置文件观察程序类似，`mip::FileHandler` 实现 `mip::FileHandler::Observers` 类，用于在文件操作期间处理异步事件通知。 该实现类似于上面详述的实现。 `FileHandlerObserver` 的部分定义如下。 

### <a name="filehandlerobserverh"></a>file_handler_observer.h

```cpp
#include "mip/file/file_handler.h"

class FileHandlerObserver final : public mip::FileHandler::Observer {
public:
  void OnCreateFileHandlerSuccess(
      const std::shared_ptr<mip::FileHandler>& fileHandler,
      const std::shared_ptr<void>& context) override;

  void OnCreateFileHandlerFailure(
      const std::exception_ptr& error,
      const std::shared_ptr<void>& context) override;

  //TODO: override remaining member functions inherited from mip::FileHandler::Observer
};
```

### <a name="filehandlerobservercpp"></a>file_handler_observer.cpp

此示例只是前两个函数，但其​​余函数使用与这些函数以及 `ProfileObserver` 类似的模式。

```cpp
#include "file_handler_observer.h"

void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_value(fileHandler);
}

void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_exception(error);
}

//TODO: override remaining member functions inherited from mip::FileHandler::Observer
```

