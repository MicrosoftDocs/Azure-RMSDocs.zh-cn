---
title: 所需的 API 权限-Microsoft 信息保护 SDK
description: Microsoft 信息保护软件开发工具包操作所需的 API 权限的技术详细信息。
author: msmbaldwin
ms.author: mbaldwin
ms.date: 08/20/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: d1d7e026ffb3b35d2d26f40c6b48baa9a0991a8d
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864866"
---
# <a name="api-permissions-for-the-microsoft-information-protection-sdk"></a>Microsoft 信息保护 SDK 的 API 权限

MIP SDK 使用两个后端 Azure 服务进行标记和保护。 在 Azure Active Directory 应用权限 "边栏选项卡中，这些服务包括：

- Azure Rights Management 服务
- Microsoft 信息保护同步服务

使用 MIP SDK 进行标记和保护时，必须向一个或多个 Api 授予应用程序权限。 各种应用程序身份验证方案可能需要不同的应用程序权限。 对于应用程序身份验证方案，请参阅 [身份验证方案](/azure/active-directory/develop/authentication-flows-app-scenarios)。

应为租户范围内的管理员许可授予要求管理员同意的应用程序权限，如 [AAD 文档](/azure/active-directory/manage-apps/grant-admin-consent#grant-admin-consent-in-app-registrations)中所述。

## <a name="application-permissions"></a>应用程序权限

应用程序权限允许 Azure Active Directory 中的应用程序充当自己的实体，而不是代表特定用户使用。

| 服务                         | 权限名称           | 说明                                  | 需要管理员许可 |
| ------------------------------- | ------------------------- | -------------------------------------------- | ---------------------- |
| Azure Rights Management 服务 | 内容。超级用户         | 读取此租户的所有受保护内容   | 是                    |
| Azure Rights Management 服务 | DelegatedReader   | 代表用户读取受保护的内容   | 是                    |
| Azure Rights Management 服务 | DelegatedWriter   | 代表用户创建受保护的内容 | 是                    |
| Azure Rights Management 服务 | 内容。编写器            | 创建受保护的内容                     | 是                    |
| MIP 同步服务                | UnifiedPolicy。读取 | 读取租户的所有统一策略      | 是                    |

### <a name="contentsuperuser"></a>内容。超级用户

当必须允许应用程序对特定租户的所有受保护的内容进行解密时，此权限是必需的。 需要超级用户权限的服务示例包括数据丢失防护或云访问安全代理服务，这些服务必须能够以纯文本形式查看所有内容，以便对数据的流动位置或存储位置做出策略决策。  

### <a name="contentdelegatedwriter"></a>DelegatedWriter

当必须允许应用程序加密由特定用户保护的内容时，此权限是必需的。 需要委托写入权限的服务的示例是需要基于用户的标签策略加密内容的业务线应用程序，以本机方式应用标签和或加密内容。 此权限允许应用程序对用户上下文中的内容进行加密。

### <a name="contentdelegatedreader"></a>DelegatedReader

当必须允许应用程序对特定用户的所有受保护的内容进行解密时，此权限是必需的。 需要委派的读者权限的服务的示例是需要基于用户标签策略解密内容的业务线应用程序，以本机方式显示内容。 此权限允许应用程序在用户的上下文中对内容进行解密和读取。

### <a name="contentwriter"></a>内容。编写器

当必须允许应用程序加密内容时，此权限是必需的。 需要编写器的服务示例包括业务线应用程序，该应用程序将分类标签应用于导出的文件。 内容。编写器将内容加密为服务主体标识，因此受保护文件的所有者将为服务主体标识。

### <a name="unifiedpolicytenantread"></a>UnifiedPolicy。读取

当必须允许应用程序下载租户的统一标签策略时，此权限是必需的。 需要将标签用作服务主体标识的应用程序示例是需要使用统一策略租户读取的服务。

## <a name="delegated-permissions"></a>委派的权限

委托权限允许 Azure Active Directory 中的应用程序代表特定用户执行操作。

| 服务                         | 权限名称         | 说明                                      | 需要管理员许可 |
| ------------------------------- | ----------------------- | ------------------------------------------------ | ---------------------- |
| Azure Rights Management 服务 | user_impersonation      | 为用户创建和访问受保护的内容 | 否                     |
| MIP 同步服务                | UnifiedPolicy。读取 | 读取用户有权访问的所有统一策略   | 否                     |

### <a name="user_impersonation"></a>user_impersonation

当应用程序必须代表用户允许用户 Azure Rights Management 服务时，此权限是必需的。 需要 User_Impersonation 权限的服务的示例是需要加密的应用程序，或基于用户标签策略访问内容的应用程序，以在本机应用标签或加密内容。
  
### <a name="unifiedpolicyuserread"></a>UnifiedPolicy。读取

当必须允许应用程序读取与用户相关的统一标签策略时，此权限是必需的。 对特定用户保护的内容进行加密。 需要委托写入权限的服务的示例是需要基于用户的标签策略加密内容以在本机应用标签和或加密内容的应用程序。