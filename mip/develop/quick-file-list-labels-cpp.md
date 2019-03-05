---
title: 快速入门 - 使用 C++ MIP SDK 列出 Microsoft 信息保护 (MIP) 租户中的敏感度标签
description: 一个演示如何使用 Microsoft 信息保护 C++ SDK 列出租户中的敏感度标签的快速入门。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/18/2019
ms.author: mbaldwin
ms.openlocfilehash: 27b6c9039277feca033298520cc0fc18d239f037
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330978"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>快速入门：列出敏感度标签 (C++)

本快速入门演示如何使用 MIP 文件 API 列出为组织配置的敏感度标签。

## <a name="prerequisites"></a>先决条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 完整[快速入门：客户端应用程序初始化 （c + +）](quick-app-initialization-cpp.md)第一种方法生成初学者的 Visual Studio 解决方案。 此“列出敏感度标签”快速入门需依赖前者来正确创建初学者解决方案。
- 可选：审阅[分类标签](concept-classification-labels.md)概念。

## <a name="add-logic-to-list-the-sensitivity-labels"></a>添加用于列出敏感度标签的逻辑

使用文件引擎对象添加用于列出组织敏感度标签的逻辑。 

1. 打开在以前创建的 Visual Studio 解决方案"快速入门：客户端应用程序初始化 （c + +）"一文。

2. 使用“解决方案资源管理器”，打开项目中包含 `main()` 方法的实现的 .cpp 文件。 它默认与包含它的项目同名，即在项目创建期间指定的名称。 

3. 在文件顶部附近的 `using mip::FileEngine;` 后面添加以下 `using` 指令：

   ```cpp
   using std::endl;
   ```

4. 年底`main()`正文中的，右大括号下方`}`的最后一个`catch`块及更高版本`return 0;`（离开的位置在前面的快速入门），插入以下代码：

   ```cpp
   // List sensitivity labels
   cout << "\nSensitivity labels for your organization:\n";
   auto labels = engine->ListSensitivityLabels();
   for (const auto& label : labels)
   {
      cout << label->GetName() << " : " << label->GetId() << endl;

      for (const auto& child : label->GetChildren())
      {
        cout << "->  " << child->GetName() << " : " << child->GetId() << endl;
      }
   }
   system("pause");
   ``` 

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>创建 PowerShell 脚本以生成访问令牌

使用以下 PowerShell 脚本生成的 SDK 中请求的访问令牌在`AuthDelegateImpl::AcquireOAuth2Token`实现。 该脚本使用先前在“MIP SDK 安装和配置”中安装的 ADAL.PS 模块中的 `Get-ADALToken` cmdlet。 

1. 创建 PowerShell 脚本文件（.ps1 扩展名），并将以下脚本复制/粘贴到该文件中：

   - `$authority` 和 `$resourceUrl` 稍后会在下一部分中更新。
   - 更新`$appId`和`$redirectUri`，以匹配你在 Azure AD 应用注册中指定的值。 

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token() 
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '0edbblll-8773-44de-b87c-b8c6276d41eb'  # App ID of the Azure AD app registration
   $redirectUri = 'bltest://authorize'              # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession 
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. 保存脚本文件，以便您可以在更高版本，运行时客户端应用程序请求它。

## <a name="build-and-test-the-application"></a>生成和测试应用程序

最后，生成和测试客户端应用程序。 

