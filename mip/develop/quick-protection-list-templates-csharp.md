---
title: 快速入门 - 使用 MIP SDK C# 包装器列出可供 Microsoft 信息保护 (MIP) 租户中经过身份验证的用户使用的保护模板
description: 快速入门介绍如何使用 Microsoft 信息保护 SDK 保护 API C# 包装器列出可供用户使用的保护模板。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.custom: has-adal-ref
ms.openlocfilehash: 7b9a8d916b0c3c4b8aaa006abdf27cd8c02a7f6e
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91588251"
---
# <a name="quickstart-list-templates-c"></a>快速入门：列出模板 (C#)

本快速入门介绍如何使用 MIP SDK 保护 API 列出可供用户使用的保护模板。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：客户端应用程序初始化 - 保护 API (C#)](quick-protection-app-initialization-csharp.md)，以生成 Visual Studio 初学者解决方案。 此“列出保护模板”快速入门需依赖前者来正确创建初学者解决方案。
- 可选：查看 [RMS 模板](/azure/information-protection/configure-policy-templates)概念。

## <a name="add-logic-to-list-the-protection-templates"></a>添加逻辑以列出保护模板

使用保护引擎对象添加逻辑以列出可供用户使用的保护模板。

1. 打开在前面的“快速入门 - 客户端应用程序初始化 - 保护 API (C#)”一文中创建的 Visual Studio 解决方案。

2. 使用“解决方案资源管理器”，打开项目中包含 `Main()` 方法的实现的 .cs 文件  。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

3. 在靠近 `Main()` 主体的末尾处，在 `Main()` 函数的应用程序关闭部分上方（即在上一快速入门中离开的位置）插入以下代码：

  ```csharp
  // List protection templates using protectionEngine and display the list

  var templates=protectionEngine.GetTemplates();

  for(int i = 0; i < templates.Count; i++)
  {
      Console.WriteLine("{0}: {1}", i.ToString(), templates[i].Name + " : " + templates[i].Id);
  }

  Console.WriteLine("Press a key to continue...");
  ```

## <a name="build-and-test-the-application"></a>生成和测试应用程序

最后，生成和测试客户端应用程序。

1. 使用 CTRL-SHIFT-B（“生成解决方案”）来生成客户端应用程序  。 如果没有生成错误，请使用 F5（开始调试  ）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireToken()` 方法时，应用程序都可能提示通过 ADAL 进行身份验证  。 如果已有缓存凭据，你就不会看到登录和查看标签列表的提示。

     [![Visual Studio 获取令牌登录](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - 可能还需同意应用程序在登录帐户下运行时访问 MIP API。 如果未事先同意 Azure AD 应用程序注册（如“MIP SDK 安装和配置”中所述），或者使用其他租户（而非应用程序注册所在的租户）中的帐户登录，就会出现这种情况。 只需单击“接受”即可记录你的同意  。

     [![Visual Studio 同意](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. 进行身份验证后，控制台输出应显示经身份验证的用户的保护模板，类似于以下示例：

  ```console
  0: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
  1: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
  2: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
  3: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
  Press a key to continue.
  ```

   > [!NOTE]
   > 复制并保存一个或多个保护模板的 ID（例如，`bb7ed207-046a-4caf-9826-647cff56b990`），因为你将在下一个快速入门中使用它。

## <a name="troubleshooting"></a>疑难解答

### <a name="problems-during-execution-of-c-application"></a>执行 C# 应用程序时出现的问题

| “摘要” | 错误消息 | 解决方案 |
|---------|---------------|----------|
| 访问令牌不正确 | 发生异常...访问令牌是否不正确/过期?<br><br>API 调用失败: profile_add_engine_asyn 失败原因: [class mip::PolicySyncException] 策略获取失败，请求失败并显示 http 状态代码:  401，x-ms-diagnostics: [2000001;reason=“无法解析随请求提交的 OAuth 令牌。”;error_category="invalid_token"]，correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) 已退出，代码为 0。<br><br>按任意键关闭此窗口... | 如果项目成功生成，但出现类似于左侧的输出，则表示 `AcquireOAuth2Token()` 方法中可能包含无效或过期的令牌。 返回到[生成并测试应用程序](#build-and-test-the-application)并重写访问令牌，再次更新 `AcquireOAuth2Token()`，然后重新生成/重新测试。 还可以使用 [jwt.ms](https://jwt.ms/) 单页 Web 应用程序检查并验证令牌及其声明。 |

## <a name="next-steps"></a>后续步骤

你已经了解如何列出可供经过身份验证的用户使用的保护模板，现在尝试下一个快速入门：

> [!div class="nextstepaction"]
> [快速入门 - 加密和解密文本](quick-protection-encrypt-decrypt-text-csharp.md)