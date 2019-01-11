---
title: 适用于启用了 RMS 的应用程序的 ADAL 身份验证 | Azure RMS
description: 使用 ADAL 进行身份验证的过程概述
keywords: 身份验证、RMS、ADAL
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: a921d71c7cb54d0db84d30baf5dd723e314405c3
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2019
ms.locfileid: "54070343"
---
# <a name="how-to-use-adal-authentication"></a>操作说明：使用 ADAL 身份验证

使用 Azure Active Directory 身份验证库 (ADAL) 为应用向 Azure RMS 进行身份验证。

通过更新应用程序来使用 ADAL 身份验证而不使用 Microsoft Online 登录助手，你和你的客户将能够：

- 使用多重身份验证
- 安装 RMS 2.1 Client，而无需对计算机的管理特权
- 验证适用于 Windows 10 的应用程序

## <a name="two-approaches-to-authentication"></a>进行身份验证的两种方法

本主题包含使用相应的代码示例进行身份验证的两种方法。

- **内部身份验证** - 由 RMS SDK 管理的 OAuth 身份验证。

  如果你希望 RMS 客户端在需要身份验证时显示 ADAL 身份验证提示时，请使用此方法。 有关如何配置应用程序的详细信息，请参阅“内部身份验证”一节。

  > [!Note]
  > 如果你的应用程序当前将 AD RMS SDK 2.1 用于登录助手，建议使用内部身份验证方法作为应用程序迁移路径。

- **外部身份验证** - 由应用程序管理的 OAuth 身份验证。

  如果希望应用程序管理其自己的 OAuth 身份验证，请使用此方法。 使用此方法，RMS 客户端将在需要进行身份验证时执行应用程序定义的回调。 有关详细示例，请参阅本主题末尾的“外部身份验证”。

  > [!Note]
  > 外部身份验证并不意味着能够更改用户；RMS 客户端对于给定 RMS 租户始终使用默认用户。

## <a name="internal-authentication"></a>内部身份验证

1. 按照[为 ADAL 身份验证配置 Azure RMS](adal-auth.md) 中的 Azure 配置步骤操作，然后返回到以下应用初始化步骤。
2. 现在即可将应用程序配置为使用由 RMS SDK 2.1 提供的内部 ADAL 身份验证。

若要配置 RMS 客户端，调用 [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) 后立即添加对 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 的调用以配置 RMS 客户端。 使用以下代码片段作为示例。

      C++
      IpcInitialize();

      IPC_AAD_APPLICATION_ID applicationId = { 0 };
      applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
      applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
      applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
      HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
      if (FAILED(hr)) {
        //Handle the error
      }

## <a name="external-authentication"></a>外部身份验证

使用此代码作为管理你自己的身份验证令牌的示例。
C++ extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

      HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &hKey)
      {
          IPC_OAUTH2_CALLBACK pfGetADALToken =
          [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -> HRESULT
          {
              wstring wstrToken;
              HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken);
              return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr;
          };

          IPC_OAUTH2_CALLBACK_INFO callbackCredentialContext =
          {
              sizeof(IPC_OAUTH2_CALLBACK_INFO),
              pfGetADALToken,
              pContextForAdal
          };

          IPC_CREDENTIAL credentialContext =
          {
              IPC_CREDENTIAL_TYPE_OAUTH2,
              NULL
          };
          credentialContext.pcOAuth2 = &callbackCredentialContext;

          IPC_PROMPT_CTX promptContext =
          {
              sizeof(IPC_PROMPT_CTX),
              NULL,
              IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
              NULL,
              &credentialContext
          };

          hKey = 0L;
          return IpcGetKey(pvLicense, 0, &promptContext, NULL, &hKey);
      }

## <a name="related-topics"></a>相关主题

- [Data types](https://msdn.microsoft.com/library/hh535288.aspx)（数据类型）
- [Environment properties](https://msdn.microsoft.com/library/hh535247.aspx)（环境属性）
- [IpcCreateOAuth2Token](https://msdn.microsoft.com/library/mt661866.aspx)
- [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx)
- [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
- [IPC_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)
- [IPC_NAME_VALUE_LIST](https://msdn.microsoft.com/library/hh535277.aspx)
- [IPC_OAUTH2_CALLBACK_INFO](https://msdn.microsoft.com/library/mt661868.aspx)
- [IPC_PROMPT_CTX](https://msdn.microsoft.com/library/hh535278.aspx)
- [IPC_AAD_APPLICATION_ID](https://msdn.microsoft.com/library/mt661867.aspx)
