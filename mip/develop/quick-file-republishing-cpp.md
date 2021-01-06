---
title: 操作说明 - 重新发布场景（C++）
description: 本文将帮助你了解如何将保护处理程序重复用于场景的重新发布 (C++)。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 05/01/2020
ms.author: mbaldwin
ms.openlocfilehash: 657a8a3e7650b8afb8c4d8384fc078e48eb64f36
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865223"
---
# <a name="file-api-re-publishing-quickstart-c"></a>文件 API 重新发布快速入门 (C++)

## <a name="overview"></a>概述

有关此方案及其使用场景的概述，请参阅[在 MIP SDK 中重新发布](concept-republishing.md)。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：设置/获取敏感度标签 (C++)](quick-file-set-get-label-cpp.md)，这可生成 Visual Studio 初学者解决方案（用于列出组织的敏感度标签），以便在文件中设置和读取敏感度标签。 本快速入门“操作说明 - 降级/删除需要理由的标签 C++”建立在前一篇快速入门的基础之上。
- 可选：查看 MIP SDK 概念中的[文件处理程序](concept-handler-file-cpp.md)。
- 可选：查看 MIP SDK 概念中的[保护处理程序](concept-handler-protection-cpp.md)。

## <a name="add-logic-to-filehandler-observer-class"></a>向 FileHandler Observer 类添加逻辑

为了能够使用 `mip::FileHandler` 公开的 `GetDecryptedTemporaryFileAsync()` 方法来解密受保护的文件，必须按如下所示定义成功和失败的异步方法回调。

1. 打开在前面的“快速入门：设置/获取敏感度标签 (C++)。

2. 使用解决方案资源管理器打开项目中的 `filehandler_observer.h` 文件。 在 FileHandler 定义的末尾，在 `};` 之前添加以下行，用于方法声明。

    ```cpp
        void OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr<void>& context) override;
        void OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
    ```

3. 使用解决方案资源管理器打开项目中的 `filehandler_observer.cpp` 文件。 在该文件的末尾，添加以下行，用于方法定义。

    ```cpp

        void FileHandlerObserver::OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::string>>(context);
        promise->set_value(decryptedFilePath);
        }

        void FileHandlerObserver::OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::string>>(context);
        promise->set_exception(error);
        }
    ```

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>添加逻辑，用于编辑并重新发布受保护的文件

1. 使用“解决方案资源管理器”，打开项目中包含 `main()` 方法的实现的 .cpp 文件。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

2. 在 main() 正文的末尾，于 system("pause"); 之下和 return 0; 之上（在上一快速入门中离开的位置），插入以下代码：

```cpp
//Originally protected file's path.
std::string protectedFilePath = "<protected-file-path>";

// Create file handler for the file
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
auto handlerFuture = handlerPromise->get_future();
engine->CreateFileHandlerAsync(protectedFilePath, 
                                protectedFilePath, 
                                true, 
                                std::make_shared<FileHandlerObserver>(), 
                                handlerPromise);
auto protectedFileHandler = handlerFuture.get();

// retieve and store protection handler from file
auto protectionHandler = protectedFileHandler->GetProtection();

//Check if the user has the 'Edit' right to the file and if so decrypt the file.
if (protectionHandler->AccessCheck("Edit")) {

    // Decrypt file to temp path using the same file handler
    auto tempPromise = std::make_shared<std::promise<string>>();
    auto tempFuture = tempPromise->get_future();
    protectedFileHandler->GetDecryptedTemporaryFileAsync(tempPromise);
    auto tempPath = tempFuture.get();

    /// Write code here to perform further operations for edit ///

    /// Follow steps below for re-protecting the edited file ///

    // Create a new file handler using the temporary file path.
    auto reprotectPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto reprotectFuture = reprotectPromise->get_future();
    engine->CreateFileHandlerAsync(tempPath, 
                                    tempPath, 
                                    true, 
                                    std::make_shared<FileHandlerObserver>(), 
                                    reprotectPromise);
    auto republishHandler = reprotectFuture.get();

    // Set protection using the ProtectionHandler from the original consumption operation.
    republishHandler->SetProtection(protectionHandler);
    std::string reprotectedFilePath = "<protected-file-path>";

    // Commit changes
    auto republishPromise = std::make_shared<std::promise<bool>>();
    auto republishFuture = republishPromise->get_future();
    republishHandler->CommitAsync(reprotectedFilePath, republishPromise);

    // Validate republishing
    cout << "Protected File: " + protectedFilePath<<endl;
    cout << "Protected Label ID: " + protectedFileHandler->GetLabel()->GetLabel()->GetId() << endl;
    cout << "Protection Owner: " + protectedFileHandler->GetProtection()->GetOwner() << endl<<endl;

    cout << "Republished File: " + reprotectedFilePath<<endl;
    cout << "Republished Label ID: " + republishHandler->GetLabel()->GetLabel()->GetId() << endl;
    cout << "Republished Owner: " + republishHandler->GetProtection()->GetOwner() << endl;
}
```

3. 在靠近 Main() 的末尾处，查找在上一篇快速入门中创建的应用程序关闭块，并在下方添加处理程序行以释放资源。

    ````csharp
        protectedFileHandler = nullptr;
        protectionHandler = nullptr;

    ````

4. 使用以下值替换源代码中的占位符值：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<protected-file-path\> | 上一篇快速入门中的受保护文件。 |
   | \<reprotected-file-path\> | 要重新发布的已修改文件的输出文件路径。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。

1. 使用 CTRL-SHIFT-B（“生成解决方案”）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireOAuth2Token()` 方法时，应用程序都会提示输入访问令牌。 如先前在“设置/获取敏感度标签”快速入门中采取的方式那样，每次使用提供的 $authority 和 $resourceUrl 值运行 PowerShell 脚本以获取令牌。

  ```console   
    Sensitivity labels for your organization:
    Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
    Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
    General : f42a3342-8706-4288-bd31-ebb85995028z
    Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
    Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to C:\Test\Test.docx
    Committing changes
    
    Label committed to file: C:\Test\Test_labeled.docx
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Getting the label committed to file: C:\Test\Test_labeled.docx
    Name: Confidential
    Id: 074e457c-5848-4542-9a6f-34a182080e7z
    Press any key to continue . . .
    Protected File: C:\Test\Test_labeled.docx
    Protected Label ID: 074e457c-5848-4542-9a6f-34a182080e7z
    Protection Owner: user1@tenant.onmicrosoft.com

    Republished File: c:\Test\Test_republished.docx
    Republished Label ID: 074e457c-5848-4542-9a6f-34a182080e7z
    Republished Owner: user1@tenant.onmicrosoft.com

    Press any key to close this window . . .

   ```
   