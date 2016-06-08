---
# required metadata

title: 适用于启用了 RMS 的应用程序的 ADAL 身份验证 | Azure RMS
description: 使用 ADAL 进行身份验证的过程概述
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 此 SDK 内容不是最新的。 在短时间内，请在 MSDN 上找到[最新版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)的文档。 **
# 适用于启用了 RMS 的应用程序的 ADAL 身份验证

现可在 RMS 客户端 2.1 中使用 Azure ADAL 对应用进行 Azure RMS 身份验证。

通过更新应用程序来使用 ADAL 身份验证而不使用 Microsoft Online 登录助手，你和你的客户将能够：

- 使用多重身份验证
- 安装 RMS 2.1 Client，而无需对计算机的管理特权
- 验证适用于 Windows 10 的应用程序

## 进行身份验证的两种方法

本主题包含使用相应的代码示例进行身份验证的两种方法。

- **内部身份验证** - 由 RMS SDK 管理的 OAuth 身份验证。 如果你希望 RMS 客户端在需要身份验证时显示 ADAL 身份验证提示时，请使用此方法。 有关如何配置应用程序的详细信息，请参阅“内部身份验证”一节。

> [!NOTE] 如果你的应用程序当前将 AD RMS SDK 2.1 用于登录助手，建议使用内部身份验证方法作为应用程序迁移路径。

- **外部身份验证** - 由应用程序管理的 OAuth 身份验证。 如果希望应用程序管理其自己的 OAuth 身份验证，请使用此方法。 使用此方法，RMS 客户端将在需要进行身份验证时执行应用程序定义的回调。 有关详细示例，请参阅本主题末尾的“外部身份验证”。

> [!NOTE] 外部身份验证并不意味着能够更改用户；RMS 客户端对于给定 RMS 租户始终使用默认用户。

### 内部身份验证

你将需要以下各项：

- [Microsoft Azure 订阅](https://azure.microsoft.com/en-us/)（使用免费试用版即可）：
- Microsoft Azure Rights Management 的订阅（使用免费的[个人 RMS](https://technet.microsoft.com/en-us/library/dn592127.aspx) 帐户即可）。

> [!NOTE] 询问你的 IT 管理员你是否具有 Microsoft Azure Rights Management 订阅，请你的 IT 管理员执行以下步骤。 如果你的组织没有订阅，应请 IT 管理员创建订阅。 此外，你的 IT 管理员应使用工作或学校帐户而不是 Microsoft 帐户（即 Hotmail）进行订阅。

注册 Microsoft Azure 后：

- 使用具有管理权限的帐户登录到组织的 [Azure 管理门户](https://manage.windowsazure.com)。

![Azure 登录名](../media/AzurePortalLogin.png)

- 向下浏览到门户右侧的 **Active Directory** 应用程序。

![选择“Active Directory”](../media/AzureADPick.png)

- 如果尚未创建目录，请选择门户左下角的**新建**按钮。

![选择“新建”](../media/AzureNewBtn.png)

- 选择 **Rights Management** 选项卡，确保 **Rights Management 状态**为**活动**、**未知**或**未授权**。 如果状态为**非活动**，请选择门户正下方的**激活**按钮并确认选择。

![选择“激活”](../media/RMTab.png)

- 现在，选择目录并选择“应用程序”，以便在该目录中创建新的*本机应用程序*。

![选择“应用程序”](../media/CreateNativeApp.png)

- 然后选择门户正下方的**添加**按钮。

![选择“添加”](../media/AddAppBtn.png)

- 出现提示时，选择**添加我的组织正在开发的应用程序**。

![选择“添加我的组织正在开发的应用程序”](../media/AddAnAppPick.png)

- 选择**本机客户端应用程序**，然后选择**下一步**按钮，以便对应用程序进行命名。

![对应用进行命名](../media/TellUsInput.png)

- 添加重定向 URI，并选择“下一步”。 重定向 URI 必须是有效的 URI 且对你的目录唯一。 例如，可以使用与 `com.mycompany.myapplication://authorize` 类似的 URI

![添加重定向 URI](../media/RedirectURI.png)

- 在目录中选择你的应用程序，然后选择**配置**。

![选择“配置”](../media/ConfigYourApp.png)

>[!NOTE] 配置 RMS 客户端时，复制**客户端 ID** 和**重定向 URI** 并将其存储供将来使用。

- 浏览到应用程序设置的底部，选择**其他应用程序的权限**下的**添加应用程序**按钮。

![选择“添加应用程序”](../media/PermissionsToOtherBtn.png)

- 现在，将此 GUID `00000012-0000-0000-c000-000000000000` 添加到**开始**编辑框，然后选中复选按钮。

![添加 GUID](../media/AddGUID.png)

- 选择 **Microsoft Rights Management** 旁边的加号 (+) 按钮。

![选择“+”按钮](../media/ChoosePlusBtn.png)

- 现在，选中对话框左下角的复选标记。

![选中复选标记](../media/ChooseCheck.png)

- 现在即可向应用程序添加 Azure RMS 依赖关系。 若要添加依赖关系，请选择**其他应用程序的权限**下的新增 **Microsoft Rights Management Services** 项，然后选择**委托的权限:** 下拉框下的**创建和访问用户受保护内容**复选框。

![设置权限](../media/AddDependency.png)

- 选择门户正下方的**保存**图标，保存应用程序以保留更改。

![选择“保存”](../media/SaveApplication.png)

- 现在即可将应用程序配置为使用由 RMS SDK 2.1 提供的内部 ADAL 身份验证。 若要配置 RMS 客户端，调用 [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize) 后立即添加对 [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/IpcSetGlobalProperty) 的调用以配置 RMS 客户端。 使用以下代码片段作为示例。


    IpcInitialize();

    IPC_AAD_APPLICATION_ID applicationId = { 0 };   applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);   applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";   applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";

    HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &amp;applicationId);

    if (FAILED(hr)) {    //Handle the error   }

### 外部身份验证

- 使用此代码作为管理你自己的身份验证令牌的示例。


    extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST&amp; Parameters, __out wstring wstrToken) throw();

    HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &amp;hKey) { IPC_OAUTH2_CALLBACK pfGetADALToken =         [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -&gt; HRESULT { wstring wstrToken; HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken); return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr; };

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
      credentialContext.pcOAuth2 = &amp;callbackCredentialContext;

      IPC_PROMPT_CTX promptContext =
      {
        sizeof(IPC_PROMPT_CTX),
        NULL,
        IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
        NULL,
        &amp;credentialContext
      };

      hKey = 0L;
      return IpcGetKey(pvLicense, 0, &amp;promptContext, NULL, &amp;hKey);
  }

### 相关主题
- [数据类型](/rights-management/sdk/2.1/api/win/Data%20types)
- [环境属性](/rights-management/sdk/2.1/api/win/Environment%20properties)
- [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/IpcCreateOAuth2Token)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/IpcGetKey)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize)
- [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC\_CREDENTIAL)
- [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC\_NAME\_VALUE\_LIST)
- [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IPC\_OAUTH2\_CALLBACK\_INFO)
- [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC\_PROMPT\_CTX)
- [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IPC\_AAD\_APPLICATION\_ID)


<!--HONumber=Jun16_HO1-->


