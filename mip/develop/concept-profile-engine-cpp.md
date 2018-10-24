---
title: 概念 - MIP SDK 中的核心概念 - 配置文件和引擎
description: 本文将帮助你了解在应用程序初始化期间创建的称为配置文件和引擎的核心 SDK 概念。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6f11944e7cceed39423af2a8104ce044d1f6eec6
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453412"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Microsoft 信息保护 SDK - 配置文件和引擎对象概念

## <a name="profiles"></a>Profiles

配置文件是 MIP SDK 中所有操作的根类。 在使用三个 API 中的任意一个之前，必须由客户端应用程序创建配置文件。 所有未来的操作都将由配置文件或*添加*到配置文件的其他对象执行。

MIP SDK 中有三种类型的配置文件：

- [`PolicyProfile`](reference/class_mip_policyprofile.md)：MIP 策略 API 的配置文件类。
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md)：MIP 保护 API 的配置文件类。
- [`FileProfile`](reference/class_mip_fileprofile.md)：MIP 文件 API 的配置文件类。

使用方应用程序中所用的 API 将确定应使用哪个配置文件类。

配置文件本身提供以下功能：

- 定义 SDK 状态的存储位置。 状态数据包括用户详细信息、下载的用户策略、日志和遥测数据。
- 定义状态是应该加载到内存中还是保存到磁盘中。
- 通过接受 `mip::AuthDelegate` 来处理身份验证。
- 设置使用 SDK 的应用的应用程序 ID 和友好名称。

### <a name="profile-settings"></a>配置文件设置

- `Path`：在其下存储日志记录、遥测和其他永久性状态的文件路径。
- `useInMemoryStorage`：一个布尔值，用于定义状态应存储在内存中还是磁盘上。
- `authDelegate`：类 `mip::AuthDelegate` 的共享指针。 
- `consentDelegate`：类 `mip::ConsentDelegate` 的共享指针。 
- `observer`：指向配置文件 `Observer` 实现的共享指针（在 `PolicyProfile`、`ProtectionProfile` 和 `EngineProfile` 中）。
- `applicationInfo`：一个 `mip::ApplicationInfo` 对象。 有关使用 SDK 的应用程序的信息。

## <a name="engines"></a>引擎

在文件 API、配置文件 API 和保护 API 中，引擎为代表特定标识执行的操作提供接口。 对于登录到应用程序的每个用户，将向配置文件对象添加一个引擎。 引擎执行的所有操作都位于该标识的上下文中。

SDK 中有三个引擎类，每个 API 一个。 以下列表显示了引擎类以及与每个引擎类相关的一些功能：

- [`mip::ProtectionEngine`]
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`：获取已加载引擎的标签列表。
  - `GetSensitivityLabel()`：从现有内容中获取标签。
  - `ComputeActions()`：获得标签 ID 和可选元数据后，返回特定项应发生的操作的列表。
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`：获取已加载引擎的标签列表。
  - `CreateFileHandler()`：为特定文件或流创建 `mip::FileHandler`。

### <a name="engine-states"></a>引擎状态

引擎可能具有以下两种状态之一：

- `CREATED`：Created 表示在调用所需的后端服务后，SDK 具有足够的本地状态信息。
- `LOADED`：SDK 为引擎生成了正常运行所需的数据结构。

必须创建并加载引擎才能执行任意操作。 `Profile` 类公开了一些引擎管理方法：`AddEngineAsync`、`RemoveEngineAsync` 和 `UnloadEngineAsync`。

下表描述了可能的引擎状态以及可更改该状态的方法。

|         | NONE              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| NONE    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>引擎 ID

每个引擎都有一个唯一标识符 `id`，用于所有引擎管理操作。 应用程序可以提供 `id`；如果应用程序未提供，SDK 将生成一个新的唯一标识符。 所有其他引擎属性（例如，标识信息中的电子邮件地址）均为 SDK 的不透明有效负载。 SDK 不执行任何逻辑来保持任何其他属性的唯一性或强制执行任何其他约束。

### <a name="engine-management-methods"></a>引擎管理方法

如上所述，SDK 中有三种引擎管理方法：`AddEngineAsync`、`DeleteEngineAsync` 和 `UnloadEngineAsync`。

#### <a name="addengineasync"></a>AddEngineAsync

此方法加载现有引擎，或者当本地状态中不存在引擎时，创建新的引擎。

如果应用程序未提供 `id`，则 `AddEngineAsync` 会生成新的 `id`。 接着，它会查看本地状态中是否已存在具有该 `id` 的引擎。 如果存在，它会加载该引擎。 如果本地状态中*不*存在引擎，则会通过调用必要的 API 和后端服务来创建新引擎。

在这两种情况下，如果该方法成功执行，则会加载引擎，并且引擎可供使用。

#### <a name="deleteengineasync"></a>DeleteEngineAsync

删除具有给定 `id` 的引擎。 该引擎的所有痕迹都会从本地状态中移除。

#### <a name="unloadengineasync"></a>UnloadEngineAsync

为具有给定 `id` 的引擎卸载内存中数据结构。 此引擎的本地状态仍保持不变，可以使用 `AddEngineAsync` 重载。

此方法允许应用程序通过卸载预计不会很快使用的引擎，明智地使用内存。

## <a name="next-steps"></a>后续步骤

- 接下来，详细了解[身份验证概念](concept-authentication-cpp.md)和[观察程序](concept-async-observers.md)。 MIP 提供可扩展的身份验证模型，而观察程序用于为异步事件提供事件通知。 两者都必不可少，适用于所有 MIP API 集。
- 然后学习文件 API、策略 API 和保护 API 的配置文件和引擎概念
  - [文件 API 配置文件概念](concept-profile-engine-file-profile-cpp.md)
  - [文件 API 引擎概念](concept-profile-engine-file-engine-cpp.md)
  - [策略 API 配置文件概念](concept-profile-engine-file-profile-cpp.md)
  - [策略 API 引擎概念](concept-profile-engine-file-engine-cpp.md)
  - [保护 API 配置文件概念](concept-profile-engine-file-profile-cpp.md)
  - [保护 API 引擎概念](concept-profile-engine-file-engine-cpp.md)  
