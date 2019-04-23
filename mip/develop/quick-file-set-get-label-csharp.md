---
title: 快速入门-Set 和 get 文件使用的敏感度标签C#MIP SDK
description: 快速入门教程演示如何使用 Microsoft 信息保护 SDK.NET 包装器来设置和获取文件的敏感度标签。
services: information-protection
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/09/2019
ms.author: mbaldwin
ms.openlocfilehash: 395c46ce1979b2ef670aa27e9329c5219ca63e13
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173217"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>快速入门：设置和获取敏感度标签 (C#)

本快速入门介绍如何使用更多的 MIP 文件 API。 使用上一个快速入门中列出的敏感度标签之一，可以使用文件处理程序对文件设置/获取标签。 文件处理程序类会公开设置/获取标签的各种操作，或受支持文件类型的保护。

## <a name="prerequisites"></a>先决条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 完整[快速入门：列出敏感度标签 (C#)](quick-file-list-labels-csharp.md)第一种方法生成初学者 Visual Studio 解决方案中，若要列出组织的敏感度标签。 此“设置和获取敏感度标签”快速入门基于前一个。
- 可选：审阅[MIP SDK 中文件处理程序](concept-handler-file-cpp.md)概念。

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>添加逻辑以设置和获取敏感度标签

使用文件引擎对象，添加逻辑以对文件设置和获取敏感度标签。 

1. 使用**解决方案资源管理器**，包含 main （） 的实现在项目中打开.cs 文件中方法。 它默认与包含它的项目同名，即在项目创建期间指定的名称。 

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
          ActionSource = ActionSource.Manual,
          AssignmentMethod = AssignmentMethod.Standard
     };

     // Set a label on input file
     handler.SetLabel(labelId, labelingOptions);

     // Commit changes, save as outputFilePath
     var result = Task.Run(async () => await handler.CommitAsync(outputFilePath)).Result;

     // Create a new handler to read the labeled file metadata
     var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, actualOutputFilePath, true)).Result;

     // Get the label from output file
     var contentLabel = handlerModified.Label;
     Console.WriteLine(string.Format("Getting the label committed to file: {0}", outputFilePath));
     Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", contentLabel.Label, contentLabel.IsProtectionAppliedFromLabel.ToString()));
     Console.WriteLine("Press a key to continue.");
     Console.ReadKey();
   ```

3. 使用以下值替换刚才粘贴的源代码中的占位符值：

   | 占位符 | ReplTest1 |
   |:----------- |:----- |
   | \<input-file-path\> | 测试输入文件的完整路径，例如：`c:\\Test\\Test.docx`。 |
   | \<label-id\> | 敏感度标签 ID，从上一快速入门中的控制台输出所复制，例如：`f42a3342-8706-4288-bd31-ebb85995028z`。 |
   | \<output-file-path\> | 输出文件的完整路径，它将是输入文件的标记副本，例如：`c:\\Test\\Test_labeled.docx`。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。 

1. 使用 CTRL-SHIFT-B (**生成解决方案**) 来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果你的项目成功生成和运行，应用程序*可能*提示进行身份验证通过 ADAL 每个时间的 SDK 调用你`AcquireToken()`方法。 如果存在缓存的凭据，不会提示您登录，并查看标签的列表后, 跟在应用的标签上的信息和修改文件。

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
