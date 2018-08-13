---
title: 通过 Azure Rights Management 解决的问题 - AIP
description: 确定组织可能具有的要求或问题，并了解 Azure RMS 技术是如何满足这些要求或解决这些问题的。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 232f0988b5566257b3f04ddfc86aec98f7ac6003
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2018
ms.locfileid: "39489842"
---
# <a name="what-problems-does-azure-rms-solve"></a>Azure RMS 解决了哪些问题？

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

使用下表了解组织在保护文档和电子邮件方面可能提出的业务要求或遇到的业务问题，以及 Azure 权限管理 (Azure RMS) 技术是如何满足这些要求或解决这些问题的。

Azure RMS 是 [Azure 信息保护](what-is-information-protection.md)使用的保护技术。

|要求或问题|Azure RMS 所解决的问题|
|--------------------------|-----------------------|
|保护多个文件类型|√ 在 Rights Management 的早期实现中，只有 Office 文件才能使用本机 Rights Management 保护功能获得保护。 
  **常规保护** 以前由 Rights Management 共享应用程序提供，现在由 Azure 信息保护客户端提供，这意味着现在可以支持更多[文件类型](./rms-client/client-admin-guide-file-types.md)。|
|随处保护文件|√ 文件一旦[受保护](./rms-client/client-classify-protect.md)，便会始终受到保护，即使它被保存或复制到不受 IT 部门控制的存储（如云存储服务），也是如此。|
|安全共享信息|√ 当文件[受保护](./rms-client/client-classify-protect.md)时，可以安全地与他人进行共享。 例如，电子邮件的附件或 SharePoint 网站的链接。 如果电子邮件中有敏感信息，则可以保护电子邮件，或只需使用 Outlook 中的“不要转发”选项。 <br /><br />附加受保护文件而不是保护整个电子邮件的好处是，电子邮件文本未加密，因此如果在组织外发送电子邮件，可以附上首次使用的说明。 任何人都可阅读说明，但由于附加文档受到保护，因此只有授权用户才能打开文档，即使将该电子邮件或文档转发给其他用户也是如此。|
|审核和监视|√ 你可以 [审核和监视受保护文件的使用情况](log-analyze-usage.md)，即使这些文件已经离开了组织的边界。<br /><br />例如，你为 Contoso, Ltd. 工作你正在与来自 Fabrikam, Inc 的三名人员一起致力于一个联合项目。你通过电子邮件向这三人发送了一个已保护并限制为只读的文档。 Azure 权限管理审核功能可以提供以下信息：<br /><br />- 你指定的来自 Fabrikam 的人是否打开了该文档，以及打开时间（如果已打开过）。<br /><br />- 你未指定的其他人是否尝试打开该文档却失败了（发生这种情况可能是因为该文档已转发或保存到其他人可以访问的共享位置）。<br /><br />- 指定的任何人是否尝试打印或更改该文档却失败了。<br /><br />此外，[文档跟踪站点](./rms-client/client-track-revoke.md)可让用户和管理员跟踪并在必要时撤销对受保护文档的访问权限。|
|支持常用设备，而不仅仅是 Windows 计算机|√ [支持的设备](./requirements-client-devices.md) 包括：<br /><br />- Windows 计算机和手机<br /><br />- Mac 计算机<br /><br />- iOS 平板电脑和手机<br /><br />- Android 平板电脑和手机|
|支持企业与企业之间的协作|√ 由于 Azure 权限管理是云服务，因此在与其他组织共享受保护内容前，不需要显式配置与这些组织的信任关系。 如果他们已有 Office 365 或 Azure AD 目录，则会自动支持组织间的协作。 但是如果没有，用户可以免费注册[个人的 RMS](rms-for-individuals.md) 订阅，或者将 Microsoft 帐户用于[支持此 Azure 信息保护身份验证的应用程序](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)。|
|支持本地服务，以及 Office 365|√ 除了 [与 Office 365 无缝集成](office-apps-services-support.md) 以外，在部署 [RMS 连接器](deploy-rms-connector.md)时，你还可以将 Azure 权限管理与以下本地服务结合使用：<br /><br />- Exchange Server<br /><br />- SharePoint Server<br /><br />- 运行文件分类基础结构的 Windows Server|
|轻松激活|√ 对于新订阅，激活是自动进行的。 对于现有订阅，只需在管理门户中单击几下鼠标即可[激活 Rights Management 服务](activate-service.md)。 或者，如果你喜欢命令行控制，只需使用两个 PowerShell 命令即可。|
|可以根据需要在整个组织内扩展|√ 由于 Azure Rights Management 可作为云服务运行并借助 Azure 灵活地向上和向外扩展，因此，不需要设置或部署其他本地服务器。|
|可以创建简单灵活的策略|√ [自定义保护模板](configure-policy-templates.md)提供了一款便捷的解决方案。通过该解决方案，管理员可以应用策略，用户可以对每个文档应用适当级别的保护，并将访问权限限制给组织内部人员。<br /><br />例如，为了与所有员工共享公司范围内的策略文档，你可以对所有内部员工应用只读策略。 此外，对于更敏感的文档，如财务报表，你可以将访问权限仅提供给高管。|
|广泛的应用程序支持|√ Azure 权限管理可与 Microsoft Office 应用程序和服务紧密集成，并使用 [Azure 信息保护客户端](./rms-client/aip-client.md )扩展对其他应用程序的支持。<br /><br />√ [Azure 信息保护 SDK](./develop/developers-guide.md) 为内部开发人员和软件供应商提供了 API，用于编写支持 Azure 信息保护的自定义应用程序。<br /><br />有关详细信息，请参阅[支持 Rights Management API 的其他应用程序](api-support.md)。|
|IT 部门必须保持对数据的控制|√ 组织可以选择管理其自己的租户密钥，使用“[自带密钥](plan-implement-tenant-key.md)”(BYOK) 解决方案，并将其租户密钥存储在硬件安全模块 (HSM) 中。<br /><br />√ 支持审核和 [使用日志记录](log-analyze-usage.md)，因此，你可以通过分析信息来获得业务见解、通过监视信息来了解滥用情况，并可在出现信息泄露的情况下执行取证分析。<br /><br />√ 使用 [超级用户功能](configure-super-users.md) 委托访问确保 IT 部门始终可以访问受保护的内容，即使文档是由后来从组织离职的员工实施保护的。 相比之下，使用对等加密解决方案会面临丧失公司数据访问权限的风险。<br /><br />√ 仅同步[Azure RMS 所需的目录属性](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms)即可对本地 Active Directory 帐户使用通用标识，而且只需使用[目录同步工具](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)（例如 Azure AD Connect）即可。<br /><br />√ 使用 AD FS 来启用单一登录，而无需将密码复制到云中。<br /><br />√ 组织始终可以选择停止使用 Azure 权限管理服务，而不会失去对以前受 Azure 权限管理保护的内容的访问权限。 有关解除授权选项的信息，请参阅 [解除 Azure Rights Management 授权和停用 Azure Rights Management](decommission-deactivate.md)。 此外，部署了 Active Directory Rights Management Services (AD RMS) 的组织还可以[迁移到 Azure 权限管理服务](migrate-from-ad-rms-to-azure-rms.md)，而不会失去对以前受 AD RMS 保护的数据的访问权限。|
> [!TIP]
> 如果你熟悉本地版的权限管理和 Active Directory Rights Management 服务 (AD RMS)，则可能会对 [比较 Azure Rights Management 和 AD RMS](compare-on-premise.md) 中的比较表感兴趣。

