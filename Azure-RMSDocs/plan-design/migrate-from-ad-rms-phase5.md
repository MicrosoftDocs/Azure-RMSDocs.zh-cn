---
title: "从 AD RMS 迁移到 Azure 信息保护 - 第 5 阶段"
description: "从 AD RMS 迁移到 Azure 信息保护的第 5 阶段包括从 AD RMS 迁移到 Azure 信息保护的步骤 10 至 12。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e07e9252837fe17c84ce17c3b1fc8e20734190fd
ms.sourcegitcommit: 237ce3a0cc4921da5a08ed5753e6491403298194
translationtype: HT
---
# <a name="migration-phase-5---post-migration-tasks"></a>迁移第 5 阶段- 迁移后任务

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*


使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的第 5 阶段。 这些过程包括[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的步骤 10-12。

## <a name="step-10-deprovison-ad-rms"></a>步骤 10： 取消预配 AD RMS

从 Active Directory 中删除服务连接点 (SCP) 以防止计算机发现你的本地权限管理基础结构。 由于在注册表中配置了重定向（例如，通过运行迁移脚本），此步骤对于已迁移的现有客户端是可选的。 但是，删除 SCP 会阻止新的客户端以及可能与 RMS 相关的服务和工具在迁移完毕后查找 SCP，并且所有连接都应转到 Azure 权限管理服务。 

若要删除 SCP，请确保你已经以域企业管理员身份登录，然后使用以下过程：

1. 在 Active Directory Rights Management Services 控制台中，右键单击 AD RMS 群集，然后单击“属性”。

2. 单击“SCP”选项卡  。

3. 选中“更改 SCP”复选框  。

4. 选择“删除当前 SCP”，然后单击“确定”。

现在监视 AD RMS 服务器的活动，例如，通过检查[系统运行状况报告中的请求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest 表](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)，或者[审核用户对受保护内容的访问权限](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)。 

当确认 RMS 客户端不再与这些服务器进行通信，并且客户端成功使用 Azure 信息保护时，可以从这些服务器中删除 AD RMS 服务器角色。 当调查为什么客户端未使用 Azure 信息保护时，如果使用的是专用服务器，可能采取警示性步骤，即先关闭服务器一段时间，以确保没有报告可能需要重启这些服务器以保证服务连续性的问题。

取消预配 AD RMS 服务器后，建议利用此机会查看你在 Azure 经典门户中的模板并将其合并以使用户有较少的选项，或重新配置它们，或者甚至添加新模板。 这还将是发布默认模板的好时机。 有关详细信息，请参阅[为 Azure Rights Management 服务配置自定义模板](../deploy-use/configure-custom-templates.md)。

>[!IMPORTANT]
> 此迁移结束时，AD RMS 群集不能与 Azure 信息保护和自控密钥 (HYOK) 选项结合使用。 如果决定要对 Azure 信息保护标签使用 HYOK，由于重定向现均已到位，因此所用 AD RMS 群集中的授权 URL 必须与已迁移群集中的授权 URL 不同。

## <a name="step-11-remove-onboarding-controls"></a>步骤 11： 删除载入控件

现有客户端均已迁移到 Azure 信息保护后，便没有理由继续使用载入控件并保留针对迁移过程创建的 **AIPMigrated** 组了。 

首先删除载入控件，然后才能删除 **AIPMigrated** 组和为了部署目录而创建的任何软件部署。

删除载入控件：

1. 在 PowerShell 会话中，请连接到 Azure Rights Management 服务，并在出现提示时，指定全局管理员凭据：

        Connect-Aadrmservice

2. 运行以下命令，并输入 **Y** 进行确认：

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False

3. 确认不再设置载入控件：

        Get-AadrmOnboardingControlPolicy

    在输出中，**授权**应显示 **False**，并且对于 **SecurityGroupOjbectId** 未显示任何 GUID

## <a name="step-12-re-key-your-azure-information-protection-tenant-key"></a>步骤 12： 更新 Azure 信息保护租户密钥
迁移完成时，如果 AD RMS 部署使用的是 RMS 加密模式 1，则此步骤是必需的，因为重新键入将创建使用 RMS 加密模式 2 的新租户密钥。 将 Azure RMS 与加密模式 1 配合使用仅在迁移过程中受支持。

即使在 RMS 加密模式 2 中运行，也建议在迁移完成后，执行此步骤（此步骤是可选的）。 在此情况下更新密钥有助于保护 Azure 信息保护租户密钥免受 AD RMS 密钥的潜在安全漏洞的影响。

更新 Azure 信息保护租户密钥（也称为“滚动密钥”）时，将创建新的密钥，并将原始密钥存档。 但是，由于将一个密钥更改为另一个密钥的操作不会立即完成，而是需要几周的时间，因此应在迁移完成时，立即更新 Azure 信息保护租户密钥，而不要等到怀疑原始密钥受到破坏时再更新。

更新 Azure 信息保护租户密钥：

- 如果租户密钥由 Microsoft 管理：请联系 [Microsoft 支持部门](../get-started/information-support.md#to-contact-microsoft-support)，并打开**带有从 AD RMS 迁移后更新 Azure 信息保护密钥请求的 Azure 信息保护支持案例**。 必须证明你是 Azure 信息保护租户的管理员，并且了解确认此过程需要几天时间。 收取标准支持费用：重新键入租户密钥并不是免费支持服务。

- 如果租户密钥由你管理 (BYOK)：在 Azure Key Vault 中，重新键入用于 Azure 信息保护租户的密钥，然后再次运行 [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) cmdlet 以指定新密钥 URL。 

有关管理 Azure 信息保护租户密钥的详细信息，请参阅[针对 Azure Rights Management 租户密钥的操作](../deploy-use/operations-tenant-key.md)。

## <a name="next-steps"></a>后续步骤

完成迁移后，请检查[部署路线图](deployment-roadmap.md)以确定是否需要执行其他任何部署任务。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
