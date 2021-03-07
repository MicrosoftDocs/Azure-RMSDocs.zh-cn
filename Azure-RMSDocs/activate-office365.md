---
title: 从 Microsoft 365 管理中心激活 Azure RMS-AIP
description: 了解如何从 Microsoft 365 管理中心激活 Azure Rights Management 服务。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a2b3e1a2-59a0-4191-bf4c-4485ae7a70a9
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 24787eda3b248cab2e6cc3c055611378e39b5c3c
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2021
ms.locfileid: "102414780"
---
# <a name="activate-azure-rights-management-protection-from-the-microsoft-365-admin-center"></a>从 Microsoft 365 管理中心激活 Azure Rights Management 保护

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>相关内容：*[AIP 统一标记客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

本文介绍如何通过 Microsoft 365 管理中心的全局管理员访问 Azure Rights Management 服务，从而激活 Azure Rights Management。

## <a name="prerequisites"></a>先决条件

若要激活 Azure 权限管理服务，必须拥有 [Azure Information Protection Premium plan](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)（Azure 信息保护高级计划）或 [Office 365 plan that includes Rights Management](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)（包含权限管理的 Office 365 计划）。 例如，组织有 Office 365 E3 或 Office 365 E5 计划。 

如果你对订阅要求有任何疑问，或需要获取激活服务方面的帮助，请[联系 Microsoft 支持部门](information-support.md#to-contact-microsoft-support)或使用标准支持渠道。

## <a name="activating-azure-rights-management"></a>激活 Azure 权限管理

1. 确认组织有包含 Azure 权限管理的计划后，转到 Microsoft 365 管理中心内的[“权限管理”页](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)。
    
    如果系统提示你登录，请使用 Microsoft 365 的全局管理员帐户。
    
    > [!TIP]
    > 有关管理中心的帮助，请参阅[关于 Microsoft 365 管理中心](/office365/admin/admin-overview/about-the-admin-center)。
    
    如果希望从管理中心导航到 "**权限管理**" 页： "**设置**  >  " "**组织设置**  >  **服务**" 选项卡 > **Microsoft Azure 信息保护**  >  **管理 Microsoft Azure 信息保护设置**

2. 在“权限管理”页上，单击“激活”。

3. 看到“是否要激活权限管理?”消息时，单击“激活”。

现在，应显示 **“权限管理已激活”** 和停用选项。

## <a name="next-steps"></a>后续步骤

继续阅读 [从 Azure 信息保护中激活保护服务](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)。

