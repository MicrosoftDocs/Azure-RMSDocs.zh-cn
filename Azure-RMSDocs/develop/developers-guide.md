---
title: "开发者指南 - AIP"
description: "开发人员可使用 Azure 信息保护来保护和管理所有类型的文件"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a53c2df2-a0a2-4f1f-995b-75ba55e4489b
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: 16e2137dead237e59ed1d4db9e88a2a29f9595a9
ms.sourcegitcommit: bf103c02966357eccad0a4912851ceae6937c7b3
translationtype: HT
---
# <a name="azure-information-protection-developers-guide"></a>Azure 信息保护开发人员指南

本指南将介绍用于扩展和集成 Azure 信息保护权限管理服务的工具。 本指南的目的是使希望利用权限管理系统的开发人员可为一系列支持的平台构建不同类型的应用程序。

>当前的 Azure 信息保护 SDK 具有权限管理组件，分类和标签处于开发阶段。

## <a name="service-applications"></a>服务应用程序

从企业内容管理系统、业务应用程序或基于云的业务解决方案导出信息时，服务应用程序可提供保护信息的功能。 数据丢失防护 (DLP) 和云应用程序安全性 (CAS) 应用程序都是服务应用程序的示例。 用于开发服务应用程序的 SDK 可通过两种编程模型获取。

