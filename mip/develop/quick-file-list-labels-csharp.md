---
title: 快速入门-使用 MIP SDK 对 Microsoft 信息保护 (MIP) 租户中的列表敏感度标签C#包装器
description: 向您展示如何使用 Microsoft 信息保护 SDK 的快速入门C#包装器，若要列出你的租户中的敏感度标签。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: mbaldwin
ms.openlocfilehash: 0b1b110fe3b2e96c258c7b94a3d356b9404d6e7e
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60175579"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>快速入门：列出敏感度标签 (C#)

本快速入门介绍如何使用 MIP SDK 文件 API 列出为你的组织配置的敏感度标签。

## <a name="prerequisites"></a>先决条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 完整[快速入门：客户端应用程序初始化 (C#)](quick-app-initialization-csharp.md)第一种方法生成初学者的 Visual Studio 解决方案。 此“列出敏感度标签”快速入门需依赖前者来正确创建初学者解决方案。
- 可选：审阅[分类标签](concept-classification-labels.md)概念。

## <a name="add-logic-to-list-the-sensitivity-labels"></a>添加用于列出敏感度标签的逻辑

使用文件引擎对象添加用于列出组织敏感度标签的逻辑。 

1. 打开在以前创建的 Visual Studio 解决方案"快速入门：客户端应用程序初始化 (C#)"一文。

2. 使用**解决方案资源管理器**，打开项目，其中包含的实现中的.cs 文件`Main()`方法。 它默认与包含它的项目同名，即在项目创建期间指定的名称。 

3. 年底`Main()`正文中的，右大括号下方`}`的`Main()`函数 （离开的位置在前面的快速入门） 中，插入以下代码：

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

1. 使用 CTRL-SHIFT-B (**生成解决方案**) 来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果你的项目成功生成和运行，应用程序*可能*提示进行身份验证通过 ADAL 每个时间的 SDK 调用你`AcquireToken()`方法。 如果存在缓存的凭据，则不会提示登录，并查看标签的列表。 

     [![Visual Studio 获取令牌登录](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - 可能还需同意应用程序在登录帐户下运行时访问 MIP API。 如果未事先同意 Azure AD 应用程序注册（如“MIP SDK 安装和配置”中所述），或者使用其他租户（而非应用程序注册所在的租户）中的帐户登录，就会出现这种情况。 只需单击“接受”即可记录你的同意。

     [![Visual Studio 同意](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. 身份验证后，控制台输出应显示类似于下面的示例的敏感度标签：

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

## <a name="troubleshooting"></a>疑难解答

### <a name="problems-during-execution-of-c-application"></a>过程的执行中出现问题C#应用程序

| 总结 | 错误消息 | 解决方案 |
|---------|---------------|----------|
| 访问令牌不正确 | *发生了异常...是不正确/已过期的访问令牌？<br><br>失败的 API 调用： profile_add_engine_async 失败: [类 mip::PolicySyncException] 无法获取策略、 请求失败，http 状态代码：401，x 的 ms-诊断: [2000001; 原因 ="与请求一起提交的 OAuth 令牌无法分析。";error_category ="invalid_token"]，相关 Id: [35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe （进程 29924） 已退出，代码 0。<br><br>按任意键关闭此窗口...* | 如果项目成功生成，但出现类似于左侧的输出，则表示 `AcquireOAuth2Token()` 方法中可能包含无效或过期的令牌。 返回到[生成和测试应用程序](#build-and-test-the-application)，并重新生成访问令牌，更新`AcquireOAuth2Token()`试，并重新生成/重新测试。 还可以使用 [jwt.ms](https://jwt.ms/) 单页 Web 应用程序检查并验证令牌及其声明。 |
| 未配置敏感度标签 | n/a | 如果项目成功生成，但在控制台窗口中没有输出，请确保正确配置了组织的敏感度标签。 请参阅 [MIP SDK 安装和配置](setup-configure-mip.md)，在“定义标签分类和保护设置”下获取详细信息。  |

## <a name="next-steps"></a>后续步骤

你已经了解如何列出组织的敏感度标签，现在尝试下一个快速入门：

> [!div class="nextstepaction"]
> [设置和获取敏感度标签](quick-file-set-get-label-csharp.md)
