---
title: 快速入门 - Microsoft信息保护 (MIP) SDK C++ 客户端的初始化
description: 快速入门教程，演示如何为 Microsoft 信息保护 (MIP) SDK 客户端应用程序编写初始化逻辑。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 49a0588f4f4d91879899fc0ccd906490906250c0
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556072"
---
# <a name="quickstart-client-application-initialization-c"></a>快速入门：客户端应用程序初始化 (C++)

本快速入门教程将演示如何实现 MIP C++ SDK 在运行时使用的客户端初始化模式。 

> [!NOTE]
> 对于使用 MIP 文件、策略或保护 AP 的任何客户端应用程序，都需要执行本快速入门中概述的步骤。 虽然本快速入门演示的是文件 API 的使用，但同样的模式也适用于使用策略和保护 API 的客户端。 按顺序完成其余的快速入门，因为每一个都是在前一个的基础上构建的，本快速入门是第一个。

## <a name="prerequisites"></a>必备条件

如果尚未准备，请务必：

- 完成 [Microsoft 信息保护 (MIP) SDK 安装和配置](setup-configure-mip.md)中的步骤。 此“客户端应用程序初始化”快速入门依赖于正确的 SDK 安装和配置。
- 可选：
  - 查看[配置文件和引擎对象](concept-profile-engine-cpp.md)。 配置文件和引擎对象是使用 MIP文件/策略/保护 API 的客户端所需的通用概念。 
  - 查看[身份验证概念](concept-authentication-cpp.md)，了解 SDK 和客户端应用程序如何实现身份验证和同意。
  - 查看[观察程序概念](concept-async-observers.md)了解有关观察程序的详细信息以及实现方法。 MIP SDK 使用观察程序模式来实现异步事件通知。

## <a name="create-a-visual-studio-solution-and-project"></a>创建 Visual Studio 解决方案和项目

首先，创建并配置 Visual Studio 初始解决方案和项目，其他快速入门以该解决方案和项目为基础。 

