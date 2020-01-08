---
title: Microsoft 信息保护 SDK C#包装概述
description: 简要概述如何开始使用 MIP SDK .NET 包装，以及 .NET 包装与C++ SDK 之间的差异。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: 21fc590388615b2917ca62fdd848b3a63ce26912
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556106"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Microsoft 信息保护 .NET 包装入门

Microsoft 信息保护 SDK .NET 包装使开发人员能够将 Microsoft 信息保护体验集成到他们自己的应用程序和服务中。 SDK 的分类、标签和保护功能有助于确保无论信息在何处进行分类、标记和保护。 

可以通过 Visual Studio 中的 NuGet 安装托管包装和所有依赖项。

## <a name="supported-platforms"></a>支持的平台

Microsoft 信息保护 .NET 包装程序在以下 .NET 平台上受支持：

* .NET Standard 2.0
* .NET 4.0

## <a name="installing-the-package"></a>安装包

在 Visual Studio 2017 的包管理器控制台中，通过运行以下内容来安装包：

`install-package Microsoft.InformationProtection.File`

不需要任何其他包。 所有第三方库都包含在内，并将在生成时复制到输出文件夹。

## <a name="wrapper-details"></a>包装器详细信息

.NET 包装是[SWIG](https://swig.org/)生成的托管包装器。 包装器使用 Microsoft C++信息保护 SDK 中的已编译库。 这些 Dll 与 SDK C++版本中包含的 dll 相同。

## <a name="concept-overlap"></a>概念重叠

SDK C++版本和托管包装之间存在一些基本差异。

* .NET 包装不需要使用观察程序进行异步操作。 所有异步操作都是通过[基于任务的异步模式](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap)实现的。
* .NET 包装确实需要作为C++ SDK 的一部分的委托： AuthDelegate 和 ConsentDelegate。 这些委托通过 `IAuthDelegate` 和 `IConsentDelegate` 接口实现

## <a name="next-steps"></a>后续步骤

接下来，查看[Microsoft 信息保护（MIP） SDK C#快速入门-初始化](quick-app-initialization-csharp.md)，开始生成启用了 MIP 的基本控制台应用程序。
