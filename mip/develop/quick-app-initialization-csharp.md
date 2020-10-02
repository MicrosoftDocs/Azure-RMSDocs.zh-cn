---
title: 快速入门 - Microsoft 信息保护 (MIP) SDK C# 客户端的初始化
description: 一个演示如何为 Microsoft 信息保护 (MIP) SDK C# 客户端应用程序编写初始化逻辑的快速入门。
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.date: 09/15/2020
ms.author: tommos
ms.custom: has-adal-ref
ms.openlocfilehash: 406068f5770f489c66963fc34a462ec7e205765b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "91108956"
---
# <a name="quickstart-client-application-initialization-c"></a>快速入门：客户端应用程序初始化 (C#)

本快速入门教程将演示如何实现 MIP SDK .NET 包装器在运行时使用的客户端初始化模式。

> [!NOTE]
> 对于使用 MIP .NET 包装器的文件或策略 API 的任何客户端应用程序，都需要执行本快速入门中概述的步骤。 保护 API 还不可用。 虽然本快速入门演示的是文件 API 的使用，但同样的模式也适用于使用策略和保护 API 的客户端。 之后的快速入门应是按顺序完成的，因为每一个都是在前一个的基础上构建的，本快速入门是第一个。

## <a name="prerequisites"></a>必备条件

如果尚未准备，请务必：

- 完成 [Microsoft 信息保护 (MIP) SDK 安装和配置](setup-configure-mip.md)中的步骤。 此“客户端应用程序初始化”快速入门依赖于正确的 SDK 安装和配置。
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

3. 重复上述步骤以添加 MIP SDK 文件 API 包，但改为将“Microsoft.Identity.Client”添加到应用程序。

## <a name="implement-an-authentication-delegate"></a>实现身份验证委托

MIP SDK 使用类可扩展性实现身份验证，该机制可与客户端应用程序共享身份验证工作。 客户端必须获取合适的 OAuth2 访问令牌，并在运行时提供给 MIP SDK。

现在，通过扩展 SDK 的 `Microsoft.InformationProtection.IAuthDelegate` 接口，并覆盖/实现 `IAuthDelegate.AcquireToken()` 虚拟函数，为身份验证委托创建实现。 `FileProfile` 和 `FileEngine` 对象稍后将实例化并使用身份验证委托。

1. 在 Visual Studio 中右键单击项目名称，依次选择“添加”、“类”   。
2. 在名称字段中输入“AuthDelegateImplementation”  。 单击“添加”  。
3. 为 Microsoft 身份验证库 (ADAL) 和 MIP 库添加 using 语句：

     ```csharp
     using Microsoft.InformationProtection;
     using Microsoft.Identity.Client;
     ```

4. 将 `AuthDelegateImplementation` 设置为继承 `Microsoft.InformationProtection.IAuthDelegate` 并实现 `Microsoft.InformationProtection.ApplicationInfo` 的专用变量和实现接受相同类型的构造函数。

     ```csharp
     public class AuthDelegateImplementation : IAuthDelegate
    {
        private ApplicationInfo _appInfo;
        // Microsoft Authentication Library IPublicClientApplication
        private IPublicClientApplication _app;
        public AuthDelegateImplementation(ApplicationInfo appInfo)
        {
            _appInfo = appInfo;
        }

    }
     ```

    `ApplicationInfo` 对象包含三个属性。 `AuthDelegateImplementation` 类中将使用 `_appInfo.ApplicationId`，以便向身份验证库提供客户端 ID。 `ApplicationName` 和 `ApplicationVersion` 将出现在 Azure 信息保护分析报告中。

5. 添加 `public string AcquireToken()` 方法。 此方法应接受 `Microsoft.InformationProtection.Identity` 和三个字符串：颁发机构 URL、资源 URI 和声明（如果需要）。 这些字符串变量将被 API 传递到身份验证库，不应对其进行操作。 请为租户输入 Azure 门户中的租户 GUID。 编辑为租户 GUID 以外的字符串可能会导致身份验证失败。

     ```csharp
    public string AcquireToken(Identity identity, string authority, string resource, string claims)
    {
        var authorityUri = new Uri(authority);
        authority = String.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

        _app = PublicClientApplicationBuilder.Create(_appInfo.ApplicationId).WithAuthority(authority).WithDefaultRedirectUri().Build();
        var accounts = (_app.GetAccountsAsync()).GetAwaiter().GetResult();

        // Append .default to the resource passed in to AcquireToken().
        string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
        var result = _app.AcquireTokenInteractive(scopes).WithAccount(accounts.FirstOrDefault()).WithPrompt(Prompt.SelectAccount)
                   .ExecuteAsync().ConfigureAwait(false).GetAwaiter().GetResult();

        return result.AccessToken;
    }

     ```

