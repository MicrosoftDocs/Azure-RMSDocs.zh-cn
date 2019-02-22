---
title: 快速入门-初始化为 Microsoft 信息保护 (MIP) SDKC#客户端
description: 向您展示如何编写的 Microsoft 信息保护 (MIP) SDK 的初始化逻辑的快速入门C#客户端应用程序。
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: b7f2b25027502fbdd9dd7bd877b8893c1940628a
ms.sourcegitcommit: ca2df73f8bba6bf0f58eea5bee15e356705276d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2019
ms.locfileid: "56589979"
---
# <a name="quickstart-client-application-initialization-c"></a>快速入门：客户端应用程序初始化 (C#)

本快速入门教程将演示如何实现 MIP SDK.NET 包装在运行时所使用的客户端初始化模式。

> [!NOTE]
> 在本快速入门中所述的步骤所需的任何使用 MIP.NET 包装器的文件或策略 Api 的客户端应用程序。 保护 API 尚不可用。 虽然本快速入门演示的是文件 API 的使用，但同样的模式也适用于使用策略和保护 API 的客户端。 之后的快速入门应是按顺序完成的，因为每一个都是在前一个的基础上构建的，本快速入门是第一个。

## <a name="prerequisites"></a>先决条件

如果尚未准备，请务必：

- 完成 [Microsoft 信息保护 (MIP) SDK 安装和配置](setup-configure-mip.md)中的步骤。 此“客户端应用程序初始化”快速入门依赖于正确的 SDK 安装和配置。
- 可选：
  - 查看[配置文件和引擎对象](concept-profile-engine-cpp.md)。 配置文件和引擎对象是使用 MIP文件/策略/保护 API 的客户端所需的通用概念。 
  - 查看[身份验证概念](concept-authentication-cpp.md)，了解 SDK 和客户端应用程序如何实现身份验证和同意。

## <a name="create-a-visual-studio-solution-and-project"></a>创建 Visual Studio 解决方案和项目

首先，创建并配置初始 Visual Studio 解决方案和项目，其他快速入门以该解决方案和项目为基础。