## <a name="security-compliance-and-regulatory-requirements"></a>安全、合规性和法规要求
Azure 权限管理支持以下安全、合规性和法规要求：

√ 使用符合业界标准的加密功能，支持 FIPS 140-2。 有关详细信息，请参阅 [Azure RMS 使用的加密控制：算法和密钥长度](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths) 信息。

√ 支持 Thales 硬件安全模块 (HSM)，允许将你的租户密钥存储在 Microsoft Azure 数据中心内。 Azure 权限管理对北美、EMEA（欧洲、中东和非洲）和亚洲的数据中心使用单独的安全体系，因此，你的密钥只能在你所在的地区使用。

√ 已针对以下项进行认证：

-   ISO/IEC 27001:2013（./包括 [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/)）

-   SOC 2 SSAE 16/ISAE 3402 证明

-   HIPAA BAA

-   欧盟示范条款

-   作为 Office 365 认证中的 Azure Active Directory 的一部分，FedRAMP 已通过 HHS 操作 FedRAMP Agency

-   PCI DSS 级别 1

有关这些外部认证的详细信息，请参阅 [Azure 信任中心](http://azure.microsoft.com/support/trust-center/compliance/)。

## <a name="next-steps"></a>后续步骤

有关更多 Azure 权限管理服务工作原理的技术信息，请参阅 [Azure RMS 的工作原理](how-does-it-work.md)
