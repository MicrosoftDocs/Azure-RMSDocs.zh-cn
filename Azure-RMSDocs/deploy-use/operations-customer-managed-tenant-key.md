---
title: "客户托管 - 租户密钥生命周期操作 | Azure RMS"
description: "有关当你自己管理 Azure Rights Management 租户密钥（自带密钥方案，简称 BYOK）时相关生命周期操作的信息。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: d3a798f14805fd8ff8377013120a33ae3642bfc3


---


# 客户托管：租户密钥生命周期操作

>*适用于：Azure Rights Management、Office 365*

如果你自己管理 Azure Rights Management 租户密钥（自带密钥方案，简称 BYOK），请阅读以下部分，获取有关此拓扑的相关生命周期操作的详细信息。

## 撤消你的租户密钥
在 Azure 密钥保管库中，可以更改密钥保管库的权限，包括 Azure RMS 租户密钥，使 Azure RMS 不再能够访问该密钥。 但是，执行此操作时，任何人都将无法打开之前使用 Azure RMS 保护的文档和电子邮件。

当你取消订阅 Azure RMS 时，Azure RMS 将停止使用你的租户密钥，无需你执行任何操作。


## 更新你的租户密钥
更新密钥也称为滚动密钥。 不要更新你的租户密钥，除非在真正必要的情况下。 旧版客户端（例如 Office 2010）无法适当处理密钥更改。 在这种情况下，你必须通过使用组策略或同等机制，清除计算机上的 RMS 状态。 但是，某些法律事件可能迫使你更新租户密钥。 例如：

-   你的公司拆分为两家或更多公司。 当你更新你的租户密钥时，新公司将无法访问你的员工发布的新内容。 如果有旧租户密钥的副本，他们可以访问旧内容。

-   你认为租户密钥的主副本（你掌握的副本）已泄漏。

当你更新租户密钥时，新内容将使用新租户密钥来保护。 这个过程是分阶段进行的，因此在一段时间内，有些新内容仍将使用旧租户密钥来保护。 以前受到保护的内容仍将使用旧租户密钥来保护。 为了支持此种方案，Azure RMS 保留你的旧密钥，使得它能够发布旧内容的许可证。

若要更新租户密钥，请先在密钥保管库中更新 Azure RMS 租户密钥。 然后再次运行 Add-AadrmKeyVaultKey cmdlet，指定新的密钥 URL。

## 备份和恢复你的租户密钥
你负责备份自己的租户密钥。 如果你在 Thales HSM 中生成租户密钥，若要备份该密钥，只需备份标记化密钥文件、安全体系文件和管理员卡即可。

因为你按照[计划和实现你的 Azure Rights Management 租户密钥](../plan-design/plan-implement-tenant-key.md)文章中的[实现自带密钥 (BYOK)](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) 部分中的程序传送密钥，因此密钥保管库将保留标记化密钥文件，以防止任何服务节点发生故障。 将此文件绑定到特定 Azure 区域或实例的安全体系。 但是，不要将它作为完全备份。 例如，如果你需要密钥的明文副本在 Thales HSM 外部使用，则 Azure 密钥保管库将无法为你检索该副本，因为它仅有不可恢复的副本。

## 导出你的租户密钥
如果使用 BYOK，则你无法从 Azure 密钥保管库或 Azure RMS 导出租户密钥。 Azure 密钥保管库中的副本是不可恢复的。 

## 对违规行为做出响应
如果没有违规响应流程，无论如何强大的安全系统都是不完整的。 你的租户密钥可能泄漏或失窃。 即便它得到了很好的保护，在当前这代的 HSM 技术或当前的密钥长度和算法方面也可以找到一些漏洞。

Microsoft 拥有一个专业团队，负责响应其产品和服务中的安全事件。 当收到某个事件的可信报告时，该团队将参与调查事件的范围、根本原因和缓解办法。 如果该事件影响到你的资产，则 Microsoft 将使用你在订阅时提供的地址，通过电子邮件通知你的 Azure RMS 租户管理员。

如果你发现了安全违规行为，你或 Microsoft 能够采取的最佳行动取决于安全违规的范围；Microsoft 将与你共同完成这个过程。 下表显示了一些典型情况以及可能的响应，但具体的响应要取决于在调查过程中揭示的所有信息。

|事件描述|可能的响应|
|------------------------|-------------------|
|你的租户密钥泄露。|更新你的租户密钥。 请参阅[更新你的租户密钥](#re-key-your-tenant-key)。|
|未经授权的个人或恶意软件获取了使用你的租户密钥的权限，但密钥本身并未泄露。|更新你的租户密钥在这种情况下并不奏效，需要进行根源分析。 如果进程或软件 Bug 是导致未经授权的个人获得访问权限的原因，则必须解决这一问题。|
|在当前这代 HSM 技术中发现的漏洞。|Microsoft 必须更新 HSM。 如果有理由认为这些漏洞泄露了密钥，则 Microsoft 将指示所有客户更新他们的租户密钥。|
|在 RSA 算法、密钥长度或暴力攻击方面发现的漏洞可能被利用。|Microsoft 必须更新 Azure 密钥保管库或 Azure RMS，以支持新的算法和具有弹性的更长密钥长度，并指示所有客户更新他们的租户密钥。|





<!--HONumber=Aug16_HO4-->


