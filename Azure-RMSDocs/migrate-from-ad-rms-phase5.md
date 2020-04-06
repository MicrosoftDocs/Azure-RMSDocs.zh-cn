---
title: 从 AD RMS 迁移到 Azure 信息保护 - 第 5 阶段
description: 从 AD RMS 迁移到 Azure 信息保护的第 5 阶段包括从 AD RMS 迁移到 Azure 信息保护的步骤 10 至 12。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/02/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8efcf7554b7c701ca5dc4e1c90a72b1afd93c195
ms.sourcegitcommit: c0fd00b057d155d6f2ed3a3ef5942d593b5be5c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2020
ms.locfileid: "80670229"
---
# <a name="migration-phase-5---post-migration-tasks"></a>迁移第 5 阶段- 迁移后任务

>适用范围：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的第 5 阶段。 这些过程包括[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的步骤 10-12。

## <a name="step-10-deprovision-ad-rms"></a>步骤 10： 取消预配 AD RMS

从 Active Directory 中删除服务连接点 (SCP) 以防止计算机发现你的本地权限管理基础结构。 由于在注册表中配置了重定向（例如，通过运行迁移脚本），此步骤对于已迁移的现有客户端是可选的。 但是，删除 SCP 会阻止新的客户端以及可能与 RMS 相关的服务和工具在迁移完毕后查找 SCP。 此时，所有计算机连接都应转到 Azure Rights Management 服务。 

若要删除 SCP，请确保你已经以域企业管理员身份登录，然后使用以下过程：

1. 在 Active Directory Rights Management Services 控制台中，右键单击 AD RMS 群集，然后单击“属性”。

2. 单击“SCP”选项卡 。

3. 选中“更改 SCP”复选框 。

4. 选择“删除当前 SCP”，然后单击“确定”。

现在监视 AD RMS 服务器的活动。 例如，检查[系统运行状况报告中的请求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest 表](https://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)，或者[审核用户对受保护内容的访问权限](https://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)。 

当确认 RMS 客户端不再与这些服务器进行通信，并且客户端成功使用 Azure 信息保护时，可以从这些服务器中删除 AD RMS 服务器角色。 如果使用的是专用服务器，则可能更倾向于在一段时间内第一次关闭服务器的采取警告步骤。 这样则可以在这段时间确保在调查客户端未使用 Azure 信息保护的原因时没有报告要求你重启这些服务器以保证服务连续性的问题。

取消预配 AD RMS 服务器后，此时需要在 Azure 门户中检查模板。 例如，将其转换为标签，将其合并以便减少可供用户选择的数量，或重新配置它们。 这还将是发布默认模板的好时机。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](./configure-policy-templates.md)。

>[!IMPORTANT]
> 此迁移结束时，AD RMS 群集不能与 Azure 信息保护和自控密钥 (HYOK) 选项结合使用。 如果决定要对 Azure 信息保护标签使用 HYOK，由于重定向现均已到位，因此所用 AD RMS 群集中的授权 URL 必须与已迁移群集中的授权 URL 不同。

### <a name="addition-configuration-for-computers-that-run-office-2010"></a>运行 Office 2010 的计算机的添加配置

如果迁移的客户端运行的是 Office 2010，则在 AD RMS 服务器取消预配后，用户在打开受保护内容时可能会遇到延迟。 或者，用户可能会看到他们没有打开受保护内容的凭据的消息。 若要解决这些问题，请为这些计算机创建网络重定向，这会将 AD RMS URL FQDN 重定向到计算机的本地 IP 地址（127.0.0.1）。 可以通过在每台计算机上配置本地 hosts 文件或使用 DNS 来实现此目的。

通过本地主机文件重定向：

- 在本地 hosts 文件中添加以下行，将 `<AD RMS URL FQDN>` 替换为 AD RMS 群集的值，不含前缀或网页：
    
        127.0.0.1 <AD RMS URL FQDN>

通过 DNS 重定向：
    
- 为 AD RMS URL FQDN 创建新的主机（A）记录，其 IP 地址为127.0.0.1。

## <a name="step-11-complete-client-migration-tasks"></a>步骤 11： 完成客户端迁移任务

对于移动设备客户端和 Mac 计算机：删除在部署 [AD RMS 移动设备扩展](https://technet.microsoft.com/library/dn673574.aspx)时创建的 DNS SRV 记录。

当这些 DNS 更改传播后，这些客户端将自动发现并开始使用 Azure Rights Management 服务。 但运行 Office Mac 的 Mac 计算机会缓存 AD RMS 中的信息。 这些计算机执行此过程最多可能需要 30 天。 

若要强制 Mac 计算机立即在密钥链中运行发现过程，请搜索“adal”并删除所有 ADAL 条目。 然后在这些计算机上运行下列命令：

````

rm -r ~/Library/Cache/MSRightsManagement

rm -r ~/Library/Caches/com.microsoft.RMS-XPCService

rm -r ~/Library/Caches/Microsoft\ Rights\ Management\ Services

rm -r ~/Library/Containers/com.microsoft.RMS-XPCService

rm -r ~/Library/Containers/com.microsoft.RMSTestApp

rm ~/Library/Group\ Containers/UBF8T346G9.Office/DRM.plist

killall cfprefsd

````

所有现有 Windows 计算机均已迁移到 Azure 信息保护后，便没有理由继续使用载入控件并保留针对迁移过程创建的 AIPMigrated 组了。 

首先删除载入控件，然后才能删除 AIPMigrated 组和为了部署迁移脚本而创建的任何软件部署方法。

删除载入控件：

1. 在 PowerShell 会话中，请连接到 Azure Rights Management 服务，并在出现提示时，指定全局管理员凭据：

        Connect-AipService

2. 运行以下命令，并输入 **Y** 进行确认：

        Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
    
    请注意，此命令会删除所有针对 Azure Rights Management 保护服务的许可证强制执行，使所有计算机都可保护文档和电子邮件。

3. 确认不再设置载入控件：

        Get-AipServiceOnboardingControlPolicy

    在输出中，**授权**应显示 **False**，并且对于 **SecurityGroupOjbectId** 未显示任何 GUID

最后，如果使用的是 Office 2010 且已在 Windows 任务计划程序库中启用了“AD RMS 权限策略模板管理（自动）”任务，请禁用此任务，因为它不用于 Azure 信息保护客户端。 此任务通常是使用组策略启用的，它支持 AD RMS 部署。 可以在以下位置找到此任务：“Microsoft” > “Windows” > “Active Directory Rights Management Services 客户端”

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>步骤 12： 重新生成 Azure 信息保护租户密钥

如果 AD RMS 部署使用的是 RMS 加密模式1，则迁移完成时需要执行此步骤，因为此模式使用1024位密钥和 SHA-1。 此配置被视为提供不充分的保护级别。 Microsoft 不允许使用较小的密钥长度，例如1024位的 RSA 密钥，以及提供不充分保护级别的协议的关联用途，如 SHA-1。

重新生成密钥会导致使用 RMS 加密模式2的保护，这将导致2048位密钥和 SHA-256。 

虽然 AD RMS 部署使用加密模式 2，但仍建议执行此步骤，因为新密钥有助于保护租户避免 AD RMS 密钥的潜在安全漏洞。

重新生成 Azure 信息保护租户密钥（也称为“滚动密钥”）时，当前活动密钥将存档，Azure 信息保护开始使用指定的其他密钥。 这个其他密钥可以是你在 Azure Key Vault 中创建的新密钥，也可以是为租户自动创建的默认密钥。

从一个密钥移到另一个密钥并不会立即发生，而是经过几周。 由于不是立即完成，因此在迁移完成后，请立即执行此步骤，而不要等到怀疑原始密钥受到破坏时才进行操作。

重新生成 Azure 信息保护租户密钥：

- **如果租户密钥由 Microsoft 托管**：运行 PowerShell cmdlet [AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) ，并指定为你的租户自动创建的密钥的密钥标识符。 可以通过运行[AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) cmdlet 来确定要指定的值。 为租户自动创建的密钥包含最早创建日期，因此可以使用以下命令对其进行标识：
    
        (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1

- **如果租户密钥由你管理 (BYOK)** ：在 Azure Key Vault 中，为 Azure 信息保护租户重复密钥创建过程，然后再次运行[AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) cmdlet 以指定此新密钥的 URI。 

若要详细了解如何管理 Azure 信息保护租户密钥，请参阅 [Azure 信息保护租户密钥操作](./operations-tenant-key.md)。


## <a name="next-steps"></a>后续步骤

完成迁移后，请检查[部署路线图](deployment-roadmap.md)以确定是否需要执行其他任何部署任务。

