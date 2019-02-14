---
title: 概念 - 在 Microsoft 信息保护 SDK 中实现 ExecutionState
description: 本文将帮助你了解如何使用 Microsoft 信息保护 SDK 中的 ExecutionState 来计算操作并提供审核日志的详细信息。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: 54e5249f7624cbc020451752d39ccb9f0b507f3a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56257682"
---
# <a name="implement-executionstate"></a>实现 ExecutionState

将信息传递到 MIP SDK 以根据当前状态和所需状态计算应执行的操作是通过 `mip::ExecutionState` 类实现的。 类似于 SDK 中的其他类，`ExecutionState` 是一个抽象类，必须由开发人员实现。

> 有关 `ExecutionState` 实现的完整示例，请查看以下示例源：
>
> * [execution_state_impl.h](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h)
> * [execution_state_impl.cpp](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.cpp)

## <a name="mipexecutionstate-members"></a>mip::ExecutionState 成员

`ExecutionState` 公开以下虚拟成员。 每一个都为策略引擎提供一些上下文，以返回关于应用程序应执行哪些操作的信息。 此外，此信息可用于向 Azure 信息保护报告功能提供审核信息。


| 成员                                                                           | 返回                                                                                                              |
|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `std::string GetNewLabelId()`                                                      | 返回要应用于对象的标签 ID。                                                                    |
| `mip::ContentState GetContentState()`                                              | 返回对象的 mip::ContentState。                                                                         |
| `std::pair<bool, std::string> IsDowngradeJustified()`                              | 返回一个用于表示降级是否合理以及依据的 std::pair。                                 |
| `std::string GetContentIdentifier()`                                               | 返回内容标识符。 应当是人工可读的标识符，指示对象的位置。   |
| `mip::ActionSource GetNewLabelActionSource()`                                      | 返回标签的 mip::ActionSource。                                                                          |
| `mip::AssignmentMethod GetNewLabelAssignmentMethod()`                              | 返回标签的 mip::AssignmentMethod                                                                        |
| `std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties()` | 返回字符串的 std::pairs 的 std :: vector，其中包含将要用于文档的自定义元数据。 |
| `std::vector<std::pair<std::string, std::string>> GetContentMetadata()`            | 返回字符串的 std::pairs 的 std :: vector，其中包含当前的内容元数据。                               |
| `std::shared_ptr<mip::ProtectionDescriptor> GetProtectionDescriptor()`           | 返回指向 mip::ProtectionDescriptor 的指针                                                                     |
| `mip::ContentFormat GetContentFormat()`                                            | 返回 mip::ContentFormat                                                                                           |
| `mip::ActionType GetSupportedActions()`                                           | 返回标签的 mip::ActionTypes。                                                                              |

每一个都必须在派生自 `mip::ExecutionState` 的类的实现中进行重写。 在上面链接的示例应用中，此过程是通过实现名为 `ExecutionStateOptions` 的结构并将其传递给派生类的构造函数来完成的。

在[示例](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h)中，名为 `ExecutionStateOptions` 的结构定义为：

```cpp
struct ExecutionStateOptions {
    std::unordered_map<std::string, std::string> metadata;
    std::string newLabelId;
    std::string contentIdentifier;
    mip::ActionSource actionSource = mip::ActionSource::MANUAL;
    mip::ContentState contentState = mip::ContentState::REST;
    mip::AssignmentMethod assignmentMethod = mip::AssignmentMethod::STANDARD;
    bool isDowngradeJustified = false;
    std::string downgradeJustification;
    std::string templateId;
    mip::ContentFormat contentFormat = mip::ContentFormat::DEFAULT;
};
```

每个属性都由应用进行设置，然后 `ExecutionStateOptions` 会被传递给派生自 `mip::ExecutionState` 的类的构造函数。 此信息用于确定要执行的操作。 `mip::ExecutionState` 中提供的数据也将显示在 Azure 信息保护分析中。

### <a name="next-steps"></a>后续步骤

- 了解如何确定[计算新的或现有标签的操作](concept-handler-policy-computeactions-cpp.md)基于当前和所需状态。
- 下载[从 GitHub 和重试策略相关 api 的策略 API 示例](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
