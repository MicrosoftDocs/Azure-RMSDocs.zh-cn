---
title: 概念 - Microsoft 信息保护 SDK 策略 API 中的审核
description: 本文将帮助你了解如何使用 Microsoft 信息保护 SDK 来将策略 API 审核事件提交到 Azure 信息保护分析。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/07/2018
ms.author: tommos
ms.openlocfilehash: c660a5f58acd87ff9047a21fea26cc2732667493
ms.sourcegitcommit: 05fdaf43f74013eecb5886b95b09dd5e00670753
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "51297783"
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

通过在 `mip::PolicyEngine` 创建 `mip::PolicyHandler` 对象时设置布尔标记，可以在策略 API 中生成发现事件。 在以下示例中，isAuditDiscoveryEnabled 的值设置为 true。 将 `mip::ExecutionState` 传递给 `ComputeActions()` 或 `GetSensitivityLabel()`（带现有元数据信息和内容标识符）时，此发现信息将提交给 Azure 信息保护分析。

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

提交到 Azure 信息保护审核管道的事件将显示在 https://portal.azure.com 的报表中。 Azure 信息保护分析处于公开预览状态，功能可能会有所变化。

## <a name="next-steps"></a>后续步骤

有关 Azure 信息保护审核体验的详细信息，请参阅[技术社区上的预览公告博客](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)。

