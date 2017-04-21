---
title: "从 AD RMS 迁移到 Azure 信息保护 - 第 3 阶段"
description: "从 AD RMS 迁移到 Azure 信息保护的第 3 阶段涉及从 AD RMS 迁移到 Azure 信息保护中的步骤 7。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0f339e66bbbdaf45e15b6b820d3f56d5385083a1
ms.sourcegitcommit: 384461f0e3fccd73cd7eda3229b02e51099538d4
translationtype: HT
---
# <a name="migration-phase-3---client-side-configuration"></a>迁移第 3 阶段 - 客户端配置

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*

使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的阶段 3。 这些过程涉及了[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)中的步骤 7。

如果无法同时迁移所有客户端，请分批对客户端运行以下过程。 对于批次中具有要迁移的 Windows 计算机的每个用户，将用户添加到之前创建的 **AIPMigrated** 组。

## <a name="step-7-reconfigure-clients-to-use-azure-information-protection"></a>步骤 7. 重新配置客户端以使用 Azure 信息保护

此步骤使用迁移脚本重新配置 AD RMS 客户端。 这些脚本将重置 Windows 计算机上的配置，以使其将使用 Azure Rights Management 服务而不是 AD RMS： 

**CleanUpRMS.cmd**：

- 删除所有文件夹的内容和 AD RMS 客户端用于存储其配置的注册表项。 此信息包括客户端的 AD RMS 群集的位置。

**MigrateClient.cmd**：

- 配置客户端，以为 Azure Rights Management 服务初始化用户环境（即启动）。

-  配置客户端以连接到 Azure Rights Management 服务，以便获取 AD RMS 群集保护的内容的使用授权。 


### <a name="client-reconfiguration-by-using-registry-edits"></a>使用注册表编辑重新配置客户端

1. 返回到之前提取的迁移脚本，**CleanUpRMS.cmd** 和 **MigrateClient.cmd**。

2.  按照 **MigrateClient.cmd** 中的说明修改脚本，以便它包含租户的 Azure Rights Management 服务 URL，以及 AD RMS 群集 Extranet 授权 URL 和 Intranet 授权 URL 的服务器名称。

    > [!IMPORTANT]
    > 仍然注意，不要在地址前后引入多余空格。
    > 
    > 此外，如果 AD RMS 服务器使用 SSL/TLS 服务器证书，请检查字符串中许可 URL 值是否包括端口号 **443**。 例如：https:// rms.treyresearch.net:443/_wmcs/licensing。 单击群集名称并查看“群集详细信息”时，Active Directory Rights Management Services 中会显示此信息。 如果端口号 443 包含在此 URL 中，修改脚本时请将该值包括在内。 例如，https://rms.treyresearch.net:**443**。 

    如果需要针对 &lt;YourTenantURL&gt; 检索 Azure Rights Management 服务 URL ，请重新参考[确定 Azure Rights Management 服务 URL](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url)。

3.  在 **AIPMigrated** 组的成员所使用的客户端计算机上依次运行 **CleanUpRMS.cmd** 和 **MigrateClient.cmd**。 例如，创建运行这些脚本的组策略对象并将其分配给此用户组。


## <a name="next-steps"></a>后续步骤
若要继续迁移，请转到[第 4 阶段 - 支持服务配置](migrate-from-ad-rms-phase3.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]