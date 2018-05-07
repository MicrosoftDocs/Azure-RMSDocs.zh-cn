---
title: Azure 信息保护客户端文件和使用情况日志记录
description: 适用于 Windows 的 Azure 信息保护客户端的客户端文件和使用情况日志记录的相关信息。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 13f82bc12fd77d4f145b059c2962af01094760c3
ms.sourcegitcommit: 5892db302bdf96538ecb3af8e3c2f678f5d1ebe2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="admin-guide-azure-information-protection-client-files-and-client-usage-logging"></a>管理员指南：Azure 信息保护客户端文件和客户端使用情况日志记录

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、带 SP1 的 Windows 7、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

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
    
    - 设置标签（较低）：信息 ID 102
    
    - 设置标签（较高）：信息 ID 103
    
    - 删除标签：信息 ID 104
   
    - 建议提示：信息 105
    
    - 应用自定义保护：信息 ID 201
    
    - 删除自定义保护：信息 ID 202
    
    - 登录（操作）：信息 ID 902
    
    - 下载策略（操作）：信息 ID 901
    
- 操作源：
    
    - 手动 
    
    - 建议
    
    - 自动  
    
    - 系统（用于登录和下载策略）
    
    - 默认
    
- 操作前后的标签 
    
- 操作前后的保护
    
- 用户理由（如果适用）
    

若要了解 Azure 权限管理服务的使用情况日志记录，请参阅[记录和分析 Azure 权限管理服务的使用情况](../deploy-use/log-analyze-usage.md)



## <a name="next-steps"></a>后续步骤
现在你已识别了与 Azure 信息保护客户端关联的所有日志文件，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
