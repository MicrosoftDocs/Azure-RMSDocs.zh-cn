---
title: 文件 API - 处理电子邮件 .msg 文件 (C#)
description: 本文可帮助你了解如何使用 MIP SDK 文件 API 处理 .msg 文件。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/08/2020
ms.author: v-anikep
ms.openlocfilehash: a9280d545cb997bef32c464685532afe7c4020df
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548099"
---
# <a name="file-api---process-email-msg-files-c"></a>文件 API - 处理电子邮件 .msg 文件 (C#)

文件 API 支持对 .msg 文件进行保护操作，操作方式与其他任何文件类型相同，不同之处在于，SDK 需要应用程序启用 MSG 功能标记。 本文将介绍如何设置此标记。

如前文所述，`IFileEngine` 实例化需要一个设置对象 `FileEngineSettings`。 FileEngineSettings 可用于传递应用程序需要为特定实例设置的自定义设置的参数。 `FileEngineSettings` 的 `CustomSettings` 属性用于设置 `enable_msg_file_type` 的标记，以便能够处理 .msg 文件。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：文件 API 应用程序初始化 (C#)](quick-app-initialization-csharp.md)，生成 Visual Studio 初学者解决方案。 本快速入门“如何处理电子邮件 .msg 文件 (C#)”建立在前一个快速入门的基础之上。
- 查看[电子邮件文件 MIP SDK](concept-email-cpp.md) 概念。
- 可选：查看 [MIP SDK 中的文件引擎](concept-profile-engine-file-engine-cpp.md)概念。
- 可选：查看 [MIP SDK 中的文件句柄](concept-handler-file-cpp.md)概念。

## <a name="set-enable_msg_file_type-and-use-file-api-for-protecting-msg-file"></a>设置 enable_msg_file_type 并使用文件 API 来保护 .msg 文件

在文件 AI 应用程序初始化快速入门的后续操作中，修改文件引擎构造代码以设置 `enable_msg_file_type flag`，然后使用文件引擎保护 .msg 文件。

1. 打开在前面的“快速入门：文件 API 应用程序初始化 (C#)”。

2. 使用“解决方案资源管理器”，打开项目中包含 `Main()` 方法的实现的 .cs 文件。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

3. 删除先前快速入门中 `Main()` 函数的实现。 在 `Main()` 主体中，插入以下代码。 在下面的代码块中，`enable_msg_file_type` 标记是在创建文件引擎期间设置的，随后 .msg 文件可通过使用文件引擎创建的 `IFileHandler` 对象进行处理。

    ```csharp
    static void Main(string[] args)
    {
        // Initialize Wrapper for File API operations.
        MIP.Initialize(MipComponent.File);

        // Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId.
        ApplicationInfo appInfo = new ApplicationInfo()
        {
                ApplicationId = clientId,
                ApplicationName = appName,
                ApplicationVersion = "1.0.0"
        };

        // Instantiate the AuthDelegateImpl object, passing in AppInfo.
        AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

        MipContext mipContext = MIP.CreateMipContext(appInfo,"mip_data",LogLevel.Trace,null,null);

        // Initialize and instantiate the File Profile.
        // Create the FileProfileSettings object.
        // Initialize file profile settings to create/use local state.
        var profileSettings = new FileProfileSettings(mipContext, CacheStorageType.OnDiskEncrypted, new ConsentDelegateImplementation());

        // Load the Profile async and wait for the result.
        var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

        // Create a FileEngineSettings object, then use that to add an engine to the profile.
        var customSettings = new List<KeyValuePair<string, string>>();
        customSettings.Add(new KeyValuePair<string, string>("enable_msg_file_type", "true"));

        // Create a FileEngineSettings object, then use that to add an engine to the profile.
        var engineSettings = new FileEngineSettings("user1@tenant.com", authDelegate, "", "en-US");
        engineSettings.Identity = new Identity("user1@tenant.com");
        //set custom settings for the engine
        engineSettings.CustomSettings = customSettings;

        //Add fileEngine to profile
        var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;

        //Set file paths
        string inputFilePath = "<input-file-path>"; //.msg file to be protected
        string actualFilePath = inputFilePath;
        string outputFilePath = "<output-file-path>"; //protected .msg file
        string actualOutputFilePath = outputFilePath;

        //Create a file handler for original file
        var fileHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(inputFilePath, actualFilePath, true)).Result;

        // List templates available to the user and use one of them to protect the mail file.

            /// Listing of protection templates has to be performed by creating protection engine as described in protection quick start

        string templateId = "<template-id>"; //protection template retrieved using protection engine

        // Construct a protection descriptor on input file and use the same to set protection to the file
        ProtectionDescriptor descriptor = new ProtectionDescriptor(templateId);
        fileHandler.SetProtection(descriptor, new ProtectionSettings());

        // Commit changes, save as outputFilePath
        var result = Task.Run(async () => await fileHandler.CommitAsync(outputFilePath)).Result;

        // Create a new handler to read the protected file metadata
        var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, actualOutputFilePath, true)).Result;

        Console.WriteLine(string.Format("Original file: {0}", inputFilePath));
        Console.WriteLine(string.Format("Protected file: {0}", outputFilePath));
        Console.WriteLine(string.Format("TemplateID applied to file: {0} \r\nProtectionOwner: {1}", 
            handlerModified.Protection.ProtectionDescriptor.TemplateId,handlerModified.Protection.Owner));
        Console.WriteLine("Press a key to continue.");
        Console.ReadKey();

        // Application Shutdown
        fileHandler = null;
        handlerModified = null;
        fileEngine = null;
        fileProfile = null;
        mipContext = null;
    }

    ```

    有关文件操作的更多详细信息，请参阅[文件处理程序概念](concept-handler-file-cpp.md)。

4. 使用以下值替换源代码中的占位符值：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<input-file-path\> | 测试输入消息文件的完整路径。例如：`c:\\Test\\message.msg`。 |
   | \<output-file-path\> | 输出文件的完整路径，它将是输入文件的标记副本，例如：`c:\\Test\\message_protected.msg`。 |
   | \<template-id\> | 使用保护引擎检索的 templateId。例如：`667466bf-a01b-4b0a-8bbf-a79a3d96f720`。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

使用 F6（生成解决方案）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

```Console
    Original file: C:\Test.msg
    Protected file: C:\Test_protected.msg
    TemplateID applied to file: 667466bf-a01b-4b0a-8bbf-a79a3d96f720
    ProtectionOwner: user1@tenant.com
    Press a key to continue.
```

## <a name="troubleshooting"></a>疑难解答

### <a name="problems-during-execution-of-c-application"></a>执行 C# 应用程序时出现的问题

| “摘要” | 错误消息 | 解决方案 |
|---------|---------------|----------|
| NetworkException：RMS 服务在请求中检测到错误输入。 RMS 错误代码：Microsoft.RightsManagement.Exceptions.BadInputException | * * 参数 TemplateId 和 Policy 无效，它们不能为 Null。CorrelationId=f265b189-ebf6-4b30-a191-41539cdff215，CorrelationId.Description=FileHandler，HttpRequest.Id=04990d53-cf12-4969-9c80-06e365b312f2；d5fb4794-ac84-4445-abc6-647e41df62b2，HttpRequest.SanitizedUrl=https://api.aadrm.com/my/v2/publishinglicenses HttpResponse.StatusCode=400，NetworkError.Category=FailureResponseCode* | 如果项目成功生成，但出现类似于左侧的输出，则表示 templateID 可能无效。 返回到代码块并更正保护模板 ID，然后重新生成/重新测试。 |
| TemplateNotFoundException | 无法识别模板 ID。CorrelationId=abb2ef59-ad09-4aa0-b731-f59a92711dad，CorrelationId.Description=FileHandler，HttpRequest.Id=8c688752-ccd2-4dca-ace3-b67b44176689；78538a57-a9fd-4717-8924-33581a04598b | 如果项目成功生成，但出现类似于左侧的输出，则表示 templateID 可能无效。 返回到代码块并更正保护模板 ID，然后重新生成/重新测试。 |