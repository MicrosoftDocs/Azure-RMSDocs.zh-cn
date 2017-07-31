---
title: "为 Azure RMS 和 AD RMS 准备环境"
description: "如果已部署 Azure Rights Management 和 AD RMS，请参阅本指南。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 577f91958c4b54c4fb023d973475c917b28f72b3
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2017
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>在已有 Active Directory Rights Management Services (AD RMS) 的情况下，为 Azure Rights Management 准备环境

>*适用于：Azure 信息保护、Office 365*

如果已在使用 Active Directory Rights Management Services (AD RMS)，并且遇到了下面的情况，请参阅此重要指南：

## <a name="you-see-an-option-to-activate-azure-rms-when-you-configure-azure-information-protection"></a>配置 Azure 信息保护时，系统显示激活 Azure RMS 的选项

可在“Azure 信息保护 - RMS 设置(预览)”边栏选项卡中选择激活 Azure Rights Management 服务 (Azure RMS)。 

如果还使用 Active Directory Rights Management Services (AD RMS)，请不要选择“激活”选项。 在还具有 AD RMS 的情况下无法激活 Azure Rights Management，因为两者不兼容。 这种情况不受支持且会产生不可靠的结果，因此，请勿在此时激活 Azure Rights Management。 

准备好将计算机从 AD RMS 移动到 Azure Rights Management 服务后，即可启动迁移过程。 迁移的其中一步是激活服务，但需先将配置信息从 AD RMS 导出到 Azure Rights Management 服务再执行此操作。 此过程能确保迁移后仍可打开受 AD RMS 保护的文档和电子邮件。

未激活 Azure Rights Management 服务时，仍可仅对应用分类的标签使用 Azure 信息保护。 将自动创建特殊的默认策略，该策略不包括数据保护，且相关配置选项在激活 Azure Rights Management 服务后才能使用。

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>步骤 1：配置 Azure 信息保护策略，以便在无保护的情况下进行分类和标记

从最初的“Azure 信息保护”边栏选项卡中，选择“全局策略”，查看和配置不包括数据保护选项的默认策略。 有关详细信息，请参阅 [配置 Azure 信息保护策略](configure-policy.md)(#配置-azure-信息保护策略)。

### <a name="step-2-start-planning-for-migration"></a>步骤 2：开始规划迁移

请遵循以下迁移指南：[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。

### <a name="step-3-start-to-configure-labels-for-protection"></a>步骤 3：开始配置标签以便进行保护

在迁移过程中激活 Azure Rights Management 服务后，可配置标签以便进行数据保护。 但是，如果分批迁移用户，请确保应用保护的标签的[适用范围](configure-policy-scope.md)仅涵盖已迁移用户。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


