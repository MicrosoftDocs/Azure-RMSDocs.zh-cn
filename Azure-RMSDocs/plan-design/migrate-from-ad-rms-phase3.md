---
title: "从 AD RMS 迁移到 Azure 信息保护 - 第 3 阶段"
description: "从 AD RMS 迁移到 Azure 信息保护的第 3 阶段涉及从 AD RMS 迁移到 Azure 信息保护中的步骤 7。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/11/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5de30d095e1c279babb8f8be74a5a9b9d54db204
ms.sourcegitcommit: 45c23b3b353ad0e438292cb1cd8d1b13061620e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2017
---
# <a name="migration-phase-3---client-side-configuration"></a>迁移第 3 阶段 - 客户端配置

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*

使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的阶段 3。 这些过程涉及了[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)中的步骤 7。

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>步骤 7. 重新配置 Windows 计算机以使用 Azure 信息保护

在 Windows 计算机中使用两个迁移脚本来重新配置 AD RMS 客户端：

- Migrate-Client.cmd

- Migrate-User.cmd

客户端配置脚本 (Migrate-Client.cmd) 在注册表中配置计算机级别设置，这意味着它必须在可进行这些更改的安全上下文中运行。 这通常指以下方法之一：

- 使用组策略，将该脚本作为计算机启动脚本运行。

- 使用组策略软件安装，将脚本分配给计算机。

- 使用软件部署解决方案，将脚本部署给计算机。 例如，使用 System Center Configuration Manager [包和程序](/sccm/apps/deploy-use/packages-and-programs)。 在包和程序的属性中，在“运行模式”下，指定在设备上使用管理权限运行该脚本。 

- 如果用户具有本地管理员特权，请使用登录脚本。

用户配置脚本 (Migrate-User.cmd) 配置用户级别设置，并清除客户端许可证存储。 这意味着此脚本必须在实际用户上下文中运行。 例如：

- 使用登录脚本。

- 使用组策略软件安装来发布脚本供用户运行。

- 使用软件部署解决方案，将脚本部署给用户。 例如，使用 System Center Configuration Manager [包和程序](/sccm/apps/deploy-use/packages-and-programs)。 在包和程序的属性中，在“运行模式”下，指定使用该用户的权限运行该脚本。 

- 用户登录到他们的计算机时要求其运行该脚本。

这两个脚本包含一个版本号并且不会重新运行，除非更改该版本号。 也就是说，可以一直在原位保留这两个脚本，直到迁移完成。 但如果确实对想要计算机和用户在 Windows 计算机上重新运行的脚本进行了更改，可将这两个脚本中的以下行更新为较高的值：

    SET Version=20170427

用户配置脚本专门设计在客户端配置脚本之后运行，并在此检查中使用版本号。 如果版本相同的客户端配置脚本未运行，它将停止。 此检查可确保这两个脚本以正确的顺序运行。 

如果无法同时迁移所有 Windows 客户端，请分批对客户端运行以下过程。 对于批次中具有要迁移的 Windows 计算机的每个用户，将用户添加到之前创建的 **AIPMigrated** 组。

### <a name="windows-client-reconfiguration-by-using-registry-edits"></a>使用注册表编辑重新配置 Windows 客户端

1. 返回到迁移脚本 Migrate-Client.cmd 和 Migrate-User.cmd 中，这是之前在[准备阶段](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration)下载这些脚本时提取的。

2.  按照 MigrateClient.cmd 中的说明修改脚本，以便它包含租户的 Azure Rights Management 服务 URL，以及 AD RMS 群集 Extranet 授权 URL 和 Intranet 授权 URL 的服务器名称。 然后，使上述脚本版本递增。 若要跟踪脚本版本，最好采用以下格式使用今天的日期：YYYYMMDD

    > [!IMPORTANT]
    > 仍然注意，不要在地址前后引入多余空格。
    > 
    > 此外，如果 AD RMS 服务器使用 SSL/TLS 服务器证书，请检查字符串中许可 URL 值是否包括端口号 **443**。 例如：https:// rms.treyresearch.net:443/_wmcs/licensing。 单击群集名称并查看“群集详细信息”时，Active Directory Rights Management Services 中会显示此信息。 如果端口号 443 包含在此 URL 中，修改脚本时请将该值包括在内。 例如，https://rms.treyresearch.net:**443**。 

    如果需要针对 &lt;YourTenantURL&gt; 检索 Azure Rights Management 服务 URL ，请重新参考[确定 Azure Rights Management 服务 URL](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url)。

3. 使用此步骤开始处的说明，配置脚本部署方法，在由 AIPMigrated 组成员使用的 Windows 客户端计算机上运行 Migrate-Client.cmd 和 Migrate-User.cmd。 

## <a name="next-steps"></a>后续步骤
若要继续迁移，请转到[第 4 阶段 - 支持服务配置](migrate-from-ad-rms-phase3.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]