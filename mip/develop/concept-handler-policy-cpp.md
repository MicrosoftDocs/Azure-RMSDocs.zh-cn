---
title: 概念 - MIP SDK 中的策略处理程序。
description: 本文将帮助你了解如何创建策略 API 处理程序并将其用于调用操作。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 37ab92e336d88d37d9e4e7631e108bbaaebdb977
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886190"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Microsoft 信息保护 SDK - 策略处理程序概念

在策略 API 中, `mip::PolicyHandler`公开用于计算策略操作和提交审核事件的操作。

## <a name="policy-handler-functions"></a>策略处理程序函数

`mip::PolicyHandler` 公开用于读取、写入和删除标签及保护信息的方法。 有关完整列表，请参阅 [API 参考](reference/class_mip_PolicyHandler.md)。

本文将介绍以下方法：

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>要求

创建 `PolicyHandler` 需要：

- `mip::MipContext`
- `mip::PolicyProfile`
- 已添加到 `mip::PolicyProfile` 的 `mip::PolicyEngine`
- 实现的类`mip::PolicyHandler::Observer`

## <a name="create-a-policy-handler"></a>创建策略处理程序

获取策略操作所需的第一步是创建 `PolicyHandler` 对象。 此类实现了获取特定标签必须采用的操作列表所需的功能。 它还实现了用于触发审核事件的函数。

创建 `PolicyHandler` 就像使用 promise/future 模式调用 `PolicyEngine` 的 `CreatePolicyHandlerAsync` 函数一样简单。

`CreatePolicyHandlerAsync` 接受单个参数：isAuditDiscoveryEnabled。 如果应用程序应在审核日志中显示检测信号和发现事件, 请将此值设置为**true** 。

> [!NOTE]
> `mip::PolicyHandler::Observer` 类必须在派生类中实现，因为 `CreatePolicyHandler` 需要 `Observer` 对象。 

```cpp
auto createPolicyHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyHandler>>>();
auto createPolicyHandlerFuture = createPolicyHandlerPromise->get_future();
PolicyEngine->CreatePolicyHandlerAsync(true);
auto handler = createPolicyHandlerFuture.get();
```

成功创建 `PolicyHandler` 对象后，可以计算操作并提交审核事件。

## <a name="next-steps"></a>后续步骤

现在, 你已了解如何创建策略处理程序:

- 了解如何[创建执行状态类, 该类](concept-handler-policy-executionstate-cpp.md)用于确定计算操作。
- [从 GitHub 下载策略 Api 示例, 并试用策略 api](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
