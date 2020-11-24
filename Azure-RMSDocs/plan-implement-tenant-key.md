---
title: 你的 Azure 信息保护租户密钥
description: 你可能想要创建和管理 Azure 信息保护的根密钥，而不是 Microsoft 管理 Azure 信息保护的根密钥，这 (称为 "自带密钥" 或 BYOK) 。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 24479014fcbd0bd93b65d6958d004deb9c7e0c95
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "95566220"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>计划和实施 Azure 信息保护租户密钥

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

Azure 信息保护租户密钥是组织的根密钥。 其他密钥可以从该根密钥派生，包括用户密钥、计算机密钥或文档加密密钥。 每当 Azure 信息保护对你的组织使用这些密钥时，它们将通过加密方式链接到你的 Azure 信息保护根租户密钥。

除了租户根密钥外，你的组织可能需要特定文档的本地安全性。 对于少量内容，通常只需要本地密钥保护，因此与租户根密钥一起配置。

## <a name="azure-information-protection-key-types"></a>Azure 信息保护密钥类型

租户根密钥可以是：

- [由 Microsoft 生成](#tenant-root-keys-generated-by-microsoft)
- 由具有 [创建自己的密钥 (BYOK) ](#bring-your-own-key-byok-protection) 保护的客户生成。

每个 AIP 客户端类型的本地密钥管理不同。 如果具有要求额外的本地保护的高度敏感内容，请使用以下方法之一：

- 仅[保留你自己的密钥 (HYOK) ](#hold-your-own-key-hyok-aip-classic-client-only) (经典客户端) 
- [双密钥加密 (DKE) ](#double-key-encryption-dke-aip-unified-labeling-client-only) 仅 (统一标签客户端) 

仅当您使用的是经典客户端时，才能使用 HYOK 保护对内容进行加密。 但是，如果你有 HYOK 保护的内容，则可以在经典标签客户端和统一标签客户端中查看该内容。 

> [!TIP]
> 不确定经典客户端和统一标签客户端之间的差异吗？ 有关详细信息，请参阅此 [常见问题](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。
>

## <a name="tenant-root-keys-generated-by-microsoft"></a>Microsoft 生成的租户根密钥

由 Microsoft 自动生成的默认密钥是专用于 Azure 信息保护的默认密钥，用于管理租户密钥生命周期的大多数方面。

如果希望快速部署 Azure 信息保护，而无需特殊的硬件、软件或 Azure 订阅，请继续使用默认的 Microsoft 密钥。 示例包括测试环境或组织，无需对密钥管理进行法规要求。

对于默认密钥，无需执行其他步骤，你可以直接转到 [你的租户根密钥](get-started-tenant-root-keys.md)入门。

> [!NOTE]
> Microsoft 生成的默认密钥是具有最低管理开销的最简单选项。
>
> 在大多数情况下，你可能不知道你具有租户密钥，因为你可以注册 Azure 信息保护，并且其他密钥管理过程的剩余部分将由 Microsoft 处理。

## <a name="bring-your-own-key-byok-protection"></a>创建自己的密钥 (BYOK) 保护

BYOK-保护使用客户在 Azure Key Vault 或本地在客户组织中创建的密钥。 然后，这些密钥将传输到 Azure Key Vault 以便进一步管理。

当你的组织具有密钥生成的符合性规则（包括对所有生命周期操作的控制）时，请使用 BYOK。 例如，当你的密钥必须受硬件安全模块保护时。

有关详细信息，请参阅 [CONFIGURE BYOK protection](byok-price-restrictions.md)。 

配置后，请继续 [使用你的租户根密钥](get-started-tenant-root-keys.md) 入门，了解有关使用和管理你的密钥的详细信息。

## <a name="hold-your-own-key-hyok-aip-classic-client-only"></a>仅保留你自己的密钥 (HYOK)  (AIP 经典客户端) 

HYOK-保护使用客户在与云隔离的位置创建和保留的密钥。 由于 HYOK 只允许访问本地应用程序和服务的数据，因此使用 HYOK 的客户也有基于云的云文档密钥。

对以下文档使用 HYOK：

- 仅限于少数人
- 不在组织外共享
- 仅在内部网络上使用。

这些文档通常在你的组织中具有最高的分类，作为 "顶级机密"。

有关详细信息，请参阅 [保存你自己的密钥 (HYOK) 详细](configure-adrms-restrictions.md)信息。

## <a name="double-key-encryption-dke-aip-unified-labeling-client-only"></a>双密钥加密 (DKE)  (仅限 AIP 统一标签客户端) 

DKE 保护通过使用以下两个密钥来为你的内容提供附加的安全性：一个密钥由 Microsoft 在 Azure 中创建和保留，另一个由客户创建和保留在本地。

DKE 要求使用这两个密钥来访问受保护的内容，确保 Microsoft 和其他第三方决不会有权访问受保护的数据。

可以在云中或本地部署 DKE，为存储位置提供完全的灵活性。

在你的组织中使用 DKE：

- 希望确保只有在所有情况下，才可以对受保护的内容进行解密。
- 不希望 Microsoft 自行访问受保护的数据。
- 具有在地理边界内保存密钥的法规要求。 通过 DKE，客户持有的密钥在客户数据中心内维护。

> [!NOTE]
> DKE 类似于要求使用银行密钥和客户密钥才能获得访问权限的安全接入框。
> DKE-保护需要 Microsoft 持有的密钥和客户持有的密钥来解密受保护的内容。

有关详细信息，请参阅 Microsoft 365 文档中的 [双密钥加密](/microsoft-365/compliance/double-key-encryption) 。