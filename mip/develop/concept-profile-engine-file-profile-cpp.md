---
title: 概念 - 文件 API 配置文件对象
description: 本文将帮助你了解在应用程序初始化期间创建的文件配置文件对象的概念。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 74937f5ef157c7807b6519a6490af80d46de6a8f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254504"
---
# <a name="microsoft-information-protection-sdk---file-api-profile-concepts"></a>Microsoft 信息保护 SDK - 文件 API 配置文件概念

配置文件是 MIP SDK 中所有操作的根类。 在使用任何文件 API 功能之前，必须先创建 `FileProfile`，并且所有未来的操作都将由配置文件或*添加*到配置文件的其他对象执行。

在尝试实例化配置文件之前，应满足一些代码先决条件：

- 实现 `AuthDelegateImpl` 以扩展 `mip::AuthDelegate`。
- 实现 `ConsentDelegateImpl` 以扩展 `mip::ConsentDelegate`。
- 应用程序已[在 Azure Active Directory 中注册](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md)，并且客户端 ID 已硬编码到应用程序或配置文件中。 
- 继承 `mip::FileProfile::Observer` 的类已得到适当实现。

## <a name="load-a-profile"></a>加载配置文件

定义 `ProfileObserver`、`ConsentDelegateImpl` 和 `AuthDelegateImpl` 后，现在可以实例化 `mip::FileProfile`。 创建 `mip::FileProfile` 对象需要使用 [`mip::FileProfile::Settings`](reference/class_mip_fileprofile_settings.md) 来存储有关 `FileProfile` 的所有设置信息。

### <a name="fileprofilesettings-parameters"></a>FileProfile::Settings 参数

`FileProfile::Settings` 构造函数接受下列五个参数：

- `std::string path`：文件路径下的日志记录、 遥测和其他持久状态存储。
- `bool useInMemoryStorage`：定义应在磁盘上而不是内存中存储的所有状态。
- `std::shared_ptr<mip::AuthDelegate> authDelegate`：类的共享的指针 `mip::AuthDelegate` 
- `std::shared_ptr<mip::ConsentDelegate>`： 
- `std::shared_ptr<mip::FileProfile::Observer> observer`：共享的指向`FileProfile::Observer`实现。
- `mip::ApplicationInfo applicationInfo`：对象。 用于定义使用 SDK 的应用程序的相关信息。

以下示例展示如何使用本地存储作为状态存储来创建 `profileSettings` 对象，以及仅在内存中创建该对象。 两者都假设已经创建了 `authDelegateImpl` 对象。

#### <a name="store-state-in-memory-only"></a>将状态仅存储在内存中

```cpp
FileProfile::Settings profileSettings(
    "",                                          //path to store settings
    true,                                        //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>在磁盘上的存储路径中读取/写入配置文件设置

以下代码片段指示 `FileProfile` 将所有应用状态数据存储在 `./mip_app_data` 中。

```cpp
FileProfile::Settings profileSettings(
    "./mip_app_data",                            //path to store settings
    false,                                       //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
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
    const string userName = "MyTestUser@consoto.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    FileProfile::Settings profileSettings("",
            false,
            authDelegateImpl,
            std::make_shared<ConsentDelegateImpl>(),
            std::make_shared<ProfileObserver>(),
            mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

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
