---
title: Azure 信息保护的符合性和信息
description: Azure 信息保护的支持信息，包括法律、合规性和 SLA。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 708d39a5f69182225a1eea23c625b4a53a7172cd
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2021
ms.locfileid: "102414746"
---
# <a name="compliance-and-supporting-information-for-azure-information-protection"></a>Azure 信息保护的合规性和支持信息

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
>相关内容：*[AIP 统一标记客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

Azure 信息保护支持其他服务，也依赖于其他服务。 如果你寻找的信息与 Azure 信息保护相关，但与如何使用 Azure 信息保护服务无关，请查看以下资源：

## <a name="suitability-for-different-countries"></a>对不同国家/地区的适用性

由于不同国家/地区间法律和法规的差异，不同用例和方案的区别，以及各业务部门要求的不同，请咨询法律顾问，了解Azure 信息保护是否适用于自己所在的国家/地区。

以下是有助于法律顾问做出决定的相关信息：

- Azure 信息保护使用 AES 256 和 AES 128 加密文档。 [详细信息](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- 使用特定于客户的根密钥（使用 RSA 2048 位）保护所有用于 Azure 信息保护的加密密钥。 RSA 1024 位也支持向后兼容。 [详细信息](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- 特定于客户的根密钥由 Microsoft 管理或由 nCipher HSM 中的客户设置，使用 "自带密钥" (BYOK) 。 Azure 信息保护还支持本地保护功能，适用于不能使用基于云的密钥保护的内容。 有关详细信息，请参阅[规划和实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

- Azure 信息保护服务托管在全球各地的区域数据中心内。 Azure 信息保护密钥和策略始终保留在最初的部署区域中。

    > [!NOTE]
    > Azure 信息保护策略仅适用于 AIP 经典客户端。
    >
  
- Azure 信息保护不会将文档内容从客户端传输到 Azure 信息保护服务。 内容加密和解密操作在客户端设备内就地执行。 或者，对基于服务的渲染而言，这些操作将在要渲染内容的服务中执行。 [详细信息](./how-does-it-work.md)

## <a name="legal-and-privacy"></a>法律和隐私

- 对于 Microsoft Azure 协议信息： [Microsoft Azure 协议](https://azure.microsoft.com/support/legal/subscription-agreement/)

- 对于 Microsoft Azure 隐私信息： [Microsoft Azure 隐私声明](https://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>安全、合规性和审核

有关 Azure Rights Management 服务的特定认证的信息，请参阅[什么是 Azure RMS？](./what-is-azure-rms.md)一文中的[安全、合规性和法规要求](./what-is-azure-rms.md#security-compliance-and-regulatory-requirements)部分。 此外：

- 对于 Azure 信息保护的外部认证：[Microsoft Azure 信任中心](https://azure.microsoft.com/support/trust-center/)

- 对于 FIPS 140 信息： [FIPS 140 验证](/windows/security/threat-protection/fips-140-validation)

若要详细了解保护技术如何工作的技术信息，请参阅 [Azure RMS 的工作原理](./how-does-it-work.md) 

## <a name="service-level-agreements"></a>服务级别协议

- [Azure 信息保护的 SLA](https://azure.microsoft.com/support/legal/sla/information-protection/v1_0/)

- [Azure Active Directory 的 SLA](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)

- [Azure Key Vault 的 SLA](https://azure.microsoft.com/support/legal/sla/key-vault/v1_0/)

## <a name="documentation"></a>文档

- Azure Active Directory 文档：[Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis)

- Microsoft 365 文档： [企业文档和资源 Microsoft 365](/Office365/Enterprise/)

