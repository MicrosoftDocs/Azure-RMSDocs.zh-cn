---
title: Azure 信息保护 (AIP) 仅限保护的部署路线图
description: 如果你只想要实施保护，请使用以下步骤为你的组织准备、实施和管理 Azure 信息保护 (AIP) 。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/23/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 40303d80ef0e1e9274d8b2258b4e400616dd875a
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583636"
---
# <a name="azure-information-protection-deployment-roadmap-for-protection-only"></a>仅限保护的 Azure 信息保护部署路线图

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

> [!TIP]
> 或者，您可能正在查找以下文章之一：
> - [分类、标签和保护的 AIP 部署路线图](deployment-roadmap-classify-label-protect.md)
> - [使用 Azure 信息保护的常见方案的操作指南](how-to-guides.md)
> - [Azure 信息保护发布路线图](information-support.md#information-about-new-releases-and-updates)

如果你只想要实施数据保护，请使用以下步骤作为建议来帮助你为你的组织准备、实施和管理 Azure 信息保护。

对于订阅不支持分类和标签的客户，建议使用此路线图，但不支持标签。 必须安装 AIP 经典客户端。 

## <a name="deployment-process"></a>部署过程

执行以下步骤：

1. [确认你有包含 AIP 保护服务的订阅](#confirm-that-you-have-a-subscription-that-includes-the-aip-protection-service) 
1. [准备租户以使用 Azure 信息保护](#prepare-your-tenant-to-use-azure-information-protection)
1. [安装 Azure 信息保护经典和客户端配置应用程序和服务以实现 Rights Management](#install-the-azure-information-protection-classic-and-client-configure-applications-and-services-for-rights-management)
1. [使用和监视数据保护解决方案](#use-and-monitor-your-data-protection-solutions)
1. [根据需要管理租户帐户的保护服务](#administer-the-protection-service-for-your-tenant-account-as-needed)

## <a name="confirm-that-you-have-a-subscription-that-includes-the-aip-protection-service"></a>确认你有包含 AIP 保护服务的订阅

验证你的组织是否具有包含所需功能和功能的订阅。 可以使用 [Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection) 页面上的订阅信息和功能列表。

将此订阅的许可证分配给组织中将保护文档和电子邮件的每个用户。

> [!IMPORTANT]
> 不要从个人订阅的免费 RMS 手动分配用户许可证，不要使用此许可证来管理组织的 Azure Rights Management 服务。 
>
> 这些许可证在 Microsoft 365 管理中心显示为“权限管理即席”，当运行 Azure AD PowerShell cmdlet [Get-MsolAccountSku](/previous-versions/azure/dn194118(v=azure.100)) 时显示为 **RIGHTSMANAGEMENT_ADHOC**。 
>
> 有关如何将个人订阅 RMS 自动授权和分配给用户的详细信息，请参阅[个人 RMS 和 Azure 信息保护](./rms-for-individuals.md)。

## <a name="prepare-your-tenant-to-use-azure-information-protection"></a>准备租户以使用 Azure 信息保护

开始使用 Azure 信息保护提供的保护服务之前，请执行以下准备工作：

1. **为 AIP 设置用户帐户和组**

    确保 Microsoft 365 租户包含 Azure 信息保护用来对组织中的用户进行身份验证和授权的用户帐户和组。 如有必要，请创建这些帐户和组，或者从本地目录同步这些帐户和组。 

    有关详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

1. **决定要如何管理租户密钥**

    决定你是希望 Microsoft 管理你的租户密钥（默认设置），还是自行生成和管理你的租户密钥（也称为“自带密钥”，简称 BYOK）。 为了获得更高的安全性，请在 HYOK) 保护中实现 "保留自己的密钥" (。 

    有关详细信息，请参阅[规划和实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

1. **安装适用于 AIP 的 PowerShell**

    在至少一台具有 internet 访问权限的计算机上安装适用于 AIPService 的 PowerShell 模块。 你可以立即执行此步骤，也可以稍后执行。 

    有关详细信息，请参阅 [安装 AIPService PowerShell 模块](./install-powershell.md)。

1. **仅 AD RMS：将数据迁移到云**

    如果当前正在使用 AD RMS：请进行迁移，将密钥、模板和 URL 移动到云中。 

    有关详细信息，请参阅[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)。

1. **激活保护**

    确保保护服务已激活，以便开始保护文档和电子邮件。 如果要分阶段部署，请配置用户载入控制以限制用户应用保护。 

    有关详细信息，请参阅[激活 Azure 信息保护的保护服务](./activate-service.md)。

1. **根据需要配置可选功能**

    考虑现在或之后配置以下任一功能。
    
    |功能  |说明  |
    |---------|---------|
    |**用于保护设置的自定义模板**     |  如果默认模板不足以满足你的组织的需要，请配置自定义模板。 </br>有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](./configure-policy-templates.md)。       |
    |**使用情况日志记录**     | 配置使用日志记录，以监视组织如何使用保护服务。 </br>有关详细信息，请参阅 [记录和分析 Azure 信息保护中的保护使用情况](./log-analyze-usage.md)。        |
    | | |

## <a name="install-the-azure-information-protection-classic-and-client-configure-applications-and-services-for-rights-management"></a>安装 Azure 信息保护经典和客户端配置应用程序和服务以实现 Rights Management

执行以下步骤：

1. **部署 Azure 信息保护经典客户端**
    
    为用户安装经典客户端以支持 Office 2010，以保护除 Office 文档和电子邮件之外的文件，以及跟踪受保护的文档，并为此客户端提供用户培训。 

    有关详细信息，请参阅适用于 windows 的 [Azure 信息保护经典客户端](./rms-client/aip-client.md) 和 [适用于 windows 和 Office 版本的 AIP 扩展支持](known-issues.md#aip-for-windows-and-office-versions-in-extended-support)。

2. **配置 Office 应用程序和服务**
    
    为信息权限管理配置 Office 应用程序和服务 (SharePoint 或 Exchange Online 中的 IRM) 功能。 

    有关详细信息，请参阅 [配置适用于 Azure Rights Management 的应用程序](./configure-applications.md)。

3. **为数据恢复配置超级用户功能**
    
    如果现有 IT 服务（例如数据泄漏防护 (DLP) 解决方案、内容加密网关 (CEG) 和反恶意软件产品）需要检查 Azure 信息保护将保护的文件，请将服务帐户配置为 Azure Rights Management 的超级用户。 

    有关详细信息，请参阅 [为 Azure 信息保护和发现服务或数据恢复配置超级用户](./configure-super-users.md)。

4. **批量保护现有文件** 
    
    可以使用 PowerShell cmdlet 批量保护或批量取消保护多种文件类型。 

    有关详细信息，请参阅管理员指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。
    
    对于基于 Windows 的文件服务器上的文件，可以将这些 cmdlet 与脚本和 Windows Server 文件分类基础结构一起使用。 有关详细信息，请参阅[使用 Windows Server 文件分类基础结构 (FCI) 进行 RMS 保护](./rms-client/configure-fci.md)。

5. **部署适用于本地服务器的连接器**
    
    如果你拥有想要与保护服务共同使用的本地服务，请安装和配置 Rights Management 连接器。 

    有关详细信息，请参阅[部署 Azure Rights Management 连接器](./deploy-rms-connector.md)。

## <a name="use-and-monitor-your-data-protection-solutions"></a>使用和监视数据保护解决方案

现在，你可以保护数据，并记录公司如何使用保护服务。 

有关详细信息，请参阅：

- [使用 Azure Rights Management 服务帮助用户保护文件](./help-users.md)
- [记录和分析 Azure 信息保护中的保护使用情况](./log-analyze-usage.md)

## <a name="administer-the-protection-service-for-your-tenant-account-as-needed"></a>根据需要管理租户帐户的保护服务

开始使用保护服务时，可以利用 PowerShell 帮助编写脚本或自动执行管理更改。 某些高级配置可能还需要使用 PowerShell。 

有关详细信息，请参阅 [使用 PowerShell 管理 Azure 信息保护中的保护](./administer-powershell.md)。

## <a name="next-steps"></a>后续步骤

部署 Azure 信息保护时，你可能会发现检查 [常见问题](faqs.md)，以及其他资源的 [信息和支持](information-support.md) 页面非常有用。