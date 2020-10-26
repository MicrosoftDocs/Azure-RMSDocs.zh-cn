---
title: 操作说明 - 重新发布场景（C#）
description: 本文将帮助你了解如何将保护处理程序重复用于场景的重新发布。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: c72d284363c1ca988692d18b7007a88c88d808b5
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2020
ms.locfileid: "91421105"
---
# <a name="microsoft-information-protection-sdk---file-api-republishing-quickstart-c"></a>Microsoft 信息保护 SDK - 文件 API 重新发布快速入门 (C#)

## <a name="overview"></a>概述

有关此方案及其使用场景的概述，请参阅[在 MIP SDK 中重新发布](concept-republishing.md)。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：设置/获取敏感度标签 (C#)](quick-file-set-get-label-csharp.md)，这可生成 Visual Studio 初学者解决方案（用于列出组织的敏感度标签），以便在文件中设置和读取敏感度标签。 本快速入门“操作说明 - 重新发布受保护的文件 - C#”以前一个快速入门为基础。
- 可选：查看 MIP SDK 概念中的[文件处理程序](concept-handler-file-cpp.md)。
- 可选：查看 MIP SDK 概念中的[保护处理程序](concept-handler-protection-cpp.md)。

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>添加逻辑，用于编辑并重新发布受保护的文件

1. 打开在前面的“快速入门：设置/获取敏感度标签 (C#)”一文中创建的 Visual Studio 解决方案。

2. 使用“解决方案资源管理器”，打开项目中包含 `Main()` 方法的实现的 .cs 文件。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

3. 在 `Main()` 正文的末尾，于 `Console.ReadKey()` 之下和应用程序关闭块之上（在上一快速入门中离开的位置），插入以下代码。

```csharp
string protectedFilePath = "<protected-file-path>" // Originally protected file's path from previous quickstart.

//Create a fileHandler for consumption for the Protected File.
var protectedFileHandler = Task.Run(async () => 
                            await fileEngine.CreateFileHandlerAsync(protectedFilePath,// inputFilePath
                                                                    protectedFilePath,// actualFilePath
                                                                    false, //isAuditDiscoveryEnabled
                                                                    null)).Result; // fileExecutionState

// Store protection handler from file
var protectionHandler = protectedFileHandler.Protection;

//Check if the user has the 'Edit' right to the file
if (protectionHandler.AccessCheck("Edit"))
{
    // Decrypt file to temp path
    var tempPath = Task.Run(async () => await protectedFileHandler.GetDecryptedTemporaryFileAsync()).Result;

    /*
        Your own application code to edit the decrypted file belongs here. 
    */

    /// Follow steps below for re-protecting the edited file. ///
    // Create a new file handler using the temporary file path.
    var republishHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(tempPath, tempPath, false)).Result;

    // Set protection using the ProtectionHandler from the original consumption operation.
    republishHandler.SetProtection(protectionHandler);

    // New file path to save the edited file
    string reprotectedFilePath = "<reprotected-file-path>" // New file path for saving reprotected file.

    // Write changes
    var reprotectedResult = Task.Run(async () => await republishHandler.CommitAsync(reprotectedFilePath)).Result;

    var protectedLabel = protectedFileHandler.Label;
    Console.WriteLine(string.Format("Originally protected file: {0}", protectedFilePath));
    Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", 
                        protectedLabel.Label.Id, 
                        protectedFileHandler.Protection.Owner, 
                        protectedLabel.IsProtectionAppliedFromLabel.ToString()));
    var reprotectedLabel = republishHandler.Label;
    Console.WriteLine(string.Format("Reprotected file: {0}", reprotectedFilePath));
    Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", 
                        reprotectedLabel.Label.Id, 
                        republishHandler.Protection.Owner, 
                        reprotectedLabel.IsProtectionAppliedFromLabel.ToString()));
    Console.WriteLine("Press a key to continue.");
    Console.ReadKey();
}
```

4. 在靠近 Main() 的末尾处，查找在上一篇快速入门中创建的应用程序关闭块，并在下方添加处理程序行以释放资源。

    ````csharp
        protectedFileHandler = null;
        protectionHandler = null;
    ````

5. 使用以下值替换源代码中的占位符值：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<protected-file-path\> | 上一篇快速入门中的受保护文件。 |
   | \<reprotected-file-path\> | 要重新发布的已修改文件的输出文件路径。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。

1. 使用 CTRL-SHIFT-B（“生成解决方案”）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireToken()` 方法时，应用程序都可能提示通过 ADAL 进行身份验证  。 如果已有缓存凭据，你就不会看到登录和查看标签列表的提示（后跟已应用标签和已修改文件的相关信息）。

  ```console
    Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
    Public : 73254501-3d5b-4426-979a-657881dfcb1e
    General : da480625-e536-430a-9a9e-028d16a29c59
    Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
    Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
    Press a key to continue.

    Getting the label committed to file: C:\Test\Test_protected.docx
    File Label: Confidential
    IsProtected: True
    Press a key to continue.
    Originally protected file: C:\Test\Test_protected.docx
    File LabelID: 569af77e-61ea-4deb-b7e6-79dc73653959
    ProtectionOwner: User1@Contoso.OnMicrosoft.com
    IsProtected: True
    Reprotected file: C:\Test\Test_reprotected.docx
    File LabelID: 569af77e-61ea-4deb-b7e6-79dc73653959
    ProtectionOwner: User1@Contoso.OnMicrosoft.com
    IsProtected: True
    Press a key to continue.
   ```