---
title: 快速入门 - 使用 C++ MIP SDK 保护 API 加密/解密文本
description: 本快速入门介绍如何使用 C++ Microsoft 信息保护 SDK 保护 API，通过保护模板来加密和解密临时文本 (C++)
services: information-protection
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 1258bfcd6c47611b439a29406ed0e78b644a5803
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535835"
---
# <a name="quickstart-encryptdecrypt-text-using-mip-sdk-c"></a>快速入门：使用 MIP SDK (C++) 加密/解密文本

本快速入门介绍如何使用更多的 MIP 保护 API。 使用上一快速入门中列出的其中一个保护模板，通过保护处理程序来加密临时文本。 保护处理程序类公开用于应用/删除保护的各种操作。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：列出保护模板 (C++)](quick-protection-list-templates-cpp.md)，这可生成 Visual Studio 初学者解决方案，以列出经过身份验证的用户可用的保护模板。 此“加密/解密文本”快速入门以上一快速入门为基础。
- 可选：查看 [MIP SDK 中的保护处理程序](concept-handler-protection-cpp.md)概念。

## <a name="implement-an-observer-class-to-monitor-the-protection-handler-object"></a>实现观察者类以监视保护处理程序对象

类似于在应用程序初始化快速入门中实现的观察者（对于保护配置文件和引擎），现在你可对保护处理程序对象实现观察者类。

通过扩展 SDK 的 `mip::ProtectionHandler::Observer` 类，创建保护处理程序观察者的基本实现。 稍后会实例化并使用观察者，以监视保护处理程序操作。

1. 打开之前的“快速入门：列出保护模板 (C++)”一文。

2. 向项目中添加一个新类，这将为你生成标头/.h 和实现/.cpp 文件：

   - 在“解决方案资源管理器”中，再次右键单击项目节点，选择“添加”，然后选择“类”    。
   - 在“添加类”对话框上： 
     - 在“类名”  字段中，输入“handler_observer”。 请注意，根据你输入的名称，会自动填充“.h 文件”和“.cpp 文件”字段   。
     - 完成后，单击“确定”  按钮。

