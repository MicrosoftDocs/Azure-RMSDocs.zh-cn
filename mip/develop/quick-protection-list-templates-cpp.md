---
title: 快速入门 - 使用 C++ MIP SDK 列出可供 Microsoft 信息保护 (MIP) 租户中经过身份验证的用户使用的保护模板
description: 本快速入门介绍如何使用 Microsoft 信息保护 C++ SDK 保护 API 列出可供用户使用的保护模板 (C++)
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 62f694248da10c7663c551240b204711b52163d5
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865059"
---
# <a name="quickstart-list-protection-templates-c"></a>快速入门：列出保护模板 (C++)

本快速入门介绍如何使用 MIP 保护 API 保护可供用户使用的模板。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 先完成[快速入门 - 客户端应用程序初始化 - 保护 API (C++)](quick-protection-app-initialization-cpp.md)，以生成 Visual Studio 初学者解决方案。 此“列出保护模板”快速入门需依赖前者来正确创建初学者解决方案。
- 可选：查看 [RMS 模板](/azure/information-protection/configure-policy-templates)概念。

## <a name="add-logic-to-list-the-protection-templates"></a>添加逻辑以列出保护模板

使用保护引擎对象添加逻辑以列出可供用户使用的保护模板。

1. 打开在前面的“快速入门 - 客户端应用程序初始化 - 保护 API (C++)”一文中创建的 Visual Studio 解决方案。

2. 使用“解决方案资源管理器”，打开项目中包含 `main()` 方法的实现的 .cpp 文件  。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

3. 在文件顶部附近的 `using mip::ProtectionEngine;` 后面添加以下 `using` 指令：

   ```cpp
   using std::endl;
   ```

4. 在 `main()` 正文的末尾，在最后一个 `catch` 块的右大括号 `}` 下面并在 `return 0;` 上面（在上一快速入门中离开的位置）插入以下代码：

   ```cpp
    // List protection templates
    const shared_ptr<ProtectionEngineObserver> engineObserver = std::make_shared<ProtectionEngineObserver>();
    // Create a context to pass to 'ProtectionEngine::GetTemplateListAsync'. That context will be forwarded to the
    // corresponding ProtectionEngine::Observer methods. In this case, we use promises/futures as a simple way to detect
    // the async operation completes synchronously.
    auto loadPromise = std::make_shared<std::promise<vector<shared_ptr<mip::TemplateDescriptor>>>>();
    std::future<vector<shared_ptr<mip::TemplateDescriptor>>> loadFuture = loadPromise->get_future();
    engine->GetTemplatesAsync(engineObserver, loadPromise);
    auto templates = loadFuture.get();

    cout << "**_ Template List: " << endl;

    for (const auto& protectionTemplate : templates) {
        cout << "Name: " << protectionTemplate->GetName() << " : " << protectionTemplate->GetId() << endl;
    }

   ```

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>创建 PowerShell 脚本以生成访问令牌

在 `AuthDelegateImpl::AcquireOAuth2Token` 实现中按照 SDK 的要求使用以下 PowerShell 脚本生成访问令牌。 该脚本使用先前在“MIP SDK 安装和配置”中安装的 ADAL.PS 模块中的 `Get-ADALToken` cmdlet。

1. 创建 PowerShell 脚本文件（.ps1 扩展名），并将以下脚本复制/粘贴到该文件中：

   - `$authority` 和 `$resourceUrl` 稍后会在下一部分中更新。
   - 更新 `$appId` 和 `$redirectUri`，以匹配在 Azure AD 应用注册中指定的值。

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token()
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '<app-ID>'                              # App ID of the Azure AD app registration
   $redirectUri = '<redirect-uri>'                  # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. 保存该脚本文件，以便稍后按照客户端应用程序的要求运行它。

## <a name="build-and-test-the-application"></a>生成和测试应用程序

最后，生成和测试客户端应用程序。

1. 使用 Ctrl+Shift+b（“生成解决方案”）来生成客户端应用程序 **。如果没有生成错误，请使用 F5（开始调试）来运行应用程序**。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireOAuth2Token()` 方法时，应用程序都会提示输入访问令牌。 如果多次提示并且请求的值相同，则可以重用以前生成的令牌：

3. 要生成用于在提示中输入的访问令牌，请返回 PowerShell 脚本并执行以下操作：

   - 更新 `$authority` 和 `$resourceUrl` 变量。 它们必须与在步骤 2 的控制台输出中指定的值匹配。
   - 运行 PowerShell 脚本。 `Get-ADALToken` cmdlet 会触发类似于以下示例的 Azure AD 身份验证提示。 指定在步骤 2 的控制台输出中提供的同一帐户。 成功登录后，访问令牌将被放置在剪贴板上。

     [![Visual Studio 获取令牌登录](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - 可能还需同意应用程序在登录帐户下运行时访问 MIP API。 如果未事先同意 Azure AD 应用程序注册（如“MIP SDK 安装和配置”中所述），或者使用其他租户（而非应用程序注册所在的租户）中的帐户登录，就会出现这种情况。 只需单击“接受”即可记录你的同意。

     [![Visual Studio 同意](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. 将访问令牌粘贴到步骤 #2 的提示符中后，控制台输出应显示保护模板，类似于以下示例：

   ```console
   **_ Template List:
   Name: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
   Name: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
   Name: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
   Name: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720

   C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
   To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.

   Press any key to continue . . .
   ```

   > [!NOTE]
   > 复制并保存一个或多个保护模板的 ID（例如，`f42a3342-8706-4288-bd31-ebb85995028z`），因为你将在下一个快速入门中使用它。

## <a name="troubleshooting"></a>疑难解答
### <a name="problems-during-execution-of-c-application"></a>执行 C++ 应用程序时出现的问题

| “摘要” | 错误消息 | 解决方案 |
|---------|---------------|----------|
| 访问令牌不正确 | _发生异常...访问令牌是否不正确/过期?<br><br>API 调用失败: profile_add_engine_asyn 失败原因: [class mip::PolicySyncException] 策略获取失败，请求失败并显示 http 状态代码:401, x-ms-diagnostics: [2000001;reason="无法解析与请求一起提交的 OAuth 令牌。";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe（进程 29924）已退出，代码为 0。<br><br>按任意键以关闭此窗口。 . .* | 如果项目成功生成，但出现类似于左侧的输出，则表示 `AcquireOAuth2Token()` 方法中可能包含无效或过期的令牌。 返回到[创建 PowerShell 脚本以生成访问令牌](#create-a-powershell-script-to-generate-access-tokens)并重写访问令牌，再次更新 `AcquireOAuth2Token()`然后重新生成/重新测试。 还可以使用 [jwt.ms](https://jwt.ms/) 单页 Web 应用程序检查并验证令牌及其声明。 |

## <a name="next-steps"></a>后续步骤

你已经了解如何列出可供经过身份验证的用户使用的保护模板，现在尝试下一个快速入门：

> [!div class="nextstepaction"]
> [加密和解密文本](quick-protection-encrypt-decrypt text-cpp.md)