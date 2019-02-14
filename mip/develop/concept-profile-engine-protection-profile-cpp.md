---
title: 概念 - 保护 API 配置文件对象
description: 本文将帮助你了解在应用程序初始化期间创建的保护配置文件对象的概念。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3fa8a7b9f787cef980722efa5036de5c3f583b35
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251698"
---
# <a name="microsoft-information-protection-sdk---protection-api-profile-concepts"></a>Microsoft 信息保护 SDK - 保护 API 配置文件概念

下面的两个示例展示如何使用本地存储作为状态存储来创建 profileSettings 对象，以及仅在内存中创建该对象。 两者都假设已经创建了 `authDelegateImpl` 对象。

## <a name="load-a-profile"></a>加载配置文件

既然已经定义了 `ProtectionProfileObserverImpl` 和 `AuthDelegateImpl`，接下来我们将使用它们实例化 `mip::ProtectionProfile`。 创建 `mip::ProtectionProfile` 对象需要 [`mip::ProtectionProfile::Settings`](reference/class_mip_ProtectionProfile_settings.md)。

### <a name="protectionprofilesettings-parameters"></a>ProtectionProfile::Settings Parameters

- `std::string path`：文件路径下的日志记录、 遥测和其他持久状态存储。
- `bool useInMemoryStorage`：定义应在磁盘上而不是内存中存储的所有状态。
- `std::shared_ptr<mip::AuthDelegate> authDelegate`：类的共享的指针`mip::AuthDelegate`。
- `std::shared_ptr<mip::ProtectionProfile::Observer> observer`：共享的指向`ProtectionProfile::Observer`实现。
- `mip::ApplicationInfo applicationInfo`：对象。 用于定义使用 SDK 的应用程序的相关信息。

下面的两个示例展示如何使用本地存储作为状态存储来创建 profileSettings 对象，以及仅在内存中创建该对象。 两者都假设已经创建了 `authDelegateImpl` 对象。

#### <a name="store-state-in-memory-only"></a>将状态仅存储在内存中

```cpp
ProtectionProfile::Settings profileSettings(
    "",                                     //path to store settings
    true,                                   //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>在磁盘上的存储路径中读取/写入配置文件设置

```cpp
ProtectionProfile::Settings profileSettings(
    "./mip_app_data",                       //path to store settings
    false,                                  //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

接下来，使用 promise/future 模式加载 `ProtectionProfile`。

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<ProtectionProfile>>>();
auto profileFuture = profilePromise->get_future();
ProtectionProfile::LoadAsync(profileSettings, profilePromise);
```

如果我们加载了配置文件，并且该操作已成功，则调用 `ProtectionProfileObserverImpl::OnLoadSuccess`（我们的 `mip::ProtectionProfile::Observer::OnLoadSuccess` 实现）。 生成的对象或异常指针以及上下文作为参数传入函数。 上下文是指向我们为处理异步操作而创建的 `std::promise` 的指针。 该函数将 promise 的值简单地设置为 ProtectionProfile 对象（上下文）。 当主函数使用 `Future.get()` 时，结果可以存储在新对象中。

```cpp
//get the future value and store in profile.
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>汇总

完全实现观察程序和身份验证委托后，现在可以完全加载配置文件。 以下代码片段假定已包含所有必需的标头。

```cpp
int main()
{
    const string userName = "MyTestUser@contoso.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    ProtectionProfile::Settings profileSettings("",
        false,
        authDelegateImpl,
        std::make_shared<ConsentDelegateImpl>(),
        std::make_shared<ProfileObserver>(),
        mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<ProtectionProfile>>>();
    auto profileFuture = profilePromise->get_future();
    ProtectionProfile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

最终结果是我们成功加载了配置文件并存储在名为 `profile` 的对象中。

## <a name="next-steps"></a>后续步骤

现在已经添加了配置文件，接下来向配置文件添加引擎。

[保护引擎概念](concept-profile-engine-protection-engine-cpp.md)
