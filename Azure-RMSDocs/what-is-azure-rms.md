---
title: Azure 权限管理是什么？ - AIP
description: 介绍 Azure Rights Management (Azure RMS)，它是由 Azure 信息保护使用的保护技术。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/22/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aeeebcd7-6646-4405-addf-ee1cc74df5df
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 36f8a3abfb93c08e9ff78bb738b6db3e734736de
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2021
ms.locfileid: "102415222"
---
# <a name="what-is-azure-rights-management"></a>Azure 权限管理是什么？

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>相关内容：*[AIP 统一标记客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

Azure Rights Management (Azure RMS) 是 [Azure 信息保护](what-is-information-protection.md)使用的基于云的保护技术。 

Azure RMS 通过使用加密、标识和授权策略来帮助跨多个设备（包括手机、平板电脑和 PC）[保护](./rms-client/clientv2-classify-protect.md)文件和电子邮件。

例如，当员工将文档通过电子邮件发送给合作伙伴公司，或者将文档保存到云驱动器时，Azure RMS 的永久性保护有助于保护数据。

- 保护设置会始终作用于你的数据，即使数据越过组织的边界，这些设置也会使你的内容在组织内外都受到保护。

- Azure RMS 可能是实现合规性、法律发现要求或信息管理最佳做法所需执行的合法措施。

- 将 Azure RMS 用于 Microsoft 365 订阅或 Azure 信息保护订阅。 有关单独订阅类型和支持的功能的详细信息，请参阅 [Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection/)网站。

Azure RMS 确保经过授权的人员和服务（例如搜索和索引）可以继续读取和检查受保护的数据。

确保维护经过授权的人员和服务的持续访问权限，这也称为“数据推理”，是保持对组织数据进行控制的关键因素。 无法通过其他使用对等加密的信息保护解决方案轻松实现此功能。
## <a name="protection-features"></a>保护功能

|功能  |说明  |
|---------|---------|
|**保护多个文件类型**     | 在 Rights Management 的早期实现中，只有 Office 文件才能使用内置 Rights Management 保护功能获得保护。 </br></br>Azure 信息保护为其他文件类型提供支持。 有关详细信息，请参阅[支持的文件类型](rms-client/clientv2-admin-guide-file-types.md)。         |
|**随时随地保护文件** | 文件一旦[受保护](./rms-client/clientv2-classify-protect.md)，便会始终受到保护，即使它被保存或复制到不受 IT 部门控制的存储（如云存储服务），也是如此。|
|     |         |


## <a name="collaboration-features"></a>协作功能

|功能  |说明  |
|---------|---------|
|**安全共享信息**     |  可以与他人安全共享[受保护的文件](./rms-client/clientv2-classify-protect.md)，例如电子邮件的附件或指向 SharePoint 站点的链接。 </br></br> 如果电子邮件中有敏感信息，则可以保护电子邮件，或使用 Outlook 中的“不要转发”选项。       |
|**支持企业与企业之间的协作**     |  由于 Azure Rights Management 是云服务，因此在与其他组织共享受保护内容前，不需要显式配置与这些组织的信任关系。 </br></br>自动支持与已有 Microsoft 365 或 Azure AD 目录的其他组织协作。 </br></br>对于没有 Microsoft 365 或 Azure AD 目录的组织，用户可以注册免费的[个人 RMS](rms-for-individuals.md) 订阅，也可以将 Microsoft 帐户用于[受支持的应用程序](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)。       |
| | |

> [!TIP]
> 附加受保护的文件，而不是保护整个电子邮件，使你能够将电子邮件文本保持未加密状态。 
>
> 例如，如果要将电子邮件发送到组织外部，可能需要包含首次使用说明。 如果你附加受保护的文件，任何人都可以读取基本说明，但只有授权用户才能打开文档，即使将该电子邮件或文档转发给其他用户也是如此。

## <a name="platform-support-features"></a>平台支持功能

Azure RMS 支持广泛的平台和应用程序，包括：

|功能  |说明  |
|---------|---------|
|**常用设备** </br>不止是 Windows 计算机     | [客户端设备](requirements.md#client-devices)包括： </br></br>- Windows 计算机和手机 </br>- Mac 计算机 </br>- iOS 平板电脑和手机 </br>- Android 平板电脑和手机        |
|**本地服务**     | Azure Rights Management 除了[与 Office 365 无缝集成](office-apps-services-support.md)以外，在部署 [RMS 连接器](deploy-rms-connector.md)时，还可以将 Azure Rights Management 与以下本地服务结合使用： </br></br>- Exchange Server </br>- SharePoint Server </br>- 运行文件分类基础结构的 Windows Server        |
|**应用程序扩展性**     |Azure Rights Management 可与 Microsoft Office 应用程序和服务紧密集成，并使用 [Azure 信息保护客户端](./rms-client/use-client.md )扩展对其他应用程序的支持。 </br></br>[Microsoft 信息保护 SDK](/information-protection/develop/) 为内部开发人员和软件供应商提供了 API，用于编写支持 Azure 信息保护的自定义应用程序。 </br></br>有关详细信息，请参阅[支持 Rights Management API 的其他应用程序](api-support.md)。         |
| | |

## <a name="infrastructure-features"></a>基础结构功能

Azure RMS 提供了以下功能来支持 IT 部门和基础结构组织：

- [创建简单灵活的策略](#create-simple-and-flexible-policies)
- [轻松激活](#easy-activation)
- [审核和监视服务](#auditing-and-monitoring-services)
- [能够在整个组织内扩展](#ability-to-scale-across-your-organization)
- [保持对数据的 IT 控制](#maintain-it-control-over-data)

> [!NOTE]
> 组织始终可以选择停止使用 Azure Rights Management 服务，而不会失去对以前受 Azure Rights Management 保护的内容的访问权限。 
> 
> 有关详细信息，请参阅[解除 Azure Rights Management 授权和停用 Azure Rights Management](decommission-deactivate.md)。 
> 

#### <a name="create-simple-and-flexible-policies"></a>创建简单灵活的策略

自定义保护模板提供了一款便捷的解决方案。通过该解决方案，管理员可以应用策略，用户可以对每个文档应用适当级别的保护，并将访问权限限制给组织内部人员。 

例如，为了与所有员工共享公司范围内的策略文档，可对所有内部员工应用只读策略。 对于更敏感的文档，如财务报表，可将访问权限仅限制为高级管理人员。

在标记管理中心配置标记策略：

- **统一标记客户端**：使用 Microsoft 365 安全中心、Microsoft 365 合规中心或 Microsoft 365 安全与合规中心。

    有关详细信息，请参阅 [Microsoft 365 敏感度标记文档](/microsoft-365/compliance/sensitivity-labels#what-label-policies-can-do)。        

- **经典客户端**：使用 Azure 门户。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)。      


#### <a name="easy-activation"></a>轻松激活

对于新订阅，激活是自动进行的。 对于现有订阅，只需在管理门户中单击几下鼠标，或单击两条 PowerShell 命令即可[激活 Rights Management 服务](activate-service.md)。

#### <a name="auditing-and-monitoring-services"></a>审核和监视服务

[审核和监视受保护文件的使用情况](log-analyze-usage.md)，即使这些文件已经越过了组织的边界也是如此。 

例如，如果 Contoso, Ltd 的员工与来自 Fabrikam, Inc 的三个人在合作一个项目，他们可能会向 Fabrikam 合作伙伴发送一份受保护且限制为只读的文档。 

Azure RMS 审核功能可以提供以下信息：

- Fabrikam 合作伙伴是否打开了该文档，以及何时打开了。 

- 其他未指定的人员是否尝试打开文档并且失败。 如果电子邮件转发或保存到共享位置，则可能会发生这种情况。

> [!NOTE]
> [文档跟踪站点](./rms-client/client-track-revoke.md)可让用户和管理员跟踪并在必要时撤销对受保护文档的访问，这仅适用于经典客户端用户。
> 

#### <a name="ability-to-scale-across-your-organization"></a>能够在整个组织内扩展

由于 Azure Rights Management 可作为云服务运行并借助 Azure 灵活地向上和向外扩展，因此，不需要设置或部署其他本地服务器。

#### <a name="maintain-it-control-over-data"></a>保持对数据的 IT 控制

组织可通过 IT 控制功能受益，例如：

|功能  |说明  |
|---------|---------|
|**租户密钥管理**    | 使用租户密钥管理解决方案，如创建自己的密钥 (BYOK) 或双重密钥加密 (DKE)。 <br><br>有关详细信息，请参阅： <br>- [计划和实现你的 AIP 租户密钥](plan-implement-tenant-key.md) <br>- [Microsoft 365 文档中的 DKE](/microsoft-365/compliance/double-key-encryption)。|
|**审核和使用情况日志记录**    |   使用审核和[使用情况日志记录](log-analyze-usage.md)功能进行分析以获得业务见解，通过监视信息来了解滥用情况，并针对信息泄露执行取证分析。      |
|**访问委托**     |  使用[超级用户功能](configure-super-users.md)委托访问，确保 IT 部门始终可以访问受保护的内容，即使文档是由后来从组织离职的员工实施保护的也是如此。 </br> 相比之下，使用对等加密解决方案会面临丧失公司数据访问权限的风险。       |
|**Active Directory 同步**     |   仅同步 [Azure RMS 所需的目录属性](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms)即可对本地 Active Directory 帐户使用通用标识，而且只需使用[混合标识解决方案](/azure/active-directory/hybrid/)（例如 Azure AD Connect）即可。      |
|**单一登录**     | 使用 AD FS 来启用单一登录，而无需将密码复制到云中。        |
|**从 AD RMS 迁移** |如果你已部署了 Active Directory Rights Management Services (AD RMS)，[迁移到 Azure 权限管理服务](migrate-from-ad-rms-to-azure-rms.md)，而不会失去对以前受 AD RMS 保护的数据的访问权限。 |
| | |


## <a name="security-compliance-and-regulatory-requirements"></a>安全、合规性和法规要求
Azure Rights Management 支持以下安全性、合规性和法规要求：

- **使用符合业界标准的加密功能，并支持 FIPS 140-2。** 有关详细信息，请参阅 [Azure RMS 使用的加密控制：算法和密钥长度](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths) 信息。

- **支持 nCipher nShield 硬件安全模块 (HSM)** 将租户密钥存储在 Microsoft Azure 数据中心内。 

    Azure 权限管理对北美、EMEA（欧洲、中东和非洲）和亚洲的数据中心使用单独的安全体系，因此，你的密钥只能在你所在的地区使用。

- 以下标准的认证：

    -   ISO/IEC 27001:2013（./包括 [ISO/IEC 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/)）
    -   SOC 2 SSAE 16/ISAE 3402 证明
    -   HIPAA BAA
    -   欧盟示范条款
    -   作为 Office 365 认证中的 Azure Active Directory 的一部分，FedRAMP 已通过 HHS 操作 FedRAMP Agency
    -   PCI DSS 1 级

有关这些外部认证的详细信息，请参阅 [Azure 信任中心](https://azure.microsoft.com/support/trust-center/compliance/)。


## <a name="next-steps"></a>后续步骤

有关更多 Azure 权限管理服务工作原理的技术信息，请参阅 [Azure RMS 的工作原理](how-does-it-work.md)

如果你熟悉本地版的权限管理和 Active Directory Rights Management 服务 (AD RMS)，则可能会对 [比较 Azure Rights Management 和 AD RMS](compare-on-premise.md) 中的比较表感兴趣。
