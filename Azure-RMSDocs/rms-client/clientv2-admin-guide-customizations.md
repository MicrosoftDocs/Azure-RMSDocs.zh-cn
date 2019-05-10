---
title: 自定义配置-Azure 信息保护统一标记客户端
description: 有关自定义 Windows 的 Azure 信息保护统一标记客户的信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: a889e29079865d41405727010e3d2060ff870e95
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64767709"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>管理员指南：Azure 信息保护统一标记客户端的自定义配置

>适用对象：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2
>
> 说明：*[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

管理 Azure 信息保护统一标记客户端时，可能需要用于特定方案或一部分用户的高级配置中使用以下信息。

这些设置需要编辑注册表。  

## <a name="sign-in-as-a-different-user"></a>以其他用户身份登录

在生产环境中，用户通常不需要其他用户在使用 Azure 信息保护时统一标记的客户端的身份登录。 不过，作为管理员，你在测试阶段可能需要以其他用户身份登录。 

可以使用“MicrosoftAzure 信息保护”对话框验证当前登录的帐户：打开 Office 应用程序并在**主页**选项卡上，选择**敏感度**按钮，并选择**帮助和反馈**。 帐户名称会显示在“客户端状态”部分中。

请确保还要检查所显示的登录帐户的域名。 很容易忽视的一点是，使用正确的帐户名登录，但域不正确。 使用错误帐户的症状包括无法下载标签，或看不到标签或预期的行为。

以其他用户身份登录：

1. 导航到 %localappdata%\Microsoft\MSIP 并删除 TokenCache 文件。

2. 重新启动任何打开的 Office 应用程序，并使用其他用户帐户登录。 如果您没有在 Office 应用程序中登录到 Azure 信息保护服务中看到在提示符下，返回到**Microsoft Azure 信息保护**对话框并选择**登录**从更新**客户端状态**部分。

此外：

- 完成这些步骤后，仍使用旧帐户 Azure 信息保护统一标记客户端已签名，如果从 Internet Explorer 中，删除所有 cookie，然后重复步骤 1 和 2。

- 如果使用的是单一登录，必须在删除令牌文件后注销 Windows，再使用其他用户帐户登录。 Azure 信息保护统一标记客户端然后自动进行身份验证使用当前登录的用户帐户中。

- 此解决方案支持以同一租户中的其他用户身份登录。 不支持以不同租户中的其他用户身份登录。 若要使用多个租户测试 Azure 信息保护，请使用不同的计算机。

- 可以使用**将设置重置**选项从**帮助和反馈**注销并从 Office 365 安全与合规中心中删除当前下载的标签和策略设置Microsoft 365 安全中心或 Microsoft 365 合规中心。


## <a name="change-the-local-logging-level"></a>更改本地日志记录级别

默认情况下，Azure 信息保护统一到的标记客户端写入客户端日志文件 **%localappdata%\Microsoft\MSIP**文件夹。 这些文件供 Microsoft 支持部门用来排除故障。
 
若要更改这些文件的日志记录级别，请在注册表中找到以下值名称，并将值数据设置为所需的日志记录级别：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

将日志记录级别设置为以下值之一：

- **关闭**：没有本地日志记录。

- **错误**：只有错误。

- **Info**：最低级别日志记录，其中不含事件 ID。

- **Debug**：完整信息。

- **Trace**：详细日志记录（客户端默认设置）。

此注册表设置不会更改发送到适用于 Azure 信息保护的信息[中央报告](../reports-aip.md)。


## <a name="next-steps"></a>后续步骤
现在，你已自定义 Azure 信息保护统一标记客户端，请参阅以下资源，可能需要支持此客户端的其他信息：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)
