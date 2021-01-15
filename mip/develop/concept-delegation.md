---
title: 概念-委托
description: 本文将帮助你了解有关 MIP SDK 中的委托的概念。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 848b0752f6158ade4fd61b562163e2e641454773
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224902"
---
# <a name="concept---delegation-in-the-mip-sdk"></a>概念-MIP SDK 中的委托

Microsoft 信息保护 SDK 为基于服务的应用程序提供了两个路径，以代表其他用户执行操作。 如果需要在不同于服务标识的用户标识上下文中标记、保护或使用文件，则可能需要进行委派。 可以在 **引擎** 或 **处理程序** 级别设置此委托标识，并在其中设置它将取决于用例。

## <a name="engine-settings-based-delegation"></a>基于引擎设置的委派

MIP SDK 支持在所有 Sdk 的 settings 对象中提供委托用户电子邮件地址;文件、保护和策略。 这可以通过设置 `DelegatedUserEmail` 设置对象上的属性来实现。 结果是，用该设置对象初始化的引擎将执行 **所有 MIP 操作** ，就像它是提供给属性的用户一样 `DelegatedUserEmail` 。 将为该特定用户提取策略，并以该用户的身份执行所有保护操作，包括受保护文件的所有者。

如果基于服务的应用程序需要完全以用户身份运行，则此模式很有用;只需为指定用户提取策略，并需要在用户标识的上下文中执行任何解密操作。 创建此引擎时，应用程序指定了唯一的引擎 ID （通常是邮件地址），这一点很重要。 这可以确保实现缓存的好处。 如果未提供唯一的引擎 ID，你的应用程序可能会遇到性能不佳的情况。

### <a name="file-sdk"></a>文件 SDK

下面的示例演示如何在 c + + 和 c # 中设置文件 SDK 应用程序的委托标识。 此模式可用于策略 SDK。

此示例演示如何在 .NET 中的文件 SDK 中创建 **委托引擎** 。

```csharp
// C# Example for creating a delegated file engine
string delegatedUserEmail = "alice@contoso.com";
var engineSettings = new PolicyEngineSettings(delegatedUserEmail, authDelegate, "", "en-US")
{
    // Provide the identity for service discovery.
    Identity = identity,
    // Set the identity for which all MIP operations will be performed.
    DelegatedUserEmail = delegatedUserEmail
};

var engine = Task.Run(async () => await profile.AddEngineAsync(engineSettings)).Result;
```

此示例演示如何在 c + + 的文件 SDK 中创建 **委托引擎** 。

```c++
// C++ Example for creating a delegated file engine
std::string delegatedUserEmail = "alice@contoso.com";
FileEngine::Settings engineSettings(delegatedUserEmail, mAuthDelegate, "", "en-US", false);
// Set the identity for which all MIP operations will be performed. 
engineSettings.SetDelegatedUserEmail(delegatedUserEmail);

auto enginePromise = std::make_shared<std::promise<std::shared_ptr<FileEngine>>>();
auto engineFuture = enginePromise->get_future();

mProfile->AddEngineAsync(engineSettings, enginePromise);
mEngine = engineFuture.get();
```

结果就是将代表指定用户创建所有文件引擎。


## <a name="handler-based-delegation"></a>基于处理程序的委托

在只需要 **保护** 特定用户标识的上下文中的文件的方案中， `FileHandler` 提供通过对象传递用户标识的方法 `ProtectionSettings` 。 策略和任何解密操作将作为经过身份验证的 **服务标识** 来执行。 将代表指定用户执行保护操作;该用户将成为该文档的 MIP protection 的 **所有者** 。

### <a name="file-sdk"></a>文件 SDK

仅当用户提供给对象时，才会执行直接或通过标签来应用保护的操作 `ProtectionSettings` 。 此对象将传递给 `SetLabel()` `SetProtection()` File SDK 中的或函数。

此示例演示如何在 .NET 中的文件 SDK 中执行 **委托保护操作** 。

