---
title: "为 Azure RMS 和 AD RMS 准备环境"
description: "如果已部署 Azure Rights Management 和 AD RMS，请参阅本指南。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: de42f0d87f42c304c2df906fe037816be7f2ba25
ms.sourcegitcommit: 23d98a405057d61a737313c8dfef042996131d3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/27/2018
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>在已有 Active Directory Rights Management Services (AD RMS) 的情况下，为 Azure Rights Management 准备环境

>*适用于：Azure 信息保护、Office 365*

如果已在使用 Active Directory Rights Management Services (AD RMS)，并且遇到了以下任一情况，请参阅此重要指南：

- [包含 Azure Rights Management 的订阅是在 2018 年 2 月期间或之后购买的](#your-subscription-was-purchased-during-or-after-february-2018)。

- [在 Azure 门户中配置你的 Azure 信息保护策略时，看到一个激活保护的选项](#you-see-an-option-to activate-azure-rights-management-when-you-configure-azure-information-protection)

## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>你的订阅是在 2018 年 2 月期间或之后购买的

至 2018 年 2 月底，包含 Azure 信息保护的新订阅默认激活 Azure 权限管理服务。 如果此服务已自动激活，且你同时使用 Active Directory Rights Management Services (AD RMS)，则此组合不兼容。 无需执行额外的步骤，一些计算机即可能会自动开始使用 Azure Rights Management 服务，并且还连接到你的 AD RMS 群集。 这种情况是不受支持的且会产生不可靠的结果，因此，请务必尽快停用 Azure Rights Management 服务。 

准备好将计算机从 AD RMS 移动到 Azure Rights Management 服务后，即可开始进行迁移过程。 迁移的其中一步是再次激活服务，但需要先将配置信息从 AD RMS 导出到 Azure Rights Management 服务后再执行此步骤。 按此顺序操作可确保迁移后仍可打开受 AD RMS 保护的文档和电子邮件。

第一步是停用 Azure Rights Management 服务。

### <a name="step-1-deactivate-azure-rights-management"></a>步骤 1：停用 Azure Rights Management
使用以下某个过程来停用[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]。

> [!TIP]
> 也可以使用 Windows PowerShell cmdlet [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) 来停用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]。

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>从 Office 365 管理中心停用权限管理

1. 转到 Office 365 管理员的 [Rights Management 页](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)。
    
    如果系统提示登录，请使用 Office 365 的全局管理员帐户。

2. 在“Rights Management”  页面中，单击“停用” 。

3.  当看到“是否要停用 Rights Management?”的提示时，请单击“停用”。

现在，你应该会看到“Rights Management 未激活”  和用于激活的选项。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>从 Azure 门户停用 Rights Management

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。
    
    如果之前尚未访问过 Azure 信息保护边栏选项卡，请参阅一次性执行的[其他步骤](configure-policy.md#to-access-the-azure-information-protection-blade-for-the-first-time)来向门户添加此边栏选项卡。

2. 在初始“Azure 信息保护”边栏选项卡上，选择“保护激活”。 

3.  在“Azure 信息保护” -“保护激活”边栏选项卡上，选择“停用”。 选择“是”以确认你的选择。

信息栏会显示“停用已成功完成”且“停用”现在已替换为“激活”。 

### <a name="step-2-start-planning-for-migration"></a>步骤 2：开始规划迁移

请参阅迁移指南：[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。

## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>配置 Azure 信息保护时，会看到一个激活保护的选项

“Azure 信息保护 - 保护激活”边栏选项卡上有一个激活 Azure 权限管理服务 (Azure RMS) 的选项。  

如果还使用 Active Directory Rights Management Services (AD RMS)，请不要选择“激活”选项。 在还具有 AD RMS 的情况下无法激活 Azure Rights Management，因为两者不兼容。 这种情况不受支持且会产生不可靠的结果，因此，请勿在此时激活 Azure Rights Management。  

准备好将计算机从 AD RMS 移动到 Azure Rights Management 服务后，即可启动迁移过程。 迁移的其中一步是激活服务，但需先将配置信息从 AD RMS 导出到 Azure Rights Management 服务再执行此操作。 此过程能确保迁移后仍可打开受 AD RMS 保护的文档和电子邮件。 

未激活 Azure Rights Management 服务时，仍可仅对应用分类的标签使用 Azure 信息保护。 将自动创建特殊的默认策略，该策略不包括数据保护，且相关配置选项在激活 Azure Rights Management 服务后才能使用。

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>步骤 1：配置 Azure 信息保护策略，以便在无保护的情况下进行分类和标记

从最初的“Azure 信息保护”边栏选项卡中，选择“全局策略”，查看和配置不包括数据保护选项的默认策略。 有关详细信息，请参阅 [配置 Azure 信息保护策略](configure-policy.md)(#配置-azure-信息保护策略)。

### <a name="step-2-start-planning-for-migration"></a>步骤 2：开始规划迁移

请参阅迁移指南：[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。

### <a name="step-3-start-to-configure-labels-for-protection"></a>步骤 3：开始配置标签以便进行保护

在迁移过程中激活 Azure Rights Management 服务后，可配置标签以便进行数据保护。 但是，如果分批迁移用户，请确保应用保护的标签的适用范围仅为已迁移用户。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

