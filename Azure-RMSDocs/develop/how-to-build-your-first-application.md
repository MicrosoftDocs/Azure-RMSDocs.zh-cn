---
# required metadata

title: IPCHelloWorld - 一个示例应用程序 | Azure RMS
description: 本主题包含用于创建启用权限的示例应用程序的说明。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 581451A2-9558-4D0D-9D01-BEAB282C5A83
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
# IPCHelloWorld - 一个示例应用程序

本主题包含用于创建启用权限的示例应用程序的说明。

这一简单应用程序 IPCHelloWorld 可帮助你熟悉启用权限的应用程序的基本概念和代码。

从 Microsoft Connect 下载示例应用程序 [Webinar\_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)。 为方便起见，该站点上的其余可下载项目在此处集成在一起。

**注意**  IPCHelloWorld 项目已针对 Rights Management Services SDK 2.1 进行了配置。 有关如何配置新项目以使用 RMS SDK 2.1 的信息，请参阅 [配置 Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)。

 
以下部分介绍所需的关键应用程序步骤和理解。

## 加载 MSIPC.dll

需要先调用 [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) 函数以加载 MSIPC.dll，然后才能调用任何 RMS SDK 2.1 函数。



    hr = IpcInitialize();

    if (FAILED(hr))
    {
      wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
      goto exit;
    }



## 枚举模板

RMS 模板定义用于保护数据的策略，即定义允许访问数据的用户及其权限。 RMS 模板安装在 RMS 服务器上。

下面的代码截图枚举默认 RMS 服务器提供的 RMS 模板。



    hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

    if (FAILED(hr))
    {
      DisplayError(L"IpcGetTemplateList failed", hr);
      goto exit;
    }



此调用会检索安装在默认服务器上的 RMS 模板，并在 *pcTil* 变量指向的 [**IPC\_TIL**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) 结构中加载结果，然后显示这些模板。



    if (0 == pcTil->cTi)
    {
      wprintf(L"* No templates configured for your RMS server * \n\n");
      wprintf(L"\\------------------------------------------------------\n\n");
      goto exit;
    }

    for (DWORD dw = 0; dw < pcTil->cTi; dw++)
    {
      wprintf(L"Template #%d:\n", dw);
      wprintf(L"    Name:         %s\n", pcTil->aTi[dw].wszName);
      wprintf(L"    Issued by:    %s\n", pcTil->aTi[dw].wszIssuerDisplayName);
      wprintf(L"    Description:  %s\n", pcTil->aTi[dw].wszDescription);
      wprintf(L"\n");
    }



## 序列化许可证

需要先序列化许可证并获取内容密钥，然后才能保护任何数据。 内容密钥用于加密敏感数据。 序列化的许可证通常会附加到加密的数据，由受保护的数据的使用者使用。 使用者需要使用序列化的许可证调用 [**IpcGetKey**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey) 函数以获取内容密钥，用于解密内容以及获取与内容关联的策略。

为简单起见，使用 [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) 返回的第一个 RMS 模板序列化许可证。

通常会使用用户界面对话框以允许用户选择所需模板。



    hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
    0, NULL, &hContentKey, &pSerializedLicense);

    if (FAILED(hr))
    {
      DisplayError(L"IpcSerializeLicense failed", hr);
      goto exit;
    }



执行此操作之后，你会获得内容密钥 *hContentKey* 和序列化的许可证 *pSerializedLicense*（需要附加到受保护的数据）。

## 保护数据

现在你已准备就绪，可以使用 [**IpcEncrypt**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt) 函数加密敏感数据。 首先，需要向 **IpcEncrypt** 函数询问加密的数据的大小。



    cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
    hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
    NULL, 0, &cbEncrypted);

    if (FAILED(hr)) {
      DisplayError(L"IpcEncrypt failed", hr);
      goto exit;
    }



此处的 *wszText* 包含要保护的纯文本。 [**IpcEncrypt**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt) 函数返回在 *cbEncrypted* 参数中返回加密的数据的大小。

现在为加密的数据分配内存。



    pbEncrypted = (PBYTE)LocalAlloc(LPTR, cbEncrypted);

    if (NULL == pbEncrypted) {
      wprintf(L"Out of memory\n");
      goto exit;
    }


最后，可以执行实际加密。



    hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
    pbEncrypted, cbEncrypted, &cbEncrypted);

    if (FAILED(hr)) {
      DisplayError(L"IpcEncrypt failed", hr);
      goto exit;
    }


在此步骤之后，你会获得加密的数据 *pbEncrypted* 和序列化的许可证 *pSerializedLicense*（将由使用者用于解密数据）。

## 错误处理

在此整个示例应用程序中，**DisplayError** 函数用于处理错误。



    void DisplayError(LPCWSTR wszErrorInfo, HRESULT hrError)
    {
        LPCWSTR wszErrorMessageText = NULL;

        if (SUCCEEDED(IpcGetErrorMessageText(hrError, 0, &wszErrorMessageText))) {
          wprintf(L"%s: 0x%08X (%s)\n", wszErrorInfo, hrError, wszErrorMessageText);
        }
        else {
          wprintf(L"%s: 0x%08X\n", wszErrorInfo, hrError);
        }
    }   


**DisplayError** 函数使用 [**IpcGetErrorMessageText**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) 函数从对应错误代码获取错误消息并将它打印到标准输出。

## 清理

完成之前，还需要释放所有已分配的资源。



    if (NULL != pbEncrypted) {
      LocalFree((HLOCAL)pbEncrypted);
    }

    if (NULL != pSerializedLicense) {
      IpcFreeMemory((LPVOID)pSerializedLicense);
    }

    if (NULL != hContentKey) {
      IpcCloseHandle((IPC_HANDLE)hContentKey);
    }

    if (NULL != pcTil) {
      IpcFreeMemory((LPVOID)pcTil);
    }


## 相关主题

* [开发人员说明](developer-notes.md)
* [配置 Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)
* [**IpcEncrypt**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt)
* [**IpcGetErrorMessageText**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext)
* [**IpcGetKey**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_TIL**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [Webinar\_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
 

 


<!--HONumber=Jun16_HO1-->