- [C++](https://www.microsoft.com/en-us/download/details.aspx?id=38397)
- [C# 托管 API](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcManagedAPI)

### <a name="examples-of-service-applications"></a>服务应用程序的示例

- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是一个启用 RMS 的示例 DLP 应用程序，通过将 RMS 文件 API 用于保护和使用受限制内容，来引导你了解启用 RMS 的 DLP 应用程序应执行的基本步骤。
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是一个示例，演示如何在 Azure 应用程序中使用 RMS SDK 来保护 Azure Blob 存储中的数据。
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是一个示例，演示如何构建监视文件系统中的目录并对每次更改（例如添加文件或修改文件）应用 RMS 保护策略的 Windows 应用程序。
- [ProtectFilesInDir](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/ProtectFilesInDir) 是一个简单的控制台应用程序示例，它将目录视为输入并保护仅在该目录中的所有文件，不允许使用递归。

## <a name="powershell-guides"></a>PowerShell 指南

这些脚本通常由 Azure Rights management 管理员使用，可用于开发和测试服务应用程序。

- [Azure 权限管理 Cmdlet](https://msdn.microsoft.com/library/azure/dn629398.aspx) 可实现从命令行管理 Azure RMS。 这不仅可以实现自动化，而且还支持使用可靠、重复的过程来帮助降低管理开销。 此外，某些 Azure RMS 高级配置和操作还需要 Azure PowerShell。
- [RMS 保护 Cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx) 可与 Azure 信息保护中的 Azure 权限管理 (Azure RMS) 数据保护结合使用，也可与 Active Directory Rights Management Services (AD RMS) 结合使用，以及补充这些权限管理部署的其他 PowerShell 模块。 使用这些 RMS 保护 cmdlet 可批量保护和取消保护任何类型的文件

## <a name="user-applications"></a>用户应用程序

可以使用 RMS SDK 2.1 或 RMS SDK 4.2 构建用户应用程序。
4.2 版本基于 REST 客户端，其 API 特定于几种常见操作系统：iOS/OSX、Android、Linux 以及 Windows。 2.1 版本用于构建基于 Windows 的本地应用程序。

### <a name="user-application-development-guides"></a>用户应用程序开发指南

- [开发应用程序](developing-your-application.md)
- [测试应用程序](how-to-set-up-your-test-environment.md)
- [部署应用程序](deploying-your-application.md)

### <a name="user-application-samples"></a>用户应用程序示例

- [AzureIP 测试](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test)是控制台应用程序示例，允许用户使用 Azure 模板或临时策略加密文档。
- [IPCNotepad](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) 是一个启用 RMS 的示例应用程序，可引导你了解在保护和使用受限制内容时每个启用 RMS 的应用程序应执行的基本步骤。
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是一个工具，可以提供有关任何受 RMS 保护的文件的信息（如内容 ID 或用户权限）。

## <a name="development-environment-setup"></a>开发环境设置

以下指南将介绍如何使用常用工具，完成应用程序开发环境中特定于操作系统的设置步骤。

[![iOS/OSX 安装程序](../media/develop/ios-icon.png)](ios-sdk.md)
[![Android 安装程序](../media/develop/android-icon.png)](android-sdk.md)
[![Windows Phone 安装程序](../media/develop/windows-phone-icon.png)](windows-phone-apps.md)
[Windows 服务安装程序![](../media/develop/windows-icon.png)](install-the-rms-sdk.md)
[![Linux 安装程序](../media/develop/linux-icon.png)](linux-setup.md)


## <a name="how-tos"></a>操作指南

下面的每个主题都为执行应用程序的某一方面提供了具体指导。 服务应用程序是使用 RMS SDK 2.x 生成的。 用户应用程序是使用 RMS SDK 4.x 生成的。 此文章链接具有应用程序类型、服务和用户。

### <a name="general"></a>常规

- [如何启用文档跟踪和撤销（服务）](tracking-content.md)
- [如何部署客户端](../rms-client/client-deployment-notes.md)
- [如何将服务应用程序部署到不同的租户] (how-to-deploy-app.md)
- [如何安装和配置 RMS 服务器（服务）](how-to-install-and-configure-an-rms-server.md)
- [如何使用文档跟踪（用户）](how-to-use-document-tracking.md)
- [如何在 Azure 信息保护中续订对称密钥](how-to-renew-symmetric-key.md)

### <a name="security-and-authentication"></a>安全性和身份验证

- [How to configure your app service application to use Azure Active Directory login](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)（如何配置应用服务应用程序以使用 Azure Active Directory 登录）
- [如何使用 Azure Active Directory 身份验证 (ADAL) 进行身份验证](how-to-use-adal-authentication.md)
- [配置 Azure RMS 进行身份验证（服务）](adal-auth.md)
- [设置 API 安全模式（服务）](setting-the-api-security-mode-api-mode.md)
- [启用应用程序以使用 Azure RMS（服务）](how-to-use-file-api-with-aadrm-cloud.md)
- [如何使用 Azure AD 注册应用并为其启用 RMS（用户）](authentication-integration.md)

### <a name="configuration-and-performance-management"></a>配置和性能管理

- [如何添加显式所有者权限（服务）](add-explicit-owner-rights.md)
- [文件 API 配置（服务）](file-api-configuration.md)
- [如何使用内置权限（用户）](built-in-rights-usage-restriction-reference.md)
- [如何启用错误和性能日志记录（用户）](enabling-logging.md)

## <a name="videos"></a>视频

来自 Microsoft 的 Dan Plastina 提供了此 [Azure 信息保护简介](https://www.microsoft.com/cloud-platform/azure-information-protection)

这些视频来源于 Micorsoft 2016 Ignite 会议

- [组织内的电子邮件安全](https://myignite.microsoft.com/videos/2787)
- [采用综合标识驱动解决方案安全地保护和共享数据](https://myignite.microsoft.com/videos/2784)
- [了解分类、标记和保护如何提供持续的数据保护](https://myignite.microsoft.com/videos/2786)

## <a name="other-resources"></a>其他资源

- [最佳安全实践指南](security-guidelines.md)
- [RMS 开发人员活动角（博客）](https://blogs.msdn.microsoft.com/rms/)
- [Azure 信息保护的常见问题](https://docs.microsoft.com/en-us/information-protection/get-started/faqs)

### <a name="support-articles"></a>支持文章

- [支持的文件格式](supported-file-formats.md)
- [支持的平台](supported-platforms.md)
- [了解使用限制](understanding-usage-restrictions.md)

### <a name="api-reference"></a>API 参考

- [Windows API 参考](https://msdn.microsoft.com/en-us/library/hh535292.aspx)
  - [Windows SDK 错误代码](https://msdn.microsoft.com/library/hh535248.aspx)
- [Windows Phone 和 Windows 应用商店 API 参考](https://msdn.microsoft.com/library/dn891914.aspx)
- [iOS/OSX API 参考](https://msdn.microsoft.com/en-us/library/dn758306.aspx)
- [Android API 参考](https://msdn.microsoft.com/en-us/library/dn758245.aspx)
- [Linux API 参考](http://azuread.github.io/rms-sdk-for-cpp/annotated.html)

### <a name="previous-versions"></a>早期版本

- [AD RMS SDK](https://msdn.microsoft.com/en-us/library/cc530379.aspx) 是 RMS SDK 的第一个版本。
- [AD RMS 脚本工具](https://msdn.microsoft.com/en-us/library/bb968797.aspx) 是 AD RMS 安装的管理工具。

### <a name="see-also"></a>另请参阅

- [开发人员术语](terms.md)
- [Azure 信息保护的术语 - IT 专业人员](../get-started/terminology.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]