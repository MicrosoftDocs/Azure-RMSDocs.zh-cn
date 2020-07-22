---
title: Azure Rights Management 保护概述-AIP
description: 介绍 Azure Rights Management (Azure RMS)，它是由 Azure 信息保护使用的保护技术。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/21/2020
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
ms.openlocfilehash: 6c479bbb5f63bbbdc98165bc0c99f43a4e9503b4
ms.sourcegitcommit: 16d2c7477b96c5e8f6e4328a61fe1dc3d12c878d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86927397"
---
# <a name="what-is-azure-rights-management"></a>Azure 权限管理是什么？

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Rights Management（通常缩写为 Azure RMS）是 [Azure 信息保护](what-is-information-protection.md)使用的保护技术。

Azure RMS 是一种基于云的保护服务，它使用加密、标识和授权策略来帮助跨多个设备（包括手机、平板电脑和 Pc）保护文件和电子邮件。 保护设置会保留你的数据，即使它离开组织的边界，也会使你的内容在组织内部和外部都受到保护。

下图显示了 Azure RMS 如何为 Office 365 以及本地服务器和服务提供保护。 运行 Windows、macOS、iOS 和 Android 的常用最终用户设备也支持保护。

![Azure RMS 工作方式](./media/AzRMS_elements.png)

将 Azure RMS 用于 Azure 信息保护的 Office 365 订阅或订阅。 有关单独订阅类型和支持的功能的详细信息，请参阅[Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection/)站点。

### <a name="sample-azure-rms-use-case"></a>示例 Azure RMS 用例

员工可以通过电子邮件将文档发送给合作伙伴公司，或者将文档保存到云驱动器。

使用 Azure RMS 的持续保护有助于保护公司数据，并且还可能需要遵守法规、法律发现要求或信息管理的最佳做法。

Azure RMS 确保授权人员和服务（如搜索和索引）可以继续读取和检查受保护的数据。

确保对经过授权的人员和服务的持续访问，也称为 "数据推理"，是保持对组织数据进行控制的关键因素。 使用对等加密的其他信息保护解决方案可能无法轻松实现此功能。 

## <a name="business-problems-solved-by-azure-rights-management"></a>通过 Azure Rights Management 解决的业务问题

使用以下列表和表来确定你的组织在保护文档和电子邮件方面可能遇到的业务要求或问题，以及 Azure Rights Management 技术如何满足你的需求。

