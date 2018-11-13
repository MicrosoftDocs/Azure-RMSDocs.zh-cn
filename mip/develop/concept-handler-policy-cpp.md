---
title: 概念 - MIP SDK 中的策略处理程序。
description: 本文将帮助你了解如何创建策略 API 处理程序并将其用于调用操作。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: c1e150de6096e070f46232e77a4749081fe0bb9f
ms.sourcegitcommit: 05fdaf43f74013eecb5886b95b09dd5e00670753
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "51297793"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Microsoft 信息保护 SDK - 策略处理程序概念

在策略 API 中，`mip::PolicyHandler` 公开可用于计算策略操作和提交审核事件的各种操作。

## <a name="policy-handler-functions"></a>策略处理程序函数

`mip::PolicyHandler` 公开用于读取、写入和删除标签及保护信息的方法。 有关完整列表，请参阅 [API 参考](reference/class_mip_PolicyHandler.md)。

本文将介绍以下方法：

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>要求

创建 `PolicyHandler` 需要：

- `PolicyProfile`
- 已添加到 `PolicyProfile` 的 `PolicyEngine`
- 继承 `mip::PolicyHandler::Observer` 的类

## <a name="create-a-policy-handler"></a>创建策略处理程序

获取策略操作所需的第一步是创建 `PolicyHandler` 对象。 此类可实现获取特定标签必须执行的操作列表所需的功能，以及用于触发审核事件的函数。

创建 `PolicyHandler` 就像使用 promise/future 模式调用 `PolicyEngine` 的 `CreatePolicyHandlerAsync` 函数一样简单。

`CreatePolicyHandlerAsync` 接受单个参数：isAuditDiscoveryEnabled。 如果应用程序应在审核日志中显示检测信号事件，则将此值设置为 true。

> [!NOTE]
> `mip::PolicyHandler::Observer` 类必须在派生类中实现，因为 `CreatePolicyHandler` 需要 `Observer` 对象。 

```cpp
auto createPolicyHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyHandler>>>();
auto createPolicyHandlerFuture = createPolicyHandlerPromise->get_future();
PolicyEngine->CreatePolicyHandlerAsync(true);
auto handler = createPolicyHandlerFuture.get();
```

成功创建 `PolicyHandler` 对象后，可以计算操作并提交审核事件。

# <a name="compute-an-action"></a>计算操作

如先前所述，策略 API 的主要功能是：

- 列出可用标签。
- 根据当前和所需状态返回应执行的特定操作集。 

该过程的最后一步是向 `ComputeActions()` 函数提供标签标识符和（可选）现有标签的元数据。

可以在 GitHub 上找到本文的示例代码。

* [mipsdk-policyapi-cpp-sample-basic](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic)

## <a name="compute-an-action-for-a-new-label"></a>计算新标签的操作

使用 [ExecutionState](concept-auditing-policy-executionstate-cpp.md) 部分中定义的 `ExecutionStateImpl`，可以计算新标签的 `mip::Actions`。

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c"; 
sample::policy::ExecutionStateOptions options;

// Set desired newLabelId in ExecutionStateOptions.
options.newLabelId = newLabelId;

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions.
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

只编写作为 `actions` 一部分返回的 `mip::MetadataActions` 会显示：

```cpp
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled : true
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate : 2018-10-23T20:39:06-0800
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method : Standard
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name : Contoso FTEs (C)
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId : 2266fbe8-a0d9-44e8-bad8-00008f2a0915
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits : 3
```

`PolicyHandler` 计算操作并返回 `mip::Action` 的 `std::vector`。 应用开发人员可将此元数据应用于文件或数据。

> [!NOTE]
> 上面的示例仅显示 `mip::MetadataAction` 输出。 有关显示其他操作类型的示例，请查看[策略 API 下载](https://aka.ms/mipsdkbins)的示例包。

## <a name="compute-actions-with-an-existing-label"></a>使用现有标签计算操作

使用策略 API 时，应用程序可读取内容中的元数据。 此元数据作为 `mip::ExecutionState` 的一部分提供给 API。 `ComputeActions()` 可以处理比将新标签应用于未标记的文档更为复杂的操作。 以下示例演示了在存在标签的情况下，将标签从较敏感的标签降级为不太敏感的标签。 通过读取逗号分隔的元数据字符串并通过 `mip::ExecutionState` 提供给 API 来模拟此过程。

> [!NOTE]
> 该示例使用名为 `SplitString()` 的实用程序函数。 可在[此处](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-advanced/blob/master/mipsdk-policyapi-cpp-sample-advanced/utils.cpp)找到示例

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c";

// Comma and Pipe Delimited Metadata.
string metadata = "MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled|true,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate|2018-10-23T21:53:31-0800,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method|Standard,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name|Contoso FTEs (C),MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId|94f6984e-8d31-4794-bdeb-3ac89ad2b660,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId|b56491d9-155f-40ff-866f-0000acd85c31,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits|7";

// Create ExecutionStateOptions and set newLabelId.
sample::policy::ExecutionStateOptions options;
options.newLabelId = newLabelId;

// Split metadata string by commas, store in vector.
vector<string> metadataPairs = sample::utils::SplitString(metadata, ','); 

// Iterate through each string, splitting by the pipe.
// Add each key/value pair to ExecutionStateOptions metadata.
for (const string& metadataPair : metadataPairs) {
    vector<string> keyValue = sample::utils::SplitString(metadataPair, '|');
    options.metadata[keyValue[0]] = keyValue[1];
}

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

上面的示例可能会导致多个操作。 这些操作取决于作为输入提供的标签和标签配置。 至少，结果将是一个包含要通过 `GetMetadataToRemove()` 删除的数据以及要通过 `GetMetadataToAdd()` 添加的数据的 `mip::MetadataAction`。

```
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Enabled : true
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SetDate : 2018-10-23T23:59:41-0800
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Method : Standard
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Name : General
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ActionId : 447a996b-28ea-482c-b0b5-000075bd4bb3
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ContentBits : 7
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId
```

## <a name="next-steps"></a>后续步骤

* 接下来，从 GitHub 下载[策略 API 示例并试用策略 API](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
* 了解如何[将审核事件传递给 Azure 信息保护分析](concept-auditing-policy-cpp.md)