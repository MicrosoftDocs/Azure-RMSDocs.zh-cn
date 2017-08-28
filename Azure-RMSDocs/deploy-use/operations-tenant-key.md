---
title: "Azure 信息保护租户密钥的操作"
description: "确定对 Azure 信息保护租户密钥具有的不同级别控制权和责任。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/19/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 75225e3a49b671449ee0f1d5fafd47de08660c41
ms.sourcegitcommit: 0fa5dd38c9d66ee2ecb47dfdc9f2add12731485e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2017
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Azure 信息保护租户密钥的操作

>*适用于：Azure 信息保护、Office 365*

实现 Azure 信息保护租户密钥之后，你可对该密钥进行不同级别的控制并承担相应责任，具体取决于你的租户密钥拓扑（由 Microsoft 管理或由客户管理）。

这种在 Azure 密钥保管库中自行管理租户密钥的方式通常称为“自带密钥”(BYOK)。 有关此方案以及如何在两种租户密钥拓扑之间进行选择的详细信息，请参阅[计划和实现你的 Azure Rights Management 租户密钥](../plan-design/plan-implement-tenant-key.md)。

下表介绍了你可以执行的操作，具体取决于你为 Azure 信息保护租户密钥选择的拓扑。

|生命周期操作|由 Microsoft 管理（默认）|由客户管理 (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|撤消你的租户密钥|否（自动）|是|
|重新生成租户密钥|是|是|
|备份和恢复你的租户密钥|否|是|
|导出你的租户密钥|是|否|
|对违规行为做出响应|是|是|

确定实施了哪一种拓扑之后，请选择以下任一部分，获取有关 Azure 信息保护租户密钥的这些操作的详细信息：

- [Microsoft 托管的租户密钥](operations-microsoft-managed-tenant-key.md)
- [客户托管的租户密钥](operations-customer-managed-tenant-key.md)

但是，如果要通过从 Active Directory Rights Management Services 导入受信任的发布域 (TPD) 来创建 Azure 信息保护租户密钥，则执行此导入操作作为[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)的一部分。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
