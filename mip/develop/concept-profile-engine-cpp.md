---
title: 概念 - MIP SDK 中的核心概念 - 配置文件和引擎
description: 本文将帮助你了解在应用程序初始化期间创建的称为配置文件和引擎的核心 SDK 概念。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/29/2019
ms.author: mbaldwin
ms.openlocfilehash: 51934a4a285368a00aaf23780c7fd6c2f315ed7d
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88563947"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Microsoft 信息保护 SDK - 配置文件和引擎对象概念

## <a name="profiles"></a>配置文件

如果 `MipContext` 是用于存储 SDK 特定的设置的类，则该配置文件是 MIP SDK 中所有 mip 标记和特定于保护的操作的根类。 使用三个 API 集中的任何一个，客户端应用程序必须创建配置文件。 将来的操作由配置文件或 *添加* 到配置文件中的其他对象执行。

MIP SDK 中有三种类型的配置文件：

- [`PolicyProfile`](reference/class_mip_policyprofile.md)： MIP 策略 API 的配置文件类。
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md)： MIP 保护 API 的配置文件类。
- [`FileProfile`](reference/class_mip_fileprofile.md)： MIP 文件 API 的配置文件类。

使用的应用程序中使用的 API 确定了应使用的配置文件类。

配置文件本身提供以下功能：

- 定义应在内存中加载状态还是将状态保存到磁盘中，如果将状态保存到磁盘，则应对其进行加密。
- 定义 `mip::ConsentDelegate` 应该用于同意操作的。
- 定义 `mip::FileProfile::Observer` 将用于配置文件操作的异步回调的实现。

### <a name="profile-settings"></a>配置文件设置

- `MipContext`： `MipContext` 已初始化为存储应用程序信息、状态路径等的对象。
- `CacheStorageType`：定义如何存储状态：在内存、磁盘上，或磁盘上的和已加密。
- `consentDelegate`：类的共享指针 [`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md) 。
- `observer`：指向 `Observer` [`PolicyProfile`](reference/class_mip_policyprofile_observer.md) 、 [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md) 和) 中的配置文件实现的共享指针 ([`FileProfile`](reference/class_mip_fileprofile_observer.md) 。
- `applicationInfo`：一个 [`mip::ApplicationInfo`](reference/mip-enums-and-structs.md#structures) 对象。 有关使用 SDK 的应用程序的信息，该信息与你的 Azure Active Directory 应用程序注册 ID 和名称匹配。

## <a name="engines"></a>引擎

文件、配置文件和保护 API 引擎为按特定标识执行的操作提供了一个接口。 向登录到应用程序的每个用户或服务主体的配置文件对象添加一个引擎。 可以通过 `mip::ProtectionSettings` 和文件或保护处理程序执行委托操作。 有关更多详细信息，请参阅 [FileHandler 概念中的 "保护设置" 部分](concept-handler-file-cpp.md) 。

SDK 中有三个引擎类，每个 API 一个。 以下列表显示了引擎类以及与每个引擎类相关的一些功能：

- [`mip::ProtectionEngine`](reference/class_mip_protectionengine.md)
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`：获取已加载引擎的标签列表。
  - `GetSensitivityLabel()`：从现有内容中获取标签。
  - `ComputeActions()`：获得标签 ID 和可选元数据后，返回特定项应发生的操作的列表。
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`：获取已加载引擎的标签列表。
  - `CreateFileHandler()`：为特定文件或流创建 `mip::FileHandler`。

创建引擎要求传入特定的引擎设置对象，该对象包含要创建的引擎类型的设置。 "设置" 对象允许开发人员指定有关引擎标识符、 `mip::AuthDelegate` 实现、区域设置和自定义设置的详细信息，以及其他 API 特定的详细信息。

### <a name="engine-states"></a>引擎状态

引擎可能具有以下两种状态之一：

- `CREATED`：Created 表示在调用所需的后端服务后，SDK 具有足够的本地状态信息。
- `LOADED`：SDK 为引擎生成了正常运行所需的数据结构。

必须创建并加载引擎才能执行任意操作。 `Profile` 类公开了一些引擎管理方法：`AddEngineAsync`、`DeleteEngineAsync` 和 `UnloadEngineAsync`。

下表描述了可能的引擎状态以及哪些方法可以更改该状态：

| 引擎状态 | 无              | CREATED           | LOADED         |
|--------------|-------------------|-------------------|----------------|
| 无         |                   |                   | AddEngineAsync |
| CREATED      | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED       | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>引擎 ID

每个引擎都有一个唯一标识符 `id`，用于所有引擎管理操作。 如果应用程序未提供，则该应用程序可提供 `id` ，或 SDK 生成一个。 所有其他引擎属性（例如，标识信息中的电子邮件地址）均为 SDK 的不透明有效负载。 SDK 不执行任何逻辑来保持任何其他属性的唯一性或强制执行任何其他约束。

> [!IMPORTANT]
> 最佳做法是使用用户唯一的引擎 Id，并在每次用户使用 SDK 执行操作时使用该 Id。 如果无法提供现有引擎 Id，将导致额外的服务往返，以获取策略，并将提取可能已为现有引擎缓存的许可证。

### <a name="engine-management-methods"></a>引擎管理方法

如前所述，SDK 中有三种引擎管理方法： `AddEngineAsync` 、 `DeleteEngineAsync` 和 `UnloadEngineAsync` 。

#### <a name="addengineasync"></a>AddEngineAsync

此方法加载现有引擎，如果本地状态中尚不存在引擎，则创建一个。

如果应用程序未提供 `id`，则 `AddEngineAsync` 会生成新的 `id`。 接着，它会查看本地状态中是否已存在具有该 `id` 的引擎。 如果存在，它会加载该引擎。 如果本地状态中*不*存在引擎，则会通过调用必要的 API 和后端服务来创建新引擎。

在这两种情况下，如果该方法成功执行，则会加载引擎，并且引擎可供使用。

#### <a name="deleteengineasync"></a>DeleteEngineAsync

删除具有给定 `id` 的引擎。 该引擎的所有痕迹都会从本地状态中移除。

#### <a name="unloadengineasync"></a>UnloadEngineAsync

为具有给定 `id` 的引擎卸载内存中数据结构。 此引擎的本地状态仍保持不变，可以使用 `AddEngineAsync` 重载。

此方法通过卸载预计不会使用的引擎，使应用程序可以合理地利用内存使用量。

## <a name="next-steps"></a>后续步骤

- 接下来，详细了解[身份验证概念](concept-authentication-cpp.md)和[观察程序](concept-async-observers.md)。 MIP 提供可扩展的身份验证模型，而观察程序用于为异步事件提供事件通知。 两者都必不可少，适用于所有 MIP API 集。
- 然后学习文件 API、策略 API 和保护 API 的配置文件和引擎概念
  - [文件 API 配置文件概念](concept-profile-engine-file-profile-cpp.md)
  - [文件 API 引擎概念](concept-profile-engine-file-engine-cpp.md)
  - [策略 API 配置文件概念](concept-profile-engine-file-profile-cpp.md)
  - [策略 API 引擎概念](concept-profile-engine-file-engine-cpp.md)
  - [保护 API 配置文件概念](concept-profile-engine-file-profile-cpp.md)
  - [保护 API 引擎概念](concept-profile-engine-file-engine-cpp.md)  