- [保护功能](#protection-features)
- [协作功能](#collaboration-features)
- [平台支持功能](#platform-support-features)
- [基础结构功能](#infrastructure-features)

> [!TIP]
> 如果你熟悉 Rights Management 的本地版本，Active Directory Rights Management Services （AD RMS），则可能会对比较[Azure Rights Management 和 AD RMS](compare-on-premise.md)的比较表感兴趣。

### <a name="protection-features"></a>保护功能

|功能  |说明  |
|---------|---------|
|**保护多个文件类型**     | 在 Rights Management 的早期实现中，只有 Office 文件才能使用本机 Rights Management 保护进行保护。 </br></br>现在，Rights Management 共享应用程序最初提供的一般保护功能，现在由 Azure 信息保护客户端提供，这意味着支持更多的[文件类型](./rms-client/client-admin-guide-file-types.md)。        |
|在**任何位置保护文件**。 | 如果文件[受到保护](./rms-client/client-classify-protect.md)，保护将保留在文件中，即使保存或复制到不受 it 控制的存储（如云存储服务）。|
|     |         |


### <a name="collaboration-features"></a>协作功能

|功能  |说明  |
|---------|---------|
|**安全共享信息**     |  [受保护的文件](./rms-client/client-classify-protect.md)可以安全地与他人共享，例如电子邮件的附件或 SharePoint 站点的链接。 </br></br> 如果敏感信息在电子邮件中，则保护电子邮件，或使用 Outlook 中的 "不**转发**" 选项。       |
|**支持企业与企业之间的协作**     |  由于 Azure Rights Management 是一种云服务，因此在与其他组织共享受保护的内容之前，不需要显式配置与这些组织的信任关系。 </br></br>自动支持与已具有 Office 365 或 Azure AD 目录的其他组织协作。 </br></br>对于没有 Office 365 或 Azure AD 目录的组织，用户可以注册免费的[个人 RMS](rms-for-individuals.md)订阅，或对[受支持的应用程序](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)使用 Microsoft 帐户。       |
| | |

> [!TIP]
> 附加受保护的文件，而不是保护整个电子邮件，使你能够将电子邮件文本保持不加密状态。 
>
> 例如，如果在组织外部发送电子邮件，则可能需要包含首次使用的说明。 如果附加受保护的文件，则任何人都可以读取基本说明，但只有经过授权的用户才能打开该文档，即使将该电子邮件或文档转发给其他人也是如此。

### <a name="platform-support-features"></a>平台支持功能

Azure RMS 支持范围广泛的平台和应用程序，包括：

|功能  |说明  |
|---------|---------|
|**常用设备** </br>不仅仅是 Windows 计算机     | [支持的设备](./requirements-client-devices.md)包括： </br></br>- Windows 计算机和手机 </br>- Mac 计算机 </br>- iOS 平板电脑和手机 </br>- Android 平板电脑和手机        |
|**本地服务**     | 除了[与 Office 365 无缝](office-apps-services-support.md)合作外，在部署[RMS 连接器](deploy-rms-connector.md)时，请将 Azure Rights Management 与以下本地服务结合使用： </br></br>- Exchange Server </br>- SharePoint Server </br>- 运行文件分类基础结构的 Windows Server        |
|**应用程序扩展性**     |Azure Rights Management 与 Microsoft Office 的应用程序和服务紧密集成，并使用[Azure 信息保护客户端](./rms-client/aip-client.md )扩展对其他应用程序的支持。 </br></br>[Azure 信息保护 sdk](./develop/developers-guide.md)为内部开发人员和软件供应商提供了 api，用于编写支持 Azure 信息保护的自定义应用程序。 </br></br>有关详细信息，请参阅[支持 Rights Management API 的其他应用程序](api-support.md)。         |
| | |

### <a name="infrastructure-features"></a>基础结构功能

Azure RMS 提供了以下功能来支持 IT 部门和基础结构组织：

- **创建简单灵活的策略**。 [自定义保护模板](configure-policy-templates.md)为管理员提供了一种快速而简单的解决方案，可让管理员应用策略，并使用户能够对每个文档应用适当的保护级别，并将访问权限限制给组织中的人员。 例如：

    - 若要与所有员工共享公司范围内的策略，请向所有内部员工应用只读策略。 
    - 对于更敏感的文档，如财务报表，只应将访问权限限制为高级管理人员。

- **易于激活**。 对于新订阅，激活是自动进行的。 对于现有订阅，[激活 Rights Management 服务](activate-service.md)只需在管理门户中单击几下鼠标，或者使用两个 PowerShell 命令。

- **审核和监视服务**。 [审核和监视](log-analyze-usage.md)受保护文件的使用情况，即使这些文件已经离开了组织的边界，也是如此。 

    例如，如果 Contoso，公司的员工在 Fabrikam，Inc. 的三个用户的联合项目中工作，则他们可能会向其客户发送一个受保护且限制为*只读*的文档。 

    Azure RMS 审核功能可以提供以下信息：

    - Fabrikam 合作伙伴是否打开了该文档，以及何时打开了。 
    - 其他人、未指定、尝试和打开文档失败。 如果电子邮件转发或保存到共享位置，则可能会发生这种情况。

    此外，[文档跟踪站点](./rms-client/client-track-revoke.md)可让用户和管理员跟踪并在必要时撤销对受保护文档的访问权限。

- **可以在整个组织中进行缩放**。 由于 Azure Rights Management 使用 Azure 弹性作为云服务运行，因此，无需设置或部署其他本地服务器。

- **保持 IT 对数据的控制**。 组织可从 IT 控制功能中受益，例如：

    |功能  |说明  |
    |---------|---------|
    |租户密钥管理    |   使用 "[创建自己的密钥](plan-implement-tenant-key.md)" （BYOK）解决方案管理自己的租户密钥，并将你的租户密钥存储在硬件安全模块（hsm）中。      |
    |审核和使用日志记录    |   使用审核和[使用情况日志记录](log-analyze-usage.md)功能来分析业务见解，监视是否滥用，并为信息泄露执行取证分析。      |
    |访问委派     |  使用[超级用户功能](configure-super-users.md)委派访问权限，确保它始终可以访问受保护的内容，即使文档是由离开组织的员工保护的。 </br> 相比之下，使用对等加密解决方案会面临丧失公司数据访问权限的风险。       |
    |Active Directory 同步     |   使用[混合标识解决方案](/azure/active-directory/hybrid/)（例如 Azure AD Connect）[只同步 Azure RMS 需要](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms)为本地 Active Directory 帐户支持公共标识的目录属性。      |
    |单一登录     | 通过使用 AD FS，启用单一登录而无需将密码复制到云中。        |
    |从 AD RMS 迁移 |如果已部署 Active Directory Rights Management Services （AD RMS），请[迁移到 Azure Rights Management 服务](migrate-from-ad-rms-to-azure-rms.md)，而不会失去对以前受 AD RMS 保护的数据的访问权限。 |
    | | |


> [!NOTE]
> 组织始终可以选择停止使用 Azure Rights Management 服务，而不会失去对以前受 Azure Rights Management 保护的内容的访问权限。 
> 
> 有关详细信息，请参阅[解除授权和停用 Azure Rights Management](decommission-deactivate.md)。 
> 



## <a name="security-compliance-and-regulatory-requirements"></a>安全、合规性和法规要求
Azure Rights Management 支持以下安全、合规性和法规要求：

- **使用行业标准加密并支持 FIPS 140-2。** 有关详细信息，请参阅 [Azure RMS 使用的加密控制：算法和密钥长度](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths) 信息。

- **支持 NCipher nShield 硬件安全模块（HSM）** ，以将你的租户密钥存储在 Microsoft Azure 数据中心。 

    Azure Rights Management 对北美、EMEA（欧洲、中东和非洲）和亚洲的数据中心使用单独的安全体系，因此，你的密钥只能在你所在的地区使用。

- **认证符合以下标准：**

    -   ISO/IEC 27001:2013 （./includes [ISO/iec 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/)）
    -   SOC 2 SSAE 16/ISAE 3402 证明
    -   HIPAA BAA
    -   欧盟示范条款
    -   作为 Office 365 认证中的 Azure Active Directory 的一部分，FedRAMP 已通过 HHS 操作 FedRAMP Agency
    -   PCI DSS 1 级

有关这些外部认证的详细信息，请参阅[Azure 信任中心](https://azure.microsoft.com/support/trust-center/compliance/)。

## <a name="next-steps"></a>后续步骤

有关更多 Azure 权限管理服务工作原理的技术信息，请参阅 [Azure RMS 的工作原理](how-does-it-work.md)
