---
title: 概念 - 文件 API 配置文件对象
description: 本文将帮助你了解在应用程序初始化期间创建的文件配置文件对象的概念。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 5534cf804422de2d02a53e8c21ceae77af52691d
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886077"
---
# <a name="microsoft-information-protection-sdk---file-api-profile-concepts"></a>Microsoft 信息保护 SDK - 文件 API 配置文件概念

配置文件是 MIP SDK 中所有操作的根类。 在使用任何文件 API 功能之前，必须先创建 `FileProfile`，并且所有未来的操作都将由配置文件或*添加*到配置文件的其他对象执行。

在尝试实例化配置文件之前，应满足一些代码先决条件：

- `MipContext`已创建并存储在`mip::FileProfile`对象可访问的对象中。
- `AuthDelegateImpl`实现`mip::AuthDelegate`。
- `ConsentDelegateImpl`实现`mip::ConsentDelegate`。
- 应用程序已[在 Azure Active Directory 中注册](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md)，并且客户端 ID 已硬编码到应用程序或配置文件中。
- 继承 `mip::FileProfile::Observer` 的类已得到适当实现。

## <a name="load-a-profile"></a>加载配置文件

定义 `ProfileObserver`、`ConsentDelegateImpl` 和 `AuthDelegateImpl` 后，现在可以实例化 `mip::FileProfile`。 创建对象要求 [`mip::MipContext`] 具有和[`mip::FileProfile::Settings`](reference/class_mip_fileprofile_settings.md) , 以`FileProfile`存储有关的所有设置信息。 `mip::FileProfile`

### <a name="fileprofilesettings-parameters"></a>FileProfile::Settings 参数

`FileProfile::Settings` 构造函数接受下列五个参数：

- `std::shared_ptr<MipContext>`：已初始化为存储应用程序信息、状态路径等的对象。`mip::MipContext`
- `mip::CacheStorageType`：定义如何存储状态:在内存、磁盘上, 或磁盘上的和已加密。
- `std::shared_ptr<mip::AuthDelegate>`：类`mip::AuthDelegate`的共享指针。
- `std::shared_ptr<mip::ConsentDelegate>`：类[`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md)的共享指针。
- `std::shared_ptr<mip::FileProfile::Observer> observer`：`Observer`指向配置文件实现的共享指针 (在[`PolicyProfile`](reference/class_mip_policyprofile_observer.md)、 [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)和[`FileProfile`](reference/class_mip_fileprofile_observer.md)中)。

以下示例展示如何使用本地存储作为状态存储来创建 `profileSettings` 对象，以及仅在内存中创建该对象。 两者都假设已经创建了 `authDelegateImpl` 对象。

#### <a name="store-state-in-memory-only"></a>将状态仅存储在内存中

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

FileProfile::Settings profileSettings(
    mipContext,                                   // mipContext object
    mip::CacheStorageType::InMemory,              // use in memory storage
    authDelegateImpl,                             // auth delegate object
    std::make_shared<ConsentDelegateImpl>(),      // new consent delegate
    std::make_shared<FileProfileObserverImpl>()); // new protection profile observer
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>在磁盘上的存储路径中读取/写入配置文件设置

以下代码片段指示 `FileProfile` 将所有应用状态数据存储在 `./mip_app_data` 中。

```cpp
mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

mMipContext = mip::MipContext::Create(appInfo,
                "mip_app_data",
                mip::LogLevel::Trace,
                nullptr /*loggerDelegateOverride*/,
                nullptr /*telemetryOverride*/);

FileProfile::Settings profileSettings(
    mipContext,                                    // mipContext object
    mip::CacheStorageType::OnDisk,                 // use on disk storage
    authDelegateImpl,                              // auth delegate object
    std::make_shared<ConsentDelegateImpl>(),       // new consent delegate
    std::make_shared<FileProfileObserverImpl>());  // new protection profile observer
```

#### <a name="load-the-profile"></a>加载配置文件

现在通过上面详述的任一方法使用 promise/future 模式来加载 `FileProfile`。

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<FileProfile>>>();
auto profileFuture = profilePromise->get_future();
FileProfile::LoadAsync(profileSettings, profilePromise);
```

如果我们加载了配置文件，并且该操作已成功，则调用 `ProfileObserver::OnLoadSuccess`（我们的 `mip::FileProfile::Observer::OnLoadSuccess` 实现）。 生成的对象或异常指针以及上下文作为参数传入函数。 上下文是指向我们为处理异步操作而创建的 `std::promise` 的指针。 该函数将 promise 的值简单地设置为针对第一个参数传入的 FileProfile 对象。 当主函数使用 `Future.get()` 时，结果可以存储在新对象中。

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

    mip::ApplicationInfo appInfo {clientId, "APP NAME", "1.2.3" };

    auto authDelegateImpl = std::make_shared<sample::auth::AuthDelegateImpl>(appInfo, userName, password);

    auto mipContext = mip::MipContext::Create(appInfo,
                        "mip_app_data",
                        mip::LogLevel::Trace,
                        nullptr /*loggerDelegateOverride*/,
                        nullptr /*telemetryOverride*/);

    FileProfile::Settings profileSettings(
        mipContext,                                    // mipContext object
        mip::CacheStorageType::OnDisk,                 // use on disk storage
        authDelegateImpl,                              // auth delegate object
        std::make_shared<ConsentDelegateImpl>(),       // new consent delegate
        std::make_shared<FileProfileObserverImpl>());  // new file profile observer

        auto profilePromise = std::make_shared<promise<shared_ptr<FileProfile>>>();
        auto profileFuture = profilePromise->get_future();
        FileProfile::LoadAsync(profileSettings, profilePromise);
        auto profile = profileFuture.get();
}
```

最终结果是我们成功加载了配置文件并存储在名为 `profile` 的对象中。

## <a name="next-steps"></a>后续步骤

现在已经添加了配置文件，接下来向配置文件添加引擎。 

- [文件引擎概念](concept-profile-engine-file-engine-cpp.md)
