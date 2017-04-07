---
title: "迁移 AD RMS-Azure 信息保护 - 第 4 阶段"
description: "从 AD RMS 迁移到 Azure 信息保护的第 4 阶段包括从 AD RMS 迁移到 Azure 信息保护的步骤 8 至 9"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d36f47e586ac1295dcc79e43a9e061b4c7c7fe1e
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="migration-phase-4---post-migration-tasks"></a>迁移阶段 4 - 迁移后任务

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*


使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的第 4 阶段。 这些过程包括[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的步骤 8-9。


## <a name="step-8-decommission-ad-rms"></a>步骤 8. 解除 AD RMS 的授权

从 Active Directory 中删除服务连接点 (SCP) 以防止计算机发现你的本地权限管理基础结构。 由于在注册表中配置了重定向（例如，通过运行迁移脚本），此步骤对于已迁移的现有客户端是可选的。 但是，删除 SCP 会阻止新的客户端以及可能与 RMS 相关的服务和工具在迁移完毕后查找 SCP，并且所有连接都应转到 Azure 权限管理服务。 

若要删除 SCP，请确保你已经以域企业管理员身份登录，然后使用以下过程：

1. 在 Active Directory Rights Management Services 控制台中，右键单击 AD RMS 群集，然后单击“属性”。

2. 单击“SCP”选项卡  。

3. 选中“更改 SCP”复选框  。

4. 选择“删除当前 SCP”，然后单击“确定”。

监视 AD RMS 服务器的活动，例如，通过检查[系统运行状况报告中的请求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest 表](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)，或者[审核用户对受保护内容的访问权限](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)。 当确认 RMS 客户端不再与这些服务器进行通信，并且客户端成功使用 Azure 信息保护时，可以从这些服务器中删除 AD RMS 服务器角色。 当调查为什么客户端未使用 Azure 信息保护时，如果使用的是专用服务器，可能采取警示性步骤，即先关闭服务器一段时间，以确保没有报告可能需要重启这些服务器以保证服务连续性的问题。

解除 AD RMS 服务器的授权后，你可能想要利用此机会来查看你在 Azure 经典门户中的模板并将其合并以使用户有较少的选项，或重新配置它们，或者甚至添加新模板。 这还将是发布默认模板的好时机。 有关详细信息，请参阅[为 Azure Rights Management 服务配置自定义模板](../deploy-use/configure-custom-templates.md)。

## <a name="step-9-re-key-your-azure-information-protection-tenant-key"></a>步骤 9. 更新 Azure 信息保护租户密钥
迁移完成时，如果 AD RMS 部署使用的是 RMS 加密模式 1，则此步骤是必需的，因为重新键入将创建使用 RMS 加密模式 2 的新租户密钥。 将 Azure RMS 与加密模式 1 配合使用仅在迁移过程中受支持。

即使在 RMS 加密模式 2 中运行，也建议在迁移完成后，执行此步骤（此步骤是可选的）。 在此情况下更新密钥有助于保护 Azure 信息保护租户密钥免受 AD RMS 密钥的潜在安全漏洞的影响。

更新 Azure 信息保护租户密钥（也称为“滚动密钥”）时，将创建新的密钥，并将原始密钥存档。 但是，由于将一个密钥更改为另一个密钥的操作不会立即完成，而是需要几周的时间，因此应在迁移完成时，立即更新 Azure 信息保护租户密钥，而不要等到怀疑原始密钥受到破坏时再更新。

更新 Azure 信息保护租户密钥：

- 如果租户密钥由 Microsoft 管理：请联系 [Microsoft 支持部门](../get-started/information-support.md#to-contact-microsoft-support)，并打开**带有从 AD RMS 迁移后更新 Azure 信息保护密钥请求的 Azure 信息保护支持案例**。 必须证明你是 Azure 信息保护租户的管理员，并且了解确认此过程需要几天时间。 收取标准支持费用：重新键入租户密钥并不是免费支持服务。

- 如果租户密钥由你管理 (BYOK)：在 Azure Key Vault 中，重新键入用于 Azure 信息保护租户的密钥，然后再次运行 [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) cmdlet 以指定新密钥 URL。 

## <a name="next-steps"></a>后续步骤

有关管理 Azure 信息保护租户密钥的详细信息，请参阅[针对 Azure Rights Management 租户密钥的操作](../deploy-use/operations-tenant-key.md)。

完成迁移后，请检查[部署路线图](deployment-roadmap.md)以确定是否需要执行其他任何部署任务。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
