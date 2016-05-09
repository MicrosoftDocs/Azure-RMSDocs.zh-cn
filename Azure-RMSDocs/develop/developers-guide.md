---
# required metadata

title: 开发人员指南 | Azure RMS
description: 开发人员工具使用的概述；SDK、其他库以及代码示例。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a22e6bd0-8ce8-45b4-9a32-273126ab831e

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 管理员指南

## 概述 ##
现在可使用三代的 Rights Management SDK：适用于 Android、iOS/OS X、Windows 设备和 Linux 的 **Microsoft Rights Management SDK 4.2**、适用于 Windows 桌面客户端的 **Microsoft Rights Management SDK 2.1** 以及被取代的 **AD RMS SDK**。

## 软件开发工具包 ##
| SDK | 描述 |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | 简化的下一代工具集，可提供轻型开发体验，以便通过 Microsoft Rights Managemen 实现对 Android、iOS、Mac OS X、Windows Phone/RT 和 Linux/C++ 设备应用的信息保护 |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | 为 Windows 桌面应用程序开发人员和基于服务器的解决方案提供商而提供的功能强大的 SDK，可实现对产品的权限管理|
|[AD RMS SDK](https://msdn.microsoft.com/en-us/library/cc530379(v=vs.85).aspx)|** 注意 ** - AD RMS SDK 利用客户端在 Msdrm.dll 中公开的功能，可用于 Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows Server 2008 和 Windows Vista。 它可能在后续版本中变更或不可用。 请改用 Microsoft Rights Management Services SDK 2.1（它利用客户端在 Msipc.dll 中公开的功能）。|
|[AD RMS 脚本编写 API](https://msdn.microsoft.com/en-us/library/bb968797(v=vs.85).aspx)| 用于创建脚本以管理 AD RMS 安装|

## 代码示例和工具
这一 Microsoft 提供的 RMS 代码示例和开发人员支持工具集合跨越所有支持的操作系统（Android、iOS/OS X、Windows Phone 和 Windows 桌面），会定期更新以保持与其支持的 SDK 之间的兼容性。

### Android

以下各项在受 [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) 及更高版本的 4.x SDK 支持的 Android 上运行。

- GitHub 上的 [UI 库和示例应用](https://github.com/AzureAD/rms-sdk-ui-for-android)，可让你快速入门并在应用中重复使用我们的标准 UI。
- Java 中的 [Android 使用方案](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx)表示重要开发方案，可让你熟悉 RMS SDK。 相关示例包括使用 Microsoft 受保护的文件格式、自定义受保护的文件格式和自定义 UI 控件。

### iOS/OS X

以下在各项受 [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) 及更高版本的 4.x SDK 支持的 iOS/OS X 上运行。

- Objective C 中的 [iOS/OS X 使用方案](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx) 表示重要开发方案，可让你熟悉 RMS SDK。 相关示例包括使用 Microsoft 受保护的文件格式、自定义受保护的文件格式和自定义 UI 控件。
- GitHub 上的 [UI 库和示例应用](https://github.com/AzureAD/rms-sdk-ui-for-ios)，可让你快速入门并在应用中重复使用我们的标准 UI。 **仅在 iOS**上受支持。

### Windows 桌面

以下各项在受 [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) 及更高版本的 2.x SDK 支持的 Windows 桌面上运行。

- [读取受 PFILE 保护的 PDF](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) 是我们 RMS 开发人员活动角博客上的一个简单代码示例，它使用 MSIPC 文件 API 来解密并打开受 PFILE 保护的 PDF 文档。
- [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是 RMS SDK 2.1 的 .NET (C#) 表示形式，通过它可方便地使托管应用程序启用 RMS。
- [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) 是一个启用 RMS 的示例应用程序，可引导你了解在保护和使用受限制内容时每个启用 RMS 的应用程序应执行的基本步骤。
- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是一个启用 RMS 的示例数据泄漏防护 (DLP) 应用程序，通过将文件 API 用于保护和使用受限制内容，来引导你了解启用 RMS 的 DLP 应用程序应执行的基本步骤。
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是一个示例，演示如何在 Azure 应用程序中使用 RMS SDK 来保护 Azure Blob 存储中的数据。
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是一个工具，可以提供有关任何受 RMS 保护的文件的信息（如内容 ID 或用户权限）。
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是一个示例，演示如何构建监视文件系统中的目录并对每次更改（例如添加文件或修改文件）应用 RMS 保护策略的 Windows 应用程序。

### Windows 应用商店和 Windows Phone

- [Windows 应用商店的 UI 库](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore) - 适用于 Windows 应用商店应用程序的 Microsoft RMS SDK v4.1 的 UI 库。 此库是可选的，开发人员在使用 Microsoft RMS SDK v4.1 时可以选择生成他们自己的 UI

- [Windows Phone 的 UI 库](https://github.com/AzureAD/rms-sdk-ui-for-winphone) - 适用于 Windows Phone 应用程序的 Microsoft RMS SDK v4.1 的 UI 库。 此库是可选的，开发人员在使用 Microsoft RMS SDK v4.1 时可以选择生成他们自己的 UI

- [示例应用程序](https://github.com/Azure-Samples/active-directory-dotnet-rms-windowsstore) - 适用于 Windows 应用商店应用程序的 Microsoft RMS SDK v4.1 的示例为平台提供基本文档使用示例。


<!--HONumber=Apr16_HO3-->


