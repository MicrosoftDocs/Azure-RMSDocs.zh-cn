---
title: 如何使服务应用程序可以使用基于云的 RMS | Azure RMS
description: 本主题概述用于设置服务应用程序以使用 Azure Rights Management 的步骤。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: a760f59effa09cf55f7618e6ab965c5e95f015d3
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "95566353"
---
# <a name="how-to-enable-your-service-application-to-work-with-cloud-based-rms"></a>操作说明：使服务应用程序可以使用基于云的 RMS

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

本主题概述用于设置服务应用程序以使用 Azure Rights Management 的步骤。 有关详细信息，请参阅 [Azure Rights Management 入门](../requirements.md)。

**重要说明**  
为了通过 Azure RMS 使用 Rights Management Services SDK 2.1 服务应用程序，你需要创建自己的租户。 有关详细信息，请参阅 [Azure RMS 要求：支持 Azure RMS 的云订阅](../requirements.md)

## <a name="prerequisites"></a>必备条件

-   必须安装并配置 RMS SDK 2.1。 有关详细信息，请参阅 [RMS SDK 2.1 入门](getting-started-with-ad-rms-2-0.md)。
-   必须使用对称密钥选项或通过其他方式来 [通过 ACS 创建服务标识](/previous-versions/azure/azure-services/gg185924(v=azure.100))，并记录来自该过程的密钥信息。

## <a name="connecting-to-the-azure-rights-management-service"></a>连接到 Azure Rights Management 服务

- 调用 [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize)。
- 设置 [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty)。

  ```cpp
  int mode = IPC_API_MODE_SERVER;
  IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));
  ```

  **注意**  有关详细信息，请参阅 [设置 API 安全模式](setting-the-api-security-mode-api-mode.md)


-   以下步骤适用于使用 *其中 pccredential* ([Ipc \_ 凭据](/previous-versions/windows/desktop/msipc/ipc-credential)创建 [ipc \_ PROMPT \_ CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)结构的实例，) 成员使用 Azure Rights Management 服务中的连接信息进行填充。
-   使用对称密钥服务标识创建中的信息 (参阅本主题前面列出的先决条件) 在创建 [IPC \_ 凭据 \_ 对称 \_ 密钥](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)结构的实例时设置 *wszServicePrincipal*、 *wszBposTenantId* 和 *cbKey* 参数。

**注意** - 由于发现服务的现有状况，如果你不在北美，则不会接受来自其他区域的对称密钥凭据，因此必须直接指定你的租户 URL。 这通过 [IpcGetTemplateList](/previous-versions/windows/desktop/msipc/ipcgettemplatelist) 或 [IpcGetTemplateIssuerList](/previous-versions/windows/desktop/msipc/ipcgettemplateissuerlist) 函数上的类型为 [IPC\_CONNECTION\_INFO](/previous-versions/windows/desktop/msipc/ipc-connection-info) 的 *pConnectionInfo* 参数来实现。

## <a name="generate-a-symmetric-key-and-collect-the-needed-information"></a>生成对称密钥并收集所需信息

### <a name="instructions-to-generate-a-symmetric-key"></a>用于生成对称密钥的说明

