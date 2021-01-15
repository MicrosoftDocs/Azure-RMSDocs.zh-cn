---
title: 常见问题解答和已知问题 - Microsoft 信息保护 SDK。
description: Microsoft 信息保护 (MIP) SDK 常见问题解答以及问题和错误的疑难解答指南。
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: da1e3f26ca4c2a0326b6ae8dfee7a13a1855044a
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212597"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Microsoft 信息保护 (MIP) SDK 常见问题解答和问题

本文提供对常见问题 (FAQ) 的解答，以及针对已知问题和常见错误的疑难解答指南。

## <a name="frequently-asked-questions"></a>常见问题

### <a name="metadata-storage-changes"></a>元数据存储更改

我们 [最近宣布](https://aka.ms/mipsdkmetadata) 你要对 office 文件 (Word、Excel、PowerPoint) 的标签元数据存储位置进行更改，以支持 office 365、SharePoint Online 和其他服务中的新增功能。

#### <a name="metadata-faq"></a>元数据常见问题解答

**问**：首个功能何时变为可用，需要这个新的存储位置？

- 我们期望第一季度的第一季度的第一天将在2021年的第二季度推出。 客户可能会提前选择参加专用或公共预览。  

**问题**：其他格式是否受影响（如 PDF）？

- 否，仅 Office 文件，尤其是 Word、Excel 和 PowerPoint 文件。

**问**：是否有必需的特定版本的 MIP SDK？

- MIP SDK 1.7 及更高版本是完全兼容的。

**问**：是否存在将需要的特定版本的 Office 客户端或使用此存储？

- 随着功能的推出，将更新 Office 客户端以利用新的存储位置。 在租户管理员启用这些功能之前，不会使用新的存储位置。

**问**：作为自定义属性存储的现有元数据是否 *custom.xml* 保持最新？

- 不是。 启用新的存储位置后，首次保存文档时，标签元数据将移动到新位置。 通过编写的元数据 [`LabelingOptions.ExtendedProperties`](https://docs.microsoft.com/dotnet/api/microsoft.informationprotection.file.labelingoptions.extendedproperties?view=mipsdk-dotnet-1.7#Microsoft_InformationProtection_File_LabelingOptions_ExtendedProperties) 将保留在 *custom.xml* 中。

**问**：是否可以读取没有 MIP SDK 的标签元数据？ 

- 是的，但您需要实现自己的代码以分析文件并提取信息。

**问**：目前，可以通过从文件中提取键/值对字符串来 "读取" 标签。 仍会以这种方式读取？ 

- 是的，在要读取的 Office 文件 XML 中，元数据仍可用。 但应注意，你的应用程序将需要了解是否已启用新功能集来了解哪个部分 ( # A0 与 labelinfo.xml) 具有权威性。 查看 [OFFCRYPTO： LabelInfo 与自定义文档属性 |Microsoft Docs。](https://docs.microsoft.com/openspecs/office_file_formats/ms-offcrypto/13939de6-c833-44ab-b213-e0088bf02341) 了解实现的详细信息。
  
**问题**：如何查明是否已启用新功能？ 

- 我们将在我们接近功能发布日期时共享此信息。 

**问**：如何迁移标签？

- 以下逻辑用于确定读取或写入标签数据的部分。

| 操作                                                                                                | 功能未启用                                                                    | 已启用功能                                              |
| ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| 读取                                                                                                  | custom.xml 中的标签 (未受保护的) 或 Doc SummaryInfo (受保护的) 。                      | 如果 labelinfo.xml 中存在标签，则它是有效标签。<br> 如果 labelinfo.xml 中没有标签，则 custom.xml 或 Doc SummaryInfo 中的标签为有效标签。 |
| 写入                                                                                                 | 所有新标签都将写入 custom.xml (未受保护的) 或 Doc SummaryInfo (受保护的) 。 | 所有新标签都将写入 labelinfo.xml。                 |


<br>
<br>

### <a name="file-parsing"></a>文件分析

**问**：我是否能写入目前正在用文件 SDK 阅读的同一文件？

MIP SDK 不支持同时读取和写入同一文件。 任何标记的文件都将导致输入文件的 *副本* 应用了标签操作。 应用程序必须将原始文件替换为标记文件。

### <a name="sdk-string-handling"></a>SDK 字符串处理

**问**： SDK 如何处理字符串，以及我应该在代码中使用哪种字符串类型？

SDK 旨在跨平台使用，并使用 [UTF-8（Unicode 转换格式 - 8 位）](https://wikipedia.org/wiki/UTF-8)来处理字符串。 具体指南取决于你所使用的平台：

| 平台        | 指南                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Windows 本机  | 对于 c + + SDK 客户端，c + + 标准库类型 [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) 用于向/从 API 函数传递字符串。 MIP SDK 在内部管理 UTF-8 的转换。 当从 API 中返回 `std::string` 时，如果转换字符串，则必须相应地进行 UTF-8 编码和管理。 在某些情况下，字符串作为 `uint8_t` 矢量的一部分返回（例如发布许可证 (PL)），但应被视为不透明 blob。<br><br>有关详细信息和示例，请参阅：<ul><li>[WideCharToMultiByte 函数](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) 用于帮助将宽字符字符串转换为多字节，例如 UTF-8。<li>以下示例文件包含在 [SDK 下载](setup-configure-mip.md#configure-your-client-workstation)中：<ul><li>`file\samples\common\string_utils.cpp` 中的示例字符串实用工具函数，用于宽 UTF-8 字符串的转换。<li>`file\samples\file\main.cpp` 中 `wmain(int argc, wchar_t *argv[])` 的实现，使用前面的字符串转换函数。</li></ul></ul> |
| .NET            | 对于 .NET SDK 客户端，所有字符串都使用默认的 UTF-16 编码，不需要使用任何特殊转换。 MIP SDK 在内部管理 UTF-16 的转换。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 其他平台 | MIP SDK 支持的所有其他平台都具有对 UTF-8 的本机支持。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## <a name="issues-and-errors-reference"></a>问题和错误参考

### <a name="error-file-format-not-supported"></a>错误：“不支持的文件格式”  

**问**：在尝试保护或标记 PDF 文件时，为什么会收到以下错误？

> 不支持的文件格式

此异常是由于尝试保护或标记已进行数字签名或密码保护的 PDF 文件导致的。 有关保护或标记 PDF 文件的详细信息，请参阅[使用 Microsoft 信息保护进行 PDF 加密的新支持](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757)。

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>错误：“无法分析获得的符合性策略”  

**问**：在下载 MIP SDK 并尝试使用该文件示例列出所有标签后，为什么会收到以下错误？

> 发生了意外：无法分析获得的符合性策略。 Failed with: [class mip::CompliancePolicyParserException] Tag not found: policy, NodeType: 15, Name: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]

此错误表明你尚未将标签从 Azure 信息保护迁移到统一的标签体验。 请按照[如何将 Azure 信息保护标签迁移到 Office 365 安全与合规中心](/azure/information-protection/configure-policy-migrate-labels)的步骤操作，以迁移标签，然后在 Office 365 安全与合规中心创建标签策略。 

### <a name="error-nopolicyexception-label-policy-did-not-contain-data"></a>错误： "NoPolicyException：标签策略不包含数据"

**问**：尝试通过 MIP SDK 读取标签或列表标签时，为什么会收到以下错误？

> NoPolicyException：标签策略不包含数据，CorrelationId = GUID，CorrelationId。 Description = PolicyProfile，NoPolicyError = SyncFile，NoPolicyError = SyncFile

此错误表示未在 Microsoft 安全性和符合性中心发布标签策略。 按照 [创建和配置敏感度标签及其策略](/microsoft-365/compliance/create-sensitivity-labels) 来配置标记策略。

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>错误： "System.componentmodel. Win32Exception： LoadLibrary failed"

**问**：在使用 MIP SDK .net 包装时，为什么会收到以下错误？

> System.componentmodel： Win32Exception： LoadLibrary 在调用 MIP.Initialize ( # A1 时 sdk_wrapper_dotnet.dll 失败。

你的应用程序没有所需的运行时，或未构建为发布。 有关详细信息，请参阅 [确保应用具有所需的运行时](setup-configure-mip.md#ensure-your-app-has-the-required-runtime) 。 

### <a name="error-proxyautherror-exception"></a>错误： "ProxyAuthError exception"

**问**：在使用 MIP SDK 时，为什么会收到以下错误？

> "ProxyAuthenticatonError：不支持代理身份验证"

MIP SDK 不支持使用经过身份验证的代理。 若要修复此消息，代理管理员应将 Microsoft 信息保护服务终结点设置为绕过代理。 " [Office 365 url 和 IP 地址范围](/office365/enterprise/urls-and-ip-address-ranges) " 页上提供了这些终结点的列表。 MIP SDK 要求 `*.protection.outlook.com` (第9行) 和 Azure 信息保护服务终结点 (行 73) 绕过代理身份验证。
