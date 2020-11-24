---
title: '概念-Microsoft 信息保护 (MIP) SDK c # 客户端的身份验证方案'
description: '有关 Microsoft Information Protection SDK c # 客户端应用程序的身份验证方案的技术详细信息。'
author: Pathak-Aniket
ms.author: v-anikep
ms.date: 09/02/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: 10d6f5ce615373f0955c42f2573b7ddd59629734
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "95566097"
---
# <a name="quickstart-public-and-confidential-clients-c"></a>快速入门：公共和机密客户端 (c # ) 

使用 MIP SDK 生成应用程序时，有两种常见方案。 一个方案会看到用户直接针对 Azure AD 进行身份验证，在其他应用程序中，使用机密服务主体密钥或证书进行身份验证。

## <a name="public-client-applications"></a>公共客户端应用程序

这些应用程序通常是桌面或移动应用程序，在设备上运行的应用程序将提示用户进行身份验证，用户直接连接到后端 MIP 服务。 在这种情况下，应该使用身份验证库来确保用户能够登录到 Azure AD、满足任何多重因素或条件访问要求，并获得相应资源的 OAuth2 令牌。

有关详细信息，请参阅 Azure AD [公有客户端身份验证流文档](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-public-client-application-from-configuration-options)

下面是一个快速代码截图，演示使用 Microsoft 身份验证 SDK 客户端应用程序的公共客户端身份验证流 (MSAL) 。

```csharp

public string AcquireToken(Identity identity, string authority, string resource, string claims)
{
     var authorityUri = new Uri(authority);
     authority = String.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

     _app = PublicClientApplicationBuilder.Create("<Application-Id>").WithAuthority(authority).WithDefaultRedirectUri().Build();

     var accounts = (_app.GetAccountsAsync()).GetAwaiter().GetResult();

     // Append .default to the resource passed in to AcquireToken().
     string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
     var result = _app.AcquireTokenInteractive(scopes).WithAccount(accounts.FirstOrDefault()).WithPrompt(Prompt.SelectAccount)
                    .ExecuteAsync().ConfigureAwait(false).GetAwaiter().GetResult();

     return result.AccessToken;
}
```

租户-GUID 表示 Azure AD 租户的租户 GUID，而应用程序 ID 是 Azure AD 门户上应用程序注册中的应用程序 ID。

## <a name="confidential-client-applications"></a>机密客户端应用程序

这些应用程序通常是基于云或服务的应用程序，用户不直接连接到后端 MIP 服务，但该服务需要标记、保护或取消保护启用了 MIP 的内容。 在此方案中，应用程序必须存储用于身份验证的一些证书或应用程序机密，才能 Azure AD，并使用该机密获取后端 MIP 服务的令牌。 然后，它可以使用 MIP SDK 的委托功能，代表经过身份验证的用户保护或使用内容。

有关详细信息，请参阅 Azure AD [机密客户端身份验证流文档](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-confidential-client-application-from-code)

下面是使用 Microsoft 身份验证 SDK 客户端应用程序的机密客户端身份验证流的快速代码截图， (MSAL) 。 应用程序可以使用 AD 证书或客户端密码进行身份验证。

```csharp
public string AcquireToken(Identity identity, string authority, string resource, string claim)
{
     AuthenticationResult result;
     var authorityUri = new Uri(authority);
     authority = string.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

     // Certification Based Auth
     if (doCertAuth)
     {
          // Build ConfidentialClientApplication using certificate.
          _app = ConfidentialClientApplicationBuilder.Create("<Application-Id>")
               .WithCertificate(certificate) //Assumption here is Application passes a certificate created using certificate thumbprint
               .WithAuthority(new Uri(authority))
               .Build();
     }

     // Client secret based Auth
     else
     {
          // Build ConfidentialClientApplication using app secret
          _app = ConfidentialClientApplicationBuilder.Create("<Application-Id>")
               .WithClientSecret(clientSecret)
               .WithAuthority(new Uri(authority))
               .Build();
     }

     // Append .default to the resource passed in to AcquireToken().
     string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };

     try{
          result = _app.AcquireTokenForClient(scopes).ExecuteAsync().Result;
     }
     catch (MsalServiceException ex) when (ex.Message.Contains("AADSTS70011"))
     {
          // Invalid scope. The scope has to be of the form "https://resourceurl/.default"
          // Mitigation: change the scope to be as expected
          Console.WriteLine("Scope provided is not supported");
          return null;
     }
            return result.AccessToken;
}

```

租户-GUID 表示 Azure AD 租户的租户 GUID，而应用程序 ID 是 Azure AD 门户上应用程序注册中的应用程序 ID。