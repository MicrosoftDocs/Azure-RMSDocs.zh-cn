---
title: 如何使服务应用程序可以使用基于云的 RMS | Azure RMS
description: 本主题概述用于设置服务应用程序以使用 Azure Rights Management 的步骤。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 624ea74db4f81b3b8194e97339c69773f6743224
ms.sourcegitcommit: 7ed2a257f68435fe6807af8975a5477801ec2537
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2018
ms.locfileid: "39501245"
---
# <a name="how-to-enable-your-service-application-to-work-with-cloud-based-rms"></a>操作说明：使服务应用程序可以使用基于云的 RMS

本主题概述用于设置服务应用程序以使用 Azure Rights Management 的步骤。 有关详细信息，请参阅 [Azure Rights Management 入门](https://technet.microsoft.com/library/jj585016.aspx)。

**重要说明**  
为了通过 Azure RMS 使用 Rights Management Services SDK 2.1 服务应用程序，你需要创建自己的租户。 有关详细信息，请参阅 [Azure RMS 要求：支持 Azure RMS 的云订阅](../requirements.md)

## <a name="prerequisites"></a>必备条件

-   必须安装并配置 RMS SDK 2.1。 有关详细信息，请参阅 [RMS SDK 2.1 入门](getting-started-with-ad-rms-2-0.md)。
-   必须使用对称密钥选项或通过其他方式来 [通过 ACS 创建服务标识](https://msdn.microsoft.com/library/gg185924.aspx)，并记录来自该过程的密钥信息。

## <a name="connecting-to-the-azure-rights-management-service"></a>连接到 Azure Rights Management 服务

-   调用 [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)。
-   设置 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)。

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **注意**  有关详细信息，请参阅 [设置 API 安全模式](setting-the-api-security-mode-api-mode.md)

     
-   以下步骤是用于创建 [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) 结构的实例的设置，其中 *pcCredential* ([IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)) 成员使用来自 Azure Rights Management 服务的连接信息进行填充。
-   创建 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) 结构的实例时，使用来自对称密钥服务标识创建的信息（请参阅本主题前面列出的先决条件）来设置 *wszServicePrincipal*、*wszBposTenantId* 和 *cbKey* 参数。

**注意** - 由于发现服务的现有状况，如果你不在北美，则不会接受来自其他区域的对称密钥凭据，因此必须直接指定你的租户 URL。 这通过 [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) 或 [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx) 函数上的类型为 [IPC\_CONNECTION\_INFO](https://msdn.microsoft.com/library/hh535274.aspx) 的 *pConnectionInfo* 参数来实现。

## <a name="generate-a-symmetric-key-and-collect-the-needed-information"></a>生成对称密钥并收集所需信息

### <a name="instructions-to-generate-a-symmetric-key"></a>用于生成对称密钥的说明

-   安装 [Microsoft Online 登录助手](http://go.microsoft.com/fwlink/p/?LinkID=286152)
-   安装 [Azure AD Powershell 模块](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)。

**注意** - 必须是租户管理员才能使用 Powershell cmdlet。

- 启动 Powershell 并运行以下命令以生成密钥

    `Import-Module MSOnline`

    `Connect-MsolService`（输入管理员凭据）

    `New-MsolServicePrincipal`（输入显示名称）

- 生成对称密钥之后，会输出有关密钥的信息（包括密钥本身和 *AppPrincipalId*）。

      The following symmetric key was created as one was not supplied
      ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

      DisplayName : RMSTestApp
      ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
      ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
      AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### <a name="instructions-to-find-out-tenantbposid-and-urls"></a>用于查明 **TenantBposId** 和 **Urls** 的说明

-   安装 [Azure RMS powershell 模块](https://technet.microsoft.com/library/jj585012.aspx)。
-   启动 Powershell 并运行以下命令以获取租户的 RMS 配置。

    `Import-Module aadrm`

    `Connect-AadrmService`（输入管理员凭据）

    `Get-AadrmConfiguration`


- 创建 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) 的实例并设置几个成员。

      // Create a key structure.
      IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

      // Set each member with information from service creation.
      symKey.wszBase64Key = "your service principal key";
      symKey.wszAppPrincipalId = "your app principal identifier";
      symKey.wszBposTenantId = "your tenant identifier";


有关详细信息，请参阅 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx)。

-   创建 [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx) 结构的实例（包含 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) 实例）。

**注意** - *connectionInfo* 成员使用来自前面的 `Get-AadrmConfiguration` 调用的 URL 进行设置，在此处使用这些字段名称进行注明。

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

### <a name="identify-a-template-and-then-encrypt"></a>标识模板，然后加密

-   选择要用于加密的模板。
    调用 [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)（传入 [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) 的同一个实例）。


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   使用来自本主题前面部分的模板调用 [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx)（传入 [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) 的同一个实例）。

[IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx) 的示例用法：

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

[IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx) 的示例用法：

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

现在已完成使应用程序可以使用 Azure Rights Management 所需的步骤。

## <a name="related-topics"></a>相关主题

* [Azure Rights Management 入门](https://technet.microsoft.com/library/jj585016.aspx)
* [RMS SDK 2.1 入门](getting-started-with-ad-rms-2-0.md)
* [通过 ACS 创建服务标识](https://msdn.microsoft.com/library/gg185924.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
* [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
* [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx)
* [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)
* [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx)
* [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx)
* [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
* [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx)
* [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx)
* [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)
* [IpcCreateLicenseFromTemplateID](https://msdn.microsoft.com/library/hh535257.aspx)
