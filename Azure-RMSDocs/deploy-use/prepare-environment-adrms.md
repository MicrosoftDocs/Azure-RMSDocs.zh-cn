---
title: "为 Azure RMS 和 AD RMS 准备环境"
description: "如果有部署了 AD RMS 的 Azure Rights Management，本文将提供指导。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6d7a1d2ed61e1d12d6ca50db50c5b516e6e4f54e
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2018
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>如果还有 Active Directory Rights Management Services (AD RMS)，请为 Azure Rights Management 准备环境

>*适用于：Azure 信息保护、Office 365*

如果已在使用 Active Directory Rights Management Services (AD RMS)，本文提供重要指南，并且以下方案适用：

## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>配置 Azure 信息保护时，可看到“激活保护”的选项

“Azure 信息保护 - 保护激活”边栏选项卡提供用于激活 Azure Rights Management 服务 (Azure RMS) 的选项。 

如果还使用 Active Directory Rights Management Services (AD RMS)，请不要选中“激活”选项。 在还使用 AD RS 的情况下激活 Azure Rights Management 不是兼容的组合。 此方案不受支持并且结果不可靠，因此请务必在此时不要激活 Azure Rights Management。 

已准备好将计算机从 AD RMS 迁移到 Azure Rights Management 服务时，可以启动迁移过程。 迁移中的一个步骤是激活该服务，但应在将从 AD RMS 导出的配置信息导入到 Azure Rights Management 服务后执行此操作。 此过程可确保受 AD RMS 保护的文档和电子邮件仍可以打开。

当 Azure Rights Management 服务未激活时，仍然可以对仅应用分类的标签使用 Azure 信息保护。 将为你创建不包含数据保护的特殊默认策略，并且在激活 Azure Rights Management 服务之前，这些配置选项仍然不可用。

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>步骤 1：为分类和标签配置 Azure 信息保护策略 - 不带保护

从初始“Azure 信息保护”边栏选项卡，选择“全局策略”以查看和配置不包含数据保护选项的默认策略。 有关详细信息，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

### <a name="step-2-start-planning-for-migration"></a>步骤 2：开始规划迁移

请按照迁移指南：[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)进行操作。

### <a name="step-3-start-to-configure-labels-for-protection"></a>步骤 3：开始为保护配置标签

在迁移过程中激活 Azure Rights Management 服务后，可以为数据保护配置标签。 但是，如果分批迁移用户，请确保应用保护的标签的[作用域](configure-policy-scope.md)限定于所迁移的用户。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


