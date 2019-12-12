---
title: 概念-缓存存储
description: 本文将帮助你了解有关 MIP SDK 中的缓存存储的概念。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: a72ae5169e4a7ee9a201876afbef0f5d33fc9b89
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "69893746"
---
# <a name="microsoft-information-protection-sdk---cache-storage"></a>Microsoft 信息保护 SDK-缓存存储

MIP SDK 实现用于维护 SDK 缓存存储的 SQLite3 数据库。 在 Microsoft 信息保护 SDK 1.3 版之前，只支持两种类型的缓存状态存储：磁盘上和内存中的。 这两种类型都以纯文本形式存储特定的数据，尤其是受保护内容和策略信息的许可证。

为了改善 SDK 的安全状况，我们添加了对磁盘缓存上第二种类型的支持，它使用平台特定的加密 Api 来保护数据库及其内容。

将配置文件作为 `FileProfileSettings`、`PolicyProfileSettings`或 `ProtectionProfileSettings` 对象的一部分进行加载时，应用程序将定义缓存类型。 缓存类型在配置文件的生存期内是静态的。 更改为不同类型的缓存存储类型需要销毁现有配置文件并创建一个新配置文件。

## <a name="cache-storage-types"></a>缓存存储类型

从 MIP SDK 版本1.3 开始，以下存储缓存类型可用。

| 类型            | 用途                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| InMemory        | 在应用程序的内存中维护存储缓存。                                                                       |
| OnDisk          | 将数据库存储在磁盘上的 "设置" 对象中提供的目录中。 数据库以纯文本形式存储。              |
| OnDiskEncrypted | 将数据库存储在磁盘上的 "设置" 对象中提供的目录中。 使用特定于 OS 的 Api 对数据库进行加密。 |

应用程序生成的每个**引擎**都会生成一个新的加密密钥。

缓存存储通过一个配置文件设置对象通过 `mip::CacheStorageType` 枚举设置。

```cpp 
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDiskEncrypted, // Define the storage type to use.
    mAuthDelegate,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());
```

## <a name="when-to-use-each-type"></a>何时使用每种类型

缓存存储对于维护对以前解密的信息的脱机访问很重要，并可确保在以前使用数据时解密操作的性能。

- **在内存存储中**：对长期进程使用此存储类型，在这种情况下，不需要在服务重新启动时保持策略或许可证缓存信息。
- **在磁盘上**：将此存储类型用于进程可能频繁停止和启动的应用程序，但必须在重启过程中维护策略、许可证和服务发现缓存。 此存储缓存类型是纯文本，因此更适合于用户无权访问状态存储的服务器工作负荷。 这种情况的示例如下所示：在服务器上运行的 Windows 服务或 Linux daemon，或只有服务管理员才能访问状态数据的 SaaS 应用程序。
- **在磁盘上并加密**：将此存储类型用于进程可能频繁停止和启动的应用程序，但必须在重新启动时维护策略、许可证和服务发现缓存。 此存储缓存已加密，因此更适用于工作站应用程序，用户可以在其中浏览和发现状态数据库。 加密有助于确保被授权的用户不能通过策略内容或纯文本形式的保护许可证内容来访问。 请务必注意，在所有情况下，都会使用用户可以访问的密钥对数据进行加密。 熟练的攻击者能够以最少的工作量对缓存进行解密，但这样做可以防止篡改和浏览。

## <a name="supported-platforms-for-encryption"></a>支持的加密平台

| 平台          | 版本                | 注释                                                                                                                               |
| ----------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Microsoft Windows | Windows 8 及更高版本    | Windows 7 仅支持 CacheStorageType：： OnDisk                                                                                    |
| macOS             | High Sierra 及更高版本  |                                                                                                                                     |
| Ubuntu Linux      | 16.04 及更高版本        | 需要[SecretService](https://developer.gnome.org/libsecret/unstable/SecretService.html)和 `LinuxEncryptedCache` 功能标志。 |
| Android           | Android 7.0 或更高版本   |                                                                                                                                     |
| iOS               | 所有支持的版本 |                                                                                                                                     |

虽然 MIP SDK 支持其他 Linux 分发，但我们未在 RedHat Enterprise Linux、CentOS 或 Debian 上测试缓存加密。

> [!NOTE]
> 用于在 Linux 上启用缓存存储的功能标志通过 `mip::MipContext::CreateWithCustomFeatureSettings()` 设置

## <a name="cache-storage-database-tables"></a>缓存存储数据库表

MIP SDK 为缓存维护两个数据库。 一种用于保护 Api，维护保护状态详细信息。 另一种是用于策略 Api 并维护策略详细信息和服务信息。 两者均存储在 settings 对象的**mip\mip.policies.sqlite3**和**mip\mip.protection.sqlite3**下定义的路径中。

### <a name="protection-database"></a>保护数据库

| 表         | 用途                                                        | 已加密 |
| ------------- | -------------------------------------------------------------- | --------- |
| AuthInfoStore | 存储身份验证质询详细信息。                       | 否        |
| ConsentStore  | 存储每个引擎的许可结果。                        | 否        |
| DnsInfoStore  | 存储 SDK 保护操作的 DNS 查找结果        | 否        |
| EngineStore   | 存储引擎详细信息、关联用户和自定义客户端数据 | 否        |
| KeyStore      | 存储每个引擎的对称加密密钥。              | “是”       |
| LicenseStore  | 存储区使用以前解密的数据的许可证信息。  | “是”       |
| SdInfoStore   | 存储服务发现结果。                              | 否        |

### <a name="policy-database"></a>策略数据库

| 表           | 用途                                                          | 已加密 |
| --------------- | ---------------------------------------------------------------- | --------- |
| KeyStore        | 存储每个引擎的对称加密密钥。                | “是”       |
| 策略        | 存储每个用户的标签策略信息。                   | “是”       |
| PoliciesUrl     | 为特定用户存储后端策略服务 URL。             | 否        |
| 敏感度     | 存储特定用户策略的分类规则。          | “是”       |
| SensitivityUrls | 为特定用户存储后端敏感度策略服务 URL。 | 否        |

## <a name="database-size-considerations"></a>数据库大小注意事项

数据库大小取决于两个因素：要添加到缓存中的引擎数量，以及缓存的保护许可证数量。 在 MIP SDK 1.3 中，没有在许可证缓存过期的情况下进行清理的机制。 如果缓存增长超过所需的大小，则必须有外部进程删除缓存。

最重要的数据库增长因素是保护许可证缓存。 如果不需要授权缓存，则这可能是因为服务往返行程不会影响应用程序性能，或者缓存可能会增长得太大，可以禁用许可证缓存。 这是通过将 `FileProfile::Settings` 对象的 `CanCacheLicenses` 设置为 false 来完成的。

```cpp
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDiskEncrypted,
    mAuthDelegate,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());

profileSettings.SetCanCacheLicenses(false);
```
