---
title: 使用 PowerShell 和 Azure 信息保护统一标记客户端
description: 说明和管理员可以使用 PowerShell 管理 Azure 信息保护统一标记客户端的信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: f3a0d3b3974714135289a8f3b262666b63739330
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181848"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理员指南：使用 PowerShell 管理 Azure 信息保护统一客户端

>适用范围：*[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> *说明：[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

在安装 Azure 信息保护统一标记客户端时，将自动安装 PowerShell 命令。 这允许通过运行可放到脚本中实现自动执行的命令来管理客户端。

Cmdlet 随 PowerShell 模块**AzureInformationProtection**，其中包含 cmdlet 进行标记。 例如：

|标记 cmdlet|示例用法|
|----------------|---------------|
|[Get AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|对于共享文件夹，请标识具有特定标签的所有文件。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|对于共享文件夹，检查文件内容，然后根据指定的条件自动标记未标记的文件。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|对于共享文件夹，将指定的标签应用于没有标签的所有文件。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|用标签标记文件以交互方式，通过使用不同的用户帐户添加到你自己。|

> [!TIP]
> 若要使用路径长度超过 260 个字符的 cmdlet，请使用自 Windows 10 版本 1607 开始提供的以下[组策略设置](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)：<br /> “本地计算机策略” > “计算机配置” > “管理模板” > “所有设置” > “NTFS” > “启用 Win32 长路径” 
> 
> 对于 Windows Server 2016，在安装 Windows 10 的最新管理模板 (.admx) 时，可以使用相同的组策略设置。
>
> 有关详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

此模块安装在 **\ProgramFiles (x86)\Microsoft Azure Information Protection** 中，并将此文件夹添加到 **PSModulePath** 系统变量。 此模块的 .dll 命名为 **AIP.dll**。

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>使用 AzureInformationProtection 模块的先决条件

除了安装 AzureInformationProtection 模块的先决条件，没有其他先决条件时标记 cmdlet 用于 Azure 信息保护：

1. 必须激活 Azure 权限管理服务。

2. 使用自己的帐户从他人的文件中删除保护： 

    - 必须为你的组织启用超级用户功能，而且必须将你的帐户配置为 Azure 权限管理的超级用户。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>先决条件 1：必须激活 Azure Rights Management 服务

如果未激活你的 Azure 信息保护租户以应用保护，请参阅的说明[激活 Azure Rights Management](../activate-service.md)。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>先决条件 2：使用自己的帐户从他人的文件中删除保护

从他人的文件中删除保护的典型方案包括数据发现或数据恢复。 如果使用标签应用保护，则可以通过设置不应用保护的新标签或通过删除标签来删除保护。

用户必须具有从文件删除保护的权限管理使用权限或者成为超级用户。 对于数据发现或数据恢复，通常会使用超级用户功能。 若要启用此功能并将你的帐户配置为超级用户，请参阅[为 Azure 管理权限和发现服务或数据恢复配置超级用户](../configure-super-users.md)。


## <a name="next-steps"></a>后续步骤
有关 cmdlet 帮助信息时在 PowerShell 会话中，键入`Get-Help <cmdlet name> -online`。 例如： 

    Get-Help Set-AIPFileLabel -online

有关支持 Azure 信息保护客户端可能需要的其他信息，请参阅以下内容：

- [自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)
