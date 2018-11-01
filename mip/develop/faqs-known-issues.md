---
title: 常见问题解答和已知问题 - Microsoft 信息保护 SDK。
description: Microsoft 信息保护 (MIP) SDK 常见问题解答和已知问题的疑难解答指南。
author: BryanLa
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 10/19/2018
ms.author: bryanla
ms.openlocfilehash: cb3bdd6f2d9328a57156580f3d345d25983fccad
ms.sourcegitcommit: cc65c3851d4b8169a1a62c83afaf0f75402f7631
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2018
ms.locfileid: "49476409"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-known-issues"></a>Microsoft 信息保护 (MIP) SDK 常见问题解答和已知问题

## <a name="frequently-asked-questions-faqs"></a>常见问题 (FAQ)

### <a name="question-which-platforms-are-supported-by-the-mip-sdk"></a>问：MIP SDK 支持哪些平台？

以下平台支持 MIP SDK：

[!INCLUDE [MIP SDK platform support](../include/mip-sdk-platform-support.md)]

### <a name="question-how-does-the-sdk-handle-strings-and-what-string-type-should-i-be-using-in-my-code"></a>问：SDK 如何处理字符串，在我的代码中应使用什么字符串类型？

SDK 旨在跨平台使用，并使用 [UTF-8（Unicode 转换格式 - 8 位）](https://wikipedia.org/wiki/UTF-8)来处理字符串。 具体指南取决于你所使用的平台：

| 平台 | 指南 |
|-|-|
| Windows 本机 | 对于 C++ SDK 客户端，C++ 标准库类型 [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) 用于将字符串传递给 API 函数或从中传递字符串。 MIP SDK 在内部管理 UTF-8 的转换。 当从 API 中返回 `std::string` 时，如果转换字符串，则必须相应地进行 UTF-8 编码和管理。 在某些情况下，字符串作为 `uint8_t` 矢量的一部分返回（例如发布许可证 (PL)），但应被视为不透明 blob。<br><br>有关详细信息和示例，请参阅：<ul><li>[WideCharToMultiByte 函数](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) 用于帮助将宽字符字符串转换为多字节，例如 UTF-8。<li>以下示例文件包含在 [SDK 下载](setup-configure-mip.md#configure-your-client-workstation)中：<ul><li>`file\samples\common\string_utils.cpp` 中的示例字符串实用工具函数，用于宽 UTF-8 字符串的转换。<li>`file\samples\file\main.cpp` 中 `wmain(int argc, wchar_t *argv[])` 的实现，使用前面的字符串转换函数。</li></ul></ul>|
| .NET | 对于 .NET SDK 客户端，所有字符串都使用默认的 UTF-16 编码，不需要使用任何特殊转换。 MIP SDK 在内部管理 UTF-16 的转换。 |
| 其他平台 | MIP SDK 支持的所有其他平台都具有对 UTF-8 的本机支持。 |

## <a name="known-issues"></a>已知问题

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>错误：“无法分析获得的符合性策略”  

你下载了 MIP SDK 并运行示例应用程序。 你使用文件示例来尝试列出所有标签，但收到以下错误：

| 错误 | 解决方案 |
|-|-|
|*发生了意外：无法分析获得的符合性策略。Failed with: [class mip::CompliancePolicyParserException] Tag not found: policy, NodeType: 15, Name: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]*| 这表示你尚未将你的标签从 Azure 信息保护迁移到统一标记体验！ 请按照[如何将 Azure 信息保护标签迁移到 Office 365 安全与合规中心](/azure/information-protection/configure-policy-migrate-labels)的步骤操作，以迁移标签，然后在 Office 365 安全与合规中心创建标签策略。 一旦完成该操作，示例将成功运行。|
