---
title: "发行说明 | Azure RMS"
description: 
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: CE379738-4E1D-42AD-83F4-F89B70456EBB
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 56d0538243af49580f24c701ad5097b30f3059b0
ms.openlocfilehash: 61df64691ac3f4d7e871043767444ea64dfe1ef3


---

# 发行说明

本主题包含有关此版本和以前版本的 RMS SDK 2.1 的重要信息。

## 2016 年 2 月新增内容 - SDK 文档更新

>[!Note]
> 本部分中的功能文档更新适用于 2015 年 12 月 11 日后下载的 SDK。

- **改进的身份验证流程** - 使用基于通过 [Azure Active Directory Authentication Library (ADAL)](https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-libraries/)（Active Directory 身份验证库）的身份验证的 OAuth2 令牌。 有关此过程及其 API 扩展的详细信息，请参阅 [ADAL authentication for your RMS enabled application](how-to-use-adal-authentication.md)（适用于启用了 RMS 的应用程序的 ADAL 身份验证）。

- **更新到 ADAL**：通过更新应用程序来使用 ADAL 身份验证而不使用 Microsoft Online 登录助手，你和你的客户将能够：

 - 使用多重身份验证
 - 安装 RMS 2.1 Client，而无需对计算机的管理特权
 - 验证适用于 Windows 10 的应用程序

- **RMS SDK 将不再支持 Microsoft Online 登录助手 (SIA)。** 我们将继续支持使用 SIA 6 个月，之后将停止对其的支持。


## 2015 年 12 月更新

- 多个方面都已实施了性能改进，包括：
    - 使用仅限许可证的服务器时，从主授权服务器发布。
    - 当没有网络连接时，RMS SDK 2.1 更快出现故障

- 引入许多更新，以改进错误消息传送和故障排除体验。
- 另请注意，[受支持的平台](supported-platforms.md)列表也进行了更新。
- RMS SDK 2.1 不再需要预生产环境，也不再需要使用应用程序清单。 本开发人员文档集中已删除这些部分，并对整个文档进行了简化和重新组织。

## 2015 年 5 月更新

