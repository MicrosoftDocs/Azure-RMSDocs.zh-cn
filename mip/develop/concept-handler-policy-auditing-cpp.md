---
title: 概念 - Microsoft 信息保护 SDK 策略 API 中的审核
description: 本文将帮助你了解如何使用 Microsoft 信息保护 SDK 来将策略 API 审核事件提交到 Azure 信息保护分析。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/07/2018
ms.author: tommos
ms.openlocfilehash: bc85a6e737c883afdc39e8730483fc2c0da720a9
ms.sourcegitcommit: ef70dab87478084fca853f389dab2408b95d1df1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304191"
---
# <a name="auditing-in-the-mip-sdk"></a>MIP SDK 中的审核

Azure 信息保护管理门户提供对管理员报表的访问。 这些报表可显示在任何集成了 MIP SDK 的应用中用户手动或自动应用的标签。 利用 SDK 的开发合作伙伴可轻松启用此功能，从而让应用中的信息显示在客户报表中。

## <a name="event-types"></a>事件类型

可通过 SDK 向 Azure 信息保护分析提交三种类型的事件。 检测信号事件、发现事件和更改事件

### <a name="heartbeat-events"></a>检测信号事件

对于已集成策略 API 的任何应用程序，系统将自动生成检测信号事件。 检测信号事件包括：

* TenantId
* 生成时间
* 用户主体名称
* 生成审核的计算机的名称
* 进程名称
* 平台
* 应用 ID - 对应于 Azure AD 应用程序 ID。

在检测企业中使用 Microsoft 信息保护 SDK 的应用程序时，这些事件会十分有用。

### <a name="discovery-events"></a>发现事件

发现事件提供关于策略 API 读取或使用的标记信息的信息。 由于这些事件可以显示设备、位置以及组织中访问信息的用户，因此它们十分有用。

在策略 API 中，通过设置一个标志，在创建时生成发现事件`mip::PolicyHandler`对象。 在下面的值的示例**isAuditDiscoveryEnabled**设置为`true`。 当`mip::ExecutionState`传递给`ComputeActions()`或`GetSensitivityLabel()`（与现有元数据信息和内容标识符），发现信息将提交到 Azure 信息保护分析。

应用调用 `ComputeActions()` 或 `GetSensitivityLabel()` 并提供 `mip::ExecutionState` 后，便会生成发现审核。 每个处理程序仅生成一次此事件。

有关执行状态的详细信息，请查看 `mip::ExecutionState` 概念文档。

```cpp
// Create PolicyHandler, passing in true for isAuditDiscoveryEnabled
auto handler = mEngine->CreatePolicyHandler(true);

// Returns vector of mip::Action and generates discovery event.
auto actions = handler->ComputeActions(*state);

//Or, get the label for a given state
auto label = handler->GetSensitivityLabel(*state);
```

实际上，在 `mip::PolicyHandler` 构造期间，isAuditDiscoveryEnabled 应当为 `true`，以允许文件访问信息流向 Azure 信息保护分析。

## <a name="change-event"></a>更改事件

更改事件提供有关文件、已应用或更改的标签以及用户提供的任何依据的信息。 通过调用 `mip::PolicyHandler` 上的 `NotifyCommittedActions()` 生成更改事件。 在将更改成功提交到文件后进行调用，以便传入用于计算操作的 `mip::ExecutionState`。

> 如果应用程序无法调用此函数，则 Azure 信息保护分析中将没有任何事件进入。

```cpp
handler->NotifyCommittedActions(*state);
```

## <a name="audit-dashboard"></a>审核仪表板

提交到 Azure 信息保护审核管道的事件将显示在 https://portal.azure.com 的报表中。 Azure 信息保护分析处于公共预览状态，功能可能会更改。

## <a name="next-steps"></a>后续步骤

- 有关 Azure 信息保护中的审核体验的详细信息，请参阅[预览公告博客上技术社区](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)。
- 下载[从 GitHub 和重试策略相关 api 的策略 API 示例](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)

