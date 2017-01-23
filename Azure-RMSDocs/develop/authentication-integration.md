---
title: "如何使用 Azure AD 注册应用并为其启用 RMS | Azure RMS"
description: "介绍针对启用 RMS 的应用的用户身份验证基础知识。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 10/18/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 200D9B23-F35D-4165-9AC4-C482A5CE1D28
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 0f5b3de4607e5e889448b381f5835b4a75c9b0c2


---

# <a name="how-to-register-and-rms-enable-your-app-with-azure-ad"></a>如何使用 Azure AD 注册应用并为其启用 RMS

本主题将指导你了解有关通过 Azure 门户注册应用和启用 RMS，以及使用 Azure Active Directory 身份验证库 (ADAL) 进行用户身份验证的基础知识。

## <a name="what-is-user-authentication"></a>什么是用户身份验证
用户身份验证是在设备应用与 RMS 基础结构之间建立通信的必要步骤。 此身份验证过程使用标准 OAuth 2.0 协议，该协议需要有关当前用户及其身份验证请求的关键信息。

## <a name="registration-via-azure-portal"></a>通过 Azure 门户注册
首先，按照此指南开始通过 Azure 门户配置应用的注册，如[为 ADAL 身份验证配置 Azure RMS](adal-auth.md) 中所述。 请务必从此过程复制并保存“客户端 ID”和“重定向 URI”以便稍后使用。

## <a name="complete-your-rights-managagment-license-agreement-rmla"></a>完成你的权限管理许可协议 (RMLA)
在部署你的应用程序之前，必须与 Microsoft 权限管理团队一起完成 RMLA。 有关完整的详细信息，请参阅该主题的第一部分 [Deploy into production - Request a Production License Agreement](deploying-your-application.md)（部署到生产环境 - 请求生产许可协议）。

## <a name="implement-user-authentication-for-your-app"></a>为你的应用实施用户身份验证
每个 RMS API 都具有回调，必须实现它才能启用用户的身份验证。 然后 RMS SDK 4.2 会在你未提供访问令牌时、你的访问令牌需要刷新时或是访问令牌已过期时使用你的回调实现。

