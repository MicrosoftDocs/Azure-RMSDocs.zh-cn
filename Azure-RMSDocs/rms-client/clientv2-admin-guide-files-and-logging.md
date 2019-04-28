---
title: Azure 信息保护统一标记客户端文件和使用情况日志记录
description: 有关客户端文件和 Azure 信息保护的使用情况日志记录信息的统一标记适用于 Windows 的客户端。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: f49495ae79dbd61e85406957c0fb7864be7116ac
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181287"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>管理员指南：Azure 信息保护统一标记客户端文件和客户端使用情况日志记录

>适用对象：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2
>
> *说明：[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

安装 Azure 信息保护统一标记客户端后，你可能需要知道文件的位置和监视客户端的使用方式。

## <a name="file-locations-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的文件位置

客户端文件：   

- 对于 64 位操作系统：**\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 对于 32 位操作系统：**\Program Files\Microsoft Azure Information Protection**

客户端日志文件：

- 对于 64 位和 32 位操作系统：**%localappdata%\Microsoft\MSIP**


## <a name="next-steps"></a>后续步骤
既然您已经标识与 Azure 信息保护统一标记客户端关联的所有日志文件，请参阅以下其他信息，您可能需要支持此客户端：

- [自定义](clientv2-admin-guide-customizations.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)

