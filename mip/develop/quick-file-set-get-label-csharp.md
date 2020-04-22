---
title: 快速入门 - 使用 C# MIP SDK 对文件设置和获取敏感度标签
description: 一个演示如何使用 Microsoft 信息保护 SDK .NET 包装器对文件设置和获取敏感度标签的快速入门。
services: information-protection
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: c081d20ba3cfffdc1db06ade5d918230f3b9eff8
ms.sourcegitcommit: a3f901e479abbe056f8936a96b7253f0826d1415
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "75554984"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>快速入门：设置和获取敏感度标签 (C#)

本快速入门介绍如何使用更多的 MIP 文件 API。 使用上一个快速入门中列出的敏感度标签之一，可以使用文件处理程序对文件设置/获取标签。 文件处理程序类会公开设置/获取标签的各种操作，或受支持文件类型的保护。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：列出敏感度标签 (C#)](quick-file-list-labels-csharp.md)，这可生成 Visual Studio 初学者解决方案，以列出组织的敏感度标签。 此“设置和获取敏感度标签”快速入门基于前一个。
- 可选：查看 [MIP SDK 中的文件句柄](concept-handler-file-cpp.md)概念。

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>添加逻辑以设置和获取敏感度标签

使用文件引擎对象，添加逻辑以对文件设置和获取敏感度标签。 

1. 使用“解决方案资源管理器”，打开项目中包含 Main()` 方法的实现的 .cs 文件  。 它默认与包含它的项目同名，即在项目创建期间指定的名称。 

2. 在 `Main()` 正文的末尾，在 `Console.ReadKey()` 下面并在 `}` 上面（在上一快速入门中离开的位置），插入以下代码：

   ```csharp
     //Set paths and label ID
     string inputFilePath = "<input-file-path>";
     string actualFilePath = inputFilePath;
     string labelId = "<label-id>";
     string outputFilePath = "<output-file-path>";
     string actualOutputFilePath = outputFilePath;

     //Create a file handler for that file
     //Note: the 2nd inputFilePath is used to provide a human-readable content identifier for admin auditing. 
     var handler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(inputFilePath, actualFilePath, true)).Result;

     //Set Labeling Options
     LabelingOptions labelingOptions = new LabelingOptions()
     {
          AssignmentMethod = AssignmentMethod.Standard
     };

     // Set a label on input file
     handler.SetLabel(engine.GetLabelById(labelId), labelingOptions, new ProtectionSettings());

     // Commit changes, save as outputFilePath
     var result = Task.Run(async () => await handler.CommitAsync(outputFilePath)).Result;

     // Create a new handler to read the labeled file metadata
     var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, actualOutputFilePath, true)).Result;

     // Get the label from output file
     var contentLabel = handlerModified.Label;
     Console.WriteLine(string.Format("Getting the label committed to file: {0}", outputFilePath));
     Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", contentLabel.Label.Name, contentLabel.IsProtectionAppliedFromLabel.ToString()));
     Console.WriteLine("Press a key to continue.");
     Console.ReadKey();
   ```

3. 在靠近 `Main()` 的末尾处，查找在第一个快速入门中创建的应用程序关闭块，并取消注释处理程序行：

   ```csharp
   // Application Shutdown
   handler = null;
   fileEngine = null;
   fileProfile = null;
   mipContext = null;
   ```

4. 使用以下值替换源代码中的占位符值：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<input-file-path\> | 测试输入文件的完整路径，例如：`c:\\Test\\Test.docx`。 |
   | \<label-id\> | 敏感度标签 ID，从上一快速入门中的控制台输出所复制，例如：`f42a3342-8706-4288-bd31-ebb85995028z`。 |
   | \<output-file-path\> | 输出文件的完整路径，它将是输入文件的标记副本，例如：`c:\\Test\\Test_labeled.docx`。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。 

1. 使用 CTRL-SHIFT-B（“生成解决方案”）来生成客户端应用程序  。 如果没有生成错误，请使用 F5（开始调试  ）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireToken()` 方法时，应用程序都可能提示通过 ADAL 进行身份验证  。 如果已有缓存凭据，你就不会看到登录和查看标签列表的提示（后跟已应用标签和已修改文件的相关信息）。

  ```console   
  Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
  Public : 73254501-3d5b-4426-979a-657881dfcb1e
  General : da480625-e536-430a-9a9e-028d16a29c59
  Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
        Recipients Only (C) : d98c4267-727b-430e-a2d9-4181ca5265b0
        All Employees (C) : 2096f6a2-d2f7-48be-b329-b73aaa526e5d
        Anyone (not protected) (C) : 63a945ec-1131-420d-80da-2fedd15d3bc0
  Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
        Recipients Only : 05ee72d9-1a75-441f-94e2-dca5cacfe012
        All Employees : 922b06ef-044b-44a3-a8aa-df12509d1bfe
        Anyone (not protected) : c83fc820-961d-40d4-ba12-c63f72a970a3
  Press a key to continue.

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes
   
   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .
  
   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

可以通过打开输出文件，并直观地检查文档的信息保护设置来验证标签的应用。

> [!NOTE]
> 如果要标记 Office 文档，但未使用获取访问令牌的 Azure Active Directory (AD) 租户中的帐户登录（并且配置了敏感度标签），则可能会提示先登录，然后才能打开标记的文档。 
