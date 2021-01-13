---
title: Azure 信息保护经典客户端文件和使用情况日志记录
description: 有关适用于 Windows 的 Azure 信息保护客户端文件和使用情况日志记录的信息。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c1d362c0a57a326bb0b99e4f0bad5c6244480a1c
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164515"
---
# <a name="admin-guide-azure-information-protection-classic-client-files-and-client-usage-logging"></a>管理员指南： Azure 信息保护经典客户端文件和客户端使用情况日志记录

>***适用于**： Active Directory Rights Management Services， [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，Windows 8，Windows Server 2019，Windows Server 2016，windows Server 2012 R2，windows server 2012 *
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标记客户端，请参阅 [统一标签客户端管理员指南](clientv2-admin-guide-files-and-logging.md)。

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

安装 Azure 信息保护经典客户端之后，您可能需要知道文件的位置，并监视客户端的使用情况。

## <a name="file-locations-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的文件位置

客户端文件：    

- 对于 64 位操作系统：**\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 对于 32 位操作系统：**\Program Files\Microsoft Azure Information Protection**

客户端日志文件和当前安装的策略文件：

- 对于 64 位和 32 位操作系统：**%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-classic-client"></a>Azure 信息保护经典客户端的使用情况日志记录

客户端将用户活动记录到本地 Windows 事件日志 **应用程序和服务日志**  >  **Azure 信息保护**。 这些事件包括以下信息：

- 客户端版本、策略 ID

- 登录用户的 IP 地址

- 文件名和位置

- 操作：

    - 设置标签：信息 ID 101
    
    - 设置标签 (降低) ：信息 ID 102
    
    - 设置标签 (更高) ：信息 ID 103
    
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
    
    - 手动 
    
    - 建议
    
    - 自动  
    
    - 系统（用于登录和下载策略）
    
    - 默认
    
- 操作前后的标签 
    
- 操作前后的保护
    
- 用户理由（如果适用）

- 自定义包括指定用户、组或组织[按编码名称排列的使用权](../configure-usage-rights.md#usage-rights-and-descriptions)的权限（若适用）

Outlook 的事件警告、对齐和阻止消息要求高级客户端设置。 有关详细信息，请参阅[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)。


## <a name="next-steps"></a>后续步骤
现在你已识别了与 Azure 信息保护客户端关联的所有日志文件，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [文档跟踪](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)

