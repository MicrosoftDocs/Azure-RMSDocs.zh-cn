---
title: "开发应用程序 | Azure RMS"
description: "有关如何使用 RMS SDK 2.1 开发应用程序的说明。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 6e2b85bc8069de7060211df4d53be7f24ae44e3e


---

# 开发应用程序

本主题包含启用了 RMS 的应用程序的核心层面的基本指南，可作为应用程序开发的基础。

## 简介

本主题中的指南以示例应用程序 *IPCHelloWorld* 为基础，可帮助你熟悉启用权限的应用程序的基本概念和代码。 *IPCHelloWorld* 项目已针对 Rights Management Services SDK 2.1 进行了配置。 有关如何配置新项目以使用 RMS SDK 2.1 的信息，请参阅 [配置 Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)。

你可以从 Microsoft Connect 下载完整的 *IPCHellowWorld* 示例应用程序 [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)。
> [!Note]
> 如果访问 Microsoft Connect 时收到错误，可能因为还未注册。 若要注册：请转到 [Connect](http://connect.microsoft.com)，使用 Microsoft 帐户登录 > Directory > 搜索 Rights Management Services > 加入。


## 加载 MSIPC.dll

需要先调用 [IpcInitialize](/information-protection/sdk/2.1/api/win/functions#msipc_ipcinitialize) 函数以加载 MSIPC.dll，然后才能调用任何 RMS SDK 2.1 函数。

        C++
        hr = IpcInitialize();
        if (FAILED(hr)) {
          wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
          goto exit;
        }

## 枚举模板

RMS 模板定义用于保护数据的策略，即定义允许访问数据的用户及其权限。 RMS 模板安装在 RMS 服务器上。

下面的代码截图枚举默认 RMS 服务器提供的 RMS 模板。

      C++
      hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

      if (FAILED(hr)) {
        DisplayError(L"IpcGetTemplateList failed", hr);
        goto exit;
      }

此调用会检索默认服务器上安装的 RMS 模板，并在 *pcTil* 变量指向的 [IPC_TIL](/information-protection/sdk/2.1/api/win/ipc_til#msipc_ipc_til) 结构中加载结果，然后显示这些模板。

      C++
      if (0 == pcTil->cTi) {
        wprintf(L"*** No templates configured for your RMS server ***\n\n");
        wprintf(L"\\------------------------------------------------------\n\n");
        goto exit;
      }

      for (DWORD dw = 0; dw < pcTil->cTi; dw++) {
        wprintf(L"Template #%d:\n", dw);
        wprintf(L"    Name:         %s\n", pcTil->aTi[dw].wszName);
        wprintf(L"    Description:  %s\n", pcTil->aTi[dw].wszDescription);
        wprintf(L"    Issued by:    %s\n", pcTil->aTi[dw].wszIssuerDisplayName);
        wprintf(L"\n");
      }

## 序列化许可证

需要先序列化许可证并获取内容密钥，然后才能保护任何数据。 内容密钥用于加密敏感数据。 序列化的许可证通常会附加到加密的数据，由受保护的数据的使用者使用。 使用者需要使用序列化的许可证调用 [IpcGetKey](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgetkey) 函数以获取内容密钥，用于解密内容以及获取与内容关联的策略。

为简单起见，使用 [IpcGetTemplateList](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) 返回的第一个 RMS 模板序列化许可证。

通常会使用用户界面对话框以允许用户选择所需模板。

      C++
      hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
        0, NULL, &hContentKey, &pSerializedLicense);

      if (FAILED(hr)) {
        DisplayError(L"IpcSerializeLicense failed", hr);
        goto exit;
      }

执行此操作之后，你会获得内容密钥 *hContentKey* 和序列化的许可证 *pSerializedLicense*（需要附加到受保护的数据）。


## 保护数据

现在你已准备就绪，可以使用 [IpcEncrypt](/information-protection/sdk/2.1/api/win/functions#msipc_ipcencrypt) 函数加密敏感数据。 首先，需要向 **IpcEncrypt** 函数询问加密的数据的大小。

      C++
      cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        NULL, 0, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

此处的 wszText 包含要保护的纯文本。 [IpcEncrypt](/information-protection/sdk/2.1/api/win/functions#msipc_ipcencrypt)函数返回在*cbEncrypted* 参数中返回加密的数据的大小。

现在为加密的数据分配内存。

      C++
      pbEncrypted = (PBYTE)LocalAlloc(LPTR, cbEncrypted);

      if (NULL == pbEncrypted) {
        wprintf(L"Out of memory\n");
        goto exit;
      }

最后，可以执行实际加密。

      C++
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        pbEncrypted, cbEncrypted, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

在此步骤之后，你会获得加密的数据 *pbEncrypted* 和序列化的许可证 *pSerializedLicense*（将由使用者用于解密数据）。

## 错误处理

在此整个示例应用程序中，*DisplayError* 函数用于处理错误。

      C++
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

*DisplayError* 函数使用 [IpcGetErrorMessageText](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) 函数从对应错误代码获取错误消息并将它打印到标准输出。

## 清理

完成之前，还需要释放所有已分配的资源。

      C++
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

- [开发人员指南和信息](developer-notes.md)
- [IpcEncrypt](/information-protection/sdk/2.1/api/win/functions#msipc_ipcencrypt)
- [IpcGetErrorMessageText](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext)
- [IpcGetKey](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcInitialize](/information-protection/sdk/2.1/api/win/functions#msipc_ipcinitialize)
- [IPC_TIL](/information-protection/sdk/2.1/api/win/ipc_til#msipc_ipc_til)
- [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)



<!--HONumber=Oct16_HO1-->