1. 打开 Visual Studio 2017，依次选择“文件”菜单、“新建”、“项目”。 在“新建项目”对话框中：
   - 在左窗格中下,**已安装**， **Visual C#** ，选择**Windows Desktop**。
   - 在中心窗格中，选择**控制台应用 (.NET Framework)**
   - 在底部窗格中，更新项目“名称”、“位置”以及对应的“解决方案名称”。
   - 完成后，单击右下方的“确定”按钮。 

     [![创建 Visual Studio 解决方案](media/quick-app-initialization-csharp/create-vs-solution.png)](media/quick-app-initialization-csharp/create-vs-solution.png#lightbox)

2. 将 MIP SDK 文件 API 的 Nuget 包添加到项目中：
   - 在“解决方案资源管理器”中，右键单击项目节点（位于 top/solution 节点正下方），然后选择“管理 NuGet 包...”：
   - 在编辑器组选项卡区域中打开“NuGet 包管理器”选项卡时：
     - 选择“浏览”。
     - 在搜索框中输入“Microsoft.InformationProtection”。
     - 选择“Microsoft.InformationProtection.File”包。
     - 单击“安装”，出现“预览更改”确认对话框时单击“确定”。

3. 重复上述步骤用于添加 MIP SDK 文件 API 包，但改为将"Microsoft.IdentityModel.Clients.ActiveDirectory"添加到应用程序。

## <a name="implement-an-authentication-delegate"></a>实现身份验证委托

MIP SDK 使用类可扩展性实现身份验证，该机制可与客户端应用程序共享身份验证工作。 客户端必须获取合适的 OAuth2 访问令牌，并在运行时提供给 MIP SDK。

现在通过扩展 SDK 的一个身份验证的委托，为创建一个实现`Microsoft.InformationProtection.IAuthDelegate`接口，并且重写/实现`IAuthDelegate.AcquireToken()`虚函数。 实例化和更高版本使用的身份验证委托`FileProfile`和`FileEngine`对象。

1. 右键单击项目名称，在 Visual Studio 中，选择**外**然后**类**。
2. 输入"AuthDelegateImplementation"中**名称**字段。 单击 **“添加”**。
3. 添加 Active Directory 身份验证库 (ADAL) 和 MIP 库 using 语句：

     ```csharp
     using Microsoft.InformationProtection;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
     ```

4. 设置`AuthDelegateImplementation`继承`Microsoft.InformationProtection.IAuthDelegate`和实现的私有变量`Microsoft.InformationProtection.ApplicationInfo`和接受相同类型的构造函数。

     ```csharp
     public class AuthDelegateImplementation : IAuthDelegate
     {
        private ApplicationInfo _appInfo;
        private string redirectUri = "mip-sdk-app://authorize";
        public AuthDelegateImplementation(ApplicationInfo appInfo)
        {
            _appInfo = appInfo;
        }
     }
     ```

`ApplicationInfo`对象包含两个属性。 `_appInfo.ApplicationId`中将使用`AuthDelegateImplementation`类以提供对身份验证库的客户端 ID。

5. 添加`public string AcquireToken()`方法。 此方法应接受`Microsoft.InformationProtection.Identity`和两个字符串： 颁发机构和资源。 这些字符串变量会传递给身份验证库 api，不应进行操作。 编辑可能会导致身份验证失败。

     ```csharp
     public string AcquireToken(Identity identity, string authority, string resource)
     {
          AuthenticationContext authContext = new AuthenticationContext(authority);
          var result = authContext.AcquireTokenAsync(resource, _appInfo.ApplicationId, new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, null), UserIdentifier.AnyUser).Result;
          return result.AccessToken;
     }
     ```

## <a name="implement-a-consent-delegate"></a>实现同意委托

现在通过扩展 SDK 的同意委托，为创建一个实现`Microsoft.InformationProtection.IConsentDelegate`接口，并且重写/实现`GetUserConsent()`。 同意委托将在以后由文件配置文件和文件引擎对象实例化并使用。 同意委托是提供服务的地址与用户必须同意在使用`url`参数。 委托通常应提供允许用户接受或拒绝同意访问服务的某些流。 此快速入门硬代码`Consent.Accept`。

1. 使用之前使用的相同 Visual Studio“添加类”功能，将另一个类添加到项目中。 这一次，输入"ConsentDelegateImplementation"中**类名**字段。 

2. 现在，更新**ConsentDelegateImpl.cs**实现新的许可委托类。 添加以下 using 语句`Microsoft.InformationProtection`并设置要继承的类`IConsentDelegate`。

     ```csharp
     class ConsentDelegateImplementation : IConsentDelegate
     {
          public Consent GetUserConsent(string url)
          {
               return Consent.Accept;
          }
     }
     ```

3. （可选） 尝试生成解决方案以确保它在编译时且未出错。

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>初始化 MIP SDK 托管的包装

1. 从**解决方案资源管理器**，打开项目，其中包含的实现中的.cs 文件`Main()`方法。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

2. 删除生成的 `main()` 实现。 

3. 托管包装器包括一个静态类`Microsoft.InformationProtection.MIP`用于初始化、 加载配置文件，并释放资源。 若要初始化文件 API 操作的包装器，请调用 MIP。初始化，并传入`MipComponent.File`加载文件操作所需的库。 

4. 在中`Main()`中*Program.cs*添加以下、 替换**\<应用程序 id\>** 以前创建的 Azure AD 应用程序注册 id。

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
            //Initialize Wrapper for File API operations 
            MIP.Initialize(MipComponent.File);
        }
    }
}
```

## <a name="construct-a-file-profile-and-engine"></a>构造文件配置文件和引擎

如前文所述，不需要使用 MIP Api 的 SDK 客户端的配置文件和引擎对象。 通过添加代码以加载本机 Dll，然后实例化的配置文件和引擎对象来完成本快速入门的编码部分。

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
               //Initialize Wrapper for File API operations
               MIP.Initialize(MipComponent.File);

               //Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId
               ApplicationInfo appInfo = new ApplicationInfo()
               {
                    ApplicationId = clientId,
                    ApplicationName = appName,
                    ApplicationVersion = "1.0.0"
               };

               //Instatiate the AuthDelegateImpl object, passing in AppInfo. 
               AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

               //Initialize and instantiate the File Profile
               //Create the FileProfileSettings object
               var profileSettings = new FileProfileSettings("mip_data", false, authDelegate, new ConsentDelegateImplementation(), appInfo, LogLevel.Trace);

               //Load the Profile async and wait for the result
               var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

               //Create a FileEngineSettings object, then use that to add an engine to the profile
               var engineSettings = new FileEngineSettings("user1@tenant.com", "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;
          }
     }
}
``` 

3. 在中，使用以下值粘贴的源代码中的占位符值替换：

   | 占位符 | 值 | 示例 |
   |:----------- |:----- |:--------|
   | \<应用程序 ID\> | 分配给在“MIP SDK 安装和配置”中注册的应用程序的 Azure AD 应用程序 ID（2 个实例）。  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<友好名称\> | 用户定义的应用程序友好名称。 | AppInitialization |


4. 现在构建应用程序的最终版本并解决任何错误。 你的代码应能成功生成。

## <a name="next-steps"></a>后续步骤

现在已完成代码的初始化，可进入下一个快速入门，开始体验 MIP 文件 API。

> [!div class="nextstepaction"]
> [列出敏感度标签](quick-file-list-labels-csharp.md)
