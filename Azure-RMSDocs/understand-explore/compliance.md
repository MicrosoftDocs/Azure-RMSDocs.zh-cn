---
title: Azure 信息保护的符合性和信息
description: Azure 信息保护的支持信息，包括法律、合规性和 SLA。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/12/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b19b118a700f86c89ce1b727a4f75c1c7017d2c8
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39369786"
---
# <a name="compliance-and-supporting-information-for-azure-information-protection"></a>Azure 信息保护的合规性和支持信息

Azure 信息保护支持其他服务，也依赖于其他服务。 如果你寻找的信息与 Azure 信息保护相关，但与如何使用 Azure 信息保护服务无关，请查看以下资源：

## <a name="suitability-for-different-countries"></a>对不同国家/地区的适用性

由于不同国家/地区间法律和法规的差异，不同用例和方案的区别，以及各业务部门要求的不同，请咨询法律顾问，了解Azure 信息保护是否适用于自己所在的国家/地区。

以下是有助于法律顾问做出决定的相关信息：

- Azure 信息保护使用 AES 256 和 AES 128 加密文档。 [详细信息](../understand-explore/how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- 使用特定于客户的根密钥（使用 RSA 2048 位）保护所有用于 Azure 信息保护的加密密钥。 但 RSA 1024 也支持向后兼容。 [详细信息](../understand-explore/how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- 特定于客户的根密钥由 Microsoft 托管，或由 Thales HSM 中的客户通过使用“[自带密钥](../plan-design/plan-implement-tenant-key.md)”(BYOK) 进行预配。 Azure 信息保护还支持本地密钥的有限功能 - 使用“[保留自己的密钥](../deploy-use/configure-adrms-restrictions.md)”(HYOK) 用于指示其不能使用基于云的密钥保护的要求影响的内容。

- Azure 信息保护服务托管在全球各地的区域数据中心内。 Azure 信息保护密钥和策略始终保留在最初的部署区域中。
 
- Azure 信息保护不会将文档内容从客户端传输到 Azure 信息保护服务。 内容加密和解密操作在客户端设备内就地执行。 或者，对基于服务的渲染而言，这些操作将在要渲染内容的服务中执行。 [详细信息](../understand-explore/how-does-it-work.md)

## <a name="legal-and-privacy"></a>法律和隐私

- 对于 Microsoft Azure 协议信息： [Microsoft Azure 协议](http://azure.microsoft.com/support/legal/subscription-agreement/)

- 对于 Microsoft Azure 隐私信息： [Microsoft Azure 隐私声明](http://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>安全、合规性和审核

请参阅 [Azure RMS 解决了哪些问题？](../understand-explore/azure-rms-problems-it-solves.md)一文中的[安全、合规性和法规要求](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements)，了解有关特定 Azure 权限管理服务证书的信息。 此外：

- 对于 Azure 信息保护的外部认证：[Microsoft Azure 信任中心](http://azure.microsoft.com/support/trust-center/)

- 对于 FIPS 140 信息： [FIPS 140 验证](https://technet.microsoft.com/library/security/cc750357.aspx)

若要详细了解保护技术如何工作的技术信息，请参阅 [Azure RMS 的工作原理](../understand-explore/how-does-it-work.md) 

## <a name="service-level-agreements"></a>服务级别协议

- [Azure 信息保护的 SLA](https://azure.microsoft.com/support/legal/sla/information-protection/v1_0/)

- [Azure Active Directory 的 SLA](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)

- [Azure Key Vault 的 SLA](https://azure.microsoft.com/support/legal/sla/key-vault/v1_0/)

## <a name="documentation"></a>文档

- Azure Active Directory 文档：[Azure Active Directory](/active-directory/)

- Office 365 库：[Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

