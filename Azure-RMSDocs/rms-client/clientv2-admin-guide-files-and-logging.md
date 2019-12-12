---
title: Azure 信息保护统一标签客户端文件和使用情况日志记录
description: 有关适用于 Windows 的 Azure 信息保护统一标签客户端的客户端文件和使用情况日志记录的信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8f29f0f282c7b9922f5d2f3f95a4cd037b0f4ba1
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935616"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>管理员指南： Azure 信息保护统一标签客户端文件和客户端使用情况日志记录

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、windows 8、带 SP1 的 windows 7、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 r2*
>
> *适用于以下内容的说明： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

安装 Azure 信息保护统一标签客户端之后，您可能需要知道文件的位置，并监视客户端的使用情况。

## <a name="file-locations-for-the-azure-information-protection-unified-labeling-client"></a>Azure 信息保护统一标签客户端的文件位置

客户端文件：   

- 对于 64 位操作系统： **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 对于 32 位操作系统： **\Program Files\Microsoft Azure Information Protection**

客户端日志文件和当前安装的策略文件：

- 对于 64 位和 32 位操作系统： **%localappdata%\Microsoft\MSIP**


## <a name="usage-logging-for-the-azure-information-protection-unified-labeling-client"></a>Azure 信息保护统一标签客户端的使用情况日志记录

统一标签客户端不会将用户活动记录到本地 Windows 事件日志中。 相反，请使用 Azure 信息保护的[中心报表](../reports-aip.md)功能。 


## <a name="next-steps"></a>后续步骤
现在，你已确定了与 Azure 信息保护统一标签客户端关联的所有日志文件，请参阅以下内容，了解支持此客户端所需的其他信息：

- [自定义](clientv2-admin-guide-customizations.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)

