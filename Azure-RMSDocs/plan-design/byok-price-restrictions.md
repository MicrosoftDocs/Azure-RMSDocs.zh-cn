---
title: "BYOK 定价和限制 - Azure 信息保护"
description: "了解结合使用客户托管的密钥（称为“自带密钥”或 BYOK）与 Azure 信息保护时的限制。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: afc25e638cff4bddc342ed29dee7fab304d67bd7
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2017
---
# <a name="byok-pricing-and-restrictions"></a>BYOK 定价和限制

>*适用于：Azure 信息保护、Office 365*


拥有订阅（包含 Azure 信息保护）的组织可以将 Azure 信息保护租户配置为使用客户托管的密钥 (BYOK)，并[记录其使用情况](../deploy-use/log-analyze-usage.md)（无需额外付费）。 

密钥必须存储在 Azure Key Vault 中（Azure Key Vault 需要 Azure 订阅）。 若要使用受 HSM 保护的密钥，则必须使用 Azure Key Vault 高级服务层。 在 Azure 密钥保管库中使用密钥会按月产生费用。 有关详细信息，请参阅 [Azure 密钥保管库定价页](https://azure.microsoft.com/en-us/pricing/details/key-vault/)。

为 Azure 信息保护租户密钥使用 Azure Key Vault 时，建议为此密钥使用具有专用订阅的专用密钥保管库。 此配置有助于确保它仅被 Azure Rights Management 服务使用。 

## <a name="benefits-of-using-azure-key-vault"></a>使用 Azure 密钥保管库的好处

除使用 Azure 信息保护使用情况日志记录之外，为实现额外的保证，你还可以使用 [Azure 密钥保管库日志记录](https://azure.microsoft.com/documentation/articles/key-vault-logging/)对其进行交叉引用，从而独立监视，确保只有 Azure 权限管理服务使用此密钥。 如有必要，可以通过删除密钥保管库上的权限来立即撤消对密钥的访问权限。

将 Azure 密钥保管库用于 Azure 信息保护租户密钥的其他好处：

- Azure 密钥保管库提供了一种集中式的密钥管理解决方案，这为许多使用加密的基于云甚至是本地的服务提供了一种一致的管理解决方案。

- Azure 密钥保管库为密钥管理提供了大量内置接口，包括 PowerShell、CLI、REST API 和 Azure 门户。 其他已经与密钥保管库集成的服务和工具 - 用于提供为特定任务而优化的功能（如监视） 例如，可以从 Operations Management Suite 中通过 Log Analytics 来分析密钥使用情况日志，设置在遇到指定条件时发出警报等。

- 作为广受认可的安全性最佳实践，Azure 密钥保管库提供角色分离。 Azure 信息保护管理员可专注于管理数据分类和保护，Azure 密钥保管库管理员则可专注于管理加密密钥和任何有可能要求安全性或合规性的特殊策略。

- 某些组织对其主密钥在何处生存有所限制。 由于该服务在许多 Azure 区域内都可用，因此 Azure 密钥保管库可提供对主密钥存储位置的高级别控制。 目前，可以从 28 个区域中进行选择，而且这个数字还将不断地增加。 有关详细信息，请参阅 Azure 网站上的 [可用产品(按区域)] 页 (https://azure.microsoft.com/regions/services/)。

除管理密钥外，Azure 密钥保管库还为安全管理员提供其他使用加密的服务和应用程序的存储、访问、管理证书和机密（如密码）的相同管理体验。 

有关 Azure 密钥保管库的详细信息，请参阅[什么是 Azure 密钥保管库？](/azure/key-vault/key-vault-whatis)并访问 [Azure 密钥保管库团队博客](https://blogs.technet.microsoft.com/kv/)，以获取最新信息并了解其他服务如何使用此技术。

## <a name="restrictions-when-using-byok"></a>使用 BYOK 时的限制

BYOK 和使用情况日志记录可无缝地适用于与 Azure 信息保护使用的 Azure Rights Management 服务集成的每个应用程序。 其中包括 SharePoint Online 等云服务、运行 Exchange 和 SharePoint 的本地服务器（它们通过使用 RMS 连接器来使用 Azure Rights Management 服务）、Office 2016 和 Office 2013 等客户端应用程序。 无论哪个应用程序请求 Azure Rights Management 服务，你都将获得密钥使用情况日志。

如果先前已通过从 Azure RMS 导入受信任的发布域 (TPD) 启用了 Exchange Online IRM，请按照 [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)（设置构建在 Azure 信息保护之上新的 Office 365 邮件加密功能）中的说明，在支持将 BYOK 用于 Azure 信息保护的 Exchange Online 中启用这些新功能。

## <a name="next-steps"></a>后续步骤

如果你已决定管理自己的密钥，转至[实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key)。

如果你已决定保留默认配置，让 Microsoft 管理你的租户密钥，请参阅“计划和实现你的 Azure Rights Management 租户密钥”文章中的[后续步骤](plan-implement-tenant-key.md#next-steps)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
