---
title: 文件 API - 处理电子邮件 .msg 文件 (C++)
description: 本文可帮助你了解如何使用 MIP SDK 文件 API 处理 .msg 文件。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/08/2020
ms.author: v-anikep
ms.openlocfilehash: ef6f8db6915242a830d252eec4509fa67eecbb8c
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86403301"
---
# <a name="file-api---process-email-msg-files-c"></a>文件 API - 处理电子邮件 .msg 文件 (C++)

文件 API 支持对 .msg 文件进行保护操作，操作方式与其他任何文件类型相同，不同之处在于，SDK 需要应用程序启用 MSG 功能标记。 本文将介绍如何设置此标记。

如前文所述，`mip::FileEngine` 实例化需要一个设置对象 `mip::FileEngineSettings`。 FileEngineSettings 可用于传递应用程序需要为特定实例设置的自定义设置的参数。 `mip::FileEngineSettings` 的 `CustomSettings` 属性用于设置 `enable_msg_file_type` 的标记，以便能够处理 .msg 文件。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：文件 API 应用程序初始化 (C++)](quick-app-initialization-cpp.md)，生成 Visual Studio 初学者解决方案。 本快速入门“如何处理电子邮件 .msg 文件 (C++)”建立在前一个快速入门的基础之上。
- 查看[快速入门：列出敏感度标签 (C++)](quick-file-list-labels-cpp.md)。
- 查看[快速入门：设置/获取敏感度标签 (C++)](quick-file-set-get-label-cpp.md)
- 查看[电子邮件文件 MIP SDK](concept-email.md) 概念。
- 可选：查看 [MIP SDK 中的文件引擎](concept-profile-engine-file-engine-cpp.md)概念。
- 可选：查看 [MIP SDK 中的文件句柄](concept-handler-file-cpp.md)概念。

## <a name="prerequisite-implementation-steps"></a>必备实现步骤

1. 打开在前面的“快速入门：客户端应用程序初始化 (C++)”一文中创建的 Visual Studio 解决方案。

