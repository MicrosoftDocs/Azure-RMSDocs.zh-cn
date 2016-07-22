---
title: "如何使服务应用程序可以使用基于云的 RMS | Azure RMS"
description: "本主题概述用于设置服务应用程序以使用 Azure Rights Management 的步骤。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4c3625676c7e794ef133c75881f666bae80e0513
ms.openlocfilehash: ad8c41c9f3f3515a817d508d8f5a8953daf4b440


---

# 操作说明：使服务应用程序可以使用基于云的 RMS

本主题概述用于设置服务应用程序以使用 Azure Rights Management 的步骤。 有关详细信息，请参阅 [Azure Rights Management 入门](https://technet.microsoft.com/library/jj585016.aspx)。

**重要**  
为了通过 Azure RMS 使用 Rights Management Services SDK 2.1 服务应用程序，你需要创建自己的租户。 有关详细信息，请参阅 [Azure RMS 要求：支持 Azure RMS 的云订阅](../get-started/requirements-subscriptions.md)

## 先决条件

-   必须安装并配置 RMS SDK 2.1。 有关详细信息，请参阅 [RMS SDK 2.1 入门](getting-started-with-ad-rms-2-0.md)。
-   必须使用对称密钥选项或通过其他方式来 [通过 ACS 创建服务标识](https://msdn.microsoft.com/en-us/library/gg185924.aspx)，并记录来自该过程的密钥信息。

## 连接到 Azure 权限管理服务

-   调用 [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)。
-   设置 [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)。

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **注意**  有关详细信息，请参阅 [设置 API 安全模式](setting-the-api-security-mode-api-mode.md)

     
-   以下步骤是用于创建 [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 结构的实例（其中 **pcCredential** ([**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)) 成员使用来自 Azure 权限管理服务的连接信息进行填充）的设置。
-   创建 [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) 结构的实例时，使用来自对称密钥服务标识创建的信息（请参阅本主题前面列出的先决条件）来设置 **wszServicePrincipal**、**wszBposTenantId** 和 **cbKey** 参数。

**注意** 由于我们发现服务的现有状况，如果你不在北美，则不会接受来自其他区域的对称密钥凭据，因此必须直接指定你的租户 URL。 这通过 [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) 或 [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist) 的 [**IPC\_CONNECTION\_INFO**](/rights-management/sdk/2.1/api/win/ipc_connection_info#msipc_ipc_connection_info) 参数来实现。

## 生成对称密钥并收集所需信息

### 用于生成对称密钥的说明

-   安装 [Microsoft Online 登录助手](http://go.microsoft.com/fwlink/p/?LinkID=286152)
-   安装 [Azure AD Powershell 模块](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)。

**注意**  你必须是租户管理员才能使用 Powershell cmdlet。

-   启动 Powershell 并运行以下命令以生成密钥         `Import-Module MSOnline`
            `Connect-MsolService`（键入管理员凭据）        `New-MsolServicePrincipal`（键入显示名称）
-   生成对称密钥之后，会输出有关密钥的信息（包括密钥本身和 **AppPrincipalId**）。


    未提供对称密钥时，将创建以下对称密钥：ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

    DisplayName : RMSTestApp ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963} ObjectId : 0ee53770-ec86-409e-8939-6d8239880518 AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### 用于查明 **TenantBposId** 和 **Urls** 的说明

-   安装 [Azure RMS powershell 模块](https://technet.microsoft.com/en-us/library/jj585012.aspx)。
-   启动 Powershell 并运行以下命令以获取租户的 RMS 配置。

    `Import-Module aadrm`

    `Connect-AadrmService` （输入管理员凭据）

    `Get-AadrmConfiguration`


-   创建 [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) 的实例并设置几个成员。

    // 创建密钥结构。
    IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

    // 使用来自服务创建的信息设置每个成员。
    symKey.wszBase64Key 是“你的服务主体密钥”；symKey.wszAppPrincipalId 是“你的应用主体标识符”；symKey.wszBposTenantId 是“你的租户标识符”；


有关详细信息，请参阅 [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)。

-   创建 [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential) 结构的实例（包含 [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) 实例）。

**注意**  *connectionInfo* 成员使用来自前面的 `Get-AadrmConfiguration` 调用的 URL 进行设置，在此处使用这些字段名称进行注明。

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

### 标识模板，然后加密

-   选择要用于加密的模板。
    调用 [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)（传入 [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 的同一个实例）。


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   使用来自本主题前面部分的模板调用 [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)（传入 [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 的同一个实例）。

[**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile) 的示例用法：

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

[**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile) 的示例用法：

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

现在已完成使应用程序可以使用 Azure Rights Management 所需的步骤。

## 相关主题

* [Azure Rights Management 入门](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [RMS SDK 2.1 入门](getting-started-with-ad-rms-2-0.md)
* [通过 ACS 创建服务标识](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx)
* [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)
* [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)
* [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcCreateLicenseFromTemplateID**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromtemplateid)
 

 



<!--HONumber=Jul16_HO3-->


