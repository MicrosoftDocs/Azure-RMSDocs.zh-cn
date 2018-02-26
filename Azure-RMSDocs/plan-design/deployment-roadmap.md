---
title: "Azure 信息保护部署路线图"
description: "使用这些步骤，为组织准备、实施和管理 Azure 信息保护。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d0ebe0456933fd3b5940d50479038200008d9a44
ms.sourcegitcommit: 67750454f8fa86d12772a0075a1d01a69f167bcb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="azure-information-protection-deployment-roadmap"></a>Azure 信息保护部署路线图

>*适用于：Azure 信息保护、Office 365*

建议使用以下步骤，为组织准备、实施和管理 Azure 信息保护。

不过，如果只想快速试用 Azure 信息保护，而不将其部署在生产环境中，请参阅 [Azure 信息保护快速入门教程](../get-started/infoprotect-quick-start-tutorial.md)。

> [!IMPORTANT]
> 在执行以下步骤之前，请确保已查看 [Azure 信息保护的要求](../get-started/requirements-azure-rms.md)。

选择适用于组织，并与所需[订阅功能和特性](https://www.microsoft.com/cloud-platform/azure-information-protection-features)相匹配的部署路线图：

- [使用分类、标记和保护](#deployment-roadmap-for-classification-labeling-and-protection)

- [仅使用数据保护](#deployment-roadmap-for-data-protection-only)


## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>用于分类、标记和保护的部署路线图

> [!NOTE]
> 已使用 Azure Rights Management 服务进行数据保护？ 可以跳过这些步骤中的许多步骤，重点关注步骤 3 和步骤 5 1。

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>步骤 1：确认订阅，分配用户许可证
查看 Azure 信息保护网站上的[订阅信息](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)和[功能列表](https://www.microsoft.com/cloud-platform/azure-information-protection-features)，以确认组织具有包含所需功能和特性的订阅。 然后，将该订阅中的许可证分配给组织中的每位用户，这些用户将对文档和电子邮件进行分类、标记和保护。

注意：不要从个人订阅的免费 RMS 手动分配用户许可证，不要使用此许可证来管理组织的 Azure Rights Management 服务。 这些许可证在 Office 365 管理中心显示为 **Rights Management 即席**，当运行 Azure AD PowerShell cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) 时显示为 **RIGHTSMANAGEMENT_ADHOC**。 有关如何将个人订阅 RMS 自动授权和分配给用户的详细信息，请参阅[个人 RMS 和 Azure 信息保护](../understand-explore/rms-for-individuals.md)。


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>步骤 2：准备租户以使用 Azure 信息保护
开始使用 Azure 信息保护之前，请执行以下准备工作：

- 请确保在 Office 365 或 Azure Active Directory 中拥有用户帐户和组，Azure 信息保护将使用这些帐户和组对组织的用户进行身份验证和授权。 如有必要，请创建这些帐户和组，或者从本地目录同步这些帐户和组。 有关详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>步骤 3：配置、部署分类和标记

如果还没有分类策略，请查看[默认的 Azure 信息保护策略](../deploy-use/configure-policy-default.md)并将此作为基础，确定要将哪些分类标签分配给组织数据。 可以自定义这些标签以满足业务需求。 

重新配置默认的 Azure 信息保护标签以按需更改，使其支持分类决策。 为用户手动标识配置策略，编写解释应用哪个标签、在何时应用标签的用户指南。 有关如何配置 Azure 信息保护策略的详细信息，请参阅 [配置 Azure 信息保护策略](../deploy-use/configure-policy.md)。

然后为用户部署 Azure 信息保护客户端，通过向用户提供何时选择标签的培训和说明，支持客户端的运行。 有关安装和支持客户端的详细信息，请参阅 [Azure 信息保护客户端管理员指南](../rms-client/client-admin-guide.md)。

一段时间后，当用户熟悉如何对文档和电子邮件添加标签时再引入更高级的配置。 这些配置可能包括下列各项：

- 应用默认的标签

- 如果用户选择较低的分类级别的标签，提示用户提供理由

- 强制所有文档和电子邮件都具有标签

- 自定义页眉、页脚或水印

- 支持推荐选项和自动设置标签的条件

在此阶段，不要选择保护文档和电子邮件的选项。

### <a name="step-4-prepare-for-rights-management-data-protection"></a>步骤 4：准备 Rights Management 数据保护

当用户熟悉对文档和电子邮件添加标签后，就可以开始为最敏感的数据引入数据保护。 此阶段需要为 Azure Rights Management 服务准备以下工作：

1. 决定你是希望 Microsoft 管理你的租户密钥（默认设置），还是自行生成和管理你的租户密钥（也称为“自带密钥”，简称 BYOK）。 有关详细信息，请参阅[计划和实施 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

2. 至少在一台可以访问 Internet 的计算机上安装适用于 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]的 Windows PowerShell 模块。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[安装适用于 Azure Rights Management 服务的 Windows PowerShell](../deploy-use/install-powershell.md)。

3. 如果你当前正在使用本地 Rights Management Services：请执行移动密钥、模板和 URL 到云中的迁移操作。 有关详细信息，请参阅[从 AD RMS 迁移到信息保护](migrate-from-ad-rms-to-azure-rms.md)。

4. 确保 Azure Rights Management 服务已激活，以便开始保护文档和电子邮件。 如果需要分阶段部署，请配置用户载入控件以将其使用限于特定用户。 有关详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md)。

（可选）考虑进行以下配置：

-   自定义模板，前提是默认权限策略模式不足以满足你组织的要求。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](../deploy-use/configure-policy-templates.md)。

-   使用日志记录，以便你能够监控你组织使用权限管理的情况。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[记录和分析 Azure 权限管理服务的使用情况](../deploy-use/log-analyze-usage.md)。

### <a name="step-5-configure-your-azure-information-protection-policy-applications-and-services-for-rights-management-data-protection"></a>步骤 5：配置 Azure 信息保护策略、Rights Management 数据保护的应用程序和服务

1. 更新 Azure 信息保护策略以应用数据保护
    
    修改 Azure 信息保护策略，使一个或多个标签应用 Rights Management 保护。 有关详细信息，请参阅[如何配置标签以进行 Rights Management 保护](../deploy-use/configure-policy-protection.md)。
    
    请注意，即使没有为信息权限管理 (IRM) 配置 Exchange，用户也可以在应用 Rights Management 保护的 Outlook 中应用标签。 但是，在为 IRM 或[具有新功能的 Office 365 邮件加密](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)配置 Exchange 之前，你的组织将无法获得将 Exchange 与 Azure Rights Management 保护配合使用的完整功能。 此附加配置包含在以下列表中（对于 Exchange Online，则为 2；对于 Exchange 本地，则为 5）。 

2. 配置 Office 应用程序和服务
    
    在 SharePoint Online 或 Exchange Online 中为信息权限管理 (IRM) 功能配置 Office 应用程序和服务。 有关详细信息，请参阅[为 Azure Rights Management 配置应用程序](../deploy-use/configure-applications.md)。

3. 为数据恢复配置超级用户功能
    
    如果现有 IT 服务（例如数据泄漏防护 (DLP) 解决方案、内容加密网关 (CEG) 和反恶意软件产品）需要检查 Azure Rights Management 保护的文件，请将服务帐户配置为 Azure Rights Management 的超级用户。 有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)。

