---
title: Microsoft 信息保护 SDKC#包装器概述
description: 有关如何开始使用 MIP SDK.NET 包装器，以及.NET 包装器之间的差异的快速概述和C++SDK。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: 6b2f26a61cd491574fd9f4a1e74fbfab4752257a
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60175175"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>开始使用 Microsoft 信息保护.NET 包装

Microsoft 信息保护 SDK.NET 包装器使开发人员能够将集成到其自己的应用程序和服务中的 Microsoft 信息保护体验。 SDK 的分类、 标记和保护功能可帮助您确保信息分类标记，并保护，无论其中间传递。 

可以通过 Visual Studio 中的 NuGet 安装的托管的包装和所有依赖项。

## <a name="supported-platforms"></a>支持的平台

以下.NET 平台上支持 Microsoft 信息保护.NET 包装器：

* .NET Standard 2.0
* .NET 4.0

## <a name="installing-the-package"></a>安装包

从 Visual Studio 2017 中的包管理器控制台中，通过运行安装包：

`install-package Microsoft.InformationProtection.File`

任何其他包不是必需的。 第三方库的所有包含，并且会将复制到生成的输出文件夹。

## <a name="wrapper-details"></a>包装器的详细信息

.NET 包装是否[SWIG](https://swig.org/)生成的托管的包装。 编译该包装器使用C++通过 Microsoft 信息保护 SDK 库。 这些 Dll 均附带的相同 DllC++版本的 SDK。

## <a name="concept-overlap"></a>概念重叠

有几个基本区别C++版本的 SDK 和托管的包装。

* .NET 包装器不需要使用观察者来异步操作。 通过实现任何异步操作[基于任务的异步模式](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap)。
* .NET 包装需要属于委托C++SDK:AuthDelegate 和 ConsentDelegate。 这些委托通过接口实现`IAuthDelegate`和 `IConsentDelegate`

## <a name="next-steps"></a>后续步骤

接下来，审阅[快速入门-初始化为 Microsoft 信息保护 (MIP) SDK C# ](quick-app-initialization-csharp.md)若要开始构建一个基本的启用 MIP 的控制台应用程序。
