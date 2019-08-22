---
title: 概念 - 策略 API 配置文件对象
description: 本文将帮助你了解在应用程序初始化期间创建的策略配置文件对象的概念。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 9b3b32464cae35560c74a05b28506ca60dc963d2
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886056"
---
# <a name="microsoft-information-protection-sdk---policy-api-profile-concepts"></a>Microsoft 信息保护 SDK - 策略 API 配置文件概念

必须先加载 `mip::Profile`，然后才能执行任意策略 API 操作。

下面的两个示例展示如何使用本地存储作为状态存储来创建 profileSettings 对象，以及仅在内存中创建该对象。 两者都假设已经创建了 `authDelegateImpl` 对象。

## <a name="load-a-profile"></a>加载配置文件

现在, 已定义`ProfileObserver`、和`AuthDelegateImpl` , 我们将使用它们来实例化`mip::PolicyProfile`。 `MipContext` 创建对象需要[`mip::PolicyProfile::Settings`](reference/class_mip_PolicyProfile_settings.md)和。`mip::MipContext` `mip::PolicyProfile`

### <a name="profilesettings-parameters"></a>Profile::Settings 参数

`PolicyProfile::Settings`构造函数接受下面列出的四个参数:

- `const std::shared_ptr<MipContext>`：已初始化为存储应用程序信息、状态路径等的对象。`mip::MipContext`
- `mip::CacheStorageType`：定义如何存储状态:在内存、磁盘上, 或磁盘上的和已加密。 有关更多详细信息, 请参阅[缓存存储概念](concept-cache-storage.md)。
- `std::shared_ptr<mip::AuthDelegate>`：类`mip::AuthDelegate`的共享指针。
- `std::shared_ptr<mip::PolicyProfile::Observer> observer`：`Observer`指向配置文件实现的共享指针 (在[`PolicyProfile`](reference/class_mip_policyprofile_observer.md)、 [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)和[`FileProfile`](reference/class_mip_fileprofile_observer.md)中)。

下面的两个示例展示如何使用本地存储作为状态存储来创建 profileSettings 对象，以及仅在内存中创建该对象。 两者都假设已经创建了 `authDelegateImpl` 对象。

#### <a name="store-state-in-memory-only"></a>将状态仅存储在内存中

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

PolicyProfile::Settings profileSettings(
    mipContext,                                   // mipContext object
    mip::CacheStorageType::InMemory,              // use in memory storage
    authDelegateImpl,                             // auth delegate object
    std::make_shared<PolicyProfileObserverImpl>()); // new protection profile observer
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>在磁盘上的存储路径中读取/写入配置文件设置

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

PolicyProfile::Settings profileSettings(
    mipContext,                                    // mipContext object
    mip::CacheStorageType::OnDisk,                 // use on disk storage
    authDelegateImpl,                              // auth delegate object
    std::make_shared<PolicyProfileObserverImpl>());  // new protection profile observer
```

接下来，使用 promise/future 模式加载 `Profile`。

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<Profile>>>();
auto profileFuture = profilePromise->get_future();
Profile::LoadAsync(profileSettings, profilePromise);
```

如果成功加载了配置文件，则会通知 `ProfileObserver::OnLoadSuccess`（我们的 `mip::Profile::Observer::OnLoadSuccess` 实现）。 生成的对象（在本例中为 `mip::Profile`）以及上下文作为参数传入观察程序函数。

*上下文*是指向我们为处理异步操作而创建的 `std::promise` 的指针。 该函数将 promise 的值简单地设置为针对第一个参数传入的 Profile 对象。 当主函数使用 `Future.get()` 时，结果可以存储在调用线程的新对象中。

```cpp
//get the future value and store in profile.
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>汇总

完全实现观察程序和身份验证委托后，现在可以完全加载配置文件。 以下代码片段假定已包含所有必需的标头。

```cpp
int main()
{
    const string userName = "MyTestUser@consoto.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";

    mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

    auto authDelegateImpl = std::make_shared<sample::auth::AuthDelegateImpl>(appInfo, userName, password);

    auto mipContext = mip::MipContext::Create(appInfo,
                        "mip_app_data",
                        mip::LogLevel::Trace,
                        nullptr /*loggerDelegateOverride*/,
                        nullptr /*telemetryOverride*/);

    PolicyProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage
        authDelegateImpl,                              // auth delegate object
        std::make_shared<PolicyProfileObserverImpl>());  // new protection profile observer

    auto profilePromise = std::make_shared<promise<shared_ptr<PolicyProfile>>>();
    auto profileFuture = profilePromise->get_future();
    Profile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

最终结果是我们成功加载了配置文件并存储在名为 `profile` 的对象中。

## <a name="next-steps"></a>后续步骤

现在已经添加了配置文件，接下来向配置文件添加引擎。

[策略引擎概念](concept-profile-engine-policy-engine-cpp.md)
