---
title: 概念 - 保护 API 引擎对象
description: 本文将帮助你了解在应用程序初始化期间创建的保护引擎对象的概念。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 1ccfc81e4b45c6ec4e4316b748d9ccc0f73561a4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886030"
---
# <a name="microsoft-information-protection-sdk---protection-api-engine-concepts"></a>Microsoft 信息保护 SDK - 保护 API 引擎概念

## <a name="implementation-add-a-protection-engine"></a>部署添加保护引擎

在文件 API 中，`mip::ProtectionProfile` 类是所有 SDK 操作的根类。 在创建了配置文件后，我们现在可以向配置文件添加引擎。

以下示例演示如何为经过身份验证的单个用户使用单个引擎。

### <a name="implementation-create-protection-engine-settings"></a>部署创建保护引擎设置

与配置文件类似，引擎也需要设置对象 `mip::ProtectionEngine::Settings`。 此对象存储唯一引擎标识符、可用于调试或遥测的可自定义客户端数据以及（可选）区域设置。

在这里，我们创建一个名为 *engineSettings* 的 `ProtectionEngine::Settings` 对象。 

```cpp
ProtectionEngine::Settings engineSettings("UniqueID", "");
```

> [!NOTE]
> 如果使用此方法创建保护设置对象, 则还必须手动将 CloudEndpointBaseUrl 设置为 https://api.aadrm.com 或 tp Active Directory Rights Management Service 群集 URL。

作为最佳做法，第一个参数 **id** 应该允许引擎轻松连接到关联用户**或** `mip::Identity` 对象。 若要使用 `mip::Identity` 初始化设置，请运行以下代码：

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity("Bob@Contoso.com", "");
```

### <a name="implementation-add-the-protection-engine"></a>部署添加保护引擎

为了添加引擎，我们将返回用于加载配置文件的 future/promise 模式。 我们将使用 `mip::ProtectionEngine`，而不是为 `mip::ProtectionProfile` 创建 promise。

```cpp

  //auto profile will be std::shared_ptr<mip::ProtectionProfile>
  auto profile = profileFuture.get();

  //Create the ProtectionEngine::Settings object
  ProtectionEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::ProtectionEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::ProtectionEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::ProtectionEngine>
  auto engine = engineFuture.get();
```

上述代码的最终结果是我们成功地将经过身份验证的用户的引擎添加到配置文件中。

## <a name="implementation-list-templates"></a>部署列出模板

现在可以使用添加的引擎通过调用 `engine->GetTemplatesAsync()` 来列出经过身份验证的用户可用的所有敏感度模板。 

`GetTemplatesAsync()` 将提取模板标识符列表。 结果存储在 `std::shared_ptr<std::string>` 的向量中。

### <a name="implementation-listsensitivitytemplates"></a>部署ListSensitivityTemplates()

```cpp
auto loadPromise = std::make_shared<std::promise<shared_ptr<vector<string>>>>();
std::future<std::shared_ptr<std::vector<std::string>>> loadFuture = loadPromise->get_future();
mEngine->GetTemplatesAsync(engineObserver, loadPromise);
auto templates = loadFuture.get();
```

### <a name="implementation-print-the-template-ids"></a>部署打印模板 Id

```cpp
//Iterate through all template IDs in the vector
for (const auto& temp : *templates) {
  cout << "Template:" << "\n\tId: " << temp << endl;
}
```

通过打印名称可轻松证明我们已成功从服务中拉取策略并能够获得模板。 若要应用模板，需要模板标识符。

只能通过检查 `ComputeActions()` 的结果，使用策略 API 将模板映射到标签。

## <a name="next-steps"></a>后续步骤

现在已经加载了配置文件、添加了引擎，并且我们有了模板，接下来可以添加处理程序，开始从文件中读取、写入或删除模板。 请参阅[保护处理程序概念](concept-handler-protection-cpp.md)。
