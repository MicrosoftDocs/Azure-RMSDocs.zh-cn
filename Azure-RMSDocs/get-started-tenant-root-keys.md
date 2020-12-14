---
title: 开始使用和管理你的租户根密钥
description: 了解规划租户根密钥管理之后的后续步骤，包括 Microsoft 和 BYOK protection 生成的默认密钥。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9756710e29c82ef953633697cb989942d1844496
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382235"
---
# <a name="getting-started-with-tenant-root-keys"></a>租户根密钥入门

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月31日** 被 **弃用**。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

根据需要 [规划、创建和配置你的租户密钥](plan-implement-tenant-key.md) 后，请继续执行以下步骤：

- [开始使用你的租户密钥](#start-using-your-tenant-key)
- [考虑使用日志记录](#consider-usage-logging)

有关租户密钥支持的生命周期操作的详细信息，请参阅 [Azure 信息保护租户密钥的操作](./operations-tenant-key.md)。

如果你的组织需要针对高度敏感内容的本地保护，请将 [DKE protection](plan-implement-tenant-key.md#double-key-encryption-dke) (仅) 的统一标签客户端。

如果需要本地保护并且使用的是经典客户端，请改为配置 [HYOK protection](configure-adrms-restrictions.md) 。
 

## <a name="start-using-your-tenant-key"></a>开始使用你的租户密钥

激活 Rights Management 服务（如果尚未激活）以使你的组织能够开始使用 Azure 信息保护。 用户立即开始使用你的租户密钥。

有关详细信息，请参阅[激活 Azure 信息保护的保护服务](./activate-service.md)。

> [!NOTE]
> 如果在激活 Rights Management 服务后决定管理自己的租户密钥，则在数周后，用户将从旧密钥逐渐过渡到新密钥。
>
>在此转换过程中，已获授权的用户仍可访问受旧租户密钥保护的文档和文件。

## <a name="consider-usage-logging"></a>考虑使用日志记录

使用量日志记录 Azure Rights Management 服务执行的每个事务。

根据你的密钥管理方法，日志记录信息可能包括有关你的租户密钥的详细信息。 下图显示了在 Excel 中显示的日志文件示例，其中 **KeyVaultDecryptRequest** 和 **KeyVaultSignRequest** 请求类型显示该租户密钥正在使用中。
    
![正在使用租户密钥的 Excel 格式日志文件](./media/RMS_Logging.png)
    
有关使用日志记录的详细信息，请参阅 [记录和分析 Azure 信息保护中的保护使用情况](./log-analyze-usage.md)。
