---
title: BYOK 详细信息-Azure 信息保护
description: 使用客户托管的密钥（称为 "自带密钥" 或 BYOK）与 Azure 信息保护配合使用来了解详细信息和限制。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d94783b491dd9ff0b099a68e009809cd7ec965fb
ms.sourcegitcommit: 479b3aaea7011750ff85a217298e5ae9185c1dd1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82224557"
---
# <a name="bring-your-own-key-byok-details-for-azure-information-protection"></a>Azure 信息保护的自带密钥（BYOK）详细信息

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


具有包含 Azure 信息保护的订阅的组织可以将其 Azure 信息保护租户配置为使用客户托管的密钥并[记录其使用情况](log-analyze-usage.md)。 客户托管的密钥配置通常称为 "携带你自己的密钥" 或 BYOK。

此客户托管密钥必须存储在 Azure Key Vault 中，这需要 Azure 订阅。 若要使用受 HSM 保护的密钥，则必须使用 Azure Key Vault 高级服务层。 在 Azure 密钥保管库中使用密钥会按月产生费用。 有关详细信息，请参阅[Azure Key Vault 定价页](https://azure.microsoft.com/pricing/details/key-vault/)。

为 Azure 信息保护租户密钥使用 Azure Key Vault 时，建议为此密钥使用专用密钥保管库，帮助确保只有 Azure Rights Management 服务能使用它。 此配置可确保其他服务的调用不会导致超出密钥保管库的[服务限制](/azure/key-vault/key-vault-service-limits)，否则可能会限制 Azure Rights Management 服务的响应时间。  

此外，由于每个使用 Azure Key Vault 的服务通常具有不同的密钥管理需求，因此建议为此密钥保管库使用单独的 Azure 订阅，帮助防止配置错误。 

但是，如果希望与使用 Azure Key Vault 的其他服务共享 Azure 订阅，请确保该订阅共用一组通用的管理员。 此预防措施意味着，使用该订阅的管理员非常了解他们有权访问的所有密钥，因此他们不太可能在配置时犯错。 

例如，如果 Azure 信息保护租户密钥的管理员同时负责管理 Office 365 Customer Key 和 CRM Online 密钥，则建议共享 Azure 订阅。 

或者，如果管理客户密钥或 CRM Online 密钥的管理员不是管理 Azure 信息保护租户密钥的人员，则我们建议你不要共享 azure 信息保护的 Azure 订阅。

## <a name="benefits-of-using-azure-key-vault"></a>使用 Azure 密钥保管库的好处

为了进一步确保，可以使用[Azure Key Vault 日志记录](/azure/key-vault/key-vault-logging)来交叉引用 Azure 信息保护使用情况日志记录。 Key Vault 日志提供了一个方法，用于独立监视 Azure Rights Management 服务是否正在使用你的密钥。 如有必要，可以通过删除密钥保管库上的权限来立即撤消对密钥的访问权限。

使用 Azure 信息保护租户密钥 Azure Key Vault 的其他好处包括：

- Azure 密钥保管库提供了一种集中式的密钥管理解决方案，这为许多使用加密的基于云甚至是本地的服务提供了一种一致的管理解决方案。

- Azure 密钥保管库为密钥管理提供了大量内置接口，包括 PowerShell、CLI、REST API 和 Azure 门户。 其他已经与密钥保管库集成的服务和工具 - 用于提供为特定任务而优化的功能（如监视） 例如，可以从 Operations Management Suite 中通过 Log Analytics 来分析密钥使用情况日志，设置在遇到指定条件时发出警报等。

- 作为广受认可的安全性最佳实践，Azure 密钥保管库提供角色分离。 Azure 信息保护管理员可专注于管理数据分类和保护，Azure 密钥保管库管理员则可专注于管理加密密钥和任何有可能要求安全性或合规性的特殊策略。

- 某些组织对其主密钥在何处生存有所限制。 由于该服务在许多 Azure 区域内都可用，因此 Azure 密钥保管库可提供对主密钥存储位置的高级别控制。 你可以从多个 Azure 区域中进行选择，并且你会希望此数字增加。 有关详细信息，请参阅 Azure 网站上的[可用产品（按区域）](https://azure.microsoft.com/regions/services/)页。

除管理密钥外，Azure 密钥保管库还为安全管理员提供其他使用加密的服务和应用程序的存储、访问、管理证书和机密（如密码）的相同管理体验。 

有关 Azure 密钥保管库的详细信息，请参阅[什么是 Azure 密钥保管库？](/azure/key-vault/key-vault-whatis)并访问 [Azure 密钥保管库团队博客](https://blogs.technet.microsoft.com/kv/)，以获取最新信息并了解其他服务如何使用此技术。

## <a name="byok-support-for-services-and-clients"></a>服务和客户端的 BYOK 支持

BYOK 和[使用情况日志记录](log-analyze-usage.md)与 Azure 信息保护用于保护数据的 azure Rights Management 服务所集成的每个应用程序无缝协作。 其中包括 SharePoint Online 等云服务、运行 Exchange 和 SharePoint 的本地服务器（它们通过使用 RMS 连接器来使用 Azure Rights Management 服务）、Office 2019、Office 2016 和 Office 2013 等客户端应用程序。 

无论应用程序向 Azure Rights Management 服务发出请求，都可以获取密钥使用情况日志。

## <a name="next-steps"></a>后续步骤

如果已决定管理自己的密钥，请转到[实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key)。

如果已决定保留默认配置，让 Microsoft 管理租户密钥，请参阅“计划和实现 Azure 信息保护租户密钥”一文中的[后续步骤](plan-implement-tenant-key.md#next-steps)。

