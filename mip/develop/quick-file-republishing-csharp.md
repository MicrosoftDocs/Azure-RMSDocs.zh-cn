---
title: 如何重新发布方案 C#
description: 本文将帮助你了解如何为重新发布方案重复使用保护处理程序的方案。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: d82424c03fe8c2e050bbd4095706fa675de5ed6e
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548201"
---
# <a name="microsoft-information-protection-sdk---file-api-re-publishing-quickstart-c"></a>Microsoft 信息保护 SDK-文件 API 重新发布快速入门（c #）

## <a name="overview"></a>概述

有关此方案及其使用位置的概述，请参阅[MIP SDK 中](concept-republishing-cpp.md)的重新发布。

## <a name="prerequisites"></a>先决条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 完成[快速入门：首先设置/获取灵敏度标签（c #）](quick-file-set-get-label-csharp.md) ，它将构建一个 Starter Visual Studio 解决方案，以列出组织的敏感度标签，以便在文件中设置和读取敏感度标签。 这是在上一个版本中的 "如何重新发布受保护的文件-c #" 快速入门。
- （可选）：查看 MIP SDK 概念中的[文件处理程序](concept-handler-file-cpp.md)。
- （可选）：在 MIP SDK 概念中查看[保护处理程序](concept-handler-protection-cpp.md)。

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>添加逻辑以编辑并重新发布受保护的文件

1. 打开在前面的 "快速入门：设置/获取敏感性标签（c #）" 一文中创建的 Visual Studio 解决方案。

2. 使用解决方案资源管理器在项目中打开 .cs 文件，其中包含方法的实现 `Main()` 。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

3. 在正文的末尾 `Main()` ， `Console.ReadKey()` 在应用程序关闭块的下方和上方（在前面的快速入门中，你离开了），插入以下代码。

    ```csharp

        string protectedFilePath = "<protected-file-path>" // Originally protected file's path from previous quickstart.

            //Create a fileHandler for consumption for the Protected File.
            var protectedFileHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(protectedFilePath,// inputFilePath
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

                /// Write code here to perform further operations for edit ///

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
                Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", protectedLabel.Label.Id, protectedFileHandler.Protection.Owner, protectedLabel.IsProtectionAppliedFromLabel.ToString()));
                var reprotectedLabel = republishHandler.Label;
                Console.WriteLine(string.Format("Reprotected file: {0}", reprotectedFilePath));
                Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", reprotectedLabel.Label.Id, republishHandler.Protection.Owner, reprotectedLabel.IsProtectionAppliedFromLabel.ToString()));
                Console.WriteLine("Press a key to continue.");
                Console.ReadKey();

            }

    ```

4. 在 Main （）的末尾找到在前面的快速入门中创建的应用程序关闭块，并添加下面的处理程序行以释放资源。

    ````csharp
        protectedFileHandler = null;
        protectionHandler = null;

    ````

5. 使用以下值替换源代码中的占位符值：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<protected-file-path\> | 以前的快速入门中的受保护文件。 |
   | \<reprotected-file-path\> | 要重新发布的已修改文件的输出文件路径。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。

1. 使用 CTRL-SHIFT-B（“生成解决方案”）来生成客户端应用程序****。 如果没有生成错误，请使用 F5（开始调试****）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireToken()` 方法时，应用程序都可能提示通过 ADAL 进行身份验证**。 如果已有缓存凭据，你就不会看到登录和查看标签列表的提示（后跟已应用标签和已修改文件的相关信息）。

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