-   安装 [Microsoft Online 登录助手](https://go.microsoft.com/fwlink/p/?LinkID=286152)
-   安装 [Azure AD Powershell 模块](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)。

**注意** - 必须是租户管理员才能使用 Powershell cmdlet。

- 启动 Powershell 并运行以下命令以生成密钥

    `Import-Module MSOnline`

    `Connect-MsolService`（输入管理员凭据）

    `New-MsolServicePrincipal`（输入显示名称）

- 生成对称密钥之后，会输出有关密钥的信息（包括密钥本身和 *AppPrincipalId*）。

  ```output
  The following symmetric key was created as one was not supplied
  ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

  DisplayName : RMSTestApp
  ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
  ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
  AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963
  ```


### <a name="instructions-to-find-out-tenantbposid-and-urls"></a>用于查明 **TenantBposId** 和 **Urls** 的说明

-   安装 [Azure RMS powershell 模块](../install-powershell.md)。
-   启动 Powershell 并运行以下命令以获取租户的 RMS 配置。

    `Import-Module AIPService`

    `Connect-AipService`（输入管理员凭据）

    `Get-AipServiceConfiguration`


- 创建  [IPC \_ 凭据 \_ 对称 \_ 密钥](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key) 的实例并设置几个成员。

  ```cpp
  // Create a key structure.
  IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

  // Set each member with information from service creation.
  symKey.wszBase64Key = "your service principal key";
  symKey.wszAppPrincipalId = "your app principal identifier";
  symKey.wszBposTenantId = "your tenant identifier";
  ```

有关详细信息，请参阅 [IPC \_ 凭据 \_ 对称 \_ 密钥](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)。

- 创建 [ipc \_ credential](/previous-versions/windows/desktop/msipc/ipc-credential) 结构的实例，该结构包含 [ipc \_ 凭据 \_ 对称 \_ 密钥](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key) 实例。

  **注意**  - *ConnectionInfo* 成员是通过上一次调用的 url 进行设置 `Get-AipServiceConfiguration` ，在此处注明这些字段名称。

  ```cpp
  // Create a credential structure.
  IPC_CREDENTIAL cred = {0};

  IPC_CONNECTION_INFO connectionInfo = {0};
  connectionInfo.wszIntranetUrl = LicensingIntranetDistributionPointUrl;
  connectionInfo.wszExtranetUrl = LicensingExtranetDistributionPointUrl;

  // Set each member.
  cred.dwType = IPC_CREDENTIAL_TYPE_SYMMETRIC_KEY;
  cred.pcCertContext = (PCCERT_CONTEXT)&symKey;

  // Create your prompt control.
  IPC_PROMPT_CTX promptCtx = {0};

  // Set each member.
  promptCtx.cbSize = sizeof(IPC_PROMPT_CTX);
  promptCtx.hwndParent = NULL;
  promptCtx.dwflags = IPC_PROMPT_FLAG_SILENT;
  promptCtx.hCancelEvent = NULL;
  promptCtx.pcCredential = &cred;
  ```

### <a name="identify-a-template-and-then-encrypt"></a>标识模板，然后加密

- 选择要用于加密的模板。
    在[IPC \_ 提示符 \_ CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)的同一个实例中调用[IpcGetTemplateList](/previous-versions/windows/desktop/msipc/ipcgettemplatelist) 。

  ```cpp
  PCIPC_TIL pTemplates = NULL;
  IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

  hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),
         IPC_GTL_FLAG_FORCE_DOWNLOAD,
         0,
         &promptCtx,
         NULL,
         &pTemplates);
  ```

- 利用本主题前面的模板，请调用 [IpcfEncrcyptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile)，并传入 [IPC \_ PROMPT \_ CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)的同一个实例。

  [IpcfEncrcyptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile) 的示例用法：

  ```cpp
  LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
  hr = IpcfEncryptFile(wszInputFilePath,
         wszContentTemplateId,
         IPCF_EF_TEMPLATE_ID,
         IPC_EF_FLAG_KEY_NO_PERSIST,
         &promptCtx,
         NULL,
         &wszOutputFilePath);
  ```

  [IpcfDecryptFile](/previous-versions/windows/desktop/msipc/ipcfdecryptfile) 的示例用法：

  ```cpp
  hr = IpcfDecryptFile(wszInputFilePath,
         IPCF_DF_FLAG_DEFAULT,
         &promptCtx,
         NULL,
         &wszOutputFilePath);
  ```

现在已完成使应用程序可以使用 Azure Rights Management 所需的步骤。

## <a name="related-topics"></a>相关主题

* [Azure Rights Management 入门](../requirements.md)
* [RMS SDK 2.1 入门](getting-started-with-ad-rms-2-0.md)
* [通过 ACS 创建服务标识](/previous-versions/azure/azure-services/gg185924(v=azure.100))
* [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty)
* [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize)
* [IPC \_ 提示符 \_ CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)
* [IPC \_ 凭据](/previous-versions/windows/desktop/msipc/ipc-credential)
* [IPC \_ 凭据 \_ 对称 \_ 密钥](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)
* [IpcGetTemplateIssuerList](/previous-versions/windows/desktop/msipc/ipcgettemplateissuerlist)
* [IpcGetTemplateList](/previous-versions/windows/desktop/msipc/ipcgettemplatelist)
* [IpcfDecryptFile](/previous-versions/windows/desktop/msipc/ipcfdecryptfile)
* [IpcfEncrcyptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile)
* [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch)
* [IpcCreateLicenseFromTemplateID](/previous-versions/windows/desktop/msipc/ipccreatelicensefromtemplateid)