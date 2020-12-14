---
title: Azure 信息保护的 azure 安全基线
description: Azure 信息保护安全基线为实现 Azure 安全基准中指定的安全建议提供过程指南和资源。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/18/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: 8cdeb7ec7bd30d6b15b832eeb080317d5b26ec08
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384615"
---
# <a name="azure-security-baseline-for-azure-information-protection"></a>Azure 信息保护的 azure 安全基线

此安全基线将 [Azure 安全基准版本 2.0](https://docs.microsoft.com/azure/security/benchmarks/overview) 中的指南应用于 Azure 信息保护。 Azure 安全基准提供有关如何在 Azure 上保护云解决方案的建议。 内容由 Azure 安全基准定义的 **安全控制** 和适用于 Azure 信息保护的相关指南进行分组。 排除了不适用于 Azure 信息保护的 **控件**。

若要查看 Azure 信息保护如何完全映射到 Azure 安全基准，请参阅 [完整的 Azure 信息保护安全基线映射文件](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines)。

## <a name="network-security"></a>网络安全

[有关详细信息，请参阅 *Azure 安全基线：* 网络安全性](/azure/security/benchmarks/security-controls-v2-network-security)。

### <a name="ns-6-simplify-network-security-rules"></a>NS-6：简化网络安全规则

**指南**：使用虚拟网络服务标记来定义网络安全组或 azure 防火墙上的网络访问控制，这些控制是针对 Azure 信息保护资源配置的。 

创建安全规则时，请使用服务标记代替特定的 IP 地址。 在规则的相应 "源" 或 "目标" 字段中指定服务标记名称（如 {AzureInformationProtection}），以允许或拒绝相应服务的流量。

Microsoft 会管理服务标记包含的地址前缀，并会在地址发生更改时自动更新服务标记。

- [了解并使用服务标记](https://docs.microsoft.com/azure/virtual-network/service-tags-overview)

- [Azure 信息保护服务标记](https://docs.microsoft.com/azure/information-protection/requirements#service-tags)

**Azure 安全中心监视**：不适用

**责任**：客户

## <a name="identity-management"></a>标识管理

有关详细信息，请参阅 [Azure 安全基准：标识管理](/azure/security/benchmarks/security-controls-v2-identity-management)。

### <a name="im-1-standardize-azure-active-directory-as-the-central-identity-and-authentication-system"></a>IM-1：将 Azure Active Directory 标准化为中央标识和身份验证系统

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) ，后者是 azure 的默认标识和访问管理服务。 将其设置为高优先级，以便在组织的云安全实践中保护 Azure AD。 

查看 Azure AD 标识安全分数，以帮助你根据 Microsoft 的最佳实践建议评估标识安全状况。 使用评分来估计你的配置与最佳做法建议的匹配程度，并改善你的安全状况。

标准化 Azure AD 来管理组织的标识和访问管理：

- Microsoft 云资源，如 Azure 门户、Azure 存储、Azure 虚拟机 (Linux 和 Windows) ，Azure Key Vault，平台即服务 (PaaS) 和软件即服务 (SaaS) 应用程序

- 你组织的资源，如 Azure 上的应用程序或你的公司网络资源

Azure AD 支持外部标识，以允许没有 Microsoft 帐户的用户使用其非 Microsoft 帐户登录到其应用程序和资源。

- [Azure Active Directory 中的租赁](https://docs.microsoft.com/azure/active-directory/develop/single-and-multi-tenant-apps)

- [如何创建和配置 Azure AD 实例](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)

- [使用应用程序的外部标识提供者](https://docs.microsoft.com/azure/active-directory/b2b/identity-providers)

- [Azure Active Directory 中的标识安全分数是什么](https://docs.microsoft.com/azure/active-directory/fundamentals/identity-secure-score)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="im-2-manage-application-identities-securely-and-automatically"></a>IM-2：安全且自动地管理应用程序标识

**指南**： Azure 信息保护与 azure 的标识和访问管理服务的 Azure Active Directory (Azure AD) 集成。 Azure Rights Management 服务使用 Azure AD 应用程序标识，同时访问与 Azure Key Vault 存储的客户密钥创建自己的密钥 (BYOK) 方案。 授权 Azure Rights Management 服务访问密钥是通过配置 Azure Key Vault 访问策略实现的，该策略可以使用 Azure 门户或使用 PowerShell 来完成。

- [授权适用于 BYOK 的 Azure Rights Management 服务](https://docs.microsoft.com/azure/information-protection/byok-price-restrictions#authorizing-the-azure-rights-management-service-to-use-your-key)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="im-3-use-azure-ad-single-sign-on-sso-for-application-access"></a>IM-3：使用 Azure AD 单一登录 (SSO) 进行应用程序访问

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) ，后者是 azure 的默认标识和访问管理服务。 

Azure 信息保护使用 Azure AD 提供对 Azure 资源、云应用程序和本地应用程序的标识和访问管理。 此内容包括企业标识（例如员工）以及外部标识（如合作伙伴和供应商）。 这使得单一登录可以在本地和云中管理和安全访问组织的数据和资源。 将所有用户、应用程序和设备连接到 Azure AD，实现无缝的安全访问和更好的可见性和控制。

- [通过 Azure Active Directory 登录到 Azure 信息保护](https://docs.microsoft.com/azure/information-protection/requirements)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="im-4-use-strong-authentication-controls-for-all-azure-active-directory-based-access"></a>IM-4：对所有基于 Azure Active Directory 的访问使用强身份验证控制

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) 集成，通过多重身份验证支持强身份验证。 若要支持 Azure 信息保护的身份验证和授权，必须有 Azure AD。 若要使用本地目录 (AD DS) 中的用户帐户，还必须配置目录集成。

- Azure 信息保护支持单一登录，因此不会重复提示用户输入其凭据。 如果使用其他供应商解决方案进行联合身份验证，请与相应供应商确认如何为它配置 Azure AD。 WS-Trust 是这些解决方案支持单一登录所需满足的常见要求。

- 当具有所需的客户端软件并正确配置了多重身份验证支持的基础结构时，Azure 信息保护支持多重身份验证。

有关详细信息，请参阅以下资源：

- [通过 Azure Active Directory 进行 Azure 信息保护身份验证](https://docs.microsoft.com/azure/information-protection/requirements)

**Azure 安全中心监视**：是

**责任**：客户

### <a name="im-5-monitor-and-alert-on-account-anomalies"></a>IM-5：监视并提醒帐户异常

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) ，后者是 azure 的默认标识和访问管理服务。 

有关 Azure AD 的其他指导：

- 登录-登录报表提供有关托管应用程序和用户登录活动的使用情况的信息。
- 审核日志 - 通过日志为 Azure AD 中的各种功能所做的所有更改提供可跟踪性。 审核日志的示例包括对 Azure AD 中的任何资源所做的更改，如添加或删除用户、应用、组、角色和策略。
- 有风险的登录是指可能已由不是用户帐户合法所有者的用户执行的登录尝试的指示符的指示。
- 已标记为存在风险的用户 - 风险用户是指可能已泄露的用户帐户。
这些数据源可以与 Azure Monitor、Azure Sentinel 或第三方 SIEM 系统集成。

Azure 安全中心还可以针对某些可疑活动（例如，过多的身份验证尝试失败，或订阅中的帐户已弃用）发出警报。

Azure 高级威胁防护 (ATP) 是一种安全解决方案，它可使用 Active Directory 信号来识别、检测和调查高级威胁、泄露的标识以及恶意的内部操作。

- [Azure Active Directory 中的“审核活动”报表](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs) 

- [如何查看 Azure AD 风险登录](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-risky-sign-ins) 

- [如何确定标记为存在风险活动的 Azure AD 用户](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-user-at-risk) 

- [如何在 Azure 安全中心内监视用户的标识和访问活动](https://docs.microsoft.com/azure/security-center/security-center-identity-access) 

- [Azure 安全中心的威胁情报保护模块中的警报](https://docs.microsoft.com//azure/security-center/alerts-reference) 

- [如何将 Azure 活动日志集成到 Azure Monitor](https://docs.microsoft.com/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="im-6-restrict-azure-resource-access-based-on-conditions"></a>IM-6：基于条件限制 Azure 资源访问

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) ，后者是 azure 的默认标识和访问管理服务。 在 Azure AD 中，配置 Azure 信息保护的条件性访问。 对于受 Azure 信息保护保护的文档，管理员可以基于标准条件访问控制阻止或授予对其租户中的用户的访问权限。

多重身份验证是最常请求的条件之一，而具有配置的 Intune 策略的设备规范是另一个条件。 您可以要求使用条件，使移动设备满足您的组织密码要求，具有最低的操作系统版本，而连接的计算机已加入域。

- [Azure 信息保护的条件性访问策略](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection)

**Azure 安全中心监视**：不适用

**责任**：客户

## <a name="privileged-access"></a>特权访问

有关详细信息，请参阅 [Azure 安全基准：特权访问](/azure/security/benchmarks/security-controls-v2-privileged-access)。

### <a name="pa-1-protect-and-limit-highly-privileged-users"></a>PA-1：保护和限制具有较高权限的用户

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) ，后者是 azure 的默认标识和访问管理服务。 

Azure 信息保护在 Azure AD 中包括了管理员级别的角色。 分配到管理员角色的用户在 Azure 信息保护服务中具有完全权限。 管理员角色可用于配置 Azure 信息保护策略的标签、管理保护模板以及激活保护。 但是，"管理员" 角色不会授予 "Identity Protection 中心"、"Privileged Identity Management"、"监视" Microsoft 365 服务运行状况或 Office 365 安全符合中心中的任何权限 &amp; 。

限制高特权帐户或角色的数量并在提升的级别保护这些帐户，因为具有此权限的用户可以直接或间接地读取和修改 Azure 环境中的每个资源。 使用 Privileged Identity Management (PIM) 启用实时 (JIT) 对 Azure 资源和 Azure AD 的特权访问。 仅当用户需要时，才能通过实时访问权限来执行特权任务。 当 Azure AD 组织中存在可疑或不安全的活动时，PIM 还会生成安全警报。

- [Azure 信息保护管理员角色](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azure AD 中的管理角色权限](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)

- [使用 Azure Privileged Identity Management 安全警报](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [确保 Azure AD 中混合部署和云部署的特权访问安全性](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="pa-2-restrict-administrative-access-to-business-critical-systems"></a>PA-2：限制对关键业务型系统的管理访问权限

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) ，后者是 azure 的默认标识和访问管理服务。 

Azure 信息保护在 Azure AD 中包括了管理员级别的角色。 分配到管理员角色的用户在 Azure 信息保护服务中具有完全权限。 管理员角色允许配置 Azure 信息保护策略的标签、管理保护模板以及激活保护。 管理员角色不会授予 "Identity Protection 中心"、"Privileged Identity Management"、"监视" Microsoft 365 服务运行状况或 Office 365 安全符合中心中的任何权限 &amp; 。

- [Azure 信息保护管理员角色](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azure 信息保护管理员可以执行的操作](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator-permissions)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="pa-3-review-and-reconcile-user-access-regularly"></a>PA-3：定期审查和协调用户访问权限

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) ，后者是 azure 的默认标识和访问管理服务。

使用 Azure AD 可定期管理资源、查看用户帐户以及访问分配，以确保帐户及其访问有效。 执行 Azure AD 访问评审，以查看组成员身份、对企业应用程序的访问权限以及角色分配。 发现具有 Azure AD 报告的过时帐户。 Azure AD 的 Privileged Identity Management 功能可用于创建访问评审报表工作流以促进审核过程。

此外，Azure Privileged Identity Management 还可配置为在创建过多管理员帐户时发出警报，并识别过时或配置不正确的管理员帐户。 请注意，某些 Azure 服务支持不通过 Azure AD 管理的本地用户和角色。 客户需要单独管理这些用户。

- [Azure 信息保护管理员角色](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azure 信息保护管理员可以执行的操作](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator-permissions)

- [在 Privileged Identity Management (PIM 中创建 Azure 资源角色的访问评审) ](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-start-access-review) 

- [如何使用 Azure AD 标识和访问评审](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overvie)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="pa-4-set-up-emergency-access-in-azure-ad"></a>PA-4：在 Azure AD 中设置紧急访问

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) 管理其资源。 为了防止意外退出 Azure AD 组织，请设置一个紧急访问帐户，以便在正常管理帐户无法使用时进行访问。 紧急访问帐户通常拥有较高的权限，因此请不要将其分配给特定的个人。 紧急访问帐户只能用于“不受限”紧急情况，即不能使用正常管理帐户的情况。

应确保妥善保管紧急访问帐户的凭据（例如密码、证书或智能卡），仅将其告诉只能在紧急情况下有权使用它们的个人。

- [在 Azure AD 中管理紧急访问帐户](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-emergency-access)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="pa-5-automate-entitlement-management"></a>PA-5：将权利管理自动化 

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) 、azure 默认标识和访问管理服务集成。

Azure AD 提供了权利管理功能来自动执行访问请求工作流，包括访问权限分配、审核和过期。 还支持两阶段或多阶段审批。

- [什么是 Azure AD 访问评审](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overview) 

- [什么是 Azure AD 权利管理](https://docs.microsoft.com/azure/active-directory/governance/entitlement-management-overview)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="pa-6-use-privileged-access-workstations"></a>PA-6：使用特权访问工作站

**指南**：可以通过 PowerShell 从客户工作站管理 Azure 信息保护。 

受保护的隔离工作站对于敏感角色（如管理员、开发人员和关键服务操作员）的安全性至关重要。 

使用高度安全的用户工作站和/或 Azure Bastion 执行管理任务。 使用 Azure Active Directory、Microsoft Defender 高级威胁防护 (ATP) 和/或 Microsoft Intune 部署安全的托管用户工作站，用于执行管理任务。 可集中管理安全工作站，强制实施安全配置，包括强身份验证、软件和硬件基线，以及受限制的逻辑和网络访问。

- [有关使用 PowerShell 进行 Azure 信息保护的指南](https://docs.microsoft.com/azure/information-protection/rms-client/client-admin-guide-powershell)

- [了解特权访问工作站](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-managed-workstation) 

- [部署特权访问工作站](https://docs.microsoft.com/azure/active-directory/devices/howto-azure-managed-workstation)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="pa-7-follow-just-enough-administration-least-privilege-principle"></a>PA-7：遵循 Just Enough Administration（最小特权原则） 

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) ，后者是 azure 的默认标识和访问管理服务。 

Azure 信息保护在 Azure AD 中包括了管理员级别的角色。 分配到管理员角色的用户在 Azure 信息保护服务中具有完全权限。 管理员角色可用于配置 Azure 信息保护策略的标签、管理保护模板以及激活保护。 但是，"管理员" 角色不会授予 "Identity Protection 中心"、"Privileged Identity Management"、"监视" Microsoft 365 服务运行状况或 Office 365 安全符合中心中的任何权限 &amp; 。

限制高特权帐户或角色的数量并在提升的级别保护这些帐户，因为具有此权限的用户可以直接或间接地读取和修改 Azure 环境中的每个资源。 使用 Privileged Identity Management (PIM) 启用实时 (JIT) 对 Azure 资源和 Azure AD 的特权访问。 仅当用户需要时，才能通过实时访问权限来执行特权任务。 当 Azure AD 组织中存在可疑或不安全的活动时，PIM 还会生成安全警报。

- [Azure 信息保护权限级别中包括的权限](https://docs.microsoft.com/azure/information-protection/configure-usage-rights#rights-included-in-permissions-levels)

- [Rights Management 颁发者和 Rights Management 所有者](https://docs.microsoft.com/azure/information-protection/configure-usage-rights#rights-management-issuer-and-rights-management-owner)

- [Azure 信息保护管理员角色](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azure AD 中的管理角色权限](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)

- [使用 Azure Privileged Identity Management 安全警报](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [确保 Azure AD 中混合部署和云部署的特权访问安全性](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="pa-8-choose-approval-process-for-microsoft-support"></a>PA-8：选择 Microsoft 支持的批准流程  

**指南**： Azure 信息保护支持 azure 客户密码箱向客户提供查看、批准和拒绝数据访问请求以及查看请求的功能。 

- [密码箱概述](https://docs.microsoft.com/azure/security/fundamentals/customer-lockbox-overview)

**Azure 安全中心监视**：不适用

**责任**：客户

## <a name="data-protection"></a>数据保护

[有关详细信息，请参阅 *Azure 安全基线：* 数据保护](/azure/security/benchmarks/security-controls-v2-data-protection)。

### <a name="dp-1-discovery-classify-and-label-sensitive-data"></a>DP-1：对敏感数据进行发现、分类和标记

**指南**： Azure 信息保护提供了对敏感信息的发现、分类和标记功能。 

Azure 信息保护是基于云的解决方案，使组织能够通过应用标签来分类和保护文档和电子邮件。 标签可通过管理员使用规则和条件来自动应用、由用户手动应用，也可通过这两者的组合进行应用（此时管理员会定义显示给用户的建议）。

- [Azure 信息保护概述](https://docs.microsoft.com/azure/information-protection/)

- [有关如何设置统一标签客户端的指导](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-user-guide)

**Azure 安全中心监视**：不适用

**责任**：共享

### <a name="dp-2-protect-sensitive-data"></a>DP-2：保护敏感数据

**指南**： Azure 信息保护提供数据保护功能，它通过加密来标记敏感信息并提供对该数据的保护。 保护由 Azure Rights Management 服务提供。

- [Azure 权限管理](https://docs.microsoft.com/azure/information-protection/what-is-azure-rms)

**Azure 安全中心监视**：不适用

**责任**：共享

### <a name="dp-3-monitor-for-unauthorized-transfer-of-sensitive-data"></a>DP-3：监视未经授权的敏感数据传输

**指南**： Azure 信息保护提供监视通过跟踪和撤消功能对敏感数据进行未授权传输的能力。 使用 "跟踪" 和 "撤消" 功能，客户可以跟踪用户如何使用其发送的文档，并在用户不能再阅读时撤销访问权限。 

- [跟踪和撤消指南](https://docs.microsoft.com/azure/information-protection/rms-client/client-track-revoke)

**Azure 安全中心监视**：不适用

**责任**：共享

## <a name="asset-management"></a>资产管理

有关详细信息，请参阅 [Azure 安全基准：资产管理](/azure/security/benchmarks/security-controls-v2-asset-management)。

### <a name="am-1-ensure-security-team-has-visibility-into-risks-for-assets"></a>AM-1：确保安全团队可以了解与资产相关的风险

**指南**：确保在 Azure 租户和订阅中向安全团队授予了安全读取者权限，以便他们可以使用 Azure 安全中心监视安全风险。 

根据安全团队责任划分方式的不同，监视安全风险可能是中心安全团队或本地团队的责任。 也就是说，安全见解和风险必须始终在组织内集中聚合。 

安全读取者权限可以广泛应用于整个租户（根管理组），也可以限制到管理组或特定订阅。 

注意：若要了解工作负载和服务，可能需要更多权限。 

- [安全读取者角色概述](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#security-reader)

- [Azure 管理组概述](https://docs.microsoft.com/azure/governance/management-groups/overview)

**Azure 安全中心监视**：目前不可用

**责任**：客户

### <a name="am-3-use-only-approved-azure-services"></a>AM-3：仅使用已批准的 Azure 服务

**指南**： Azure 信息保护不支持 Azure 资源管理器部署，也不允许客户通过内置的 Azure 策略定义（例如 "允许资源" 或 "拒绝资源"）限制部署。 但是，客户可以通过安全和合规中心中的标签策略限制 Azure 信息保护的使用。 

- [通过安全和合规中心管理信息保护](https://docs.microsoft.com/microsoft-365/compliance/protect-information?view=o365-worldwide&amp;preserve-view=true)

**Azure 安全中心监视**：不适用

**责任**：客户

## <a name="logging-and-threat-detection"></a>日志记录和威胁检测

有关详细信息，请参阅 [Azure 安全基准：日志记录和威胁检测](/azure/security/benchmarks/security-controls-v2-logging-threat-protection)。

### <a name="lt-2-enable-threat-detection-for-azure-identity-and-access-management"></a>LT-2：启用 Azure 标识和访问管理的威胁检测

**指南**： Azure 信息保护与 Azure Active Directory (Azure AD) ，后者是 azure 的默认标识和访问管理服务。 

查看 Azure AD 提供的用户日志，其中包含 Azure AD 报表和其他解决方案，如 Azure Monitor、Azure Sentinel 或其他 SIEM/监视工具，以实现更复杂的监视和分析用例。 

它们是： 

-   登录报告–登录报告提供有关托管应用程序和用户登录活动的使用情况的信息。

-   审核日志 - 通过日志为 Azure AD 中的各种功能所做的所有更改提供可跟踪性。 审核日志的示例包括对 Azure AD 中的任何资源所做的更改，如添加或删除用户、应用、组、角色和策略。

-   有风险的登录-有风险登录是指可能由不是用户帐户合法所有者的用户执行的登录尝试。

-   已标记为存在风险的用户 - 风险用户是指可能已泄露的用户帐户。

Azure 安全中心还可以针对某些可疑活动（例如，过多的身份验证尝试失败，以及订阅中不推荐使用的帐户）发出警报。 除了基本的安全卫生监视之外，安全中心的威胁防护模块还可以从单个 Azure 计算 (资源（例如虚拟机、容器、应用服务) 、数据资源 (如 SQL 数据库和存储) 以及 Azure 服务层）收集更深入的安全警报。 通过此功能可查看单个资源中的帐户异常情况。

- [Azure AD 中的审核活动报告](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs)

- [启用 Azure 标识保护](https://docs.microsoft.com/azure/active-directory/identity-protection/overview-identity-protection)

- [Azure 安全中心的威胁防护](https://docs.microsoft.com/azure/security-center/threat-protection)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="lt-4-enable-logging-for-azure-resources"></a>LT-4：为 Azure 资源启用日志记录

**指南**： Azure 信息保护为组织的文档和电子邮件提供数据保护，以及每个请求的日志。  这些请求包括当用户保护文档和电子邮件时，当用户使用此内容时，管理员对此服务执行的操作，以及由 Microsoft 操作员执行的、用于支持 Azure 信息保护部署的操作。

Azure 信息保护生成的日志类型包括：

- 管理日志-为保护服务记录管理任务。 例如，在停用服务的情况下，启用超级用户功能时，以及向用户委派服务的管理员权限时。

- 文档跟踪-使用户可以跟踪和撤销他们使用 Azure 信息保护客户端跟踪的文档。 全局管理员也可以代表用户跟踪这些文档。

- 客户端事件日志-Azure 信息保护客户端的使用情况活动，登录到本地 Windows 应用程序和服务事件日志，以及 Azure 信息保护。

- 客户端日志文件-Azure 信息保护客户端的疑难解答日志

保护使用日志可用于识别 "谁" 正在访问受保护的数据、从 "哪些设备" 和 "位置"。 日志显示用户是否能够成功读取受保护的内容，并确定哪些用户已阅读受保护的重要文档。 

- [记录和分析 Azure 信息保护中的保护使用情况](https://docs.microsoft.com/azure/information-protection/log-analyze-usage)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="lt-5-centralize-security-log-management-and-analysis"></a>LT-5：集中管理和分析安全日志

**指南**：确保支持人员可通过查询和使用不同的数据源来构建事件期间发生的事件的完整视图，因为他们调查的可能是事件。 

通过收集不同的日志并将它们发送到中心 SIEM 解决方案（例如 Azure Sentinel）来避免盲人斑点，以跟踪跨 kill 链的潜在攻击者的活动。 日志可揭示用户是否能够成功读取受保护的内容，并确定哪些用户已阅读受保护的重要文档。 确保为其他分析师捕获见解和知识，并为将来的历史参考提供。  

Azure Sentinel 提供几乎针对任何日志源的广泛数据分析，并提供一个事例管理门户来管理事件的整个生命周期。 调查过程中的情报信息可与事件相关联，以便进行跟踪和报告。 

- [记录和分析 Azure 信息保护中的保护使用情况](https://docs.microsoft.com/azure/information-protection/log-analyze-usage)

- [使用 Azure Sentinel 调查事件](https://docs.microsoft.com/azure/sentinel/tutorial-investigate-cases)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="lt-6-configure-log-storage-retention"></a>LT-6：配置日志存储保留期

**指南**： Azure 信息保护为组织的文档和电子邮件提供数据保护，并为每个请求提供日志。  这些请求包括当用户保护文档和电子邮件时，当用户使用此内容时，管理员为此服务执行的操作，以及由 Microsoft 操作员执行的、用于支持 Azure 信息保护部署的操作。

在 Azure 信息保护工作区中收集和存储的数据量及其保留期对于每个租户都有很大的差异，具体取决于你的 Azure 信息保护客户端和其他受支持的终结点的数量，无论你是在收集终结点发现数据、已访问的受保护文档数，等等。

使用 Azure Monitor 日志的使用情况和估计成本功能来帮助估计和查看存储的数据量，还可以控制 Log Analytics 工作区的数据保留期。 

- [记录和分析 Azure 信息保护中的保护使用情况](https://docs.microsoft.com/azure/information-protection/log-analyze-usage)

- [使用 Azure Monitor 日志管理使用情况和成本](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)

**Azure 安全中心监视**：不适用

**责任**：客户

## <a name="incident-response"></a>事件响应

[有关详细信息，请参阅 *Azure 安全基线：* 事件响应](/azure/security/benchmarks/security-controls-v2-incident-response)。

### <a name="ir-1-preparation--update-incident-response-process-for-azure"></a>IR-1：准备 - 更新 Azure 的事件响应流程

**指导**：确保组织具有响应安全事件的流程，已为 Azure 更新这些流程，并定期运用这些流程来确保就绪性。

- [在企业环境中实现安全性](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [事件响应参考指南](https://docs.microsoft.com/microsoft-365/downloads/IR-Reference-Guide.pdf)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="ir-2-preparation--setup-incident-notification"></a>IR-2：准备 - 设置事件通知

**指导**：在 Azure 安全中心中设置安全事件联系人信息。 如果 Microsoft 安全响应中心 (MSRC) 发现非法或未经授权的一方访问了你的数据，Microsoft 将使用此联系信息来与你取得联系。 还可以选择基于事件响应需求在不同的 Azure 服务中自定义事件警报和通知。 

- [如何设置 Azure 安全中心安全联系人](https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details)

**Azure 安全中心监视**：是

**责任**：客户

### <a name="ir-3-detection-and-analysis--create-incidents-based-on-high-quality-alerts"></a>IR-3：检测和分析 - 基于高质量警报创建事件

**指导**：确保具有创建高质量警报和衡量警报质量的流程。 这样，你就可以从过去的事件中吸取经验，并为分析人员确定警报的优先级，这样他们就不会浪费时间来处理误报。 

可以基于过去的事件经验、经验证的社区源以及旨在通过融合和关联各种信号源来生成和清理警报的工具构建高质量警报。 

Azure 安全中心可跨多个 Azure 资产提供高质量的警报。 可以使用 ASC 数据连接器将警报流式传输到 Azure Sentinel。 借助 Azure Sentinel，可创建高级警报规则来自动生成事件以进行调查。 

使用导出功能导出 Azure 安全中心警报和建议，以帮助识别 Azure 资源的风险。 手动导出或持续导出警报和建议。

- [如何配置导出](https://docs.microsoft.com/azure/security-center/continuous-export)

- [如何将警报流式传输到 Azure Sentinel](https://docs.microsoft.com/azure/sentinel/connect-azure-security-center)

**Azure 安全中心监视**：目前不可用

**责任**：客户

### <a name="ir-4-detection-and-analysis--investigate-an-incident"></a>IR-4：检测和分析 - 调查事件

**指南**：确保分析师可以在调查潜在事件时，通过查询和使用不同的数据源来构建完整的视图。 通过收集各种不同的日志来跟踪跨 kill 链的潜在攻击者的活动，避免盲人斑点。 此外，请确保为其他分析师捕获见解和知识，并为将来的历史参考提供。  

用于调查的数据源包括已从作用域内服务和正在运行的系统中收集的集中式日志记录源，但还可以包括以下内容：

- 网络数据 - 使用网络安全组的流日志、Azure 网络观察程序和 Azure Monitor 来捕获网络流日志和其他分析信息。 

- 正在运行的系统的快照： 

    - 使用 Azure 虚拟机的快照功能创建正在运行的系统磁盘的快照。 

    - 使用操作系统的内置内存转储功能来创建运行系统内存的快照。

    - 使用 Azure 服务的快照功能或软件自带的功能来创建正在运行的系统的快照。

Azure Sentinel 提供几乎针对任何日志源的广泛数据分析，并提供一个事例管理门户来管理事件的整个生命周期。 调查过程中的情报信息可与事件相关联，以便进行跟踪和报告。 

- [Windows 计算机的磁盘快照](https://docs.microsoft.com/azure/virtual-machines/windows/snapshot-copy-managed-disk)

- [Linux 计算机的磁盘快照](https://docs.microsoft.com/azure/virtual-machines/linux/snapshot-copy-managed-disk)

- [Microsoft Azure 支持诊断信息和内存转储收集](https://azure.microsoft.com/support/legal/support-diagnostic-information-collection/) 

- [使用 Azure Sentinel 调查事件](https://docs.microsoft.com/azure/sentinel/tutorial-investigate-cases)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="ir-5-detection-and-analysis--prioritize-incidents"></a>IR-5：检测和分析 - 确定事件优先级

**指南**：根据警报严重性和资产敏感度，为分析人员提供上下文来确定应首要关注哪些事件。 

Azure 安全中心为每条警报分配严重性，方便你根据优先级来确定应该最先调查的警报。 严重性取决于安全中心对调查结果或用于发出警报的分析的可信度，以及对导致警报的活动背后存在恶意意图的可信度级别。

此外，使用标记来标记资源，并创建命名系统来对 Azure 资源进行标识和分类，特别是处理敏感数据的资源。  你的责任是根据发生事件的 Azure 资源和环境的关键性确定修正警报的优先级。

- [Azure 安全中心中的安全警报](https://docs.microsoft.com/azure/security-center/security-center-alerts-overview)

- [使用标记整理 Azure 资源](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

**Azure 安全中心监视**：目前不可用

**责任**：客户

### <a name="ir-6-containment-eradication-and-recovery--automate-the-incident-handling"></a>IR-6：包含、根除和恢复 - 自动执行事件处理

**指导**：自动执行手动重复性任务来加快响应时间并减轻分析人员的负担。 执行手动任务需要更长的时间，这会导致减慢每个事件的速度，并减少分析人员可以处理的事件数量。 手动任务还会使分析人员更加疲劳，这会增加可导致延迟的人为错误的风险，并降低分析人员专注于复杂任务的工作效率。 使用 Azure 安全中心和 Azure Sentinel 中的工作流自动化功能，可自动触发操作或运行 playbook，对传入的安全警报作出响应。 playbook 执行多项操作，如发送通知、禁用帐户和隔离有问题的网络。 

- [在安全中心配置工作流自动化](https://docs.microsoft.com/azure/security-center/workflow-automation)

- [在 Azure 安全中心设置自动威胁响应](https://docs.microsoft.com/azure/security-center/tutorial-security-incident#triage-security-alerts)

- [在 Azure Sentinel 中设置自动威胁响应](https://docs.microsoft.com/azure/sentinel/tutorial-respond-threats-playbook)

**Azure 安全中心监视**：目前不可用

**责任**：客户

## <a name="posture-and-vulnerability-management"></a>安全状况和漏洞管理

有关详细信息，请参阅 [Azure 安全基准：安全状况和漏洞管理](/azure/security/benchmarks/security-controls-v2-vulnerability-management)。

### <a name="pv-1-establish-secure-configurations-for-azure-services"></a>PV-1：为所有 Azure 服务建立安全配置 

**指南**： Azure 信息保护可以通过安全和合规中心进行配置，也可以通过 PowerShell 进行配置。 

在安全与合规中心内，管理员可以创建敏感度标签、定义每个标签可以执行的操作，以及发布标签。 

创建标签：根据组织的不同内容敏感度级别的分类分类创建和命名你的敏感度标签。 使用对用户有意义的通用名称或术语。 如果还没有已建立的分类，请考虑以标签名称（如 "个人"、"公共"、"常规"、"机密" 和 "高度机密"）开头。 然后，可以使用子标签按类别将相似的标签分组。 创建标签时，使用工具提示文本可帮助用户选择适当的标签。

定义每个标签可以执行的操作：配置要与每个标签关联的保护设置。 例如，你可能想要 (（例如 "常规" 标签）的低敏感度内容) 仅应用页眉或页脚，而较高的灵敏度内容 (如 "机密" 标签) 应具有水印和加密。

发布标签：配置敏感度标签后，使用标签策略发布它们。 确定哪些用户和组应具有标签以及要使用的策略设置。 单个标签可重复使用-你定义一次，然后可以将其包含在分配给不同用户的多个标签策略中。 例如，你可以通过将标签策略分配给几个用户，来试验你的敏感度标签。 然后，当你准备好在你的组织中推出标签时，你可以为标签创建新的标签策略，此时请指定 "所有用户"。

若要使用 PowerShell，请安装 AIPService PowerShell 模块。 在 PowerShell 中，管理员可以执行以下任务及其他任务： 

- 从本地 Rights Management (AD RMS 或 Windows RMS) 迁移到 Azure 信息保护
- 生成和管理自己的租户密钥-自带密钥 (BYOK) 方案
- 激活或停用组织的 Rights Management 服务
- 为 Azure Rights Management 服务的分阶段部署配置加入控制
- 为你的组织创建和管理 Rights Management 模板
- 管理有权为你的组织管理 Rights Management 服务的用户和组
- 记录和分析 Rights Management 的使用情况

有关详细信息，请参阅以下资源：

- [安全和合规中心中的敏感度标签入门](https://docs.microsoft.com/microsoft-365/compliance/get-started-with-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)

- [创建和发布敏感度标签](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)

- [将加密应用于敏感度标签](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)

- [适用于 Azure 信息保护的 PowerShell](https://docs.microsoft.com/azure/information-protection/administer-powershell)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="pv-8-conduct-regular-attack-simulation"></a>PV-8：执行定期攻击模拟

**指导**：根据需要，对 Azure 资源进行渗透测试或红队活动，并确保修正所有关键安全发现。
请遵循 Microsoft 云渗透测试互动规则，确保你的渗透测试不违反 Microsoft 政策。 使用 Microsoft 红队演练策略和执行，以及针对 Microsoft 托管云基础结构、服务和应用程序执行现场渗透测试。

- [Azure 中的渗透测试](https://docs.microsoft.com/azure/security/fundamentals/pen-testing)

- [参与的渗透测试规则](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Microsoft 云红色组合](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Azure 安全中心监视**：不适用

**责任**：共享

## <a name="backup-and-recovery"></a>备份和恢复

有关详细信息，请参阅 [Azure 安全基准：备份和恢复](/azure/security/benchmarks/security-controls-v2-backup-recovery)。

### <a name="br-4-mitigate-risk-of-lost-keys"></a>BR-4：减少密钥丢失风险

**指南**：通过 Azure 信息保护，客户可以通过创建自己的密钥 (BYOK) ，使用自己的密钥配置其租户。 客户生成的密钥必须存储在 Azure Key Vault 中进行保护。 Azure Key Vault 有助于防止密钥通过软删除、角色分隔和分隔安全域丢失。 

- [Azure 信息保护创建自己的密钥和与 Azure Key Vault 的集成](https://docs.microsoft.com/azure/information-protection/byok-price-restrictions)
- [在 Key Vault 中启用软删除](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete?tabs=azure-portal)

**Azure 安全中心监视**：是

**责任**：客户

## <a name="governance-and-strategy"></a>治理和策略

有关详细信息，请参阅 [Azure 安全基准：治理和策略](/azure/security/benchmarks/security-controls-v2-governance-strategy)。

### <a name="gs-1-define-asset-management-and-data-protection-strategy"></a>GS-1：定义资产管理和数据保护策略 

**指导**：确保为系统和数据的持续监视和保护记录并传达明确的策略。 确定业务关键数据和系统的发现、评估、保护和监视优先级。 

此策略应包括针对以下元素的记录在案的指南、策略和标准： 

-   与业务风险相符的数据分类标准

-   安全组织对风险和资产清单的洞察力 

-   安全组织对 Azure 服务使用的审批 

-   资产在其生命周期中的安全性

-   与组织数据分类相符的必需访问控制策略

-   使用 Azure 内置和第三方数据保护功能

-   传输中数据用例和静态数据用例的数据加密要求

-   合适的加密标准

有关详细信息，请参阅以下资源：

- [Azure 安全体系结构建议 - 存储、数据和加密](https://docs.microsoft.com/azure/architecture/framework/security/storage-data-encryption?toc=/security/compass/toc.json&amp;bc=/security/compass/breadcrumb/toc.json)

- [Azure 安全基础知识 - Azure 数据安全、加密和存储](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview)

- [云采用框架 - Azure 数据安全和加密最佳做法](https://docs.microsoft.com/azure/security/fundamentals/data-encryption-best-practices?toc=/azure/cloud-adoption-framework/toc.json&amp;bc=/azure/cloud-adoption-framework/_bread/toc.json)

- [Azure 安全基准 - 资产管理](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-asset-management)

- [Azure 安全基准 - 数据保护](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-data-protection)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="gs-2-define-enterprise-segmentation-strategy"></a>GS-2：定义企业分段策略 

**指导**：建立企业范围的策略，以便使用标识、网络、应用程序、订阅、管理组和其他控件的组合来细分对资产的访问。

仔细权衡安全分离需求与为需要彼此通信并访问数据的系统启用日常操作的需求。

确保跨控制类型（包括网络安全、标识和访问模型、应用程序权限/访问模型，以及人机过程控制）一致地实现分段策略。

- [有关 Azure 中的分段策略的指南（视频）](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151)

- [有关 Azure 中的分段策略的指南（文档）](https://docs.microsoft.com/security/compass/governance#enterprise-segmentation-strategy)

- [使网络分段与企业分段策略相匹配](https://docs.microsoft.com/security/compass/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="gs-3-define-security-posture-management-strategy"></a>GS-3：定义安全状况管理策略

**指导**：持续衡量并缓解你的个人资产及其托管环境的风险。 确定高价值资产和暴露程度高的受攻击面（例如已发布的应用程序、网络入口和出口点、用户和管理员终结点等）的优先级。

- [Azure 安全基准 - 状况和漏洞管理](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-posture-vulnerability-management)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="gs-4-align-organization-roles-responsibilities-and-accountabilities"></a>GS-4：协调组织角色、职责和责任

**指导**：确保为安全组织中的角色和责任记录并传达明确的策略。 优先考虑提供涉及安全决策的明确责任，对每个人进行共同职责模式培训，并为技术团队传授保护云的技术。

- [Azure 安全最佳做法 1 - 人员：针对云安全历程培训团队](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#1-people-educate-teams-about-the-cloud-security-journey)

- [Azure 安全最佳做法 2 - 人员：针对云安全技术培训团队](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#2-people-educate-teams-on-cloud-security-technology)

- [Azure 安全最佳做法 3 - 流程：针对云安全决策分配责任](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="gs-5-define-network-security-strategy"></a>GS-5：定义网络安全策略

**指导**：建立 Azure 网络安全方法，作为组织整体安全访问控制策略的一部分。  

此策略应包括针对以下元素的记录在案的指南、策略和标准： 

-   集中化的网络管理和安全职责

-   符合企业分段策略的虚拟网络分段模型

-   各种威胁和攻击场景中的补救策略

-   Internet 边缘及入口和出口策略

-   混合云和本地互连策略

-   最新的网络安全项目（例如网络关系图、参考网络体系结构）

有关详细信息，请参阅以下资源：
- [Azure 安全最佳做法 11 - 体系结构。单一的统一安全策略](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Azure 安全基准 - 网络安全](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-network-security)

- [Azure 网络安全概述](https://docs.microsoft.com/azure/security/fundamentals/network-overview)

- [企业网络体系结构策略](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/architecture)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="gs-6-define-identity-and-privileged-access-strategy"></a>GS-6：定义标识和特权访问策略

**指导**：建立 Azure 标识和特权访问方法，作为组织整体安全访问控制策略的一部分。  

此策略应包括针对以下元素的记录在案的指南、策略和标准： 

-   集中化的标识和身份验证系统及其与其他内部和外部标识系统的互连

-   各种用例和条件中的强身份验证方法

-   保护权限高的用户

-   异常用户活动监视和处理  

-   用户标识和访问评审及协调流程

有关详细信息，请参阅以下资源：

- [Azure 安全基准 - 标识管理](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-identity-management)

- [Azure 安全基准 - 特权访问](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-privileged-access)

- [Azure 安全最佳做法 11 - 体系结构。单一的统一安全策略](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Azure 标识管理安全概述](https://docs.microsoft.com/azure/security/fundamentals/identity-management-overview)

**Azure 安全中心监视**：不适用

**责任**：客户

### <a name="gs-7-define-logging-and-threat-response-strategy"></a>GS-7：定义日志记录和威胁响应策略

**指导**：建立日志记录和威胁响应策略，以快速检测和修正威胁，同时满足合规性要求。 优先为分析人员提供高质量警报和无缝体验，以便他们能够专注于威胁而不是集成和手动步骤。 

此策略应包括针对以下元素的记录在案的指南、策略和标准： 

-   安全运营 (SecOps) 组织的角色和职责 

-   符合 NIST 或其他行业框架要求的明确定义的事件响应流程 

-   日志捕获和保留，用于支持威胁检测、事件响应和合规性需求

-   使用 SIEM、内置的 Azure 功能和其他源，集中查看和关联有关威胁的信息 

-   与客户、供应商和公开的利益相关方之间的通信和通知计划

-   使用 Azure 内置和第三方平台进行事件处理，如日志记录和威胁检测、辩论以及攻击补救和根除

-   处理事件和事件后活动的流程，例如经验教训和证据保留

有关详细信息，请参阅以下资源：

- [Azure 安全基准 - 日志记录和威胁检测](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-logging-threat-detection)

- [Azure 安全基准 - 事件响应](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-incident-response)

- [Azure 安全最佳做法 4 - 流程。更新云的事件响应流程](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Azure 采用框架、日志记录和报告决策指南](https://docs.microsoft.com/azure/cloud-adoption-framework/decision-guides/logging-and-reporting/)

- [Azure 企业规模、管理和监视](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/management-and-monitoring)

**Azure 安全中心监视**：不适用

**责任**：客户

## <a name="next-steps"></a>后续步骤

- 参阅 [Azure 安全基准 V2 概述](/azure/security/benchmarks/overview)
- 详细了解 [Azure 安全基线](/azure/security/benchmarks/security-baselines-overview)