2. 如快速入门“[列表敏感度标签 (C++)](quick-file-list-labels-cpp.md#create-a-powershell-script-to-generate-access-tokens)”中所述，创建一个 PowerShell 脚本以生成访问令牌。

3. 如快速入门“[设置/获取灵敏度标签 (C++)](quick-file-set-get-label-cpp.md#implement-an-observer-class-to-monitor-the-file-handler-object)”中所述，实现观察程序类以监视 `mip::FileHandler`。

## <a name="set-enable_msg_file_type-and-use-file-api-to-protect-msg-file"></a>设置 enable_msg_file_type 并使用文件 API 来保护 .msg 文件

添加以下文件引擎构造代码以设置 `enable_msg_file_type flag`，并使用文件引擎来保护 .msg 文件。

1. 使用“解决方案资源管理器”，打开项目中包含 `main()` 方法的实现的 .cpp 文件。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

2. 在文件顶部的相应现有指令下面，添加以下 #include 和 using 指令：

    ```cpp
    #include "filehandler_observer.h" 
    #include "mip/file/file_handler.h" 
    #include <iostream>
    #include "mip/protection/protection_descriptor_builder.h"
    #include "mip/protection_descriptor.h"
    using mip::FileHandler;
    using mip::ProtectionDescriptor;
    using mip::ProtectionDescriptorBuilder;
    using mip::ProtectionSettings;
    using std::endl;
    ```

3. 删除先前快速入门中 `main()` 函数的实现。 在 `main()` 主体中，插入以下代码。 在下面的代码块中，`enable_msg_file_type` 标记是在创建文件引擎期间设置的，随后 .msg 文件可通过使用文件引擎创建的 `mip::FileHandler` 对象进行处理。

```cpp
int main()
{
    // Construct/initialize objects required by the application's profile object
    ApplicationInfo appInfo { "<application-id>",                    // ApplicationInfo object (App ID, name, version)
                              "<application-name>", 
                              "1.0" 
    };

    auto mipContext = mip::MipContext::Create(appInfo,
                                                "file_sample",
                                                mip::LogLevel::Trace,
                                                false,
                                                nullptr /*loggerDelegateOverride*/,
                                                nullptr /*telemetryOverride*/);

    auto profileObserver = make_shared<ProfileObserver>();                      // Observer object
    auto authDelegateImpl = make_shared<AuthDelegateImpl>("<application-id>");  // Authentication delegate object (App ID)
    auto consentDelegateImpl = make_shared<ConsentDelegateImpl>();              // Consent delegate object

    // Construct/initialize profile object
    FileProfile::Settings profileSettings(mipContext,mip::CacheStorageType::OnDisk,authDelegateImpl,
        consentDelegateImpl,profileObserver);

    // Set up promise/future connection for async profile operations; load profile asynchronously
    auto profilePromise = make_shared<promise<shared_ptr<FileProfile>>>();
    auto profileFuture = profilePromise->get_future();
    try
    {
        mip::FileProfile::LoadAsync(profileSettings, profilePromise);
    }
    catch (const std::exception& e)
    {
        std::cout << "An exception occurred. Are the Settings and ApplicationInfo objects populated correctly?\n\n"<< e.what() << "'\n";
        system("pause");
        return 1;
    }

    auto profile = profileFuture.get();

    // Construct/initialize engine object
    FileEngine::Settings engineSettings(
                            mip::Identity("<engine-account>"),      // Engine identity (account used for authentication)
                            "<engine-state>",                       // User-defined engine state
                            "en-US");                               // Locale (default = en-US)

    //Set enamble_msg_file_type flag as true
    std::vector<std::pair<string, string>> customSettings;
    customSettings.emplace_back(mip::GetCustomSettingEnableMsgFileType(), "true");
    engineSettings.SetCustomSettings(customSettings);

    // Set up promise/future connection for async engine operations; add engine to profile asynchronously
    auto enginePromise = make_shared<promise<shared_ptr<FileEngine>>>();
    auto engineFuture = enginePromise->get_future();
    profile->AddEngineAsync(engineSettings, enginePromise);
    std::shared_ptr<FileEngine> engine;

    try
    {
        engine = engineFuture.get();
    }
    catch (const std::exception& e)
    {
        cout << "An exception occurred... is the access token incorrect/expired?\n\n"<< e.what() << "'\n";
        system("pause");
        return 1;
    }

    //Set file paths
    string inputFilePath = "<input-file-path>"; //.msg file to be protected
    string actualFilePath = inputFilePath;
    string outputFilePath = "<output-file-path>"; //protected .msg file
    string actualOutputFilePath = outputFilePath;

    //Create a file handler for original file
    auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto handlerFuture = handlerPromise->get_future();

    engine->CreateFileHandlerAsync(inputFilePath,
                                    actualFilePath,
                                    true,
                                    std::make_shared<FileHandlerObserver>(),
                                    handlerPromise);

    auto fileHandler = handlerFuture.get();

    //List templates available to the user and use one of them to protect the mail file.

    ///Listing of protection templates must be performed by creating protection engine as described in protection quick start

    string templateId = "<template-id>"; //protection template retrieved using protection engine

    //Create a protection descriptor using templateID and use it to set protection to the file
    auto descriptorBuilder = mip::ProtectionDescriptorBuilder::CreateFromTemplate(templateId);
    const std::shared_ptr<mip::ProtectionDescriptor>& descriptor = descriptorBuilder->Build();
    fileHandler->SetProtection(descriptor, ProtectionSettings());

    // Commit changes, save as outputFilePath
    auto commitPromise = std::make_shared<std::promise<bool>>();
    auto commitFuture = commitPromise->get_future();
    fileHandler->CommitAsync(outputFilePath, commitPromise);
    if (commitFuture.get()) {
        cout << "\n Protection applied to file: " << outputFilePath << endl;
    }
    else {
        cout << "Failed to protect: " + outputFilePath << endl;
        return 1;
    }

    // Create a new handler to read the protected file metadata
    auto protectedHandlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto protectedHandlerFuture = protectedHandlerPromise->get_future();
    engine->CreateFileHandlerAsync(outputFilePath, 
                                   actualOutputFilePath, 
                                   true, 
                                   std::make_shared<FileHandlerObserver>(), 
                                   protectedHandlerPromise);

    auto protectedFileHandler = protectedHandlerFuture.get();

    cout << "Original file: " << inputFilePath << endl;
    cout << "Protected file: " << outputFilePath << endl;
    cout << "TemplateID applied to protected file : " 
            << protectedFileHandler->GetProtection()->GetProtectionDescriptor()->GetTemplateId() 
            << endl;
    cout << "Protection Owner of protected file : " 
            << protectedFileHandler->GetProtection()->GetProtectionDescriptor()->GetOwner() 
            << endl;

    // Application shutdown. Null out profile and engine, call ReleaseAllResources();
    // Application may crash at shutdown if resources aren't properly released.
    protectedFileHandler = nullptr;
    fileHandler = nullptr;
    engine = nullptr;
    profile = nullptr;
    mipContext = nullptr;

    return 0;
}
```

有关文件操作的更多详细信息，请参阅[文件处理程序概念](concept-handler-file-cpp.md)。

4. 使用以下值替换源代码中的占位符值：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<application-id\> | 向 Azure AD 租户注册的应用程序 ID。例如：`0edbblll-8773-44de-b87c-b8c6276d41eb`。 |
   | \<engine-account\> | 用于引擎标识的帐户。例如：`user@tenant.onmicrosoft.com`。 |
   | \<engine-state\> | 用户定义的应用程序状态。例如：`My engine state`。 |
   | \<input-file-path\> | 测试输入消息文件的完整路径。例如：`c:\\Test\\message.msg`。 |
   | \<output-file-path\> | 输出文件的完整路径，它将是输入文件的标记副本，例如：`c:\\Test\\message_protected.msg`。 |
   | \<template-id\> | 使用保护引擎检索的 templateId。例如：`667466bf-a01b-4b0a-8bbf-a79a3d96f720`。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

使用 F6（生成解决方案）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

```Console
    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://syncservice.o365syncservice.com/
    Sign in with user account: User@Contoso.onmicrosoft.com
    Enter access token: <Paste token here>
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: User@Contoso.onmicrosoft.com
    Enter access token: <Paste token here>
    Press any key to continue . . .

    Protection applied to file: C:\Test_protected.msg

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: User@Contoso.onmicrosoft.com
    Enter access token: <Paste token here>
    Press any key to continue . . .
    Original file: C:\Test.msg
    Protected file: C:\Test_protected.msg
    TemplateID applied to protected file : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
    Protection Owner of protected file : User@Contoso.OnMicrosoft.com

```

## <a name="troubleshooting"></a>疑难解答

### <a name="problems-during-execution-of-c-application"></a>执行 C# 应用程序时出现的问题

| “摘要” | 错误消息 | 解决方案 |
|---------|---------------|----------|
| TemplateNotFoundException | 无法识别模板 ID。CorrelationId=abb2ef59-ad09-4aa0-b731-f59a92711dad，CorrelationId.Description=FileHandler，HttpRequest.Id=8c688752-ccd2-4dca-ace3-b67b44176689；78538a57-a9fd-4717-8924-33581a04598b| 如果项目成功生成，但出现类似于左侧的输出，则表示 templateID 可能无效。 返回到代码块并更正保护模板 ID，然后重新生成/重新测试。 |