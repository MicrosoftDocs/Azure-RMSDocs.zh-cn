---
title: Azure 信息保护客户端文件和使用情况日志记录
description: 适用于 Windows 的 Azure 信息保护客户端的客户端文件和使用情况日志记录的相关信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: abf4b87198f2997aa7a452d0c34931c55220ee5f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255064"
---
# <a name="admin-guide-azure-information-protection-client-files-and-client-usage-logging"></a>管理员指南：Azure 信息保护客户端文件和客户端使用情况日志记录

>适用范围：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*

安装 Azure 信息保护客户端后，请了解文件所在位置并监控客户端的使用状况。

## <a name="file-locations-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的文件位置

客户端文件：   

- 对于 64 位操作系统：**\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 对于 32 位操作系统：**\Program Files\Microsoft Azure Information Protection**

客户端日志文件和当前安装的策略文件：

- 对于 64 位和 32 位操作系统：**%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的使用情况日志记录

客户端将用户活动记录到本地 Windows 事件日志“应用程序和服务日志” > “Azure 信息保护”中。 这些事件包括以下信息：

- 客户端版本、策略 ID

- 登录用户的 IP 地址

- 文件名和位置

- 操作:

    - 设置标签：信息 ID 101
    
    - 设置标签（较低）：信息 ID 101
    
    - 设置标签（较高）：信息 ID 101
    
    - 删除标签：信息 ID 104
   
    - 建议提示：信息 105
    
    - 应用自定义保护：信息 ID 201
    
    - 删除自定义保护：信息 ID 202
    
    - 登录（可操作）：信息 ID 902
    
    - 下载策略（可操作）：信息 ID 901
    
- 操作源：
    
    - 手动 
    
    - 建议
    
    - 自动  
    
    - 系统（用于登录和下载策略）
    
    - 默认
    
- 操作前后的标签 
    
- 操作前后的保护
    
- 用户理由（如果适用）

- 自定义包括指定用户、组或组织[按编码名称排列的使用权](../configure-usage-rights.md#usage-rights-and-descriptions)的权限（若适用）

若要了解保护服务的使用情况日志记录，请参阅[记录和分析 Azure 权限管理服务的使用情况](../log-analyze-usage.md)

## <a name="next-steps"></a>后续步骤
现在你已识别了与 Azure 信息保护客户端关联的所有日志文件，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)

