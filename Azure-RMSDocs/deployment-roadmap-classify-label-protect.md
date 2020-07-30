---
title: 部署 Azure 信息保护（AIP）以进行分类、标记和保护
description: 当你要对数据进行分类、标记和保护时，可以使用以下步骤为你的组织准备、实施和管理 Azure 信息保护（AIP）。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/23/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f4039b1c74ae8b341c5afb13a02a743267f00930
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87298384"
---
# <a name="aip-deployment-roadmap-for-classification-labeling-and-protection"></a>分类、标签和保护的 AIP 部署路线图

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

当你要对数据进行分类、标记和保护时，请使用以下步骤作为建议来帮助你为你的组织准备、实施和管理 Azure 信息保护。

对于任何具有支持订阅的客户，建议使用此路线图。 其他功能包括发现敏感信息以及标记文档和电子邮件以进行分类。 

标签还可以应用保护，以便为用户简化此步骤。 

使用经典客户端创建的 AIP 标签和使用[统一标签平台](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)的灵敏度标签都支持此路线图。

> [!TIP]
> 或者，您可能正在查找以下文章之一：
> - [仅适用于数据保护的 AIP 路线图](deployment-roadmap-protect-only.md)
> - [使用 Azure 信息保护的常见方案的操作指南](how-to-guides.md)
>- [Azure 信息保护发布路线图](information-support.md#information-about-new-releases-and-updates)

## <a name="deployment-process"></a>部署过程

执行以下步骤：

1. [确认订阅，分配用户许可证](#confirm-your-subscription-and-assign-user-licenses)
1. [准备租户以使用 Azure 信息保护](#prepare-your-tenant-to-use-azure-information-protection)
1. [配置、部署分类和标记](#configure-and-deploy-classification-and-labeling)
1. [准备数据保护](#prepare-for-data-protection)
1. [为数据保护配置标签和设置、应用程序和服务](#configure-labels-and-settings-applications-and-services-for-data-protection)
1. [使用和监视数据保护解决方案](#use-and-monitor-your-data-protection-solutions)
1. [根据需要管理租户帐户的保护服务](#administer-the-protection-service-for-your-tenant-account-as-needed)

> [!TIP]
> 已在使用 Azure 信息保护提供的保护功能？ 可以跳过这些步骤中的许多步骤，重点关注步骤[3](#configure-and-deploy-classification-and-labeling)和[5.1](#configure-labels-and-settings-applications-and-services-for-data-protection)。

## <a name="confirm-your-subscription-and-assign-user-licenses"></a>确认订阅，分配用户许可证

确认你的组织具有包含所需功能和功能的订阅。 可以在[Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection)页上找到这些详细信息。

然后，将该订阅中的许可证分配给组织中的每位用户，这些用户将对文档和电子邮件进行分类、标记和保护。

> [!IMPORTANT]
> 不要从免费的个人 RMS 订阅手动分配用户许可证，也不要使用此许可证来管理组织的 Azure Rights Management 服务。 
>
> 这些许可证在 Microsoft 365 管理中心显示为“权限管理即席”****，当运行 Azure AD PowerShell cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) 时显示为 **RIGHTSMANAGEMENT_ADHOC**。 
>
> 有关详细信息，请参阅[个人 RMS 和 Azure 信息保护](./rms-for-individuals.md)。
> 
## <a name="prepare-your-tenant-to-use-azure-information-protection"></a>准备租户以使用 Azure 信息保护

在开始使用 Azure 信息保护之前，请确保你的用户帐户和组位于 Office 365 或 Azure Active Directory 中，AIP 可用于对用户进行身份验证和授权。

如有必要，请创建这些帐户和组，或者从本地目录同步这些帐户和组。 

有关详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

## <a name="configure-and-deploy-classification-and-labeling"></a>配置、部署分类和标记

确定是使用 AIP 经典还是 AIP 统一标签客户端，或者是否需要这两个客户端。

1. **确定要使用的客户端。**

    确定此时需要的客户端，以便知道在配置标签和策略设置时要使用的管理门户。

    有关详细信息，请参阅[选择要使用的 Azure 信息保护客户端](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers)。

1. **扫描文件（可选，但建议使用）。**

    [部署并运行 AIP 扫描程序](deploy-aip-scanner.md)，以发现本地数据存储区上的敏感信息。 扫描程序找到的信息有助于进行类别分类，提供有关所需的标签类型以及需要保护的文件的重要信息。

    "扫描程序发现模式" 不需要任何标签配置或分类，因此适用于部署的这一早期阶段。 你还可以在配置建议或自动标记之前，将此扫描程序配置与以下部署步骤并行使用。

1. **自定义默认的 AIP 策略**。

    如果还没有分类策略，请使用[默认的 Azure 信息保护策略](./configure-policy-default.md)作为确定数据所需的标签的基础。 根据需要自定义这些标签以满足你的需求。

    例如，你可能希望通过以下详细信息重新配置标签：

    - 请确保您的标签支持您的分类决定。
    - 配置用户手动标识的策略
    - 编写用户指南来帮助说明应在每个方案中应用的标签。
    - 如果默认策略是使用自动应用保护的标签创建的，则在测试设置时，你可能需要临时删除保护设置或禁用标签。 

    有关如何配置标签和策略设置的详细信息，请参阅：

    - **经典客户端：** [配置 Azure 信息保护策略](./configure-policy.md)
    - **统一标签客户端：** [了解敏感度标签](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)
    
1. **部署客户端**

    配置策略后，为用户部署 Azure 信息保护经典和/或统一标签客户端。 提供用户培训和特定说明，以便选择标签。 

    有关详细信息，请参阅：

    - **经典客户端**：[管理员指南](./rms-client/client-admin-guide.md)
    - **统一标签客户端**：[管理员指南](./rms-client/clientv2-admin-guide.md)

1. **引入更高级的配置**

    请等待用户对文档和电子邮件中的标签更熟悉。 准备就绪后，请引入高级配置，例如：

    - 应用默认标签
    - 如果用户选择了具有较低分类级别的标签或删除标签，则提示用户提供理由
    - 所有文档和电子邮件都具有标签
    - 自定义页眉、页脚或水印
    - 建议和自动标记

    有关详细信息，请参阅：

    - **经典客户端**：[管理员指南：自定义配置](rms-client/client-admin-guide-customizations.md)
    - **统一标签客户端**：[管理员指南：自定义配置](rms-client/clientv2-admin-guide-customizations.md)
     
    > [!TIP]
    > 如果已将标签配置为自动标签，请在发现模式下再次在本地数据存储上运行[Azure 信息保护扫描程序](deploy-aip-scanner-manage.md)，并匹配策略。 
    > 
    > 如果在发现模式下运行扫描程序，则会告诉你哪些标签将应用于文件，这有助于微调你的标签配置并准备批量分类和保护文件。 
    > 

## <a name="prepare-for-data-protection"></a>准备数据保护

一旦用户对文档和电子邮件进行了舒适的标记，就会为最敏感数据引入数据保护。

执行以下步骤来准备数据保护：

1. **确定要管理租户密钥的方式**。

    决定你是希望 Microsoft 管理你的租户密钥（默认设置），还是自行生成和管理你的租户密钥（也称为“自带密钥”，简称 BYOK）。 

    > [!NOTE]
    > 根据你的客户端，可以使用其他选项 "自带密钥（HYOK）" 或双密钥加密来提高安全性。 .
    >
 
    有关详细信息，请参阅[计划和实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md)

1. **安装适用于 AIP 的 PowerShell**。

    在至少一台具有 internet 访问权限的计算机上安装适用于 AIPService 的 PowerShell 模块。 你可以立即执行此步骤，也可以稍后执行。 

    有关详细信息，请参阅[安装 AIPService PowerShell 模块](./install-powershell.md)。

1. **仅 AD RMS**：将密钥、模板和 url 迁移到云。

    如果你当前正在使用 AD RMS，请执行迁移，将密钥、模板和 Url 移动到云。 
    
    有关详细信息，请参阅[从 AD RMS 迁移到信息保护](migrate-from-ad-rms-to-azure-rms.md)。

1. **激活保护**。

    确保保护服务已激活，以便开始保护文档和电子邮件。 如果要以多个阶段进行部署，请配置用户载入控制以限制用户应用保护。 

    有关详细信息，请参阅[激活 Azure 信息保护的保护服务](./activate-service.md)。

1. **请考虑使用日志记录（可选）**。

    请考虑使用日志记录使用情况来监视组织如何使用保护服务。 你可以立即执行此步骤，也可以稍后执行。 

    有关详细信息，请参阅[记录和分析 Azure 信息保护中的保护使用情况](./log-analyze-usage.md)。

## <a name="configure-labels-and-settings-applications-and-services-for-data-protection"></a>为数据保护配置标签和设置、应用程序和服务

执行以下步骤：

1. **更新标签以应用保护**
    
    根据你的客户端，使用以下指南之一：

    - 经典：[如何为 Rights Management 保护配置标签](./configure-policy-protection.md)
    - 统一标签：[使用敏感度标签中的加密限制对内容的访问](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)
    
    > [!IMPORTANT]
    > 即使没有为信息权限管理（IRM）配置 Exchange，用户也可以在应用 Rights Management 保护的 Outlook 中应用标签。 
    > 
    > 但是，在为 IRM 或[具有新功能的 Office 365 邮件加密](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)配置 Exchange 之前，你的组织将无法获得将 Exchange 与 Azure Rights Management 保护配合使用的完整功能。 此附加配置包含在以下列表中（对于 Exchange Online，则为 2；对于 Exchange 本地，则为 5）。 
    > 

1. **配置 Office 应用程序和服务**
    
    为 Microsoft SharePoint 或 Exchange Online 中的信息权限管理（IRM）功能配置 Office 应用程序和服务。 

    有关详细信息，请参阅[配置适用于 Azure Rights Management 的应用程序](configure-applications.md)。

1. **为数据恢复配置超级用户功能**
    
    如果现有 IT 服务（例如数据泄露防护 (DLP) 解决方案、内容加密网关 (CEG) 和反恶意软件产品）需要检查 Azure 信息保护将保护的文件，请将服务帐户配置为 Azure Rights Management 的超级用户。 

    有关详细信息，请参阅[为 Azure 信息保护和发现服务或数据恢复配置超级用户](./configure-super-users.md)。

1. **批量分类和保护现有文件**
    
    对于本地数据存储，现在以强制模式运行 [Azure 信息保护扫描程序](deploy-aip-scanner.md)，以便自动标记文件。
    
    对于 Pc 上的文件，请使用 PowerShell cmdlet 来分类和保护文件。 有关详细信息，请参阅以下指南，具体取决于你的客户端：
    
    - **经典客户端：** [将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)
    - **统一标签客户端：** [将 PowerShell 与 Azure 信息保护统一标签客户端配合使用](./rms-client/clientv2-admin-guide-powershell.md)

    对于基于云的数据存储，请使用 [Azure Cloud App Security](https://docs.microsoft.com/cloud-app-security)。 

    > [!TIP]
    > 虽然批量分类和保护现有文件不是 cloud app security 的主要用例之一，但[文档记录的解决方法](https://docs.microsoft.com/cloud-app-security/azip-integration#enable-azure-information-protection)可帮助你将文件分类并保护。

6. **在 SharePoint Server 上部署受 IRM 保护的库的连接器，为本地 Exchange 部署受 IRM 保护的电子邮件**
    
    如果具有本地 SharePoint 和 Exchange 并希望使用其信息权限管理 (IRM) 功能，请安装和配置 Rights Management 连接器。 

    有关详细信息，请参阅[部署 Azure Rights Management 连接器](./deploy-rms-connector.md)。

## <a name="use-and-monitor-your-data-protection-solutions"></a>使用和监视数据保护解决方案

现在，你可以监视你的组织如何使用已配置的标签，并确认你正在保护敏感信息。 

有关详细信息，请参阅以下页面：

- [Azure 信息保护的中心报告](reports-aip.md)-当前提供预览版
- Azure 信息保护经典客户端的[Windows 事件监视器的本地使用情况日志记录](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)
- [记录和分析 Azure 信息保护中的保护使用情况](./log-analyze-usage.md)

## <a name="administer-the-protection-service-for-your-tenant-account-as-needed"></a>根据需要管理租户帐户的保护服务

开始使用保护服务时，可以利用 PowerShell 帮助编写脚本或自动执行管理更改。 某些高级配置可能还需要使用 PowerShell。 

有关详细信息，请参阅[使用 PowerShell 管理 Azure 信息保护中的保护](./administer-powershell.md)。

## <a name="next-steps"></a>后续步骤

部署 Azure 信息保护时，你可能会发现检查[常见问题](faqs.md)，以及其他资源的[信息和支持](information-support.md)页面非常有用。