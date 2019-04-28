---
title: 概念 - 策略 API 引擎对象
description: 本文将帮助你了解在应用程序初始化期间创建的策略引擎对象的概念。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 52d036bd58d4f24710e765ca42493696a3cd5330
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175385"
---
# <a name="microsoft-information-protection-sdk---policy-api-engine-concepts"></a>Microsoft 信息保护 SDK - 策略 API 引擎概念

`mip::PolicyEngine` 实现了策略 API 可以执行的所有操作，但加载配置文件除外。 

## <a name="implementation-add-a-policy-engine"></a>实现：添加策略引擎

### <a name="implementation-create-policy-engine-settings"></a>实现：创建策略引擎设置

与配置文件类似，引擎也需要设置对象 `mip::PolicyEngine::Settings`。 此对象存储唯一引擎标识符、可用于调试或遥测的可自定义客户端数据以及（可选）区域设置。

在这里，我们创建一个名为 *engineSettings* 的 `PolicyEngine::Settings` 对象。

```cpp
PolicyEngine::Settings engineSettings("UniqueID", "");
```

作为最佳做法，第一个参数 **id** 应该允许引擎轻松连接到关联用户，最好是用户主体名称。

### <a name="implementation-add-the-policy-engine"></a>实现：添加策略引擎

为了添加引擎，我们将返回用于加载配置文件的 future/promise 模式。 我们将使用 `mip::PolicyEngine`，而不是为 `mip::Profile` 创建 promise。

```cpp

  //auto profile will be std::shared_ptr<mip::Profile>
  auto profile = profileFuture.get();

  //Create the PolicyEngine::Settings object
  PolicyEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::PolicyEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::PolicyEngine>
  auto engine = engineFuture.get();
```

上述代码的最终结果是我们成功地将经过身份验证的用户的引擎添加到配置文件中。

## <a name="implementation-list-sensitivity-labels"></a>实现：列出敏感度标签

现在可以使用添加的引擎通过调用 `engine->ListSensitivityLabels()` 来列出经过身份验证的用户可用的所有敏感度标签。

`ListSensitivityLabels()` 将从服务中提取特定用户的标签和标签属性列表。 结果存储在 `std::shared_ptr<mip::Label>` 的向量中。

### <a name="implementation-listsensitivitylabels"></a>实现：ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

### <a name="implementation-print-the-labels"></a>实现：打印标签

```cpp
//Iterate through all labels in the vector
for (const auto& label : labels) {
  //print the label name
  cout << label->GetName() << endl;
  //Iterate through all child labels
  for (const auto& child : label->GetChildren()) {
    //Print the label with some formatting
    cout << "->  " << child->GetName() << endl;
  }
}
```

通过打印名称可轻松证明我们已成功从服务中拉取策略并能够获得标签。 若要应用标签，需要标签标识符。 修改上述代码段以返回标签 ID 会导致：

```cpp
for (const auto& label : labels) {
  //Print label name and GUID
  cout << label->GetName() << " : " << label->GetId() << endl;

  //Print child label name and GUID
  for (const auto& child : label->GetChildren()) {    
    cout << "->  " << child->GetName() <<  " : " << child->GetId() << endl;
  }
}
```

`GetSensitivityLabels()` 返回的 `mip::Label` 集合可用于显示用户可用的所有标签，并在用户选定标签后使用 ID 将其应用于文件。

