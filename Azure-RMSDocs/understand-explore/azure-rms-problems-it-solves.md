---
title: "Azure RMS 解决了哪些问题 | Azure RMS"
description: "使用下表了解组织可能提出的业务要求或遇到的业务问题，以及 Azure RMS 是如何满足这些要求或解决这些问题的。"
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c7b194493073bcd76fa7a7d06bb31a7811e8cc3e
ms.openlocfilehash: 7aec5c26acb78cd85eee614a603745f3ee5938a2


---


# Azure RMS 解决了哪些问题？

>*适用于：Azure Rights Management、Office 365*

使用下表了解组织可能提出的业务要求或遇到的业务问题，以及 Azure RMS 是如何满足这些要求或解决这些问题的。

|要求或问题|Azure RMS 所解决的问题|
|--------------------------|-----------------------|
|保护所有文件类型|√ 以前，在实施权限管理的过程中，只有 Office 文件才能使用本机保护功能来保护。 现在，[通用保护](../rms-client/sharing-app-dialog-box.md#what-s-the-difference-between-generic-protection-and-built-in-native-protection)意味着支持对所有文件类型进行保护。|
|随处保护文件|√ 当文件保存到某个位置（[就地保护](../rms-client/sharing-app-protect-in-place.md)）时，该文件一直会受到保护，即使它被复制到不受 IT 部门控制的存储（如云存储服务），也是如此。|
|通过电子邮件安全地共享文件|√ 当文件通过电子邮件共享（[共享保护](../rms-client/sharing-app-protect-by-email.md)）时，该文件会作为电子邮件的附件受到保护，电子邮件中包含如何打开受保护附件的说明。 电子邮件文本没有加密，因此，收件人始终能够阅读这些说明。 但是，由于附加的文档受到保护，因此只有授权用户才能将其打开，即使将该电子邮件或文档转发给其他用户。|
|审核和监视|√ 你可以 [审核和监视受保护文件的使用情况](../deploy-use/log-analyze-usage.md)，即使这些文件已经离开了组织的边界。<br /><br />例如，你为 Contoso, Ltd. 工作 你正在与来自 Fabrikam, Inc 的 3 名人员一起致力于一个联合项目你通过电子邮件向这 3 人发送了一个已保护并限制为只读的文档。 Azure RMS 审核功能可以提供以下信息：<br /><br />- 你指定的来自 Fabrikam 的人是否打开了该文档，以及打开时间（如果已打开过）。<br /><br />- 你未指定的其他人是否尝试打开该文档却失败了（发生这种情况可能是因为该文档已转发或保存到其他人可以访问的共享位置）。<br /><br />- 指定的任何人是否尝试打印或更改该文档却失败了。|
|支持所有常用设备，而不仅仅是 Windows 计算机|√ [支持的设备](../get-started/requirements-client-devices.md) 包括：<br /><br />- Windows 计算机和手机<br /><br />- Mac 计算机<br /><br />- iOS 平板电脑和手机<br /><br />- Android 平板电脑和手机|
|支持企业与企业之间的协作|√ 由于 Azure RMS 是云服务，因此在与其他组织共享受保护内容前，不需要显式配置与这些组织的信任关系。 如果他们已有 Office 365 或 Azure AD 目录，则会自动支持组织间的协作。 如果他们没有 Office 365 或 Azure AD 目录，则用户可以注册免费的 [个人 RMS](rms-for-individuals.md) 订阅。|
|支持本地服务，以及 Office 365|√ 除了 [与 Office 365 无缝集成](office-apps-services-support.md) 以外，在部署 [RMS 连接器](../deploy-use/deploy-rms-connector.md)时，你还可以将 Azure RMS 与以下本地服务结合使用：<br /><br />- Exchange Server<br /><br />- SharePoint Server<br /><br />- 运行文件分类基础结构的 Windows Server|
|轻松激活|√ 为用户 [激活权限管理服务](../deploy-use/activate-service.md) 只需在 Azure 经典门户中单击几下鼠标。|
|可以根据需要在整个组织内扩展|√ 由于 Azure RMS 可作为云服务运行并借助 Azure 灵活地向上和向外扩展，因此，你不需要设置或部署其他本地服务器。|
|可以创建简单灵活的策略|√ [自定义权限策略模板](../deploy-use/configure-custom-templates.md) 提供了一款便捷的解决方案。通过该解决方案，管理员可以应用策略，用户可以对每个文档应用适当级别的保护，并将访问权限限制给组织内部人员。<br /><br />例如，为了与所有员工共享公司范围内的策略文档，你可以对所有内部员工应用只读策略。 此外，对于更敏感的文档，如财务报表，你可以将访问权限仅提供给高管。|
|广泛的应用程序支持|√ Azure RMS 可与 Microsoft Office 应用程序和服务紧密集成，并使用 RMS 共享应用程序扩展对其他应用程序的支持。<br /><br />√ [Microsoft Rights Management SDK](../develop/developers-guide.md#software-development-kits) 为内部开发人员和软件供应商提供了 API，用于编写支持 Azure RMS 的自定义应用程序。<br /><br />有关详细信息，请参阅 [支持 RMS API 的其他应用程序](api-support.md)。|
|IT 部门必须保持对数据的控制|√ 组织可以选择管理其自己的租户密钥，使用“[自带密钥](../plan-design/plan-implement-tenant-key.md)”(BYOK) 解决方案，并将其租户密钥存储在硬件安全模块 (HSM) 中。<br /><br />√ 支持审核和 [使用日志记录](../deploy-use/log-analyze-usage.md)，因此，你可以通过分析信息来获得业务见解、通过监视信息来了解滥用情况，并可在出现信息泄露的情况下执行取证分析。<br /><br />√ 使用 [超级用户功能](../deploy-use/configure-super-users.md) 委托访问确保 IT 部门始终可以访问受保护的内容，即使文档是由后来从组织离职的员工实施保护的。 相比之下，使用对等加密解决方案会面临丧失公司数据访问权限的风险。<br /><br />√ 仅同步[Azure RMS 所需的目录属性](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms)即可对本地 Active Directory 帐户使用通用标识，而且只需使用[目录同步工具](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)（例如 Azure AD Connect）即可。<br /><br />√ 使用 AD FS 来启用单一登录，而无需将密码复制到云中。<br /><br />√ 组织始终可以选择停止使用 Azure RMS，而不会失去对以前受 Azure RMS 保护的内容的访问权限。 有关解除授权选项的信息，请参阅 [解除 Azure Rights Management 授权和停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)。 此外，部署了 Active Directory Rights Management Services (AD RMS) 的组织还可以 [迁移到 Azure RMS](../plan-design/migrate-from-ad-rms-to-azure-rms.md)，而不会失去对以前受 AD RMS 保护的数据的访问权限。|
> [!TIP]
> 如果你熟悉本地版的权限管理和 Active Directory Rights Management 服务 (AD RMS)，则可能会对 [比较 Azure Rights Management 和 AD RMS](compare-azure-rms-ad-rms.md) 中的比较表感兴趣。

## 安全、合规性和法规要求
Azure RMS 支持以下安全、合规性和法规要求：

√ 使用符合业界标准的加密功能，支持 FIPS 140-2。 有关详细信息，请参阅 [Azure RMS 使用的加密控制：算法和密钥长度](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths) 信息。

√ 支持 Thales 硬件安全模块 (HSM)，允许将你的租户密钥存储在 Microsoft Azure 数据中心内。 Azure RMS 对北美、EMEA（欧洲、中东和非洲）和亚洲的数据中心使用单独的安全体系，因此，你的密钥只能在你所在的地区使用。

√ 已针对以下项进行认证：

-   ISO/IEC 27001:2013（包括 [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/)）

-   SOC 2 SSAE 16/ISAE 3402 证明

-   HIPAA BAA

-   欧盟示范条款

-   作为 Office 365 认证中的 Azure Active Directory 的一部分，FedRAMP 已通过 HHS 操作 FedRAMP Agency

-   PCI DSS 级别 1

有关这些外部认证的详细信息，请参阅 [Azure 信任中心](http://azure.microsoft.com/support/trust-center/compliance/)。

## 后续步骤

若要了解 Azure RMS 对于管理员和用户所呈现的内容，请参阅 [运行中的 Azure RMS](what-admins-users-see.md)。

如果对有关 Azure RMS 工作的详细技术信息感兴趣，请参阅 [Azure RMS 的工作原理](how-does-it-work.md) 


<!--HONumber=Aug16_HO4-->