-   **服务应用程序和基于云的 RMS** - [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) 需要三部分信息；对称密钥、**AppPrincipalId** 和 **TenantBposId**。 有关此内容的主题已更新，提供了关于处理此获取信息的指导。 有关此更新，请参阅更新版本的[使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

## 2015 年 4 月更新

-   现在可通过一组新的 API 进行**文档跟踪**。 有关详细信息，请参阅[跟踪内容](tracking-content.md)。
-   **加密类型** - 我们现在支持针对加密包选择的 API 级别控制。 有关详细信息，请参阅[使用加密](working-with-encryption.md)。

    **注意**：我们将不再公开 API 中的 **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** 标志。 这意味着，如果以后的应用程序引用此标志，则这些应用程序将无法再编译，但已构建的应用程序可以继续工作，因为我们遵循 API 代码中的专用标志。 只需更改一个标志，仍然能获得旧的不推荐使用的加密算法标志的益处。 有关详细信息，请参阅[使用加密](working-with-encryption.md)。

-   **服务器模式应用程序**，其 [**API 模式值**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)为 **IPC\_API\_MODE\_SERVER**，不再需要应用程序清单。 你可以针对生产 RMS 服务器对应用程序进行测试，切换到生产环境时无需获取生产许可证。 有关服务器模式应用程序的详细信息，请参阅[应用程序类型](application-types.md)。
-   现在通过文件和针对 Windows 的事件跟踪这两种方法实施**日志记录**。
-   如果是在 **Windows 7 SP1 或 Windows Server 2008 R2 计算机**上运行，请参阅“重要的开发人员说明”下面的说明。

## 2015 年 1 月更新

-   **受支持的保护文件 (pfile) 大小增加** - 现在支持大小超过 1 千兆字节 (1 GB) 的 pfile。 有关 pfile 的详细信息，请参阅[支持文件格式](supported-file-formats.md)。
-   **改进日志记录以提高诊断性能** - 对于应审查的消息，日志记录级别将显示 **ERROR** 或 **WARNING**。 其他所有消息（包括仍会显示的例外）将记录为 **INFO**。

    我们选择此方法是希望你不错过任何详细信息。 现在，只有重要的消息会显示为 WARNING 级别。

-   **获取公司模板** – 基于客户报告和反馈，对模板获取代码进行了大量修复。
-   改进的本地化一致性

## 2014 年 10 月更新

-   SDK 的文件 API 组件的默认行为已更新。 有关详细信息，请参阅[文件 API 配置](file-api-configuration.md)。
-   开发人员说明主题[启用电子邮件通知](how-to-enable-email-notification.md)中介绍了一项新功能，即电子邮件通知。

## 2014 年 7 月更新

SDK 的文件 API 组件已扩展并提供以下功能：

-   标识要使用的保护程序。
-   在文件的粒度级别提供 RMS 保护。

    本版本中添加的功能：

    **注意**：文件 API 扩展中添加了更多支持数据类型和结构，但此处未列出。 本版本中已更新的所有主题都标记为**初步文档，可能随时更改**。

    -   [**IpcfOpenFileOnHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfopenfileonhandle)
    -   [**IpcfOpenFileOnILockBytes**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfopenfileonilockbytes)
    -   [**IpcfGetFileProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetfileproperty)
    -   [**IpcfLogicalFileRangeToRawFileRange**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcflogicalfilerangetorawfilerange)
    -   [**IpcfReadFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfreadfile)
    -   [**IpcfSetEndOfFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfsetendoffile)
    -   [**IpcfWriteFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfwritefile)

## 2014 年 4 月更新

-   **文件 API 内存使用**显著改善，尤其对于大型 PFile 更是如此。
-   现在可通过属性 **IPC\_LI\_CONTENT\_ID** 编写**内容 ID**。 有关详细信息，请参阅[**许可证属性类型**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA)。
-   **生产清单要求** - 在服务器模式下运行启用 RMS 的应用程序/服务时，我们不再需要清单。 有关详细信息，请参阅[应用程序类型](application-types.md)。
-   **文档更新**

    **测试最佳实践** - 增加了有关在使用 Azure RMS 之前使用本地服务器的指导 有关详细信息，请参阅[使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

## 重要的开发人员说明

-   **针对所有文件类型的本机支持**

    在本版本的 Rights Management Services SDK 2.1 中，可为任何文件类型（扩展）添加本机支持。 例如，对于任何扩展 &lt;ext&gt;（非 office 和 pdf），如果该扩展的管理配置是“NATIVE”，则将使用 \*.p&lt;ext&gt;。

    有关受支持的文件类型的详细信息，请参阅[文件 API 配置](file-api-configuration.md)。

-   不带更新 [KB2533623](https://support.microsoft.com/en-us/kb/2533623) 的 **Windows 7 SP1 和 Windows Server 2008 R2 SP1 计算机**可能出现以下错误以保护任何 office 文件“参数不正确。 错误代码 0x80070057”。 如果看到此错误，请安装更新，然后重试。 如果问题仍然存在，请联系 RMS SDK Beta 反馈别名 <rmcstbeta@microsoft.com>。

    **注意**：自 2015 年 4 月版本起，此 KB 的安装流程中添加了检查程序。

     

-   **文件 API 集成**

    添加了文件 API 后的 Active Directory Rights Management Services 文件 API 具有以下好处和功能。

      - 你可以通过自动化方式保护机密数据，而无需知道不同文件格式所使用的信息权限管理 (IRM) 实施的详细信息。

      - Microsoft Office 文件、可移植文档格式 (PDF) 文件以及选定的其他文件类型都可使用本机保护进行保护。 有关可通过本机保护进行保护的文件类型的完整列表，请参阅[文件 API 配置](file-api-configuration.md)。

      - 除了系统文件和 Office 文件以外的所有文件都可使用 RMS 受保护的文件格式 (PFile) 进行保护。

    文件 API 通过以下四个新函数实现：[IpcfDecryptFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)[IpcfEncryptFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)、[IpcfGetSerializedLicenseFromFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetserializedlicensefromfile) 和 [IpcfIsFileEncrypted](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfisfileencrypted)。

    文件 API 要求客户端计算机上安装 Rights Management Service 客户端 2.1 ，并要求该计算机连接到 RMS 服务器。 有关 RMS 服务器、RMS 客户端及其功能的详细信息，请参阅 TechNet 内容以获取[针对 RMS 的 IT 专业人员文档](https://technet.microsoft.com/en-us/library/cc771234(v=ws.10).aspx)。

-   **问题**：从头开始创建许可证时，必须明确授予所有权。

    **解决方案**：使用 [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch) 从头开始创建许可证时，你的应用程序必须向许可证所有者显式添加“所有者”权限。 有关详细信息，请参阅[添加显式所有者权限](add-explicit-owner-rights.md)。

-   **问题**：如果应用程序使用手柄为同一窗口两次调用 [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) 或 [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow)，则 RMS SDK 2.1 将在 **HRESULT** 中返回一个故障。

    **解决方案**：有关此问题的具体指导，请参阅 [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) 和 [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow) 中的“备注”部分。

-   **问题**：为多个体系结构进行构建时，必须使用此指导。

    **解决方案**：如果要对不同的体系结构使用 Ipcsecproc\*isv.dll（例如，你已经在 64 位计算机上安装了 64 位 SDK，但现在想要在需要 Ipcsecproc\*isv.dll 的 32 位计算机上部署），则你必须安装在其他计算机上安装 32 位 SDK，然后将 Ipcsecproc\*isv.dll 文件从“%PROGRAMFILES%\\Microsoft Information Protection And Control”文件夹（默认位置，或者你选择安装 SDK 的任何位置）复制到该计算机上。

## 常见问题

**Q**：默认语言行为如何使用包含 LCID 参数的功能？

**A**：使用 0 作为默认区域设置。 在这种情况下，AD RMS Client 2.1 会按以下顺序查找名称和描述，并检索第一个可用名称：

    1 - User preferred LCID.
    2 - System locale LCID.
    3 - The first available language specified in the Rights Management Server (RMS) template.

如果检索不到任何名称和描述，则将返回一个错误。 特定 LCID 只能有一个名称和描述。

## 相关主题

* [概述](ad-rms-overview.md)
* [添加显式所有者权限](add-explicit-owner-rights.md)
* [文件 API 配置](file-api-configuration.md)
* [**IpcfGetSerializedLicenseFromFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetserializedlicensefromfile)
* [**IpcfEncryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfIsFileEncrypted**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfisfileencrypted)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow)
* [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow)
 

 



<!--HONumber=Jun16_HO4-->