3. 生成类的 .h 和 .cpp 文件之后，会在“编辑器组”选项卡中打开这两个文件。 现在更新每个文件以实现新的观察程序类：

   - 通过选择/删除生成的 `handler_observer` 类，更新“handler_observer.h”。 请勿删除上一步生成的预处理器指令 (#pragma, #include)  。 然后将以下源复制/粘贴到文件中，并放在任何现有的预处理器指令之后：

     ```cpp
     #include <memory>
     #include "mip/protection/protection_engine.h"
     using std::shared_ptr;
     using std::exception_ptr;

     class ProtectionHandlerObserver final : public mip::ProtectionHandler::Observer {
          public:
          ProtectionHandlerObserver() { }
          void OnCreateProtectionHandlerSuccess(const shared_ptr<mip::ProtectionHandler>& protectionHandler, const shared_ptr<void>& context) override;
          void OnCreateProtectionHandlerFailure(const exception_ptr& Failure, const shared_ptr<void>& context) override;
          };

     ```

   - 通过选择/删除生成的 `handler_observer` 类实现，更新“handler_observer.cpp”。 请勿删除上一步生成的预处理器指令 (#pragma, #include)  。 然后将以下源复制/粘贴到文件中，并放在任何现有的预处理器指令之后：

     ```cpp
     #include "handler_observer.h"
     using std::shared_ptr;
     using std::promise;
     using std::exception_ptr;

     void ProtectionHandlerObserver::OnCreateProtectionHandlerSuccess(
          const shared_ptr<mip::ProtectionHandler>& protectionHandler,const shared_ptr<void>& context) {
               auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
               createProtectionHandlerPromise->set_value(protectionHandler);
               };

     void ProtectionHandlerObserver::OnCreateProtectionHandlerFailure(
          const exception_ptr& Failure, const shared_ptr<void>& context) {
               auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get())
               createProtectionHandlerPromise->set_exception(Failure);
               };

     ```

4. （可选）使用 Ctrl+Shift+B（生成解决方案）运行解决方案的某个测试编译/链接，确保它成功生成后再继续  。

## <a name="add-logic-to-encrypt-and-decrypt-ad-hoc-text"></a>添加逻辑以加密和解密临时文本

使用保护引擎对象添加逻辑以加密和解密临时文本。

1. 使用“解决方案资源管理器”，打开项目中包含 `main()` 方法的实现的 .cpp 文件  。

2. 在文件顶部的相应现有指令下面，添加以下 #include 和 using 指令：

   ```cpp
     #include "mip/protection/protection_descriptor_builder.h"
     #include "mip/protection_descriptor.h"
     #include "handler_observer.h"

     using mip::ProtectionDescriptor;
     using mip::ProtectionDescriptorBuilder;
     using mip::ProtectionHandler;
   ```

3. 在 `Main()` 正文的末尾（在上一快速入门中离开的位置），插入以下代码：

   ```cpp
   //Encrypt/Decrypt text:
   string templateId = "<Template-ID>";//Template ID from previous QuickStart e.g. "bb7ed207-046a-4caf-9826-647cff56b990"
   string inputText = "<Sample-Text>";//Sample Text

   //Refer to ProtectionDescriptor docs for details on creating the descriptor
   auto descriptorBuilder = mip::ProtectionDescriptorBuilder::CreateFromTemplate(templateId);
   const std::shared_ptr<mip::ProtectionDescriptor>& descriptor = descriptorBuilder->Build();

   //Create Publishing settings using a descriptor
   mip::ProtectionHandler::PublishingSettings publishingSettings = mip::ProtectionHandler::PublishingSettings(descriptor);

   //Create a publishing protection handler using Protection Descriptor
   auto handlerObserver = std::make_shared<ProtectionHandlerObserver>();
   engine->CreateProtectionHandlerForPublishingAsync(publishingSettings, handlerObserver, pHandlerPromise);
   auto publishingHandler = pHandlerFuture.get();

   std::vector<uint8_t> inputBuffer(inputText.begin(), inputText.end());

   //Show action plan
   cout << "Applying Template ID " + templateId + " to: " << endl << inputText << endl;

   //Encrypt buffer using Publishing Handler
   std::vector<uint8_t> encryptedBuffer;
   encryptedBuffer.resize(static_cast<size_t>(publishingHandler->GetProtectedContentLength(inputText.size(), true)));

   publishingHandler->EncryptBuffer(0,
                         &inputBuffer[0],
                         static_cast<int64_t>(inputBuffer.size()),
                         &encryptedBuffer[0],
                         static_cast<int64_t>(encryptedBuffer.size()),
                         true);

   std::string encryptedText(encryptedBuffer.begin(), encryptedBuffer.end());
   cout << "Encrypted Text :" + encryptedText;

   //Show action plan
   cout << endl << "Decrypting string: " << endl << endl;

   //Generate publishing licence, so it can be used later to decrypt text.
   auto serializedPublishingLicense = publishingHandler->GetSerializedPublishingLicense();

   //Use same PL to decrypt the encryptedText.
   auto cHandlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
   auto cHandlerFuture = cHandlerPromise->get_future();
   shared_ptr<ProtectionHandlerObserver> cHandlerObserver = std::make_shared<ProtectionHandlerObserver>();

   //Create consumption settings using serialised publishing licence.
   mip::ProtectionHandler::ConsumptionSettings consumptionSettings = mip::ProtectionHandler::ConsumptionSettings(serializedPublishingLicense);
   engine->CreateProtectionHandlerForConsumptionAsync(consumptionSettings, cHandlerObserver, cHandlerPromise);

   auto consumptionHandler = cHandlerFuture.get();

   //Use consumption handler to decrypt the text.
   std::vector<uint8_t> decryptedBuffer(static_cast<size_t>(encryptedText.size()));

   int64_t decryptedSize = consumptionHandler->DecryptBuffer(
        0,
        &encryptedBuffer[0],
        static_cast<int64_t>(encryptedBuffer.size()),
        &decryptedBuffer[0],
        static_cast<int64_t>(decryptedBuffer.size()),
        true);

   decryptedBuffer.resize(static_cast<size_t>(decryptedSize));

   std::string decryptedText(decryptedBuffer.begin(), decryptedBuffer.end());

   // Output decrypted content. Should match original input text.
   cout << "Decrypted Text :" + decryptedText << endl;

   ```

4. 在靠近 `main()` 的末尾处，查找在第一个快速入门中创建的应用程序关闭块，并添加以下行以释放处理程序资源：

   ```cpp
    publishingHandler = nullptr;
    consumptionHandler = nullptr;
   ```

5. 使用字符串常量替换源代码中的占位符值，如下所示：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<sample-text\> | 要保护的示例文本，例如：`"cipher text"`。 |
   | \<Template-Id\> | 要用于保护文本的模板 ID。 例如： `"bb7ed207-046a-4caf-9826-647cff56b990"` |
  
## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。

1. 使用 Ctrl+Shift+B（“生成解决方案”）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireOAuth2Token()` 方法时，应用程序都会提示输入访问令牌。 如先前在“列出保护模板”快速入门中采取的方式那样，每次使用提供的 $authority 和 $resourceUrl 值运行 PowerShell 脚本以获取令牌。

   ```console
   *** Template List:
   Name: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
   Name: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
   Name: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
   Name: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
   Applying Template ID bb7ed207-046a-4caf-9826-647cff56b990 to:
   <Sample-Text>
   Encrypted Text :y¬╩$Ops7Γ╢╖¢t
   Decrypting string:

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/94f69844-8d34-4794-bde4-3ac89ad2b664/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Decrypted Text :<Sample-Text>
   C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
   To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.
   Press any key to close this window . . .
   ```