1. 打开 Visual Studio 2017，依次选择“文件”菜单、“新建”、“项目”    。 在“新建项目”对话框中： 
   - 在左窗格中的“已安装”、“其他语言”下，选择“Visual C++”    。
   - 在中间窗格中，选择“Windows 控制台应用程序” 
   - 在底部窗格中，更新项目“名称”、“位置”以及对应的“解决方案名称”    。
   - 完成后，单击右下方的“确定”按钮  。

     [![创建 Visual Studio 解决方案](media/quick-app-initialization-cpp/create-vs-solution.png)](media/quick-app-initialization-cpp/create-vs-solution.png#lightbox)

2. 将 MIP SDK 文件 API 的 Nuget 包添加到项目中：
   - 在“解决方案资源管理器”中，右键单击项目节点（位于 top/solution 节点正下方），然后选择“管理 NuGet 包...”   ：
   - 在编辑器组选项卡区域中打开“NuGet 包管理器”选项卡时： 
     - 选择“浏览”  。
     - 在搜索框中输入“Microsoft.InformationProtection”。
     - 选择“Microsoft.InformationProtection.File”包。
     - 单击“安装”，出现“预览更改”确认对话框时单击“确定”  。
   
     [![在 Visual Studio 中添加 NuGet 包](media/quick-app-initialization-cpp/add-nuget-package.png)](media/quick-app-initialization-cpp/add-nuget-package.png#lightbox)
 
## <a name="implement-an-observer-class-to-monitor-the-file-profile-and-engine-objects"></a>实现一个观察程序类来监视 File 配置文件和引擎对象

现在，通过扩展 SDK 的 `mip::FileProfile::Observer` 类，为 File 配置文件观察程序类创建一个基本实现。 观察程序将被实例化并在以后使用，以监视 File 配置文件对象的加载，并将引擎对象添加到配置文件。

1. 向项目中添加一个新类，这将为你生成标头/.h 和实现/.cpp 文件：

   - 在“解决方案资源管理器”中，再次右键单击项目节点，选择“添加”，然后选择“类”    。
   - 在“添加类”对话框上： 
     - 在“类名”字段中，输入“profile_observer”  。 请注意，根据你输入的名称，会自动填充“.h 文件”和“.cpp 文件”字段   。
     - 完成后，单击“确定”按钮  。

     [![在 Visual Studio 中添加类](media/quick-app-initialization-cpp/add-class.png)](media/quick-app-initialization-cpp/add-class.png#lightbox)

2. 生成类的 .h 和 .cpp 文件之后，会在“编辑器组”选项卡中打开这两个文件。 现在更新每个文件以实现新的观察程序类：

   - 通过选择/删除生成的 `profile_observer` 类来更新“profile_observer.h”。 请勿删除上一步生成的预处理器指令 (#pragma, #include)  。 然后将以下源复制/粘贴到文件中，并放在任何现有的预处理器指令之后：

     ```cpp
     #include <memory>
     #include "mip/file/file_profile.h"

     class ProfileObserver final : public mip::FileProfile::Observer {
     public:
          ProfileObserver() { }
          void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
          void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
          void OnAddEngineSuccess(const std::shared_ptr<mip::FileEngine>& engine, const std::shared_ptr<void>& context) override;
          void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
     };
     ```

   - 通过选择/删除生成的 `profile_observer` 类实现，更新“profile_observer.cpp”。 请勿删除上一步生成的预处理器指令 (#pragma, #include)  。 然后将以下源复制/粘贴到文件中，并放在任何现有的预处理器指令之后：

     ```cpp
     #include <future>

     using std::promise;
     using std::shared_ptr;
     using std::static_pointer_cast;
     using mip::FileEngine;
     using mip::FileProfile;

     void ProfileObserver::OnLoadSuccess(const shared_ptr<FileProfile>& profile, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_value(profile);
     }

     void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_exception(error);
     }

     void ProfileObserver::OnAddEngineSuccess(const shared_ptr<FileEngine>& engine, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_value(engine);
     }

     void ProfileObserver::OnAddEngineFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_exception(error);
     }
     ```

3. （可选）使用 F6（生成解决方案）运行解决方案的某个测试编译/链接，确保它成功生成后再继续  。

## <a name="implement-an-authentication-delegate"></a>实现身份验证委托

MIP SDK 使用类可扩展性实现身份验证，该机制可与客户端应用程序共享身份验证工作。 客户端必须获取合适的 OAuth2 访问令牌，并在运行时提供给 MIP SDK。 

现在，通过扩展 SDK 的 `mip::AuthDelegate` 类，并覆盖/实现 `mip::AuthDelegate::AcquireOAuth2Token()` 纯虚函数，为身份验证委托创建实现。 身份验证委托将在以后由文件配置文件和文件引擎对象实例化并使用。

1. 使用我们在上一节的步骤 #1 中使用的相同 Visual Studio“添加类”功能，将另一个类添加到项目中。 这次，在“类名”字段中输入“auth_delegate”  。 

2. 现在更新每个文件以实现新的身份验证委托类：

   - 通过使用以下源替换所有生成的 `auth_delegate` 类代码来更新“auth_delegate.h”。 请勿删除上一步生成的预处理器指令 (#pragma, #include)： 

     ```cpp
     #include <string>
     #include "mip/common_types.h"

     class AuthDelegateImpl final : public mip::AuthDelegate {
     public:
          AuthDelegateImpl() = delete;        // Prevents default constructor

          AuthDelegateImpl(
            const std::string& appId)         // AppID for registered AAD app
            : mAppId(appId) {};

          bool AcquireOAuth2Token(            // Called by MIP SDK to get a token
            const mip::Identity& identity,    // Identity of the account to be authenticated, if known
            const OAuth2Challenge& challenge, // Authority (AAD tenant issuing token), and resource (API being accessed; "aud" claim).
            OAuth2Token& token) override;     // Token handed back to MIP SDK

     private:
          std::string mAppId;
          std::string mToken;
          std::string mAuthority;
          std::string mResource;
     };
     ```

   - 通过使用以下源替换所有生成的 `auth_delegate` 类实现来更新“auth_delegate.cpp”。 请勿删除上一步生成的预处理器指令 (#pragma, #include)  。 

     > [!IMPORTANT]
     > 以下令牌获取代码不适合生产使用。 在生产中，必须使用以下代码将其替换为动态获取令牌的代码：
     > - Azure AD 应用注册中指定的 appId 和 reply/redirect URI（回复/重定向 URI 必须与应用注册匹配） 
     > - SDK 在 `challenge` 参数中传递的权限和资源 URL（资源 URL 必须匹配应用注册的 API/权限） 
     > - 有效的应用/用户凭据，其中帐户与 SDK 传递的 `identity` 参数匹配。 OAuth2“本机”客户端应提示用户输入凭据并使用“授权代码”流。 OAuth2“机密客户端”可以使用自己的安全凭据和“客户端凭据”流（例如服务），或使用“授权代码”流（例如 Web 应用）提示用户输入凭据。 
     >
     > 获取 OAuth2 令牌是一种复杂的协议，通常使用库来完成。 根据需要，MIP SDK 将仅调用 TokenAcquireOAuth2Token()  。

     ```cpp
     #include <iostream>
     using std::cout;
     using std::cin;
     using std::string;

     bool AuthDelegateImpl::AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) 
     {
          // Acquire a token manually, reuse previous token if same authority/resource. In production, replace with token acquisition code.
          string authority = challenge.GetAuthority();
          string resource = challenge.GetResource();
          if (mToken == "" || (authority != mAuthority || resource != mResource))
          {
              cout << "\nRun the PowerShell script to generate an access token using the following values, then copy/paste it below:\n";
              cout << "Set $authority to: " + authority + "\n";
              cout << "Set $resourceUrl to: " + resource + "\n";
              cout << "Sign in with user account: " + identity.GetEmail() + "\n";
              cout << "Enter access token: ";
              cin >> mToken;
              mAuthority = authority;
              mResource = resource;
              system("pause");
          }

          // Pass access token back to MIP SDK
          token.SetAccessToken(mToken);

          // True = successful token acquisition; False = failure
          return true;
     }
     ```

3. （可选）使用 F6（生成解决方案）运行解决方案的某个测试编译/链接，确保它成功生成后再继续  。

## <a name="implement-a-consent-delegate"></a>实现同意委托

现在，通过扩展 SDK 的 `mip::ConsentDelegate` 类，并覆盖/实现 `mip::AuthDelegate::GetUserConsent()` 纯虚函数，为同意委托创建实现。 同意委托将在以后由文件配置文件和文件引擎对象实例化并使用。

1. 使用之前使用的相同 Visual Studio“添加类”功能，将另一个类添加到项目中。 这次，在“类名”字段中输入“consent_delegate”  。 

2. 现在更新每个文件以实现新的同意委托类：

   - 通过使用以下源替换所有生成的 `consent_delegate` 类代码来更新“consent_delegate.h”。 请勿删除上一步生成的预处理器指令 (#pragma, #include)： 

     ```cpp
     #include "mip/common_types.h"
     #include <string>

     class ConsentDelegateImpl final : public mip::ConsentDelegate {
     public:
          ConsentDelegateImpl() = default;
          virtual mip::Consent GetUserConsent(const std::string& url) override;
     };
     ```

   - 通过使用以下源替换所有生成的 `consent_delegate` 类实现来更新“consent_delegate.cpp”。 请勿删除上一步生成的预处理器指令 (#pragma, #include)  。 

     ```cpp
     #include <iostream>
     using mip::Consent;
     using std::string;

     Consent ConsentDelegateImpl::GetUserConsent(const string& url) 
     {
          // Accept the consent to connect to the url
          std::cout << "SDK will connect to: " << url << std::endl;
          return Consent::AcceptAlways;
     }
     ``` 
     
3. （可选）使用 F6（生成解决方案）运行解决方案的某个测试编译/链接，确保它成功生成后再继续  。

## <a name="construct-a-file-profile-and-engine"></a>构造文件配置文件和引擎

如前文所述，使用 MIP API 的 SDK 客户端需要配置文件和引擎对象。 通过添加代码来实例化配置文件和引擎对象，完成本快速入门的编码部分： 

1. 在“解决方案资源管理器”中，打开项目中包含 `main()` 方法的实现的 .cpp 文件  。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

2. 删除生成的 `main()` 实现。 请勿删除在项目创建期间 (#pragma, #include) 由 Visual Studio 生成的预处理程序指令  。 在任何预处理程序指令之后追加以下代码：

   ```cpp
   #include "mip/mip_init.h"
   #include "mip/mip_context.h"  
   #include "auth_delegate.h"
   #include "consent_delegate.h"
   #include "profile_observer.h"

   using std::promise;
   using std::future;
   using std::make_shared;
   using std::shared_ptr;
   using std::string;
   using std::cout;
   using mip::ApplicationInfo;
   using mip::FileProfile;
   using mip::FileEngine;

   int main()
   {
     // Construct/initialize objects required by the application's profile object
     ApplicationInfo appInfo{"<application-id>",                    // ApplicationInfo object (App ID, name, version)
                 "<application-name>",
                 "<application-version>"};

     auto mipContext = mip::MipContext::Create(appInfo,
                         "file_sample",
                         mip::LogLevel::Trace,
                         nullptr /*loggerDelegateOverride*/,
                         nullptr /*telemetryOverride*/);

     auto profileObserver = make_shared<ProfileObserver>();         // Observer object
     auto authDelegateImpl = make_shared<AuthDelegateImpl>(         // Authentication delegate object (App ID)
                 "<application-id>");
     auto consentDelegateImpl = make_shared<ConsentDelegateImpl>(); // Consent delegate object
 
     // Construct/initialize profile object
     FileProfile::Settings profileSettings(
       mipContext,
       mip::CacheStorageType::OnDisk,
       authDelegateImpl,
       consentDelegateImpl,
       profileObserver);

     // Set up promise/future connection for async profile operations; load profile asynchronously
     auto profilePromise = make_shared<promise<shared_ptr<FileProfile>>>();
     auto profileFuture = profilePromise->get_future();
    try
    { 
        mip::FileProfile::LoadAsync(profileSettings, profilePromise);
    }
    catch (const std::exception& e)
    {
        cout << "An exception occurred... are the Settings and ApplicationInfo objects populated correctly?\n\n"
            << e.what() << "'\n";
        system("pause");
        return 1;

    }
    auto profile = profileFuture.get();

     // Construct/initialize engine object
     FileEngine::Settings engineSettings(
       mip::Identity("<engine-account>"),         // Engine identity (account used for authentication)
       "<engine-state>",                          // User-defined engine state
       "en-US");                                  // Locale (default = en-US)

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
       cout << "An exception occurred... is the access token incorrect/expired?\n\n"
        << e.what() << "'\n";
       system("pause");
       return 1;
     }

   // Application shutdown. Null out profile and engine, call ReleaseAllResources();
   // Application may crash at shutdown if resources aren't properly released.
   // handler = nullptr; // This will be used in later quick starts.
   engine = nullptr;
   profile = nullptr;   
   mipContext = nullptr;

   return 0;
   }
   ``` 

3. 使用字符串常量替换刚才粘贴的源代码中的所有占位符值：

   | 占位符 | 值 | 示例 |
   |:----------- |:----- |:--------|
   | \<应用程序 ID\> | 分配给在[“MIP SDK 安装和配置”](/information-protection/develop/setup-configure-mip#register-a-client-application-with-azure-active-directory) 一文步骤 #2 中注册的应用程序的 Azure AD 应用程序 ID (GUID)。 替换 2 个实例。 | `"0edbblll-8773-44de-b87c-b8c6276d41eb"` |
   | \<application-name\> | 用户定义的应用程序友好名称。 必须包含有效的 ASCII 字符（不包括“;”），且最好与注册 Azure AD 时使用的应用程序名称一致。 | `"AppInitialization"` |
   | \<application-version\> | 用户定义的应用程序版本信息。 必须包含有效的 ASCII 字符（不包括“;”）。 | `"1.1.0.0"` |
   | \<引擎帐户\> | 用于引擎标识的帐户。 在令牌获取期间使用用户帐户进行身份验证时，它必须与此值匹配。 | `"user1@tenant.onmicrosoft.com"` |
   | \<引擎状态\> | 用户定义的与引擎关联的状态。 | `"My App State"` |


4. 现在构建应用程序的最终版本并解决任何错误。 代码应已成功构建，但在完成下一个快速入门之前，代码将无法正常运行。 如果运行该应用程序，将看到类似于以下内容的输出。 除非完成下一个快速入门，否则你将没有访问令牌可提供。

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account:
   Enter access token:
   ```

## <a name="next-steps"></a>后续步骤

现在已完成代码的初始化，可进入下一个快速入门，开始体验 MIP 文件 API。

> [!div class="nextstepaction"]
> [列出敏感度标签](quick-file-list-labels-cpp.md)