```csharp
string delegatedUserEmail = "bob@contoso.com";
ProtectionSettings protectionSettings = new ProtectionSettings()
{
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};
handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, protectionSettings);
// Similar pattern for SetProtection()
// handler.SetProtection(protectionDescriptor, protectionSettings);
```

此示例演示如何在 c + + 的文件 SDK 中执行 **委托保护操作** 。

```c++
mip::ProtectionSettings protectionSettings;
// Set the delegated mail address 
protectionSettings.SetDelegatedUserEmail(delegatedUserEmail);
handler->SetLabel(mEngine->GetLabelById(labelId), labelingOptions, protectionSettings);
```

结果就是，应用保护的所有处理程序 **写入** 操作都将作为委托用户执行。 

### <a name="protection-sdk"></a>保护 SDK

保护 SDK 的功能与文件 SDK 不同。 可创建 **两种类型的处理程序** ，一个用于发布，一个用于使用。 与文件 SDK 类似，委托的邮件地址是通过每种类型的处理程序的 settings 对象设置的。

#### <a name="net"></a>.NET

此示例演示如何执行 **委托发布**。

```csharp
string delegatedUserEmail = "bob@contoso.com";
PublishingSettings publishingSettings = new PublishingSettings(protectionDescriptor)
{
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};          
var protectionHandler = engine.CreateProtectionHandlerForPublishing(publishingSettings);
```

此示例演示如何执行 **委托消耗**。

```csharp
string delegatedUserEmail = "bob@contoso.com";
ConsumptionSettings consumptionSettings = new ConsumptionSettings(plInfo)
{                
    ContentName = "A few bytes.",
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};
var protectionHandler = engine.CreateProtectionHandlerForConsumption(consumptionSettings);
```

#### <a name="c"></a>C++

此示例演示如何执行 **委托消耗**。

```c++
string delegatedUserEmail = "bob@contoso.com";
mip::ProtectionHandler::PublishingSettings publishingSettings = mip::ProtectionHandler::PublishingSettings(descriptor);
// Set the delegated mail address 
publishingSettings.SetDelegatedUserEmail(delegatedUserEmail);
mEngine->CreateProtectionHandlerForPublishingAsync(publishingSettings, handlerObserver, handlerPromise);
auto handler = handlerFuture.get(); 
```

此示例演示如何执行 **委托发布**。

```c++
string delegatedUserEmail = "bob@contoso.com";
mip::ProtectionHandler::ConsumptionSettings consumptionSettings = mip::ProtectionHandler::ConsumptionSettings(serializedPublishingLicense);
// Set the delegated mail address 
consumptionSettings.SetDelegatedUserEmail(delegatedUserEmail);
mEngine->CreateProtectionHandlerForConsumptionAsync(consumptionSettings, handlerObserver, handlerPromise);
auto handler = handlerFuture.get(); 
```

## <a name="required-permissions"></a>所需的权限

上述每种方案都需要一组不同的权限。 

| 方案                             | 所需的权限                                                             |
| ------------------------------------ | ------------------------------------------------------------------------------- |
| 文件 SDK 委托引擎            | UnifiedPolicy。读取<br>DelegatedReader<br>DelegatedWriter |
| 策略 SDK 委托引擎          | UnifiedPolicy。读取                                                       |
| 文件 SDK 委托处理程序           | DelegatedWriter                                                         |
| 保护 SDK 委托发布     | DelegatedWriter                                                         |
| 保护 SDK 委托消耗 | DelegatedReader                                                         |

若要全面了解权限以及在何处设置权限，请参阅 [Microsoft Information PROTECTION SDK 的 API 权限](concept-api-permissions.md)

## <a name="next-steps"></a>后续步骤

- 查看 [Microsoft 信息保护 SDK 的 API 权限](concept-api-permissions.md)
- 查看 <TODO> 添加服务主体身份验证参考。