4. 批量分类和保护文件 - 按需而定
    
    PowerShell cmdlet 允许你对文件提供分类和保护以及删除分类和保护，随 Azure 信息保护客户端一起自动安装。 有关详细信息，请参阅管理员指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](..\rms-client\client-admin-guide-powershell.md)。

6. 部署适用于本地服务器的连接器
    
    如果你拥有想要与 Azure Rights Management 服务共同使用的本地服务，请安装和配置 Rights Management 连接器。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。

### <a name="step-6-use-and-monitor-your-data-protection-solutions"></a>第 6 步：使用和监视数据保护解决方案
现在，你可以保护数据，并记录公司如何使用已配置的标签和 Rights Management 数据保护。 有关支持此部署阶段的其他信息，请参阅以下内容：

- [使用 Azure Rights Management 服务帮助用户保护文件](../deploy-use/help-users.md)

-  [记录和分析 Azure 权限管理服务的使用情况](../deploy-use/log-analyze-usage.md)

- [客户端文件和使用情况日志记录](../rms-client/client-admin-guide-files-and-logging.md)

如果你对在基于 Windows 的文件服务器上使用文件分类基础结构自动保护文件感兴趣，请参阅[使用 Windows Server 文件分类基础结构 (FCI) 的 RMS 保护](../rms-client/configure-fci.md)。

### <a name="step-7-administer-the-rights-management-service-for-your-tenant-account-as-needed"></a>第 7 步：根据需要为租户帐户管理 Rights Management 服务
开始使用 Azure Rights Management 服务时，可能发现 Windows PowerShell 对帮助编写脚本或自动执行管理更改很有用。 有关详细信息，请参阅[使用 Windows PowerShell 管理 Azure Rights Management 服务](../deploy-use/administer-powershell.md)。


## <a name="deployment-roadmap-for-data-protection-only"></a>仅用于数据保护的部署路线图

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-azure-rights-management"></a>步骤 1：确认你有一个包含 Azure Rights Management 的订阅
查看 Azure 信息保护网站上的[订阅信息](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)和[功能列表](https://www.microsoft.com/cloud-platform/azure-information-protection-features)，以确认组织具有包含所需功能和特性的订阅。 然后，将该订阅中的许可证分配给组织中的每位用户，这些用户通过使用 Azure Rights Management 服务，保护文档和电子邮件。

注意：不要从个人订阅的免费 RMS 手动分配用户许可证，不要使用此许可证来管理组织的 Azure Rights Management 服务。 这些许可证在 Office 365 管理中心显示为 **Rights Management 即席**，当运行 Azure AD PowerShell cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) 时显示为 **RIGHTSMANAGEMENT_ADHOC**。 有关如何将个人订阅 RMS 自动授权和分配给用户的详细信息，请参阅[个人 RMS 和 Azure 信息保护](../understand-explore/rms-for-individuals.md)。


