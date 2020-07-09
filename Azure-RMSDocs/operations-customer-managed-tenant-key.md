---
title: 客户托管 - AIP 租户密钥生命周期操作
description: 当你自己管理 Azure 信息保护租户密钥（自带密钥方案，简称 BYOK）时的生命周期操作相关信息。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 12/06/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 14b3c9d4db202abb18555eb695fe7e3e0769af40
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136320"
---
# <a name="customer-managed-tenant-key-life-cycle-operations"></a>客户托管：租户密钥生命周期操作

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

如果你自己管理 Azure 信息保护租户密钥（自带密钥方案，简称 BYOK），请阅读以下部分，详细了解此拓扑相关的生命周期操作。

## <a name="revoke-your-tenant-key"></a>撤消你的租户密钥

在极少数情况下，可能需要吊销密钥，而不是重新生成密钥。 撤消密钥时，除非你有可以还原的密钥的备份，否则使用该密钥的租户所保护的所有内容将无法访问（包括 Microsoft、全局管理员和超级用户）。 撤消密钥后，你将无法保护新内容，直到你为 Azure 信息保护创建和配置新的租户密钥。 

若要吊销客户托管的租户密钥，请在 Azure Key Vault 中更改包含 Azure 信息保护租户密钥的密钥保管库的权限，使 Azure Rights Management 服务无法再访问该密钥。 此操作可以有效地吊销 Azure 信息保护的租户密钥。

取消 Azure 信息保护订阅时，Azure 信息保护会停止使用租户密钥，用户无需执行任何操作。

## <a name="rekey-your-tenant-key"></a>重新生成租户密钥
重新生成密钥也称为滚动密钥。 执行此操作时，Azure 信息保护会停止使用现有租户密钥保护文档和电子邮件，而开始使用其他密钥。 策略和模板将立即进行重新签名，但对于使用 Azure 信息保护的现有客户端和服务，此转换将逐渐完成。 因此在一段时间内，有些新内容继续使用旧租户密钥进行保护。

要重新生成密钥，必须配置租户密钥对象并指定要使用的备用密钥。 然后，以前使用的密钥将自动为 Azure 信息保护 标记为“已存档”。 此配置可确保通过使用此密钥进行保护的内容仍可访问。

可能需要重新生成 Azure 信息保护密钥的情况示例：

- 你的公司拆分为两家或更多公司。 在重新生成租户密钥时，新公司将无法访问员工发布的新内容。 如果有旧租户密钥的副本，他们可以访问旧内容。

- 想从一个密钥管理拓扑移动到另一个拓扑。 

- 你认为租户密钥的主控副本（你掌握的副本）已泄露。

若要将密钥重新生成为所管理的其他密钥，可在 Azure Key Vault 中创建新的密钥，或使用 Azure Key Vault 中已有的其他密钥。 然后按照为 Azure 信息保护实现 BYOK 的相同过程进行操作。 

1. 仅当新密钥与你已用于 Azure 信息保护的密钥保管库位于不同的密钥保管库中时：通过使用[AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy) Cmdlet 将 Azure 信息保护授权为使用密钥保管库。

2. 如果 Azure 信息保护尚未知道要使用的密钥，请运行[AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) cmdlet。

3. 使用运行[AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) cmdlet 配置租户密钥对象。

关于每个步骤的详细信息：

- 若要将密钥重新生成为所管理的其他密钥，请参阅[为 Azure 信息保护租户密钥实现 BYOK](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key)。
    
    如果你重新生成在本地创建的受 HSM 保护的密钥并传输到密钥保管库，则可以使用与当前密钥相同的安全环境和访问卡。

- 若要重新生成改为由 Microsoft 为你管理的密钥，请参阅 Microsoft 托管操作的[重新生成租户密钥](operations-microsoft-managed-tenant-key.md#rekey-your-tenant-key)部分。

## <a name="backup-and-recover-your-tenant-key"></a>备份和恢复你的租户密钥
由于是你本人管理自己的租户密钥，因此你需负责备份 Azure 信息保护使用的密钥。 

如果在本地生成租户密钥，请在 nCipher HSM：若要备份密钥，请备份标记化密钥文件、世界文件和管理员卡。 将密钥传送到 Azure Key Vault 时，该服务将保存已标记化的密钥文件，以防出现任何服务节点故障。 将此文件绑定到特定 Azure 区域或实例的安全体系。 但是，不要将此标记化密钥文件作为完全备份。 例如，如果你需要密钥的明文副本在 nCipher HSM 外部使用，Azure Key Vault 无法为你检索该副本，因为它仅有不可恢复的副本。

Azure Key Vault 具有一个[备份 cmdlet](/powershell/module/az.keyvault/backup-azkeyvaultkey)，可通过将其下载并存储到一个文件中来备份密钥。 由于下载的内容已加密，因此它不能在 Azure Key Vault 外使用。 

## <a name="export-your-tenant-key"></a>导出你的租户密钥
如果使用 BYOK，则你无法从 Azure 密钥保管库或 Azure 信息保护导出租户密钥。 Azure 密钥保管库中的副本是不可恢复的。 

## <a name="respond-to-a-breach"></a>对违规行为做出响应
如果没有违规响应流程，无论如何强大的安全系统都是不完整的。 你的租户密钥可能泄漏或失窃。 即便它得到了很好的保护，在当前这代密钥技术或当前的密钥长度和算法方面也可以找到一些漏洞。

Microsoft 拥有一个专业团队，负责响应其产品和服务中的安全事件。 当收到某个事件的可信报告时，该团队将参与调查事件的范围、根本原因和缓解办法。 如果此事件影响到资产，Microsoft 将通过电子邮件通知你的租户全局管理员。

如果你发现了安全违规行为，则你或 Microsoft 能够采取的最佳行动取决于安全违规的范围；Microsoft 将与你共同完成这个过程。 下表显示了一些典型情况以及可能的响应，但具体的响应要取决于在调查过程中揭示的所有信息。

|事件描述|可能的响应|
|------------------------|-------------------|
|你的租户密钥泄露。|重新生成租户密钥。 请参阅重新[生成租户密钥](#rekey-your-tenant-key)。|
|未经授权的个人或恶意软件获取了使用你的租户密钥的权限，但密钥本身并未泄露。|重新生成租户密钥在这种情况下并不奏效，需要进行根源分析。 如果进程或软件 Bug 是导致未经授权的个人获得访问权限的原因，则必须解决这一问题。|
|在当前这代 HSM 技术中发现的漏洞。|Microsoft 必须更新 HSM。 如果有理由认为这些漏洞泄露了密钥，Microsoft 将指示所有客户重新生成他们的租户密钥。|
|在 RSA 算法、密钥长度或暴力攻击方面发现的漏洞可能被利用。|Microsoft 必须更新 Azure 密钥保管库或 Azure 信息保护以支持新的算法和具有弹性的更长密钥长度，并指示所有客户重新生成他们的租户密钥。|
