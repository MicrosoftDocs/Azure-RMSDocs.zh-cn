---
title: Azure 信息保护客户端文件和使用情况日志记录
description: 适用于 Windows 的 Azure 信息保护客户端的客户端文件和使用情况日志记录的相关信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9011a6b7fc282c1e170959c31ce1e01bc22aa9c5
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935293"
---
# <a name="admin-guide-azure-information-protection-client-files-and-client-usage-logging"></a>管理员指南：Azure 信息保护客户端文件和客户端使用情况日志记录

>*适用于： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、带 SP1 的 windows 7、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 r2*
>
> *适用于[Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*

安装 Azure 信息保护客户端后，请了解文件所在位置并监控客户端的使用状况。

## <a name="file-locations-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的文件位置

客户端文件：   

- 对于 64 位操作系统： **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 对于 32 位操作系统： **\Program Files\Microsoft Azure Information Protection**

客户端日志文件和当前安装的策略文件：

- 对于 64 位和 32 位操作系统： **%localappdata%\Microsoft\MSIP**

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
    
    - 建议的标签工具提示：信息105
    
    - 应用自定义保护：信息 ID 201
    
    - 删除自定义保护：信息 ID 202
    
    - Outlook 警告消息：信息 ID 301
    
    - Outlook 调整消息：信息 ID 302
    
    - Outlook 阻止消息：信息 ID 303
    
    - 登录（操作）：信息 ID 902
    
    - 下载策略（操作）：信息 ID 901
    
- 操作源：
    
    - Manual 
    
    - 建议
    
    - 自动  
    
    - 系统（用于登录和下载策略）
    
    - 默认值
    
- 操作前后的标签 
    
- 操作前后的保护
    
- 用户理由（如果适用）

- 自定义包括指定用户、组或组织[按编码名称排列的使用权](../configure-usage-rights.md#usage-rights-and-descriptions)的权限（若适用）

Outlook 的事件警告、对齐和阻止消息要求高级客户端设置。 有关详细信息，请参阅[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)。


## <a name="next-steps"></a>后续步骤
现在你已识别了与 Azure 信息保护客户端关联的所有日志文件，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)

