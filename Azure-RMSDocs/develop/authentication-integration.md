---
# required metadata

title: 如何&#58;向应用添加身份验证 | Azure RMS
description: 介绍针对启用 RMS 的应用的用户身份验证基础知识。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 94697eb5-1fab-4591-bd40-b5646daac8a3

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 如何：向应用添加身份验证

本主题介绍针对启用 RMS 的应用的用户身份验证基础知识。

## 什么是用户身份验证
用户身份验证是在设备应用与 RMS 基础结构之间建立通信的必要步骤。 此身份验证过程使用标准 OAuth 2.0 协议，该协议需要有关当前用户及其身份验证请求的以下几部分信息；**颁发机构**、**资源** 和 **用户 Id**。

**注意**  范围当前未使用，但可能会使用，因此保留供将来使用。

 

**用户身份验证回调** - Microsoft Rights Management SDK 4.2 会在你未提供访问令牌时、你的访问令牌需要刷新时或是访问令牌已过期时使用你的身份验证回调实现。

每个平台 RMS API 都具有回调，必须实现它才能启用用户的身份验证。

-   Android API 使用 [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) 和 [**AuthenticationCompletionCallback**](/rights-management/sdk/4.2/api/android/authenticationcompletioncallback#msipcthin2_authenticationcompletioncallback_interface_java) 接口。
-   iOS/OS X API 使用 [**MSAuthenticationCallback**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msauthenticationcallback_protocol_objc) 协议。
-   WinPhone API 使用 [**IAuthenticationCallback**](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_iauthenticationcallback) 接口。
-   Linux API 使用 [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html) 接口。

## 要用于身份验证的库是什么

若要实现身份验证回调，需要下载相应的库并配置开发环境以使用它。 可在 GitHub 上找到适用于这些平台的 ADAL 库。 以下每个资源都包含设置环境和使用库的指南。

-   [适用于 iOS 的 Windows Azure Active Directory 身份验证库 (ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [适用于 Mac 的 Windows Azure Active Directory 身份验证库 (ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [适用于 Android 的 Windows Azure Active Directory 身份验证库 (ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [适用于 dotnet 的 Windows Azure Active Directory 身份验证库 (ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   对于 Linux SDK，ADAL 库与 SDK 源（可通过 [Github](https://github.com/AzureAD/rms-sdk-for-cpp) 获取）一起打包。

**注意**  建议使用以上 Active Directory 身份验证库 (ADAL) 之一，不过可以使用其他身份验证库。

## 使用 Azure Active Director 身份验证库 (ADAL) 进行身份验证的输入

ADAL 需要多个参数才能成功地向 Azure RMS（或 AD RMS）验证用户身份。 这些是标准 OAuth 2.0 参数，通常任何 Azure AD 应用都需要它们（与启用 RMS 的应用一样）。 可以在前面列出的对应 Github 存储库的自述文件中找到有关 ADAL 使用的当前指导原则。

以下这些参数和指导原则对于 RMS 工作流是必需的：

-   **颁发机构** – 身份验证终结点（通常是 AAD 或 ADFS）的 URL。 此参数由 RMS SDK 身份验证回调向应用提供。
-   **资源** - 尝试访问的服务应用程序（通常是 Azure RMS 或 AD RMS）的 URL/URI。 此参数由 RMS SDK 身份验证回调向应用提供。
-   **用户 Id** – 要访问应用的用户的 UPN（通常是电子邮件地址）。 此参数在用户未知时可以为空，还用于缓存用户令牌或从缓存中请求令牌。 这通常也用作用户提示的“提示”。
-   **客户端 Id** – 客户端应用的 ID。 这必须是有效 Azure AD 应用程序 ID。 有关详细信息，请参阅“如何：获取 Azure 应用程序 ID”。
-   **重定向 Uri** – 向身份验证库提供身份验证代码的 URI 目标。 请注意，iOS 和 Android 需要特定格式，在 ADAL 的对应 GitHub 存储库的自述文件中进行了说明。

    Android： `msauth://packagename/Base64UrlencodedSignature`

    iOS： `<app-scheme>://<bundle-id>`

**注意**  如果应用未遵循这些指导原则，则 Azure RMS 和 Azure AD 工作流可能会失败，并且不受 Microsoft.com 支持。 而且，如果在生产应用中使用无效客户端 Id，则可能会违反权限管理许可协议 (RMLA)。

## 身份验证回调实现应呈现的内容

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


**iOS/OS X 用户身份验证** - 有关详细信息，请参阅 [iOS/OS X 代码示例](ios-os-x-code-examples.md) 中

第一个方案“使用受 RMS 保护的文件”的 **步骤 2**。


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



**Linux/C++ 用户身份验证** - 有关详细信息，请参阅 [Linux 代码示例](linux-c-code-examples.md)。



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



 

 


<!--HONumber=Apr16_HO3-->


