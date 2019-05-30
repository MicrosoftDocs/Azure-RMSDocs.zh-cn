---
title: 快速入门 - 使用 MIP SDK C# 包装器列出 Microsoft 信息保护 (MIP) 租户中的敏感度标签
description: 一个演示如何使用 Microsoft 信息保护 SDK C# 包装器列出租户中的敏感度标签的快速入门。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: mbaldwin
ms.openlocfilehash: 0b1b110fe3b2e96c258c7b94a3d356b9404d6e7e
ms.sourcegitcommit: fe23bc3e24eb09b7450548dc32b4ef09c8970615
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2019
ms.locfileid: "60175579"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>快速入门：列出敏感度标签 (C#)

本快速入门演示如何使用 MIP SDK 文件 API 列出为组织配置的敏感度标签。

## <a name="prerequisites"></a>先决条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：客户端应用程序初始化 (C#)](quick-app-initialization-csharp.md)，生成 Visual Studio 初学者解决方案。 此“列出敏感度标签”快速入门需依赖前者来正确创建初学者解决方案。
- 可选：查看[分类标签](concept-classification-labels.md)概念。

## <a name="add-logic-to-list-the-sensitivity-labels"></a>添加用于列出敏感度标签的逻辑

使用文件引擎对象添加用于列出组织敏感度标签的逻辑。 

1. 打开在前面的“快速入门：客户端应用程序初始化 (C#)”一文中创建的 Visual Studio 解决方案。

2. 使用“解决方案资源管理器”，打开项目中包含 `Main()` 方法的实现的 .cs 文件  。 它默认与包含它的项目同名，即在项目创建期间指定的名称。 

3. 在 `Main()` 正文的末尾，在 `Main()` 函数的右大括号 `}` 下面（在上一快速入门中离开的位置）插入以下代码：

  ```csharp
  // List sensitivity labels from fileEngine and display name and id  
  foreach(var label in fileEngine.SensitivityLabels)
  {
      Console.WriteLine(string.Format("{0} : {1}", label.Name, label.Id));

      if (label.Children.Count != 0)
      {
          foreach (var child in label.Children)
          {
              Console.WriteLine(string.Format("{0}{1} : {2}", "\t",child.Name, child.Id));
          }
      }
  }
  ``` 

## <a name="build-and-test-the-application"></a>生成和测试应用程序

最后，生成和测试客户端应用程序。 

1. 使用 CTRL-SHIFT-B（“生成解决方案”）来生成客户端应用程序  。 如果没有生成错误，请使用 F5（开始调试  ）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireToken()` 方法时，应用程序都可能提示通过 ADAL 进行身份验证  。 如果已存在缓存凭据，则不会提示登录和查看标签列表。 

     [![Visual Studio 获取令牌登录](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - 可能还需同意应用程序在登录帐户下运行时访问 MIP API。 如果未事先同意 Azure AD 应用程序注册（如“MIP SDK 安装和配置”中所述），或者使用其他租户（而非应用程序注册所在的租户）中的帐户登录，就会出现这种情况。 只需单击“接受”即可记录你的同意  。

     [![Visual Studio 同意](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. 进行身份验证后，控制台输出应显示敏感度标签，类似于以下示例：

  ```console
  Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
  Public : 73254501-3d5b-4426-979a-657881dfcb1e
  General : da480625-e536-430a-9a9e-028d16a29c59
  Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
        Recipients Only (C) : d98c4267-727b-430e-a2d9-4181ca5265b0
        All Employees (C) : 2096f6a2-d2f7-48be-b329-b73aaa526e5d
        Anyone (not protected) (C) : 63a945ec-1131-420d-80da-2fedd15d3bc0
  Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
        Recipients Only : 05ee72d9-1a75-441f-94e2-dca5cacfe012
        All Employees : 922b06ef-044b-44a3-a8aa-df12509d1bfe
        Anyone (not protected) : c83fc820-961d-40d4-ba12-c63f72a970a3
  Press a key to continue.
  ```

   > [!NOTE]
   > 复制并保存一个或多个敏感度标签的 ID（例如，`f42a3342-8706-4288-bd31-ebb85995028z`），因为你将在下一个快速入门中使用它。

## <a name="troubleshooting"></a>故障排除

### <a name="problems-during-execution-of-c-application"></a>执行 C# 应用程序时出现的问题

| 摘要 | 错误消息 | 解决方案 |
|---------|---------------|----------|
| 访问令牌不正确 | 发生异常...访问令牌是否不正确/过期?<br><br>API 调用失败: profile_add_engine_asyn 失败原因: [class mip::PolicySyncException] 策略获取失败，请求失败并显示 http 状态代码:  401，x-ms-diagnostics: [2000001;reason=“无法解析随请求提交的 OAuth 令牌。”;error_category="invalid_token"]，correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (process 29924) 已退出，代码为 0。<br><br>按任意键关闭此窗口... | 如果项目成功生成，但出现类似于左侧的输出，则表示 `AcquireOAuth2Token()` 方法中可能包含无效或过期的令牌。 返回到[生成并测试应用程序](#build-and-test-the-application)并重写访问令牌，再次更新 `AcquireOAuth2Token()`，然后重新生成/重新测试。 还可以使用 [jwt.ms](https://jwt.ms/) 单页 Web 应用程序检查并验证令牌及其声明。 |
| 未配置敏感度标签 | n/a | 如果项目成功生成，但在控制台窗口中没有输出，请确保正确配置了组织的敏感度标签。 请参阅 [MIP SDK 安装和配置](setup-configure-mip.md)，在“定义标签分类和保护设置”下获取详细信息。  |

## <a name="next-steps"></a>后续步骤

你已经了解如何列出组织的敏感度标签，现在尝试下一个快速入门：

> [!div class="nextstepaction"]
> [设置和获取敏感度标签](quick-file-set-get-label-csharp.md)