## <a name="implement-a-consent-delegate"></a>实现同意委托

现在，通过扩展 SDK 的 `Microsoft.InformationProtection.IConsentDelegate` 接口，并覆盖/实现 `GetUserConsent()`，为同意委托创建实现。 同意委托将在以后由文件配置文件和文件引擎对象实例化并使用。 向同意委托提供在 `url` 参数中使用的、用户必须同意的服务的地址。 委托通常应提供一些流程，使用户能接受或拒绝同意服务访问请求。 对于此快速入门，硬编码 `Consent.Accept`。

1. 使用之前使用的相同 Visual Studio“添加类”功能，将另一个类添加到项目中。 这次，在“类名”字段中输入“ConsentDelegateImplementation”****。

2. 现在更新 ConsentDelegateImpl.cs 以实现新的同意委托类****。 为 `Microsoft.InformationProtection` 添加 using 语句并将类设置为继承 `IConsentDelegate`。

     ```csharp
     class ConsentDelegateImplementation : IConsentDelegate
     {
          public Consent GetUserConsent(string url)
          {
               return Consent.Accept;
          }
     }
     ```

3. 或可尝试生成解决方案以确保其编译时不出错。

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>初始化 MIP SDK 托管的包装器

1. 在“解决方案资源管理器”中，打开项目中包含 `Main()` 方法的实现的 .cs 文件****。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

2. 删除生成的 `main()` 实现。

3. 托管包装器包含静态类 `Microsoft.InformationProtection.MIP`，用于初始化、创建 `MipContext`、加载配置文件和发布资源。 若要为文件 API 操作初始化包装器，请调用 `MIP.Initialize()`，同时传入 `MipComponent.File`，以加载文件操作所需的库。

4. 在 Program.cs 的 `Main()` 中添加以下内容，将 \<application-id\> 替换为之前创建的、Azure AD 应用程序注册的 ID。

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.File;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
    class Program
    {
        private const string clientId = "<application-id>";
        private const string appName = "<friendly-name>";

        static void Main(string[] args)
        {
            //Initialize Wrapper for File API operations
            MIP.Initialize(MipComponent.File);
        }
    }
}
```

## <a name="construct-a-file-profile-and-engine"></a>构造文件配置文件和引擎

如前文所述，使用 MIP API 的 SDK 客户端需要配置文件和引擎对象。 通过添加代码来加载本机 DLL，然后实例化配置文件和引擎对象，以完成本快速入门的编码部分。


   ```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.File;

namespace mip_sdk_dotnet_quickstart
{
     class Program
     {
          private const string clientId = "<application-id>";
          private const string appName = "<friendly-name>";

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

               MipContext mipContext = MIP.CreateMipContext(appInfo,
                                        "mip_data",
                                        LogLevel.Trace,
                                        null,
                                        null);

               // Initialize and instantiate the File Profile.
               // Create the FileProfileSettings object.
               // Initialize file profile settings to create/use local state.
               var profileSettings = new FileProfileSettings(mipContext,
                                        CacheStorageType.OnDiskEncrypted,
                                        new ConsentDelegateImplementation());

               // Load the Profile async and wait for the result.
               var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

               // Create a FileEngineSettings object, then use that to add an engine to the profile.
               var engineSettings = new FileEngineSettings("user1@tenant.com", authDelegate "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;

               // Application Shutdown
               // handler = null; // This will be used in later quick starts.
               fileEngine = null;
               fileProfile = null;
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
   | \<Tenant-GUID\> | 你的 Azure AD 租户的租户-ID | TenantID |


4. 现在构建应用程序的最终版本并解决任何错误。 你的代码应能成功生成。

## <a name="next-steps"></a>后续步骤

现在已完成代码的初始化，可进入下一个快速入门，开始体验 MIP 文件 API。

> [!div class="nextstepaction"]
> [列出敏感度标签](quick-file-list-labels-csharp.md)
