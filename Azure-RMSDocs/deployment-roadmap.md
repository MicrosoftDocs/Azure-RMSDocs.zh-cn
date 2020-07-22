---
title: Azure 信息保护部署路线图
description: 使用这些步骤，为组织准备、实施和管理 Azure 信息保护。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 63a3fcc9ee6b7e59ceab31eb63455d53929d028c
ms.sourcegitcommit: 16d2c7477b96c5e8f6e4328a61fe1dc3d12c878d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86927805"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Azure 信息保护部署路线图

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

建议使用以下步骤，为组织准备、实施和管理 Azure 信息保护。

也可使用以下命令： 

- 正在寻找 Azure 信息保护的基于方案的说明？ 请参阅操作[指南，了解使用 Azure 信息保护的常见方案](how-to-guides.md)。

- 正在寻找 Azure 信息保护发布路线图？ 查看[有关新版本和更新的信息](information-support.md#information-about-new-releases-and-updates)。

### <a name="identify-your-deployment-roadmap"></a>标识部署路线图

在执行以下任意步骤以部署 Azure 信息保护之前，请确保已查看 [Azure 信息保护要求](./requirements.md)。

然后选择适用于组织，并与所需[订阅功能和特性](https://azure.microsoft.com/pricing/details/information-protection/)相匹配的部署路线图：

- [使用分类、标记和保护](#deployment-roadmap-for-classification-labeling-and-protection)
    
    当你具有支持订阅时的推荐路径，因为其他功能支持查找敏感信息，以及为分类的文档和电子邮件添加标签。 标签还可以应用保护，从而从用户抽象出这一复杂性。
    
    部署步骤适用于 Azure 信息保护标签和使用[统一标签平台](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)的敏感度标签。

- [仅使用数据保护](#deployment-roadmap-for-data-protection-only)
    
    当你没有支持分类和标签的订阅时要使用的路径，但不支持带标签的保护。

## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>用于分类、标记和保护的部署路线图

> [!NOTE]
> 已在使用 Azure 信息保护提供的保护功能？ 可以跳过这些步骤中的许多步骤，重点关注步骤 3 和步骤 5 1。

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>步骤 1：确认订阅，分配用户许可证
查看 [Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection)页面上的订阅信息和功能列表，以确认组织具有包含所需功能和特性的订阅。 然后，将该订阅中的许可证分配给组织中的每位用户，这些用户将对文档和电子邮件进行分类、标记和保护。

注意：不要从个人订阅的免费 RMS 手动分配用户许可证，不要使用此许可证来管理组织的 Azure Rights Management 服务。 这些许可证在 Microsoft 365 管理中心显示为“权限管理即席”****，当运行 Azure AD PowerShell cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) 时显示为 **RIGHTSMANAGEMENT_ADHOC**。 有关如何将个人订阅 RMS 自动授权和分配给用户的详细信息，请参阅[个人 RMS 和 Azure 信息保护](./rms-for-individuals.md)。

### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>步骤 2：准备租户以使用 Azure 信息保护

在开始使用 Azure 信息保护之前，请确保在 Office 365 或 Azure Active Directory 中具有用户帐户和组。 Azure 信息保护将使用这些用户帐户和组对组织中的用户进行身份验证和授权。 如有必要，请创建这些帐户和组，或者从本地目录同步这些帐户和组。 

有关详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>步骤 3：配置、部署分类和标记

在配置标签和策略设置之前，确定要使用的 Azure 信息保护客户端：经典客户端或统一标签客户端。 或者，可能需要这两个客户端。 现在需要此客户端决策，因此你知道使用哪个管理门户来配置标签和策略设置。 若要详细了解此决定，请参阅[选择要使用的 Azure 信息保护客户端](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers)。

> [!TIP]
> **可选，但建议**使用：请考虑使用[扫描器快速入门](quickstart-findsensitiveinfo.md)来发现本地数据存储区中的敏感信息。 扫描程序找到的信息有助于进行类别分类，提供有关所需的标签类型以及需要保护的文件的重要信息。
> 
> 由于扫描程序发现模式不要求你配置标签甚至定义了分类分类，因此以这种方式运行扫描程序适用于部署的这一初期阶段。 你还可以与以下部署步骤一起使用扫描程序的这一配置，直到你配置建议或自动标记为止。

如果还没有分类策略，请查看[默认的 Azure 信息保护策略](./configure-policy-default.md)，并使用此策略来决定要分配给组织数据的分类标签。 可以自定义这些标签以满足业务需求。

重新配置标签以进行所需的任何更改以支持分类决策。 为用户手动标识配置策略，编写解释应用哪个标签、在何时应用标签的用户指南。 如果默认策略在创建时带有自动应用保护的标签，请暂时删除保护设置或禁用标签。 有关如何配置标签和策略设置的详细信息，请参阅以下文档：

- 经典客户端的 azure 信息保护标签：[配置 Azure 信息保护策略](./configure-policy.md)

- 统一标签客户端的敏感度标签：[了解敏感度标签](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)

然后，为用户部署 Azure 信息保护客户端（经典）或 Azure 信息保护统一标签客户端。 提供用户培训和特定说明，以便选择标签。 有关安装和支持客户端的详细信息，请参阅管理员指南：

- [Azure 信息保护客户端管理员指南](./rms-client/client-admin-guide.md)

- [Azure 信息保护统一标签客户端管理员指南](./rms-client/clientv2-admin-guide.md)

一段时间后，当用户熟悉如何对文档和电子邮件添加标签时再引入更高级的配置。 其中可能包括：

- 应用默认的标签

- 如果用户选择分类级别较低的标签或删除标签，提示用户提供理由

- 强制所有文档和电子邮件都具有标签

- 自定义页眉、页脚或水印

- 建议和自动标记

在此阶段，不要选择保护文档和电子邮件的选项。 但是，在为自动标签配置标签后，请在发现模式下在本地数据存储上运行 [Azure 信息保护扫描程序](deploy-aip-scanner.md)并匹配策略。 使用此配置运行扫描程序可明白应用到文件的标签类型。 此信息有助于微调标签配置，并为批量分类和保护文件做好准备。 

### <a name="step-4-prepare-for-data-protection"></a>步骤 4：准备数据保护

当用户熟悉对文档和电子邮件添加标签后，就可以开始为最敏感的数据引入数据保护。 此阶段需要进行以下准备工作：

1. 决定你是希望 Microsoft 管理你的租户密钥（默认设置），还是自行生成和管理你的租户密钥（也称为“自带密钥”，简称 BYOK）。 有关详细信息，请参阅[规划和实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

2. 在至少一台具有 internet 访问权限的计算机上安装适用于 AIPService 的 PowerShell 模块。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[安装 AIPService PowerShell 模块](./install-powershell.md)。

3. 如果当前正在使用 AD RMS：请进行迁移，将密钥、模板和 URL 移动到云中。 有关详细信息，请参阅[从 AD RMS 迁移到信息保护](migrate-from-ad-rms-to-azure-rms.md)。

4. 确保保护服务已激活，以便开始保护文档和电子邮件。 如果需要分阶段部署，请配置用户载入控制以限制用户应用保护的能力。 有关详细信息，请参阅[激活 Azure 信息保护的保护服务](./activate-service.md)。

（可选）考虑进行以下配置：

- 使用日志记录，以便你能够监视组织如何使用保护服务。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[记录和分析 Azure 信息保护中的保护使用情况](./log-analyze-usage.md)。

### <a name="step-5-configure-labels-and-settings-applications-and-services-for-data-protection"></a>步骤5：为数据保护配置标签和设置、应用程序和服务

1. **更新标签以应用保护**
    
    对于 Azure 信息保护客户端（经典），请参阅[如何为 Rights Management 保护配置标签](./configure-policy-protection.md)。
    
    有关 Azure 信息保护统一标签客户端的信息，请参阅[使用敏感度标签中的加密限制对内容的访问](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)。
    
    请注意，即使没有为信息权限管理 (IRM) 配置 Exchange，用户也可以在应用 Rights Management 保护的 Outlook 中应用标签。 但是，在为 IRM 或[具有新功能的 Office 365 邮件加密](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)配置 Exchange 之前，你的组织将无法获得将 Exchange 与 Azure Rights Management 保护配合使用的完整功能。 此附加配置包含在以下列表中（对于 Exchange Online，则为 2；对于 Exchange 本地，则为 5）。 

2. **配置 Office 应用程序和服务**
    
    为 Microsoft SharePoint 或 Exchange Online 中的信息权限管理（IRM）功能配置 Office 应用程序和服务。 有关详细信息，请参阅[配置适用于 Azure Rights Management 的应用程序](configure-applications.md)。

3. **为数据恢复配置超级用户功能**
    
    如果现有 IT 服务（例如数据泄露防护 (DLP) 解决方案、内容加密网关 (CEG) 和反恶意软件产品）需要检查 Azure 信息保护将保护的文件，请将服务帐户配置为 Azure Rights Management 的超级用户。 有关详细信息，请参阅[为 Azure 信息保护和发现服务或数据恢复配置超级用户](./configure-super-users.md)。

4. **批量分类和保护现有文件**
    
    对于本地数据存储，现在以强制模式运行 [Azure 信息保护扫描程序](deploy-aip-scanner.md)，以便自动标记文件。
    
    对于 Pc 上的文件，请使用 PowerShell cmdlet 来分类和保护文件。 有关详细信息，请参阅以下管理指南：
    
    - Azure 信息保护客户端（经典）：[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)
    
    - Azure 信息保护统一标签客户端：[将 PowerShell 与 Azure 信息保护统一标签客户端配合使用](./rms-client/clientv2-admin-guide-powershell.md)

    对于基于云的数据存储，请使用 [Azure Cloud App Security](https://docs.microsoft.com/cloud-app-security)。 

    > [!TIP]
    > 虽然批量分类和保护现有文件不是 cloud app security 的主要用例之一，但[文档记录的解决方法](https://docs.microsoft.com/cloud-app-security/azip-integration#enable-azure-information-protection)可帮助你将文件分类并保护。

6. **在 SharePoint Server 上部署受 IRM 保护的库的连接器，为本地 Exchange 部署受 IRM 保护的电子邮件**
    
    如果具有本地 SharePoint 和 Exchange 并希望使用其信息权限管理 (IRM) 功能，请安装和配置 Rights Management 连接器。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](./deploy-rms-connector.md)。

### <a name="step-6-use-and-monitor-your-data-protection-solutions"></a>第 6 步：使用和监视数据保护解决方案
现在，你可以监视你的组织如何使用已配置的标签，并确认你正在保护敏感信息。 有关支持此部署阶段的其他信息，请参阅以下内容：

- [Azure 信息保护的中心报告](reports-aip.md)-当前提供预览版

- Azure 信息保护客户端的[Windows 事件监视器的本地使用情况日志记录](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)（经典）

- [记录和分析 Azure 信息保护中的保护使用情况](./log-analyze-usage.md)

### <a name="step-7-administer-the-protection-service-for-your-tenant-account-as-needed"></a>步骤 7：根据需要管理租户帐户的保护服务

开始使用保护服务时，可以利用 PowerShell 帮助编写脚本或自动执行管理更改。 某些高级配置可能还需要使用 PowerShell。 

有关详细信息，请参阅[使用 PowerShell 管理 Azure 信息保护中的保护](./administer-powershell.md)。


## <a name="deployment-roadmap-for-data-protection-only"></a>仅用于数据保护的部署路线图

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-the-protection-service-from-azure-information-protection"></a>步骤 1：确认你拥有包括 Azure 信息保护所提供保护服务的订阅

查看 [Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection)页面上的订阅信息和功能列表，以确认组织具有包含所需功能和特性的订阅。 然后，将该订阅中的许可证分配给组织中的每位用户，这些用户将对文档和电子邮件进行保护。

注意：不要从个人订阅的免费 RMS 手动分配用户许可证，不要使用此许可证来管理组织的 Azure Rights Management 服务。 这些许可证在 Microsoft 365 管理中心显示为“权限管理即席”****，当运行 Azure AD PowerShell cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) 时显示为 **RIGHTSMANAGEMENT_ADHOC**。 有关如何将个人订阅 RMS 自动授权和分配给用户的详细信息，请参阅[个人 RMS 和 Azure 信息保护](./rms-for-individuals.md)。


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>步骤 2：准备租户以使用 Azure 信息保护

开始使用 Azure 信息保护提供的保护服务之前，请执行以下准备工作：

1. 确保 Office 365 租户包含 Azure 信息保护用来对组织中的用户进行身份验证和授权的用户帐户和组。 如有必要，请创建这些帐户和组，或者从本地目录同步这些帐户和组。 有关详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

2. 决定你是希望 Microsoft 管理你的租户密钥（默认设置），还是自行生成和管理你的租户密钥（也称为“自带密钥”，简称 BYOK）。 有关详细信息，请参阅[规划和实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

3. 在至少一台具有 internet 访问权限的计算机上安装适用于 AIPService 的 PowerShell 模块。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[安装 AIPService PowerShell 模块](./install-powershell.md)。

4. 如果当前正在使用 AD RMS：请进行迁移，将密钥、模板和 URL 移动到云中。 有关详细信息，请参阅[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)。

5. 确保保护服务已激活，以便开始保护文档和电子邮件。 如果需要分阶段部署，请配置用户载入控制以限制用户应用保护的能力。 有关详细信息，请参阅[激活 Azure 信息保护的保护服务](./activate-service.md)。

（可选）考虑进行以下配置：

- 如果默认模板不足以满足你组织的要求，可自定义保护设置模板。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](./configure-policy-templates.md)。

- 使用日志记录，以便你能够监视组织如何使用保护服务。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[记录和分析 Azure 信息保护中的保护使用情况](./log-analyze-usage.md)。

### <a name="step-3-install-the-azure-information-protection-client-classic-and-configure-applications-and-services-for-rights-management"></a>步骤3：安装 Azure 信息保护客户端（经典），并为 Rights Management 配置应用程序和服务

1. 部署 Azure 信息保护客户端（经典）
    
    为用户安装经典客户端以支持 Office 2010，以保护除 Office 文档和电子邮件之外的文件，以及跟踪受保护的文档。 提供此客户端的用户培训。 有关详细信息，请参阅[适用于 Windows 的 Azure 信息保护客户端](./rms-client/aip-client.md)。

2. 配置 Office 应用程序和服务
    
    为 SharePoint 或 Exchange Online 中的信息权限管理（IRM）功能配置 Office 应用程序和服务。 有关详细信息，请参阅[配置适用于 Azure Rights Management 的应用程序](./configure-applications.md)。

3. 为数据恢复配置超级用户功能
    
    如果现有 IT 服务（例如数据泄露防护 (DLP) 解决方案、内容加密网关 (CEG) 和反恶意软件产品）需要检查 Azure 信息保护将保护的文件，请将服务帐户配置为 Azure Rights Management 的超级用户。 有关详细信息，请参阅[为 Azure 信息保护和发现服务或数据恢复配置超级用户](./configure-super-users.md)。

4. 批量保护现有文件 
    
    可以使用 PowerShell cmdlet 批量保护或批量取消保护多种文件类型。 有关详细信息，请参阅管理员指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。
    
    对于基于 Windows 的文件服务器上的文件，可以将这些 cmdlet 与脚本和 Windows Server 文件分类基础结构一起使用。 有关详细信息，请参阅[使用 Windows Server 文件分类基础结构 (FCI) 进行 RMS 保护](./rms-client/configure-fci.md)。

5. 部署适用于本地服务器的连接器
    
    如果你拥有想要与保护服务共同使用的本地服务，请安装和配置 Rights Management 连接器。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](./deploy-rms-connector.md)。

### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>步骤 4：使用和监视数据保护解决方案

现在，你可以保护数据，并记录公司如何使用保护服务。 有关支持此部署阶段的其他信息，请参阅[使用 azure Rights Management 服务帮助用户保护文件](./help-users.md)和[记录和分析 Azure 信息保护中的保护使用情况](./log-analyze-usage.md)。

### <a name="step-5-administer-the-protection-service-for-your-tenant-account-as-needed"></a>步骤 5：根据需要管理租户帐户的保护服务

开始使用保护服务时，可以利用 PowerShell 帮助编写脚本或自动执行管理更改。 某些高级配置可能还需要使用 PowerShell。 

有关详细信息，请参阅[使用 PowerShell 管理 Azure 信息保护中的保护](./administer-powershell.md)。

## <a name="next-steps"></a>后续步骤

部署 Azure 信息保护时，你可能会发现检查[常见问题](faqs.md)，以及其他资源的[信息和支持](information-support.md)页面非常有用。