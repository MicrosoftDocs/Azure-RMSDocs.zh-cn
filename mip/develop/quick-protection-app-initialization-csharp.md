---
title: 快速入门 - 客户端应用程序初始化 - 保护 API (C#)
description: 本快速入门介绍如何为 Microsoft 信息保护 (MIP) SDK - 保护 API C# 客户端应用程序编写初始化逻辑 (C#)
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: mbaldwin
ms.openlocfilehash: bfa1866618e65f1f9f215cb70fd76254623777d0
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865172"
---
# <a name="quickstart-client-application-initialization-for-protection-apis-c"></a>快速入门：保护 API (C#) 的客户端应用程序初始化

本快速入门教程将演示如何实现 MIP SDK .NET 包装器在运行时使用的客户端初始化模式。

> [!NOTE]
> 对于使用 MIP .NET 包装器的保护 API 的任何客户端应用程序，都需要执行本快速入门中概述的步骤。 此快速入门应在应用程序初始化并实现身份验证委托和同意委托类后按顺序进行。

## <a name="prerequisites"></a>必备条件

如果尚未准备，请务必：

- 完成 [Microsoft 信息保护 (MIP) SDK 安装和配置](setup-configure-mip.md)中的步骤。 此“保护配置文件和引擎设置”快速入门依赖于正确的 SDK 设置和配置。
- 可选：
  - 查看[配置文件和引擎对象](concept-profile-engine-cpp.md)。 配置文件和引擎对象是使用 MIP文件/策略/保护 API 的客户端所需的通用概念。
  - 查看[身份验证概念](concept-authentication-cpp.md)，了解 SDK 和客户端应用程序如何实现身份验证和同意。

## <a name="create-a-visual-studio-solution-and-project"></a>创建 Visual Studio 解决方案和项目

首先，创建并配置初始 Visual Studio 解决方案和项目，其他快速入门以该解决方案和项目为基础。

1. 打开 Visual Studio 2017，依次选择“文件”菜单、“新建”、“项目”    。 在“新建项目”对话框中： 
   - 在左窗格中的“已安装”、“Visual C#”下，选择“Windows 桌面”    。
   - 在中间窗格中，选择“控制台应用(.NET Framework)” 
   - 在底部窗格中，更新项目“名称”、“位置”以及对应的“解决方案名称”    。
   - 完成后，单击右下方的“确定”按钮  。

     [![创建 Visual Studio 解决方案](media/quick-app-initialization-csharp/create-vs-solution.png)](media/quick-app-initialization-csharp/create-vs-solution.png#lightbox)

2. 将 MIP SDK 文件 API 的 Nuget 包添加到项目中：
   - 在“解决方案资源管理器”中，右键单击项目节点（位于 top/solution 节点正下方），然后选择“管理 NuGet 包...”   ：
   - 在编辑器组选项卡区域中打开“NuGet 包管理器”选项卡时： 
     - 选择“浏览”  。
     - 在搜索框中输入“Microsoft.InformationProtection”。
     - 选择“Microsoft.InformationProtection.File”包。
     - 单击“安装”，出现“预览更改”确认对话框时单击“确定”  。

3. 重复上述步骤以添加 MIP SDK 保护 API 包，但改为将“Microsoft.IdentityModel.Clients.ActiveDirectory”添加到应用程序。

## <a name="implement-an-authentication-delegate-and-a-consent-delegate"></a>实现身份验证委托和同意委托

如果尚未实现，请按照 [文件 API 应用程序初始化](quick-app-initialization-csharp.md)中列出的步骤来实现身份验证和同意委托。

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>初始化 MIP SDK 托管的包装器

1. 在“解决方案资源管理器”中，打开项目中包含 `Main()` 方法的实现的 .cs 文件  。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

2. 删除生成的 `main()` 实现。

3. 托管包装器包含静态类 `Microsoft.InformationProtection.MIP`，用于初始化、创建 `MipContext`、加载配置文件和发布资源。 若要为文件 API 操作初始化包装器，请调用 `MIP.Initialize()`，同时传入 `MipComponent.Protection`，以加载保护操作所需的库。

4. 在 Program.cs 的 `Main()` 中添加以下内容，将 \<application-id\> 替换为之前创建的、Azure AD 应用程序注册的 ID。

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
    class Program
    {
        private const string clientId = "<application-id>";
        private const string appName = "<friendly-name>";

        static void Main(string[] args)
        {
            //Initialize Wrapper for Protection API operations
            MIP.Initialize(MipComponent.Protection);
        }
    }
}
```

## <a name="construct-a-protection-profile-and-engine"></a>构造保护配置文件和引擎

如前文所述，使用 MIP API 的 SDK 客户端需要配置文件和引擎对象。 通过添加代码来加载本机 DLL，然后实例化配置文件和引擎对象，以完成本快速入门的编码部分。

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
     class Program
     {
          private const string clientId = "<application-id>";
          private const string appName = "<friendly-name>";

          static void Main(string[] args)
          {
               // Initialize Wrapper for Protection API operations.
               MIP.Initialize(MipComponent.Protection);

               // Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId.
               ApplicationInfo appInfo = new ApplicationInfo()
               {
                    ApplicationId = clientId,
                    ApplicationName = appName,
                    ApplicationVersion = "1.0.0"
               };

               // Instantiate the AuthDelegateImpl object, passing in AppInfo.
               AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

               MipContext mipContext = MIP.CreateMipContext(appInfo,
                                        "mip_data",
                                        LogLevel.Trace,
                                        null,
                                        null);

               // Initialize and instantiate the ProtectionProfile.
               // Create the ProtectionProfileSettings object.
               // Initialize protection profile settings to create/use local state.
               var profileSettings = new ProtectionProfileSettings(mipContext,
                                        CacheStorageType.OnDiskEncrypted,                                        
                                        new ConsentDelegateImplementation());

               // Load the Profile async and wait for the result.
               var protectionProfile = Task.Run(async () => await MIP.LoadProtectionProfileAsync(profileSettings)).Result;

               // Create a ProtectionEngineSettings object, then use that to add an engine to the profile.
               var engineSettings = new ProtectionEngineSettings("user1@tenant.com", authDelegate, "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var protectionEngine = Task.Run(async () => await protectionProfile.AddEngineAsync(engineSettings)).Result;

               // Application Shutdown
               // handler = null; // This will be used in later quick starts.
               protectionEngine = null;
               protectionProfile = null;
               mipContext = null;
          }
     }
}
```

3. 使用以下值替换刚才粘贴的源代码中的占位符值：

   | 占位符 | 值 | 示例 |
   |:----------- |:----- |:--------|
   | \<application-id\> | 分配给在“MIP SDK 安装和配置”中注册的应用程序的 Azure AD 应用程序 ID（2 个实例）。  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<friendly-name\> | 用户定义的应用程序友好名称。 | AppInitialization |


4. 现在构建应用程序的最终版本并解决任何错误。 你的代码应能成功生成。

## <a name="next-steps"></a>后续步骤

现在已完成代码的初始化，可进入下一个快速入门，开始体验 MIP 保护 API。

> [!div class="nextstepaction"]
> [列出保护模板](quick-protection-list-templates-csharp.md)
