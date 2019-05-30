---
title: 快速入门 - 使用 C++ MIP SDK 对文件设置和获取敏感度标签
description: 一个演示如何使用 Microsoft 信息保护 C++ SDK 对文件设置和获取敏感度标签的快速入门。
services: information-protection
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/18/2019
ms.author: mbaldwin
ms.openlocfilehash: 2ac8c6bbfba6f460ac016a103f32f20856bff2aa
ms.sourcegitcommit: fe23bc3e24eb09b7450548dc32b4ef09c8970615
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2019
ms.locfileid: "60184886"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>快速入门：设置和获取敏感度标签 (C++)

本快速入门介绍如何使用更多的 MIP 文件 API。 使用上一个快速入门中列出的敏感度标签之一，可以使用文件处理程序对文件设置/获取标签。 文件处理程序类会公开设置/获取标签的各种操作，或受支持文件类型的保护。

## <a name="prerequisites"></a>先决条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：列出敏感度标签 (C++)](quick-file-list-labels-cpp.md)，这可生成 Visual Studio 初学者解决方案，以列出组织的敏感度标签。 此“设置和获取敏感度标签”快速入门基于前一个。
- 可选：查看 [MIP SDK 中的文件句柄](concept-handler-file-cpp.md)概念。

## <a name="implement-an-observer-class-to-monitor-the-file-handler-object"></a>实现观察者类以监视文件处理程序对象

类似于在应用程序初始化快速入门中实现的观察者（对于文件配置文件和引擎），现在你可对文件处理程序对象实现观察者类。

通过扩展 SDK 的 `mip::FileHandler::Observer` 类，创建文件句柄观察程序的基本实现。 稍后会实例化并使用观察者，以监视文件处理程序操作。

1. 打开之前的“快速入门：列出敏感度标签 (C++)”一文中使用的 Visual Studio 解决方案。

2. 向项目中添加一个新类，这将为你生成标头/.h 和实现/.cpp 文件：

   - 在“解决方案资源管理器”中，再次右键单击项目节点，选择“添加”，然后选择“类”    。
   - 在“添加类”对话框上： 
     - 在“类名”  字段中，输入“filehandler_observer”。 请注意，根据你输入的名称，会自动填充“.h 文件”  和“.cpp 文件”  字段。
     - 完成后，单击“确定”  按钮。

