---
title: 概念 - 文件 API 引擎对象
description: 本文将帮助你了解在应用程序初始化期间创建的文件引擎对象的概念。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 09b4db10523539f093a54c54d1fc6b7de8f7ddb0
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259280"
---
# <a name="microsoft-information-protection-sdk---file-api-engine-concepts"></a>Microsoft 信息保护 SDK - 文件 API 引擎概念

MIP SDK 文件 API 中的 `mip::FileEngine` 为代表指定标识执行的所有操作提供一个接口。 将为登录到应用程序的每个用户添加一个引擎，并在该标识的上下文中执行引擎执行的所有操作。

`FileEngine`具有两个主要职责：列出用于身份验证的用户的标签和创建文件处理程序来执行代表用户的文件操作。 

- [`mip::FileEngine`](reference/class_mip_fileengine.md)
- `ListSensitivityLabels()`：获取加载的引擎的标签列表。
- `CreateFileHandler()`：创建`mip::FileHandler`特定文件或流。

## <a name="add-a-file-engine"></a>添加文件引擎

如[配置文件和引擎对象](concept-profile-engine-cpp.md)中所述，引擎可以有两种状态 - `CREATED` 或 `LOADED`。 如果不为这两种状态之一，则表示它不存在。 若要创建并加载状态，只需对 `FileProfile::LoadAsync` 进行一次调用。 如果引擎已存在于缓存状态中，则它将为 `LOADED`。 如果引擎不存在，则它将为 `CREATED` 和 `LOADED`。 `CREATED` 表示应用程序具有加载引擎所需的服务的所有信息。 `LOADED` 表示已在内存中创建利用引擎所需的所有数据结构。

### <a name="create-file-engine-settings"></a>创建文件引擎设置

与配置文件类似，引擎也需要设置对象 `mip::FileEngine::Settings`。 此对象存储唯一引擎标识符、可用于调试或遥测的可自定义客户端数据以及（可选）区域设置。

在这里，我们创建一个名为 *engineSettings* 的 `FileEngine::Settings` 对象。 

```cpp
FileEngine::Settings engineSettings("UniqueID", "");
```

作为最佳做法，第一个参数 `id` 应该允许引擎轻松连接到关联用户。 像电子邮件地址、UPN 或 AAD 对象 GUID 之类的信息将确保 ID 既是唯一的，又可以从本地状态中加载而无需调用服务。

### <a name="add-the-file-engine"></a>添加文件引擎

为了添加引擎，我们将返回用于加载配置文件的 promise/future 模式。 将使用 `mip::FileEngine` 创建引擎，而不是为 `mip::FileProfile` 创建 promise。

```cpp
  //auto profile will be std::shared_ptr<mip::FileProfile>
  auto profile = profileFuture.get();

  //Create the FileEngine::Settings object
  FileEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::FileEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::FileEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::FileEngine>
  auto engine = engineFuture.get();
```

上述代码的最终结果是将经过身份验证的用户的引擎添加到配置文件中。

## <a name="list-sensitivity-labels"></a>列出敏感度标签

现在可以使用添加的引擎通过调用 `engine->ListSensitivityLabels()` 来列出经过身份验证的用户可用的所有敏感度标签。

`ListSensitivityLabels()` 将从服务中提取特定用户的标签和标签属性列表。 结果存储在 `std::shared_ptr<mip::Label>` 的向量中。

请在[此处]()了解有关 `mip::Label` 的详细信息。

### <a name="listsensitivitylabels"></a>ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

或简化版：

```cpp
auto labels = engine->ListSensitivityLabels();
```

### <a name="print-the-labels-and-ids"></a>打印标签和 ID

通过打印名称可轻松证明我们已成功从服务中拉取策略并能够获得标签。 若要应用标签，需要标签标识符。 以下代码会循环访问所有标签，并显示每个父标签和子标签的 `name` 和 `id`。

```cpp
//Iterate through all labels in the vector
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

## <a name="next-steps"></a>后续步骤

现在已经加载了配置文件、添加了引擎，并且我们有了标签，接下来可以添加处理程序，开始从文件中读取、写入或删除标签。 请参阅 [MIP SDK 中的文件处理程序](concept-handler-file-cpp.md)。

