---
title: 从 AD RMS 迁移到 Azure 信息保护 - 第 5 阶段
description: 从 AD RMS 迁移到 Azure 信息保护的第 5 阶段包括从 AD RMS 迁移到 Azure 信息保护的步骤 10 至 12。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: bf2675aa43e2c15761fdd46b94e3bb19253cadc3
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67522068"
---
# <a name="migration-phase-5---post-migration-tasks"></a>迁移第 5 阶段- 迁移后任务

>适用范围：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的第 5 阶段。 这些过程包括[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的步骤 10-12。

## <a name="step-10-deprovision-ad-rms"></a>步骤 10： 取消预配 AD RMS

从 Active Directory 中删除服务连接点 (SCP) 以防止计算机发现你的本地权限管理基础结构。 由于在注册表中配置了重定向（例如，通过运行迁移脚本），此步骤对于已迁移的现有客户端是可选的。 但是，删除 SCP 会阻止新的客户端以及可能与 RMS 相关的服务和工具在迁移完毕后查找 SCP。 此时，所有计算机连接都应转到 Azure Rights Management 服务。 

若要删除 SCP，请确保你已经以域企业管理员身份登录，然后使用以下过程：

1. 在 Active Directory Rights Management Services 控制台中，右键单击 AD RMS 群集，然后单击“属性”  。

2. 单击“SCP”选项卡  。

3. 选中“更改 SCP”复选框  。

4. 选择“删除当前 SCP”  ，然后单击“确定”  。

现在监视 AD RMS 服务器的活动。 例如，检查[系统运行状况报告中的请求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest 表](https://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)，或者[审核用户对受保护内容的访问权限](https://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)。 

当确认 RMS 客户端不再与这些服务器进行通信，并且客户端成功使用 Azure 信息保护时，可以从这些服务器中删除 AD RMS 服务器角色。 如果使用的是专用服务器，则可首选完成警告的步骤，即先关闭服务器一段时间。 这样则可以在这段时间确保在调查客户端未使用 Azure 信息保护的原因时没有报告要求你重启这些服务器以保证服务连续性的问题。

取消预配 AD RMS 服务器后，此时需要在 Azure 门户中检查模板。 例如，将其转换为标签，将其合并以便减少可供用户选择的数量，或重新配置它们。 这还将是发布默认模板的好时机。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](./configure-policy-templates.md)。

>[!IMPORTANT]
> 此迁移结束时，AD RMS 群集不能与 Azure 信息保护和自控密钥 (HYOK) 选项结合使用。 如果决定要对 Azure 信息保护标签使用 HYOK，由于重定向现均已到位，因此所用 AD RMS 群集中的授权 URL 必须与已迁移群集中的授权 URL 不同。

### <a name="addition-configuration-for-computers-that-run-office-2010"></a>运行 Office 2010 的计算机的其他配置

如果迁移运行 Office 2010 的客户端，用户可能会遇到延迟在我们的 AD RMS 服务器取消预配后打开受保护的内容。 或者，用户可能会看到，没有凭据才能打开受保护的内容的消息。 若要解决这些问题，创建的网络重定向为这些计算机，将 AD RMS URL FQDN 重定向到的本地 IP 地址 (127.0.0.1) 的计算机。 通过配置每台计算机上的本地 hosts 文件或通过使用 DNS，你可以执行此操作。

通过本地主机文件的重定向：

- 在本地主机文件中，添加以下行替换为`<AD RMS URL FQDN>`与你的 AD RMS 群集，而无需前缀或网页的值：
    
        127.0.0.1 <AD RMS URL FQDN>

通过 DNS 重定向：
    
- 为 AD RMS URL FQDN，它具有 IP 地址 127.0.0.1 创建新的主机 (A) 记录。

## <a name="step-11-complete-client-migration-tasks"></a>步骤 11： 完成客户端迁移任务

对于移动设备客户端和 Mac 计算机：删除在部署 [AD RMS 移动设备扩展](https://technet.microsoft.com/library/dn673574.aspx)时创建的 DNS SRV 记录。

当这些 DNS 更改得到传播时，这些客户端会自动发现并开始使用 Azure Rights Management 服务。 但运行 Office Mac 的 Mac 计算机会缓存 AD RMS 中的信息。 这些计算机执行此过程最多可能需要 30 天。 

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

所有现有 Windows 计算机均已迁移到 Azure 信息保护后，便没有理由继续使用载入控件并保留针对迁移过程创建的 AIPMigrated  组了。 

首先删除载入控件，然后才能删除 AIPMigrated  组和为了部署迁移脚本而创建的任何软件部署方法。

删除载入控件：

1. 在 PowerShell 会话中，请连接到 Azure Rights Management 服务，并在出现提示时，指定全局管理员凭据：

        Connect-AipService

2. 运行以下命令，并输入 **Y** 进行确认：

        Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
    
    请注意，此命令会删除所有针对 Azure Rights Management 保护服务的许可证强制执行，使所有计算机都可保护文档和电子邮件。

3. 确认不再设置载入控件：

        Get-AipServiceOnboardingControlPolicy

    在输出中，**授权**应显示 **False**，并且对于 **SecurityGroupOjbectId** 未显示任何 GUID

最后，如果使用的是 Office 2010 且已在 Windows 任务计划程序库中启用了“AD RMS 权限策略模板管理（自动）”任务，请禁用此任务，因为它不用于 Azure 信息保护客户端  。 此任务通常是使用组策略启用的，它支持 AD RMS 部署。 可以在以下位置找到此任务：“Microsoft” > “Windows” > “Active Directory Rights Management Services 客户端”   

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>步骤 12： 重新生成 Azure 信息保护租户密钥

如果你的 AD RMS 部署正在使用 RMS 加密模式 1，因为此模式下使用 1024年位的密钥和 sha-1 完成迁移后时，此步骤是必需的。 此配置被视为提供了不充分的保护级别。 Microsoft 不赞同将较低的密钥长度，例如 1024年位 RSA 密钥的使用和关联的产品/服务的保护措施，如 sha-1 不足级别的协议。

重新生成密钥保护使用 RMS 加密模式 2 中的结果，这会产生 2048年位密钥和 SHA-256。 

虽然 AD RMS 部署使用加密模式 2，但仍建议执行此步骤，因为新密钥有助于保护租户避免 AD RMS 密钥的潜在安全漏洞。

重新生成 Azure 信息保护租户密钥（也称为“滚动密钥”）时，当前活动密钥将存档，Azure 信息保护开始使用指定的其他密钥。 这个其他密钥可以是你在 Azure Key Vault 中创建的新密钥，也可以是为租户自动创建的默认密钥。

从一个密钥更改到另一个密钥的操作不会立即完成，而是需要几周的时间。 由于不是立即完成，因此在迁移完成后，请立即执行此步骤，而不要等到怀疑原始密钥受到破坏时才进行操作。

重新生成 Azure 信息保护租户密钥：

- **如果租户密钥由 Microsoft 托管**：运行 PowerShell cmdlet[集 AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)并指定为你的租户自动创建的密钥的密钥标识符。 可以标识要通过运行指定的值[Get AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) cmdlet。 为租户自动创建的密钥包含最早创建日期，因此可以使用以下命令对其进行标识：
    
        (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1

- **如果租户密钥由你管理 (BYOK)** ：在 Azure 密钥保管库，为 Azure 信息保护租户重复密钥创建流程，然后再运行[使用 AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) cmdlet 再次来指定此新密钥的 URI。 

若要详细了解如何管理 Azure 信息保护租户密钥，请参阅 [Azure 信息保护租户密钥操作](./operations-tenant-key.md)。


## <a name="next-steps"></a>后续步骤

完成迁移后，请检查[部署路线图](deployment-roadmap.md)以确定是否需要执行其他任何部署任务。