3. 生成类的 .h 和 .cpp 文件之后，会在“编辑器组”选项卡中打开这两个文件。 现在更新每个文件以实现新的观察者类：

   - 通过选择/删除生成的 `filehandler_observer` 类，更新“filehandler_observer.h”。 请勿  删除上一步生成的预处理器指令 (#pragma, #include)。 然后将以下源复制/粘贴到文件中，在任何现有的预处理器指令之后：

     ```cpp
     #include <memory>
     #include "mip/file/file_engine.h"
     #include "mip/file/file_handler.h"

     class FileHandlerObserver final : public mip::FileHandler::Observer {
     public:
        FileHandlerObserver() { }
        // Observer implementation
        void OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) override;
        void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
        void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) override;
        void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;       
     };
     ```

   - 通过选择/删除生成的 `filehandler_observer` 类实现，更新“filehandler_observer.cpp”。 请勿  删除上一步生成的预处理器指令 (#pragma, #include)。 然后将以下源复制/粘贴到文件中，并放在任何现有的预处理器指令之后：

     ```cpp
     void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_value(fileHandler);
     }

     void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_exception(error);
     }

     void FileHandlerObserver::OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_value(committed);
     }

     void FileHandlerObserver::OnCommitFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_exception(error);
     }
     ```

4. （可选）使用 F6（生成解决方案  ）运行解决方案的某个测试编译/链接，以确保它成功生成然后再继续。

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>添加逻辑以设置和获取敏感度标签

使用文件引擎对象，添加逻辑以对文件设置和获取敏感度标签。 

1. 使用“解决方案资源管理器”  ，打开项目中包含 `main()` 方法的实现的 .cpp 文件。 它默认与包含它的项目同名，即在项目创建期间指定的名称。 

2. 在文件顶部的相应现有指令下面，添加以下 `#include` 和 `using` 指令：

   ```cpp
   #include "filehandler_observer.h" 
   #include "mip/file/file_handler.h" 

   using mip::FileHandler;
   ```
3. 在 `main()` 正文的末尾，在 `system("pause");` 下面并在 `return 0;` 上面（在上一快速入门中离开的位置），插入以下代码：

   ```cpp
   // Set up async FileHandler for input file operations
   string inputFilePath = "<input-file-path>";
   string actualFilePath = "<content-identifier>";
   std::shared_ptr<FileHandler> handler;
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(
             inputFilePath,
             actualFilePath,                       
             true, 
             std::make_shared<FileHandlerObserver>(), 
             handlerPromise);
        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid input file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Set a label on input file
   try
   {
        string labelId = "<label-id>";
        cout << "\nApplying Label ID " << labelId << " to " << filePathIn << endl;
        mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED, mip::ActionSource::MANUAL);
        handler->SetLabel(labelId, labelingOptions);
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Commit changes, save as a different/output file
   string filePathOut = "<output-file-path>";
   try
   {
        cout << "Committing changes" << endl;
        auto commitPromise = std::make_shared<std::promise<bool>>();
        auto commitFuture = commitPromise->get_future();
        handler->CommitAsync(filePathOut, commitPromise);
        if (commitFuture.get()) {
            cout << "\nLabel committed to file: " << filePathOut << endl;
        }
        else {
            cout << "Failed to label: " + filePathOut << endl;
            return 1;
        }
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid commit file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }
   system("pause");

   // Set up async FileHandler for output file operations
   actualFilePath = "<content-identifier>";
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(
             filePathOut,
             actualFilePath,
             true,
             std::make_shared<FileHandlerObserver>(),
             handlerPromise);

        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid output file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Get the label from output file
   try
   {
        cout << "\nGetting the label committed to file: " << filePathOut << endl;
        auto label = handler->GetLabel();
        cout << "Name: " + label->GetLabel()->GetName() << endl;
        cout << "Id: " + label->GetLabel()->GetId() << endl;
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }
   system("pause");
   ```

4. 使用字符串常量替换刚才粘贴的源代码中的占位符值，如下所示：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<input-file-path\> | 测试输入文件的完整路径，例如：`"c:\\Test\\Test.docx"`。 |
   | \<content-identifier\> | 内容的可读标识符。 例如： <ul><li>文件可考虑使用 path\filename：`"c:\Test\Test.docx"`</li><li>电子邮件可考虑使用 subject:sender：`"RE: Audit design:user1@contoso.com"`</li></ul> |
   | \<label-id\> | 敏感度标签 ID，从上一快速入门中的控制台输出所复制，例如：`"f42a3342-8706-4288-bd31-ebb85995028z"`。 |
   | \<output-file-path\> | 输出文件的完整路径，它将是输入文件的标记副本，例如：`"c:\\Test\\Test_labeled.docx"`。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。 

1. 使用 F6（生成解决方案  ）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试  ）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireOAuth2Token()` 方法时，应用程序都会提示输入访问令牌。 如先前在“列出敏感度标签”快速入门中采取的方式那样，每次使用提供的 $authority 和 $resourceUrl 值运行 PowerShell 脚本以获取令牌。 

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Sensitivity labels for your organization:
   Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
   Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
   General : f42a3342-8706-4288-bd31-ebb85995028z
   Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
   Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
   Press any key to continue . . .

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/94f69844-8d34-4794-bde4-3ac89ad2b664/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

可以通过打开输出文件，并直观地检查文档的信息保护设置来验证标签的应用。

> [!NOTE]
> 如果要标记 Office 文档，但未使用获取访问令牌的 Azure Active Directory (AD) 租户中的帐户登录（并且配置了敏感度标签），则可能会提示先登录，然后才能打开标记的文档。 



