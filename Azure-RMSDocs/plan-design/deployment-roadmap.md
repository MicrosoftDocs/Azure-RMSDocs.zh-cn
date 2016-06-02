---
# required metadata

title: Azure Rights Management 部署路线图 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Rights Management 部署路线图

*适用于：Azure Rights Management、Office 365*

使用以下步骤为你的组织准备、实现和管理 Azure Rights Management (Azure RMS)。

不过，如果你只想快速试用 Azure RMS，而不是将它部署在生产环境中，请参阅 [Azure Rights Management 快速入门教程](../get-started/quick-start-tutorial.md).

有关特定方案和关联的配置步骤和最终用户文档的列表，请参阅 [Azure Rights Management 快速部署指南](../get-started/rapid-deployment-guide.md).

> [!IMPORTANT]
> 在执行以下步骤之前，请确保已查看 [Azure Rights Management 的要求](../get-started/requirements-azure-rms.md).

## 步骤 1：确认你有一个包含 Azure Rights Management 的订阅
有多种类型的订阅包含 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]。 请参阅[支持 Azure RMS 的云订阅](../get-started/requirements-subscriptions.md)，并参考 [Rights Management Services (RMS) 产品比较](https://technet.microsoft.com/dn858608)中的表格，检查订阅是否包含你要在组织中使用的功能。 你将需要从此订阅中为组织内为使用 Azure RMS 保护文件和电子邮件的每位用户分配许可证。

## 步骤 2：准备你的租户帐户以便使用权限管理
开始使用[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]之前，请进行以下准备工作：

1.  确保 Azure 或 Office 365 租户包含 Azure RMS 用来对你组织中的用户进行身份验证的用户帐户和组。 如有必要，请创建这些帐户和组，或者从本地目录同步这些帐户和组。 有关详细信息，请参阅[准备 Azure Rights Management](prepare.md).

2.  决定你是希望 Microsoft 管理你的租户密钥（默认设置），还是自行生成和管理你的租户密钥（也称为“自带密钥”，简称 BYOK）。 请注意，如果你当前使用了 Exchange Online，则不能使用 BYOK。 有关详细信息，请参阅[计划和实施你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md).

3.  至少在一台可以访问 Internet 的计算机上安装适用于 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]的 Windows PowerShell 模块。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md).

4.  如果你当前正在使用本地 Rights Management Services：请执行移动密钥、模板和 URL 到云中的迁移操作。 有关详细信息，请参阅[从 AD RMS 迁移到 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).

5.  激活权限管理，然后即可使用该服务。 如果需要分阶段部署，请配置用户载入控件以将其使用限于特定用户。 有关详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md).

（可选）考虑进行以下配置：

-   自定义模板，前提是默认权限策略模式不足以满足你组织的要求。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[为 Azure Rights Management 配置自定义模板](../deploy-use/configure-custom-templates.md).

-   使用日志记录，以便你能够监控你组织使用权限管理的情况。 你可以立即执行此步骤，也可以稍后执行。 有关详细信息，请参阅[记录和分析 Azure Rights Management 使用情况](../deploy-use/log-analyze-usage.md).

## 步骤 3：配置要运行 Rights Management 的应用程序和服务
配置应用程序和服务的过程可能包括安装权限管理共享应用程序、在 SharePoint Online 或 Exchange Online 中启用对信息权限管理 (IRM) 功能的支持。 有关详细信息，请参阅[为 Azure Rights Management 配置应用程序](../deploy-use/configure-applications.md).

如果你的现有 IT 服务（例如数据泄漏防护 (DLP) 解决方案、内容加密网关 (CEG) 和反恶意软件产品）需要检查 Azure RMS 将要保护的文件，请将服务帐户配置为 Azure RMS 的超级用户。 有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md).

为了能够批量保护或批量取消保护所有文件类型，请安装 RMS 保护工具，该工具使用 RMS Protection PowerShell 模块。 有关详细信息，请参阅 [RMS 保护 Cmdlet](https://msdn.microsoft.com/library/mt433195.aspx).

如果你希望将 Azure 权限管理用于本地服务，请安装和配置权限管理连接器。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md).

## 步骤4：发布和使用受权限保护的内容
现在，你可以发布和使用受保护的内容，并记录公司如何使用 Rights Management。 有关详细信息，请参阅[使用Azure Rights Management 帮助用户保护文件](../deploy-use/help-users.md)和[记录和分析 Azure Rights Management 使用情况](../deploy-use/log-analyze-usage.md).

如果你对在基于 Windows 的文件服务器上使用文件分类基础结构自动保护文件感兴趣，请参阅 [使用 Windows Server 文件分类基础结构 (FCI) 的 RMS 保护](../rms-client/configure-fci.md).

## 步骤 5：根据需要管理租户帐户的权限管理
开始使用[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]时，你可能发现适用于 Windows PowerShell 的[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]模块可以帮助你编写脚本或自动执行管理更改。 有关详细信息，请参阅[使用 Windows PowerShell 管理 Azure Rights Management](../deploy-use/administer-powershell.md).




<!--HONumber=May16_HO2-->


