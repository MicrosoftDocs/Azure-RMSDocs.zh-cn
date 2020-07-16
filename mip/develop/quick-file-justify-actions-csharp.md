---
title: '如何降级/删除需要理由的标签（c #）'
description: 本文可帮助你了解如何降级或删除需要理由的标签。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 88c55d973dde25e1571750e51e36f5fa726770f5
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86403215"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>Microsoft 信息保护 SDK 文件 API-在文件上降低敏感度标签的操作理由（c #）

此快速入门介绍了当标签策略需要理由时对降级标签操作的处理。在这里，我们将使用 `IFileHandler` 接口来更改文件的标签。 有关更多详细信息，请参阅 [API 参考](/dotnet/api/?term=microsoft.informationprotection)。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 完成[快速入门：设置/获取灵敏度标签（c #）](quick-file-set-get-label-csharp.md) ，它生成一个 Starter Visual Studio 解决方案来列出组织的敏感度标签，并对文件设置和读取敏感度标签。 这会 "如何降级/删除需要论证 c # 的标签" 快速入门版本。
- 可选：查看 MIP SDK 概念中的[文件处理程序概念](concept-handler-file-cpp.md)。

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>添加逻辑，向受保护的文件设置级别较低的标签

添加逻辑以使用文件处理程序对象设置文件的敏感度标签。

1. 打开在前面的 "快速入门：设置/获取灵敏度标签（c #）" 中创建的 Visual Studio 解决方案。

2. 使用“解决方案资源管理器”，打开项目中包含 `Main()` 方法的实现的 .cs 文件。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

3. 将以前的快速入门中的 `<label-id>` 值更新为需要降级理由的敏感度标签。 在此快速入门中，首先设置此标签，然后尝试在后续步骤中通过代码片段降低此标签的级别。

4. 在正文的末尾 `Main()` ， `Console.ReadKey()` 在应用程序关闭块的下方和上方（在前面的快速入门中，你离开了），插入以下代码。

    ```csharp
    //Set paths and label ID
    string lowerInput = actualOutputFilePath;
    string lowerActualInput = lowerInput;
    string newLabelId = "<new-label-id>";
    string lowerOutput = "<downgraded-labled-output>";
    string lowerActualOutput = lowerOutput;

    //Create a file handler for that file
    var downgradeHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(lowerInput, lowerActualInput, true)).Result;

    //Set Labeling Options
    LabelingOptions options = new LabelingOptions()
    {
        AssignmentMethod = AssignmentMethod.Standard
    };

    try
    {
        //Try to set new label
        downgradeHandler.SetLabel(fileEngine.GetLabelById(newLabelId), options, new ProtectionSettings());
    }

    catch (Microsoft.InformationProtection.Exceptions.JustificationRequiredException)
    {
        //Request justification from user
        Console.Write("Please provide justification for downgrading a label: ");
        string justification = Console.ReadLine();

        options.IsDowngradeJustified = true;
        options.JustificationMessage = justification;

        //Set new label
        downgradeHandler.SetLabel(fileEngine.GetLabelById(newLabelId), options, new ProtectionSettings());
    }

    // Commit changes, save as outputFilePath
    var downgradedResult = Task.Run(async () => await downgradeHandler.CommitAsync(lowerActualOutput)).Result;

    // Create a new handler to read the labeled file metadata
    var commitHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(lowerOutput, lowerActualOutput, true)).Result;

    // Get the label from output file
    var newContentLabel = commitHandler.Label;
    Console.WriteLine(string.Format("Getting the new label committed to file: {0}", lowerOutput));
    Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", newContentLabel.Label.Name, newContentLabel.IsProtectionAppliedFromLabel.ToString()));
    Console.WriteLine("Press a key to continue.");
    Console.ReadKey();

    ```

5. 对于 Main （）的末尾，查找在上一个快速入门中创建的应用程序关闭块，并添加下面的处理程序行以释放资源。

    ````csharp
    downgradeHandler = null;
    commitHandler = null;
    ````

6. 使用以下值替换源代码中的占位符值：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<downgraded-labled-output\> | 保存修改后的文件的输出文件路径。 |
   | \<new-label-id\> | 从前面的快速入门中的控制台输出复制的模板 ID，例如： `bb7ed207-046a-4caf-9826-647cff56b990` 。 确保与之前受保护的文件标签相比，它的敏感度更低。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。

1. 使用 CTRL-SHIFT-B（“生成解决方案”）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireToken()` 方法时，应用程序都可能提示通过 ADAL 进行身份验证**。 如果已有缓存凭据，你就不会看到登录和查看标签列表的提示（后跟已应用标签和已修改文件的相关信息）。

  ```console
    Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
    Public : 73254501-3d5b-4426-979a-657881dfcb1e
    General : da480625-e536-430a-9a9e-028d16a29c59
    Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
    Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
    Press a key to continue.

    Getting the label committed to file: c:\Test\Test_labeled.docx
    Name: Confidential
    IsProtected: True
    Press any key to continue . . .

    Please provide justification for downgrading a label: Lower label approved.
    Getting the new label committed to file: c:\Test\Test_downgraded.docx
    File Label: General
    IsProtected: False
    Press a key to continue.
   ```

请注意，类似的方法也适用于 `DeleteLabel()` 操作，在从文件中删除标签时，需要根据每个标签策略进行调整。`DeleteLabel()` `JustificationRequiredException` `IsDowngradeJustified` 在成功删除标签之前，函数将引发异常并将标志设置为 true。