- Android -  [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) 和 [AuthenticationCompletionCallback](https://msdn.microsoft.com/library/dn758250.aspx) 接口。
- iOS / OS X -  [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) 协议。
-  Windows Phone / Window RT -  [IAuthenticationCallback](https://msdn.microsoft.com/library/microsoft.rightsmanagement.iauthenticationcallback.aspx) 接口。
- Linux -  [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html) 接口。

### <a name="what-library-to-use-for-authentication"></a>要用于身份验证的库是什么
若要实现身份验证回调，需要下载相应的库并配置开发环境以使用它。 可在 GitHub 上找到适用于这些平台的 ADAL 库。

以下每个资源都包含设置环境和使用库的指南。

-   [适用于 iOS 的 Windows Azure Active Directory 身份验证库 (ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [适用于 Mac 的 Windows Azure Active Directory 身份验证库 (ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [适用于 Android 的 Windows Azure Active Directory 身份验证库 (ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [适用于 dotnet 的 Windows Azure Active Directory 身份验证库 (ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   对于 Linux SDK，ADAL 库与 SDK 源（可通过 [Github](https://github.com/AzureAD/rms-sdk-for-cpp) 获取）一起打包。

>[!NOTE]  
> 我们建议使用 ADAL 之一，不过你可以使用其他身份验证库。

### <a name="authentication-parameters"></a>身份验证参数

ADAL 需要多项关键信息才能成功地向 Azure RMS（或 AD RMS）验证用户身份。 这些是标准 OAuth 2.0 参数，通常任何 Azure AD 应用都需要它们。 将在前面列出的对应 Github 存储库的自述文件中找到有关 ADAL 使用的当前指导原则。

- **颁发机构** – 身份验证终结点（通常是 AAD 或 ADFS）的 URL。
- **资源** - 尝试访问的服务应用程序（通常是 Azure RMS 或 AD RMS）的 URL/URI。
- **用户 Id** – 要访问应用的用户的 UPN（通常是电子邮件地址）。 此参数在用户未知时可以为空，还用于缓存用户令牌或从缓存中请求令牌。 它通常也用作用户提示的*提示*。
- **客户端 Id** – 客户端应用的 ID。 这必须是有效 Azure AD 应用程序 ID。
来自上一个注册步骤（通过 Azure 门户）。
- **重定向 Uri** – 向身份验证库提供身份验证代码的 URI 目标。 iOS 和 Android 需要特定的格式。 ADAL 相应的 GitHub 存储库的 README 文件中对此已有说明。 该值来自上一个注册步骤（通过 Azure 门户）。

>[!NOTE]
> “范围”当前未使用，但可能会使用，因此会保留供将来使用。

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

>[!NOTE] 
> 如果应用未遵循这些指导原则，则 Azure RMS 和 Azure AD 工作流可能会失败，并且不受 Microsoft.com 支持。 而且，如果在生产应用中使用无效客户端 Id，则可能会违反权限管理许可协议 (RMLA)。

### <a name="what-should-an-authentication-callback-implementation-look-like"></a>身份验证回调实现应呈现的内容
**身份验证代码示例** - 此 SDK 具有演示身份验证回调的使用的示例代码。 为方便起见，这些代码示例在此处以及以下每个链接的主题中进行了表示。

**Android 用户身份验证** - 有关详细信息，请参阅 [Android 代码示例](android-code.md) 中第一个方案“使用受 RMS 保护的文件”的 **步骤 2**。


    class MsipcAuthenticationCallback implements AuthenticationRequestCallback
    {
    ...

    @Override
    public void getToken(Map<String, String> authenticationParametersMap,
                         final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
    {
        String authority = authenticationParametersMap.get("oauth2.authority");
        String resource = authenticationParametersMap.get("oauth2.resource");
        String userId = authenticationParametersMap.get("userId");
        mClientId = “12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”; // get your registered Azure AD application ID here
        mRedirectUri = “urn:ietf:wg:oauth:2.0:oob”;
        final String userHint = (userId == null)? "" : userId;
        AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
        if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
        {
            try
            {
                authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                App.getInstance().setAuthenticationContext(authenticationContext);
            }
            catch (NoSuchAlgorithmException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
            catch (NoSuchPaddingException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
       }
        App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                       "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                        {
                            @Override
                            public void onError(Exception exc)
                            {
                                …
                                if (exc instanceof AuthenticationCancelError)
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onCancel();
                                }
                                else
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onFailure();
                                }
                            }

                            @Override
                            public void onSuccess(AuthenticationResult result)
                            {
                                …
                                if (result == null || result.getAccessToken() == null
                                        || result.getAccessToken().isEmpty())
                                {
                                     …
                                }
                                else
                                {
                                    // request is successful
                                    …
                                    authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                }
                            }
                        });
                         }


**iOS/OS X 用户身份验证** - 有关详细信息，请参阅 [iOS/OS X 代码示例](ios-os-x-code-examples.md)*第一个方案“使用受 RMS 保护的文件”的步骤 2*。


    // AuthenticationCallback holds the necessary information to retrieve an access token.
    @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

    @end

    @implementation MsipcAuthenticationCallback

    - (void)accessTokenWithAuthenticationParameters:
         (MSAuthenticationParameters *)authenticationParameters
                                completionBlock:
         (void(^)(NSString *accessToken, NSError *error))completionBlock
    {
    ADAuthenticationError *error;
    ADAuthenticationContext* context = [ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority error:&error];

    NSString *appClientId = @”12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”;

    // get your registered Azure AD application ID here

    NSURL *redirectURI = [NSURL URLWithString:@”ms-sample://com.microsoft.sampleapp”];

    // get your <app-scheme>://<bundle-id> here
    // Retrieve token using ADAL
    [context acquireTokenWithResource:authenticationParameters.resource
                             clientId:appClientId
                          redirectUri:redirectURI
                               userId:authenticationParameters.userId
                      completionBlock:^(ADAuthenticationResult *result)
                      {
                          if (result.status != AD_SUCCEEDED)
                          {
                              NSLog(@"Auth Failed");
                              completionBlock(nil, result.error);
                          }
                          else
                          {
                              completionBlock(result.accessToken, result.error);
                          }
                      }

        ];
    }



**Linux 用户身份验证** - 有关详细信息，请参阅 [Linux 代码示例](linux-c-code-examples.md)。



    // Class Header
    class AuthCallback : public IAuthenticationCallback {
    private:

      std::shared_ptr<rmsauth::FileCache> FileCachePtr;
      std::string clientId_;
      std::string redirectUrl_;

      public:

      AuthCallback(const std::string& clientId,
               const std::string& redirectUrl);
      virtual std::string GetToken(shared_ptr<AuthenticationParameters>& ap) override;
    };

    class ConsentCallback : public IConsentCallback {
      public:

      virtual ConsentList Consents(ConsentList& consents) override;
    };

    // Class Implementation
    AuthCallback::AuthCallback(const string& clientId, const string& redirectUrl)
    : clientId_(clientId), redirectUrl_(redirectUrl) {
      FileCachePtr = std::make_shared<FileCache>();
    }

    string AuthCallback::GetToken(shared_ptr<AuthenticationParameters>& ap)
    {
      string redirect =
      ap->Scope().empty() ? redirectUrl_ : ap->Scope();

      try
      {
        if (redirect.empty()) {
        throw rmscore::exceptions::RMSInvalidArgumentException(
              "redirect Url is empty");
      }

      if (clientId_.empty()) {
      throw rmscore::exceptions::RMSInvalidArgumentException("client Id is empty");
      }

      AuthenticationContext authContext(
        ap->Authority(), AuthorityValidationType::False, FileCachePtr);

      auto result = authContext.acquireToken(ap->Resource(),
                                           clientId_, redirect,
                                           PromptBehavior::Auto,
                                           ap->UserId());
      return result->accessToken();
      }

      catch (const rmsauth::Exception& ex)
      {
        // out logs
        throw;
      }
    }

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