1. 使用 F6（“生成解决方案”）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果你的项目生成并运行成功，应用程序会提示输入访问令牌，每次 SDK 调用你`AcquireOAuth2Token()`方法。 如果多次提示并且请求的值相同，则可以重用以前生成的令牌：

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token:
   ```

3. 若要生成访问令牌的提示时，请返回到 PowerShell 脚本和：

   - 更新 `$authority` 和 `$resourceUrl` 变量。 它们必须与在步骤 2 的控制台输出中指定的值匹配。 这些值由 MIP SDK 在 `AcquireOAuth2Token()` 的 `challenge` 参数中提供：
     - `$authority` 应为 `https://login.windows.net/common/oauth2/authorize`
     - `$resourceUrl` 应为 `https://syncservice.o365syncservice.com/` 或 `https://aadrm.com`
   - 运行 PowerShell 脚本。 `Get-ADALToken` Cmdlet 触发 Azure AD 身份验证提示，类似于下面的示例。 指定在步骤 2 的控制台输出中提供的同一帐户。 成功登录后，访问令牌将被放置在剪贴板上。

     [![Visual Studio 获取令牌登录](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - 可能还需同意应用程序在登录帐户下运行时访问 MIP API。 如果未事先同意 Azure AD 应用程序注册（如“MIP SDK 安装和配置”中所述），或者使用其他租户（而非应用程序注册所在的租户）中的帐户登录，就会出现这种情况。 只需单击“接受”即可记录你的同意。

     [![Visual Studio 同意](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. 后将访问令牌粘贴到步骤 #2 中的提示，控制台输出应显示类似于下面的示例的敏感度标签：

   ```console
   Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
   Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
   General : f42a3342-8706-4288-bd31-ebb85995028z
   Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
   Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z

   Press any key to continue . . .
   ```

   > [!NOTE]
   > 复制并保存一个或多个敏感度标签的 ID（例如，`f42a3342-8706-4288-bd31-ebb85995028z`），因为你将在下一个快速入门中使用它。

## <a name="troubleshooting"></a>疑难解答

### <a name="problems-during-execution-of-powershell-script"></a>执行 PowerShell 脚本时出现的问题 

| 总结 | 错误消息 | 解决方案 |
|---------|---------------|----------|
| 应用程序注册或 PowerShell 脚本中的重定向 URI 不正确 (AADSTS50011) |*AADSTS50011:答复请求中指定的 url 与应用程序配置的答复 url 不匹配:"ac6348d6-0d2f-4786-af33-07ad46e69bfc"。* | 通过完成以下步骤之一，验证正在使用的重定向 URI：<br><br><li>更新 Azure AD 应用程序配置中的重定向 URI，以匹配 PowerShell 脚本。 请参阅 [MIP SDK 安装和配置](setup-configure-mip.md#register-a-client-application-with-azure-active-directory)，验证是否已正确配置重定向 URI 属性。<br><li>更新 PowerShell 脚本中的 `redirectUri` 变量，以匹配应用程序注册。 |
| 登录帐户不正确 (AADSTS50020) | *AADSTS50020:用户帐户user@domain.com从标识提供者 https://sts.windows.net/72f988bl-86f1-41af-91ab-2d7cd011db47/租户组织名称中不存在且无法访问应用程序 0edbblll-8773-44de-b87c-b8c6276d41eb 该租户中。* | 完成以下步骤之一：<br><br><li>重新运行 PowerShell 脚本，但务必使用 Azure AD 应用程序注册所在的同一租户中的帐户。<br><li>如果登录帐户是正确的，则 PowerShell 主机会话可能已在其他帐户下进行身份验证。 在这种情况下，请在退出脚本主机后重新打开，然后再次尝试运行它。<br><li>如果将此快速入门用于 Web 应用（而非本机应用），并且需要使用其他租户中的帐户登录，请确保为 Azure AD 应用程序注册启用多租户使用。 可以使用应用程序注册中的“编辑清单”功能进行验证，并确保它指定 `"availableToOtherTenants": true,`。 |
| 应用程序注册中的权限不正确 (AADSTS65005) | *AADSTS65005:无效的资源。客户端已请求访问某个资源，但该资源未在客户端应用程序注册中的所需权限中列出。客户端应用程序 ID:0edbblll-8773-44de-b87c-b8c6276d41eb.来自请求的资源值: https://syncservice.o365syncservice.com/。资源应用程序 ID:870c4f2e-85b6-4 d 43-bdda-6ed9a579b725。应用注册中的有效资源的列表：00000002-0000-0000-c000-000000000000.* | 更新 Azure AD 应用程序配置中的权限请求。 请参阅 [MIP SDK 安装和配置](setup-configure-mip.md#register-a-client-application-with-azure-active-directory)，验证是否在应用程序注册中正确配置了权限请求。 |

### <a name="problems-during-execution-of-c-application"></a>执行 C++ 应用程序时出现的问题

| 总结 | 错误消息 | 解决方案 |
|---------|---------------|----------|
| 访问令牌不正确 | *发生了异常...是不正确/已过期的访问令牌？<br><br>失败的 API 调用： profile_add_engine_async 失败: [类 mip::PolicySyncException] 无法获取策略、 请求失败，http 状态代码：401，x 的 ms-诊断: [2000001; 原因 ="与请求一起提交的 OAuth 令牌无法分析。";error_category ="invalid_token"]，相关 Id: [35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe （进程 29924） 已退出，代码 0。<br><br>按任意键关闭此窗口...* | 如果项目成功生成，但出现类似于左侧的输出，则表示 `AcquireOAuth2Token()` 方法中可能包含无效或过期的令牌。 返回到[更新令牌获取逻辑](#update-the-token-acquisition-logic-with-a-valid-access-token)并重新生成访问令牌，再次更新 `AcquireOAuth2Token()`，然后重新生成/重新测试。 还可以使用 [jwt.ms](https://jwt.ms/) 单页 Web 应用程序检查并验证令牌及其声明。 |
| 未配置敏感度标签 | n/a | 如果项目成功生成，但在控制台窗口中没有输出，请确保正确配置了组织的敏感度标签。 请参阅 [MIP SDK 安装和配置](setup-configure-mip.md)，在“定义标签分类和保护设置”下获取详细信息。  |

## <a name="next-steps"></a>后续步骤

你已经了解如何列出组织的敏感度标签，现在尝试下一个快速入门：

> [!div class="nextstepaction"]
> [设置和获取敏感度标签](quick-file-set-get-label-cpp.md)
