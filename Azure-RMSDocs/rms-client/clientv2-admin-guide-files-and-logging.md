---
title: Azure 信息保护统一标签客户端文件和使用情况日志记录
description: 有关适用于 Windows 的 Azure 信息保护统一标签客户端的客户端文件和使用情况日志记录的信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4e254b5de68e340565ec8ccd50cd0eed1897a00f
ms.sourcegitcommit: d3ac12c51b41bd1ec4ce4009303d124efc95353b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70180588"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>管理员指南：Azure 信息保护统一标签客户端文件和客户端使用情况日志记录

>适用范围： *[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> 说明： *[适用于 Windows 的 Azure 信息保护统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

安装 Azure 信息保护统一标签客户端之后, 您可能需要知道文件的位置, 并监视客户端的使用情况。

## <a name="file-locations-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的文件位置

客户端文件：   

- 对于 64 位操作系统： **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 对于 32 位操作系统： **\Program Files\Microsoft Azure Information Protection**

客户端日志文件:

- 对于64位和32位操作系统: **%localappdata%\Microsoft\MSIP\Logs**


## <a name="next-steps"></a>后续步骤
现在, 你已确定了与 Azure 信息保护统一标签客户端关联的所有日志文件, 请参阅以下内容, 了解支持此客户端所需的其他信息:

- [自定义](clientv2-admin-guide-customizations.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)

