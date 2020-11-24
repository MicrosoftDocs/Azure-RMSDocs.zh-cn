---
title: 适用于启用了 RMS 的应用程序的 ADAL 身份验证 | Azure RMS
description: 请参阅如何使用 Azure RMS 通过 Azure Active Directory 身份验证库 (ADAL) 对应用程序进行身份验证。
keywords: 身份验证、RMS、ADAL
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: a7cf207b0976db31ffa4df83d20e172876c7ee88
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "95566361"
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

若要配置 RMS 客户端，调用 [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize) 后立即添加对 [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty) 的调用以配置 RMS 客户端。 使用以下代码片段作为示例。

```cpp
IpcInitialize();

IPC_AAD_APPLICATION_ID applicationId = { 0 };
applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
if (FAILED(hr)) {
  //Handle the error
}
```

## <a name="external-authentication"></a>外部身份验证

使用此代码作为管理你自己的身份验证令牌的示例。

```cpp
extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

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
```

## <a name="related-topics"></a>相关主题

- [数据类型](/previous-versions/windows/desktop/msipc/microsoft-information-protection-and-control-client-data-types)
- [环境属性](/previous-versions/windows/desktop/msipc/environment-properties)
- [IpcCreateOAuth2Token](/previous-versions/windows/desktop/msipc/ipccreateoauth2token)
- [IpcGetKey](/previous-versions/windows/desktop/msipc/ipcgetkey)
- [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize)
- [IPC_CREDENTIAL](/previous-versions/windows/desktop/msipc/ipc-credential)
- [IPC_NAME_VALUE_LIST](/previous-versions/windows/desktop/msipc/ipc-name-value-list)
- [IPC_OAUTH2_CALLBACK_INFO](/previous-versions/windows/desktop/msipc/ipc-oath2-callback-info)
- [IPC_PROMPT_CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)
- [IPC_AAD_APPLICATION_ID](/previous-versions/windows/desktop/msipc/ipc-aad-application-id)