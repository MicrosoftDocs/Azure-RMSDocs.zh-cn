---
title: 'Microsoft 信息保护 SDK c # 包装概述'
description: 有关如何开始使用 MIP SDK .NET 包装的简要概述，以及 .NET 包装与 c + + SDK 之间的差异。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: da563bc385658d716d6813710495d91b42bbcc83
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "95566041"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Microsoft 信息保护 .NET 包装入门

Microsoft 信息保护 SDK .NET 包装使开发人员能够将 Microsoft 信息保护体验集成到他们自己的应用程序和服务中。 SDK 的分类、标签和保护功能有助于确保无论信息在何处进行分类、标记和保护。 

可以通过 Visual Studio 中的 NuGet 安装托管包装和所有依赖项。

## <a name="supported-platforms"></a>支持的平台

Microsoft 信息保护 .NET 包装程序在以下 .NET 平台上受支持：

* .NET Standard 2.0
* .NET 4。0

## <a name="installing-the-package"></a>安装包

在 Visual Studio 2017 的包管理器控制台中，通过运行以下内容来安装包：

`install-package Microsoft.InformationProtection.File`

不需要任何其他包。 所有第三方库都包含在内，并将在生成时复制到输出文件夹。

## <a name="wrapper-details"></a>包装器详细信息

.NET 包装是 [SWIG](https://swig.org/) 生成的托管包装器。 包装器使用 Microsoft 信息保护 SDK 中的编译的 c + + 库。 这些 Dll 与 c + + 版本的 SDK 中包含的 Dll 相同。

## <a name="concept-overlap"></a>概念重叠

SDK 的 c + + 版本和托管包装之间存在一些基本差异。

* .NET 包装不需要使用观察程序进行异步操作。 所有异步操作都是通过 [基于任务的异步模式](/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap)实现的。
* .NET 包装需要属于 c + + SDK 的委托： AuthDelegate 和 ConsentDelegate。 这些委托通过接口实现 `IAuthDelegate` 并 `IConsentDelegate`

## <a name="next-steps"></a>后续步骤

接下来，查看 [Microsoft 信息保护的快速入门-初始化 (MIP) SDK c #](quick-app-initialization-csharp.md) ，开始生成启用了 MIP 的基本控制台应用程序。