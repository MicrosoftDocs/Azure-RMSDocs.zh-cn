---
# required metadata

title: 常见错误情形和解决方案 | Azure RMS
description: 本主题包括在使用 RMS SDK 2.1 开发人员工具时可能遇到的最常见的错误信息。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ac6453e1-e24f-480e-99bd-02ba9a49f468

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
# 常见错误情形和解决方案
本主题包括在使用 Rights Management Services SDK 2.1 开发人员工具时可能遇到的最常见的错误信息。 它还提供修复错误的推荐操作（如果适用）。

**重要提示** - 对于错误情形的处理，在 SDK API 调用失败后，务必使用对 [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) 的调用，这样一来，你可获得有关错误本质的完整信息。

 

## 错误和操作 ##
下表包含错误常数、相关描述和处理错误情形的推荐操作的列表。

**错误** - *IPCERROR_DEBUGGER_DETECTED* - RMS SDK 2.1 已经检测到调试器

**操作** - RMS SDK 2.1 的开发人员版本不会检查是否存在调试器。 如果可能，请使用此版本的 RMS SDK 2.1 来调试应用程序。
如果必须调试 RMS SDK 2.1 的生产版本，请使用以下指南。

RMS SDK 2.1 中的某些函数在调试器下可能失效：
- [IpcGetKey</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)

要在调用这些函数后调试代码，必须进入此进程，在函数调用完成后附加调试器。 一种方法是使用 assert 语句进入调试器。 ASSERTE 宏包含在 *Crtdbg.h* 标头中。
有关 _ASSERTE 的详细信息，请参阅 [_ASSERT、_ASSERTE 宏](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)

**错误** - *IPCERROR_BROKEN_CERT_CHAIN* - 证书链不匹配。

**操作** - 请确保层次结构项包含基于用来对你的 AD RMS 应用程序清单进行签名的密钥的正确值。
这些是签名密钥和相关联的值（层次结构 **DWORD**）：
- ISV—1
- 生产—0 或不存在

**错误** - *IPCERROR_MACHINE_CERT_NOT_TRUSTED* - 你正在使用 ISV 签名密钥签名的应用程序，但它正在尝试与生产 AD RMS 服务器通信，反之亦然。

- 如果正在使用 AD RMS 服务器的开发人员版本，请确保你要使用 ISV 签名密钥对你的应用程序签名。
- 如果正在使用 AD RMS 服务器的生产版本，请确保你要使用生产签名密钥对你的应用程序签名。

**错误** - *IPCERROR_APPLICATION_AUTH_ERROR_MANIFEST* -应用程序清单无效。 原因可能是已重新生成二进制文件（应用程序），且未重新生成清单。

**操作** - 请确保每次重新生成你的应用程序时，重新生成应用程序清单。

## 相关主题 ##
* [开发人员说明](developer-notes.md)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [_ASSERT、_ASSERTE 宏](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)
 

 


<!--HONumber=Apr16_HO3-->


