---
title: "从 AD RMS 迁移到 Azure 信息保护 - 第 5 阶段"
description: "从 AD RMS 迁移到 Azure 信息保护的第 5 阶段包括从 AD RMS 迁移到 Azure 信息保护的步骤 10 至 12。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/24/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 11775c64cbd5abd7c10a145a2d48f335db2d5b69
ms.sourcegitcommit: 8251e4db274519a2eb8033d3135a22c27130bd30
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2017
---
# <a name="migration-phase-5---post-migration-tasks"></a>迁移第 5 阶段- 迁移后任务

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*


使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的第 5 阶段。 这些过程包括[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的步骤 10-12。

## <a name="step-10-deprovision-ad-rms"></a>步骤 10： 取消预配 AD RMS

从 Active Directory 中删除服务连接点 (SCP) 以防止计算机发现你的本地权限管理基础结构。 由于在注册表中配置了重定向（例如，通过运行迁移脚本），此步骤对于已迁移的现有客户端是可选的。 但是，删除 SCP 会阻止新的客户端以及可能与 RMS 相关的服务和工具在迁移完毕后查找 SCP。 此时，所有计算机连接都应转到 Azure Rights Management 服务。 

若要删除 SCP，请确保你已经以域企业管理员身份登录，然后使用以下过程：

1. 在 Active Directory Rights Management Services 控制台中，右键单击 AD RMS 群集，然后单击“属性”。

2. 单击“SCP”选项卡  。

3. 选中“更改 SCP”复选框  。

4. 选择“删除当前 SCP”，然后单击“确定”。

现在监视 AD RMS 服务器的活动。 例如，检查[系统运行状况报告中的请求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest 表](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)，或者[审核用户对受保护内容的访问权限](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)。 

当确认 RMS 客户端不再与这些服务器进行通信，并且客户端成功使用 Azure 信息保护时，可以从这些服务器中删除 AD RMS 服务器角色。 如果使用的是专用服务器，则可首选完成警告的步骤，即先关闭服务器一段时间。 这样则可以在这段时间确保在调查客户端未使用 Azure 信息保护的原因时没有报告要求你重启这些服务器以保证服务连续性的问题。

取消预配 AD RMS 服务器后，此时需要在 Azure 门户中检查模板。 例如，将其转换为标签，将其合并以便减少可供用户选择的数量，或重新配置它们。 这还将是发布默认模板的好时机。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](../deploy-use/configure-policy-templates.md)。

>[!IMPORTANT]
> 此迁移结束时，AD RMS 群集不能与 Azure 信息保护和自控密钥 (HYOK) 选项结合使用。 如果决定要对 Azure 信息保护标签使用 HYOK，由于重定向现均已到位，因此所用 AD RMS 群集中的授权 URL 必须与已迁移群集中的授权 URL 不同。

## <a name="step-11-remove-onboarding-controls"></a>步骤 11： 删除载入控件

现有客户端均已迁移到 Azure 信息保护后，便没有理由继续使用载入控件并保留针对迁移过程创建的 **AIPMigrated** 组了。 

首先删除载入控件，然后才能删除 AIPMigrated 组和为了部署重定向而创建的任何软件部署任务。

删除载入控件：

1. 在 PowerShell 会话中，请连接到 Azure Rights Management 服务，并在出现提示时，指定全局管理员凭据：

        Connect-Aadrmservice

2. 运行以下命令，并输入 **Y** 进行确认：

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False

3. 确认不再设置载入控件：

        Get-AadrmOnboardingControlPolicy

    在输出中，**授权**应显示 **False**，并且对于 **SecurityGroupOjbectId** 未显示任何 GUID

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>步骤 12： 重新生成 Azure 信息保护租户密钥

如果 AD RMS 部署使用 RMS 加密模式 1，则迁移完成后建议执行此步骤。 重新生成密钥将生成保护，该保护使用 RMS 加密模式 2。 

虽然 AD RMS 部署使用加密模式 2，但仍建议执行此步骤，因为新密钥有助于保护租户避免 AD RMS 密钥的潜在安全漏洞。

但是，如果将 Exchange Online 和 AD RMS 配合使用，请勿重新生成密钥。 Exchange Online 不支持更改加密模式。 

重新生成 Azure 信息保护租户密钥（也称为“滚动密钥”）时，当前活动密钥将存档，Azure 信息保护开始使用指定的其他密钥。 这个其他密钥可以是你在 Azure Key Vault 中创建的新密钥，也可以是为租户自动创建的默认密钥。

从一个密钥更改到另一个密钥的操作不会立即完成，而是需要几周的时间。 由于不是立即完成，因此在迁移完成后，请立即执行此步骤，而不要等到怀疑原始密钥受到破坏时才进行操作。

重新生成 Azure 信息保护租户密钥：

- 如果租户密钥由 Microsoft 托管：请运行 PowerShell cmdlet [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)，然后为针对租户自动创建的密钥指定密钥标识符。 通过运行 [Get-AadrmKeys](/powershell/module/aadrm/get-aadrmkeys) cmdlet 可标识要指定的值。 为租户自动创建的密钥包含最早创建日期，因此可以使用以下命令对其进行标识：
    
        (Get-AadrmKeys) | Sort-Object CreationTime | Select-Object -First 1

- 如果租户密钥由你管理 (BYOK)：在 Azure Key Vault 中，为 Azure 信息保护租户重复密钥创建流程，然后再次运行 [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) cmdlet 以指定新密钥的 URI。 

有关管理 Azure 信息保护租户密钥的详细信息，请参阅[针对 Azure Rights Management 租户密钥的操作](../deploy-use/operations-tenant-key.md)。


## <a name="next-steps"></a>后续步骤

完成迁移后，请检查[部署路线图](deployment-roadmap.md)以确定是否需要执行其他任何部署任务。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