### <a name="step-2-prepare-your-tenant-to-use-the-azure-rights-management-service"></a>步骤 2：准备租户以使用 Azure 权限管理服务
开始使用[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]之前，请进行以下准备工作：

1.  确保 Office 365 租户包含 Azure 信息保护用来对组织中的用户进行身份验证和授权的用户帐户和组。 如有必要，请创建这些帐户和组，或者从本地目录同步这些帐户和组。 有关详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

2. 决定你是希望 Microsoft 管理你的租户密钥（默认设置），还是自行生成和管理你的租户密钥（也称为“自带密钥”，简称 BYOK）。 有关详细信息，请参阅[计划和实施 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

3. 至少在一台可以访问 Internet 的计算机上安装适用于 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]的 Windows PowerShell 模块。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[安装 AADRM PowerShell 模块](../deploy-use/install-powershell.md)。

4. 如果你当前正在使用本地 Rights Management Services：请执行移动密钥、模板和 URL 到云中的迁移操作。 有关详细信息，请参阅[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)。

5. 确保 Azure Rights Management 服务已激活，以便开始保护文档和电子邮件。 如果需要分阶段部署，请配置用户载入控件以将其使用限于特定用户。 有关详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md)。

（可选）考虑进行以下配置：

-   自定义模板，前提是默认模板不足以满足你组织的要求。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](../deploy-use/configure-policy-templates.md)。

- 使用日志记录，以便你能够监控你组织使用权限管理的情况。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[记录和分析 Azure 权限管理服务的使用情况](../deploy-use/log-analyze-usage.md)。

### <a name="step-3-install-the-client-and-configure-applications-and-services-for-rights-management"></a>步骤 3：安装客户端和配置要运行 Rights Management 的应用程序和服务

1. 部署 Azure 信息保护客户端
    
    为用户安装 Azure 信息保护，以支持 Office 2010、保护除 Office 文档和电子邮件以外的文件，并跟踪受保护文档。 提供此客户端的用户培训。 有关详细信息，请参阅[适用于 Windows 的 Azure 信息保护客户端](../rms-client/aip-client.md)。

2. 配置 Office 应用程序和服务
    
    在 SharePoint Online 或 Exchange Online 中为信息权限管理 (IRM) 功能配置 Office 应用程序和服务。 有关详细信息，请参阅[为 Azure Rights Management 配置应用程序](../deploy-use/configure-applications.md)。

3. 为数据恢复配置超级用户功能
    
    如果现有 IT 服务（例如数据泄漏防护 (DLP) 解决方案、内容加密网关 (CEG) 和反恶意软件产品）需要检查 Azure Rights Management 保护的文件，请将服务帐户配置为 Azure Rights Management 的超级用户。 有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)。

4. 批量保护文件 - 按需而定 
    
    PowerShell cmdlet 允许你批量保护或批量取消保护多个文件类型，随 Azure 信息保护客户端一起自动安装。 有关详细信息，请参阅管理员指南中的[将 PowerShell 与 Azure 信息保护客户端配合使用](..\rms-client\client-admin-guide-powershell.md)。

5. 部署适用于本地服务器的连接器
    
    如果你拥有想要与 Azure Rights Management 服务共同使用的本地服务，请安装和配置 Rights Management 连接器。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。


### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>步骤 4：使用和监视数据保护解决方案
现在，你可以保护数据，并记录公司如何使用 Rights Management。 有关支持此部署阶段的其他信息，请参阅[通过使用 Azure 权限管理服务帮助用户保护文件](../deploy-use/help-users.md)和[记录和分析 Azure 权限管理服务的使用情况](../deploy-use/log-analyze-usage.md)。

如果你对在基于 Windows 的文件服务器上使用文件分类基础结构自动保护文件感兴趣，请参阅[使用 Windows Server 文件分类基础结构 (FCI) 的 RMS 保护](../rms-client/configure-fci.md)。

### <a name="step-5-administer-the-rights-management-service-for-your-tenant-account-as-needed"></a>步骤 5：根据需要管理租户帐户的 Rights Management 服务
开始使用 Azure Rights Management 服务时，可能发现 Windows PowerShell 对帮助编写脚本或自动执行管理更改很有用。 有关详细信息，请参阅[使用 Windows PowerShell 管理 Azure Rights Management 服务](../deploy-use/administer-powershell.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
