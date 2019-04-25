---
title: 为 Azure RMS 和 AD RMS 准备环境
description: 如果已部署 Azure Rights Management 和 AD RMS，请参阅本指南。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/29/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c8219221fe9b932e0d09901dccf496df5f83ef76
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60183919"
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>在已有 Active Directory Rights Management Services (AD RMS) 的情况下，为 Azure Rights Management 准备环境

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

> [!IMPORTANT]
> 使用 Active Directory Rights Management Services (AD RMS) 时的指南

如果 Azure Rights Management 服务已激活，且同时还要使用 AD RMS，这样的组合不兼容。 无需执行额外的步骤，一些计算机即可能会自动开始使用 Azure Rights Management 服务，并且还连接到你的 AD RMS 群集。 这种方案不受支持，且结果不可靠，因此请务必采取其他措施。 

**若要检查是否已部署 AD RMS，请执行以下操作：**

1. 虽然是可选的，但大多数 AD RMS 部署都会将服务连接点 (SCP) 发布到 Active Directory，以便域计算机能够发现 AD RMS 群集。 
    
    使用 ADSI 编辑功能，确定是否已在 Active Directory 中发布 SCP：`CN=Configuration [server name], CN=Services, CN=RightsManagementServices, CN=SCP`

2. 如果不要使用 SCP，必须使用以下 Windows 注册表来配置连接到 AD RMS 群集的 Windows 计算机，以实现客户端服务发现或授权重定向：`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation` 或 `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\ServiceLocation`
    
    若要详细了解这些注册表配置，请参阅[使用 Windows 注册表启用客户端服务发现](./rms-client/client-deployment-notes.md#enabling-client-side-service-discovery-by-using-the-windows-registry)和[重定向授权服务器流量](./rms-client/client-deployment-notes.md#redirecting-licensing-server-traffic)。   

如果为组织部署了 AD RMS，请考虑能否迁移到 Azure 信息保护。 与 AD RMS 相比，Azure 信息保护有许多优势。 例如，可以更好地支持移动设备，并与 Office 365 服务以及 Exchange Server 和 SharePoint Server 集成。 有关详细信息，请参阅[比较 Azure 信息保护和 AD RMS](compare-on-premise.md)。

迁移到 Azure 信息保护后，不会失去对以前受保护内容的访问权限，也不必取消保护或重新保护内容。 即使在取消预配 AD RMS 后，仍可以打开受 AD RMS 保护的文档和电子邮件。

无论决定是迁移到 Azure 信息保护，还是接受使用当前 AD RMS 部署存在的限制，都必须先确保已停用 Azure Rights Management 服务。 有关说明，请按照适用的方案步骤操作：

- [包含 Azure Rights Management 的订阅是在 2018 年 2 月期间或之后购买](#your-subscription-was-purchased-during-or-after-february-2018)

- [订阅是在 2018 年 2 月之前或期间购买，且已安装 Exchange Online](#your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online)

- [在 Azure 门户中配置你的 Azure 信息保护策略时，看到一个激活保护的选项](#you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection)


## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>你的订阅是在 2018 年 2 月期间或之后购买的

至 2018 年 2 月底，包含 Azure 信息保护的新订阅默认激活 Azure 权限管理服务。 如果此服务已自动激活，且同时还要使用 Active Directory Rights Management Services (AD RMS)，这样的组合不兼容。因此，请务必尽快停用 Azure Rights Management 服务。 

### <a name="step-1-deactivate-azure-rights-management"></a>步骤 1：停用 Azure Rights Management
使用以下某个过程来停用 Azure Rights Management。

> [!TIP]
> 也可以使用 Windows PowerShell cmdlet [Disable-Aadrm](/powershell/module/aadrm/disable-aadrm) 来停用 Azure Rights Management 服务。

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>从 Microsoft 365 管理中心停用权限管理

1. 转到 Office 365 管理员的 [Rights Management 页](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)。
    
    如果系统提示登录，请使用 Office 365 的全局管理员帐户。

2. 在“Rights Management”  页面中，单击“停用” 。

3.  当看到“是否要停用 Rights Management?”的提示时，请单击“停用”。

现在，你应该会看到“Rights Management 未激活”  和用于激活的选项。

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>从 Azure 门户停用 Rights Management

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。
    
    如果之前尚未访问过 Azure 信息保护边栏选项卡，请参阅一次性执行的[其他步骤](configure-policy.md#to-access-the-azure-information-protection-blade-for-the-first-time)来向门户添加此边栏选项卡。

2. 选择菜单选项中的“保护激活”。 

3.  在“Azure 信息保护” -“保护激活”边栏选项卡上，选择“停用”。 选择“是”以确认你的选择。

信息栏会显示“停用已成功完成”且“停用”现在已替换为“激活”。 

### <a name="step-2-start-planning-for-migration"></a>步骤 2：开始规划迁移

请参阅迁移指南：[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)


## <a name="your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online"></a>订阅是在 2018 年 2 月之前或期间购买，且已安装 Exchange Online

Microsoft 即将开始为包含 Azure Rights Management 或 Azure 信息保护的订阅以及使用 Exchange Online 的租户激活 Azure Rights Management 服务。 对于这些租户，自动激活将于 2018 年 8 月 1 日开始推出。

如果此服务已自动激活，且同时还要使用 AD RMS，这样的组合不兼容。因此，请务必让租户选择退出自动服务更新。 

### <a name="step-1-opt-out-from-the-automatic-service-update"></a>步骤 1：选择退出自动服务更新

运行以下 [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration) Exchange Online PowerShell 命令：`Set-IRMConfiguration -AutomaticServiceUpdateEnabled $false`

[详细信息](https://support.office.com/article/protection-features-in-azure-information-protection-rolling-out-to-existing-office-365-tenants-7ad6f58e-65d7-4c82-8e65-0b773666634d) 

### <a name="step-2-start-planning-for-migration"></a>步骤 2：开始规划迁移

请参阅迁移指南：[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)


## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>配置 Azure 信息保护时，会看到一个激活保护的选项

“Azure 信息保护 - 保护激活”边栏选项卡上有一个选项，可用于激活 Azure Rights Management 服务。  

如果还要使用 AD RMS，请勿选择“激活”选项。 未激活 Azure Rights Management 服务时，仍可仅对应用分类的标签使用 Azure 信息保护。 将自动创建特殊的默认策略，该策略不包括数据保护，且相关配置选项在激活 Azure Rights Management 服务后才能使用。

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>步骤 1：配置 Azure 信息保护策略，以便在无保护的情况下进行分类和标记

在“Azure 信息保护 - 标签”边栏选项卡中，查看和配置不包括数据保护选项的标签。 若要详细了解如何配置标签和策略设置，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

### <a name="step-2-start-planning-for-migration"></a>步骤 2：开始规划迁移

请参阅迁移指南：[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)

### <a name="step-3-configure-labels-for-protection"></a>步骤 3：为实现保护而配置标签

在迁移过程中激活 Azure Rights Management 服务后，可配置标签以便进行数据保护。 但是，如果分批迁移用户，请确保应用保护的标签的适用范围仅为已迁移用户。


