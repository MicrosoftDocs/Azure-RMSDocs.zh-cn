---
title: Azure 信息保护的常见问题解答
description: 有关 Azure 信息保护及其数据保护服务 Azure Rights Management (Azure RMS) 的一些常见问题。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4e7ffa1fa4121d7a0aecc4474d50497c7c300b1b
ms.sourcegitcommit: 55782e58508051f0ecf460e8b126f70ab9b9ceec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2019
ms.locfileid: "56756141"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Azure 信息保护的常见问题

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

是否有关于 Azure 信息保护或 Azure Rights Management 服务 (Azure RMS) 的问题？ 请查看此处是否有答案。

这些常见问题页将定期更新，其中新添加的内容将在 [Azure 信息保护技术博客](https://aka.ms/AIPblog)上的每月文档更新公告中列出。

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Azure 信息保护和 Microsoft 信息保护之间有何不同？

与 Azure 信息保护不同，Microsoft 信息保护不是可以购买的订阅或产品。 相反，它是可帮助你保护组织的敏感信息的产品和集成功能的框架：

- 此框架中的各个产品包括 Azure 信息保护、Office 365 信息保护（例如，Office 365 DLP）、Windows 信息保护和 Microsoft Cloud App Security。 

- 此框架中的集成功能包括统一标记管理、基于 Office 应用的最终用户标记体验、Windows 了解统一标记并将保护应用于数据的能力、Microsoft 信息保护 SDK、以及 Adobe Acrobat Reader 中用于查看已标记且受保护的 PDF 的新功能。

有关详细信息，请参阅[宣布推出信息保护功能以帮助保护你的敏感数据](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)。

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Azure 信息保护中的标签和 Office 365 中的标签之间有何不同？

最初，Office 365 还只有[保留标签](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30)，用于在文档和电子邮件处于 Office 365 服务中时，对该内容进行分类以供审核和保留。 相比之下，通过 Azure 信息保护标记，可对文档和电子邮件应用一致分类和保护策略，无论它们在本地还是在云中。

除了 Office 365 安全与合规中心的保留标签外，现在还可以选择创建和配置[敏感度标签](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels)的选项，该选项是在奥兰多的 Microsoft Ignite 2018 大会上推出的。 当前该选项处于预览状态，你可以将现有的 Azure 信息保护标签迁移到新的统一标签存储，以用作 Office 365 的敏感度标签。 

有关统一标记管理以及如何支持这些标记的详细信息，请阅读博客文章[宣布推出信息保护功能以帮助保护你的敏感数据](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)。

有关迁移现有标记的详细信息，请参阅[如何将 Azure 信息保护标记迁移到 Office 365 安全与合规中心](configure-policy-migrate-labels.md)。

## <a name="when-is-the-right-time-to-migrate-my-labels-to-office-365"></a>何时将我的标签迁移到 Office 365？

Office 365 安全与合规中心中的敏感度标签已正式发布，但迁移 Azure 信息保护标签的选项仍处于预览状态。 将标签迁移到统一标签存储后，可以发布这些标签，然后由[支持统一标签的客户端](configure-policy-migrate-labels.md#clients-that-support-unified-labeling)下载。 目前，并非所有客户端都支持统一标签或已公开发布。

我们建议首先使用测试租户测试预览功能，然后再迁移生产租户。 此外：

- **如果刚开始接触 Azure 信息保护：** 
    
    由于 Azure 信息保护具有加速部署的默认标签，因此我们建议先迁移这些默认标签，然后从 Office 365 安全与合规中心进行管理。

- **如果并非刚开始接触 Azure 信息保护，但是正在定义和配置要使用的标签：**
    
    我们建议先在 Azure 门户中完成标签配置，然后迁移这些标签。 此策略可以避免在迁移过程中重复标签，然后需要在安全与合规中心进行编辑。

在迁移标签之前，请确保你了解[安全与合规中心不支持的注意事项和标签设置](configure-policy-migrate-labels.md#considerations-for-unified-labels)。

另请参阅[安装哪个预览客户端来测试新功能？](faqs-infoprotect.md#which-preview-client-do-i-install-for-testing-new-functionality)

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>迁移我的标签后，该使用哪个管理门户？

在 Azure 门户中迁移标签后：

- 如果拥有[统一标签客户端](configure-policy-migrate-labels.md#clients-that-support-unified-labeling)，请转至 Office 365 安全与合规中心以发布这些标签，并为统一标签客户端配置策略设置。 对于未来的标签更改，请使用安全与合规中心。 统一标签客户端从安全与合规中心下载标签和策略设置。

- 如果拥有 [Azure 信息保护客户端](./rms-client/aip-client.md)，请继续使用 Azure 门户编辑标签和策略设置。 Azure 信息保护客户端继续从 Azure 下载标签和策略设置。

- 如果同时拥有[统一标签客户端](configure-policy-migrate-labels.md#clients-that-support-unified-labeling)和 [Azure 信息保护客户端](./rms-client/aip-client.md)，则可以使用任一门户进行标签更改。 但是，要使 Azure 信息保护客户端选择你在安全与合规中心中所做的标签更改，则必须返回 Azure 门户：使用 Azure 门户中“Azure 信息保护 - 统一标签”边栏选项卡的“发布”选项。 

继续使用 Azure 门户进行[集中报告](reports-aip.md)和[扫描程序](deploy-aip-scanner-preview.md)。

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure 信息保护和 Azure Rights Management 之间有何不同？

Azure 信息保护对组织的文档和电子邮件进行分类、标记和保护。 该保护技术使用 Azure Rights Management 服务；现在该服务是 Azure 信息保护的一个组件。

## <a name="what-is-the-role-of-identity-management-for-azure-information-protection"></a>Azure 信息保护的身份管理的角色是什么？

用户必须具有有效的用户名和密码才能访问受 Azure 信息保护保护的内容。 要详细了解 Azure 信息保护如何帮助保护数据，请参阅 [Azure 信息保护在保护数据方面的角色](/enterprise-mobility-security/solutions/azure-information-protection-securing-data)。 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>需要为 Azure 信息保护准备哪个订阅，以及它包括哪些功能？

请参阅 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)页面上的订阅信息和功能列表。

如果你的 Office 365 订阅包含 Azure Rights Management 数据保护，请下载 [Azure 信息保护许可数据表](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)。

还有关于许可的问题吗？ 查看[许可的常见问答解答](https://azure.microsoft.com/pricing/details/information-protection#faq)部分是否有答案。

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Azure 信息保护客户端是否只适用于包含分类和标记的订阅？

不能。 尽管你所参阅的关于 Azure 信息保护客户端的大部分演示文稿和演示都指出此类客户端支持分类和标记，但它还可以与只包含 Azure Rights Management Service 的订阅结合使用来共同保护数据。

如果安装了适用于 Windows 的 Azure 信息保护客户端，但没有 Azure 信息保护策略，那么客户端会在[仅保护模式](./rms-client/client-protection-only-mode.md)下自动运行。 在这种模式下，用户可以轻松应用 Rights Management 模板和自定义权限。 如果以后购买确实包含分类和标记的订阅，客户端会在下载 Azure 信息保护策略后自动切换到标准模式。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>是否必须是全局管理员才能配置 Azure 信息保护？我可以委派给其他管理员吗？

很显然，Office 365 租户或 Azure AD 租户的全局管理员可以运行 Azure 信息保护的所有管理任务。 但是，如果想要将管理权限分配给其他用户，可以使用以下选项：

- **信息保护管理员**：此 Azure Active Directory 管理员角色允许管理员配置 Azure 信息保护的所有方面，但不能配置其他服务。 具有此角色的管理员可以激活和停用 Azure Rights Management 保护服务，配置保护设置和标签，并配置 Azure 信息保护策略。 此外，具有此角色的管理员可以运行针对 [Azure 信息保护客户端](./rms-client/client-admin-guide-powershell.md)以及来自 [AADRM 模块](administer-powershell.md)的所有 PowerShell cmdlet。 
    
    若要将用户分配到此管理角色，请参阅[将用户分配到 Azure Active Directory 中的管理员角色](/azure/active-directory/active-directory-users-assign-role-azure-portal)。

- **安全读者**：仅适用于 [Azure 信息保护分析](reports-aip.md)。 此 Azure Active Directory 管理员角色允许管理员查看标签的使用方式，监视用户对标记文档和电子邮件的访问权限以及对其分类所做的任何更改，并且可以识别包含必须受到保护的敏感信息的文档。 由于此功能使用 Azure Log Analytics，因此用户还必须具有支持的 [RBAC 角色](reports-aip.md#permissions-required-for-azure-information-protection-analytics)。

- **安全管理员**：此 Azure Active Directory 管理员角色允许管理员在 Azure 门户中配置 Azure 信息保护的所有方面，同时还可以配置其他 Azure 服务的某些方面。 具有此角色的管理员无法运行任何[来自 AADRM 模块的 PowerShell cmdlet](administer-powershell.md)。
    
    若要将用户分配到此管理角色，请参阅[将用户分配到 Azure Active Directory 中的管理员角色](/azure/active-directory/active-directory-users-assign-role-azure-portal)。 若要查看具有此角色的用户还拥有哪些其他权限，请参阅 Azure Active Directory 文档的[可用角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles)部分。

- Azure Rights Management 全局管理员和连接器管理员：对于这些 Azure Rights Management 管理员角色，第一个可授予用户权限以运行所有[来自 AADRM 模块的 PowerShell cmdlet](administer-powershell.md) 而不使其成为其他云服务的全局管理员，第二个角色授予权限来仅运行 Rights Management (RMS) 连接器。 这两种管理角色都不会授权访问管理控制台，也不会授权在文档跟踪网站中使用管理模式。

    若要分配其中任一管理角色，请使用 AADRM PowerShell cmdlet [Add-aadrmrolebasedadministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator)。

需要注意的事项：

- 如果配置了[加入控制](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，此配置不会影响管理 Azure 信息保护的能力（RMS 连接器除外）。 例如，如果配置了加入控制，以致仅允许“IT 部门”组保护内容，那么，用于安装和配置 RMS 连接器的帐户必须是该组的成员。 

- 分配了管理角色的用户无法从受 Azure 信息保护保护的文档或电子邮件中自动删除保护。 只有在启用了超级用户功能的情况下，分配为超级用户的用户才能执行此操作。 但是，你将管理权限分配给 Azure 信息保护的任何用户可以将用户分配为超级用户，包括其自己的帐户。 他们还可以启用超级用户功能。 这些操作记录在管理员日志中。 有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](configure-super-users.md)中的“最佳安全做法”部分。 

- 如果要将 Azure 信息保护标签迁移到 Office 365，请务必阅读标签迁移文档中的以下部分：[有关管理角色的重要信息](configure-policy-migrate-labels.md#important-information-about-administrative-roles)。

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure 信息保护是否支持本地和混合方案？

是。 尽管 Azure 信息保护是基于云的解决方案，但它可对存储在本地和云中的文档和电子邮件进行分类、标签设置和保护。

如果具有 Exchange Server、SharePoint Server 和 Windows 文件服务器，可以部署 [Rights Management 连接器](deploy-rms-connector.md)，以便这些本地服务器使用 Azure Rights Management 服务保护电子邮件和文档。 还可以使用 [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect)，将 Active Directory 域控制器与 Azure AD 同步和联合，为用户提供更为契合的身份验证体验。

Azure Rights Management 服务根据需要自动生成并管理 XrML 证书，因此它不使用本地 PKI。 有关 Azure Rights Management 如何使用证书的详细信息，请参阅 [Azure RMS 工作原理演练：首次使用、内容保护、内容使用](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)部分（[Azure RMS 的工作原理](./how-does-it-work.md)文章中）。

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Azure 信息保护可以分类和保护哪些类型的数据？

Azure 信息保护可以分类和保护电子邮件和文档，无论它们是位于本地还是云中。 这些文档包括 Word 文档、Excel 电子表格，PowerPoint 演示文稿、PDF 文档、基于文本的文件和图像文件。 有关支持的文档类型的列表，请参阅管理员指南中的[支持文件类型](./rms-client/client-admin-guide-file-types.md)列表。

Azure 信息保护不能分类和保护结构化数据，如数据库文件、日历项、PowerBI 报表、Yammer 帖子、Sway 内容和 OneNote 笔记本。

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>我看到 Azure 信息保护被列为可用于条件访问的云应用 - 工作原理是什么？

是，作为预览版产品/服务，现可为 Azure 信息保护配置 Azure AD 条件访问。

当用户打开受 Azure 信息保护保护的文档时，管理员现可基于标准条件访问控制，阻止其租户中用户的访问或授予他们访问权限。 最常见的请求条件之一是需要多重身份验证 (MFA)。 另一常见请求条件是，设备必须[遵守 Intune 策略](/intune/conditional-access-intune-common-ways-use)（以便移动设备满足密码要求和最低操作系统版本），并且计算机必须已加入域。

有关详细信息和部分演示示例，请参阅以下博客文章：[Azure 信息保护的条件性访问策略](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/)。

其他信息:

- 对于 Windows 计算机：对于当前预览版本，[初始化用户环境](./how-does-it-work.md#initializing-the-user-environment)时会对 Azure 信息保护的条件访问策略进行评估（此过程也称为引导），之后每 30 天评估一次。

- 建议对条件访问策略的评估频率进行微调。 可通过配置令牌生存期来执行此操作。 有关详细信息，请参阅 [Azure Active Directory 中的可配置令牌生存期](/azure/active-directory/active-directory-configurable-token-lifetimes)。

- 建议不要将管理员帐户添加到条件访问策略，因为这些帐户无法访问 Azure 门户中的“Azure 信息保护”边栏选项卡。

- 如果在条件访问策略中使用 MFA 与其他组织展开协作 (B2B)，则必须使用 [Azure AD B2B 协作](/azure/active-directory/b2b/what-is-b2b)，并为要在其他组织中共享的用户创建来宾帐户。

- 由于 Azure AD 2018 年 12 月预览版的发布，现在可以在用户第一次打开受保护文档之前提示他们接受使用条款。 有关详细信息，请参阅以下博客文章声明：[条件访问范围内对 Azure AD 使用条款功能的更新](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822)

- 如果针对条件访问使用许多云应用，则列表中可能不会显示“Microsoft Azure 信息保护”选项，因此无法进行选择。 在这种情况下，可使用列表顶部的搜索框。 开始键入“Microsoft Azure 信息保护”，筛选可用应用。 如果已有受支持的订阅，则可以看到“Microsoft Azure 信息保护”选项，可进行选择。 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>我看到 Azure 信息保护被列为 Microsoft Graph 安全提供商，它是如何工作的？我将收到哪些警报？

是，作为公共预览版产品/服务，现可收到有关 **Azure 信息保护异常数据访问**的警报。 当尝试访问由 Azure 信息保护进行保护的数据存在异常时，将触发此警报。 例如，访问大量的数据，在某天的异常时间访问或者从未知位置访问。

此类警报可以帮助你检测环境中与数据相关的高级攻击和内部威胁。 这些警报使用机器学习来分析访问受保护数据的用户的行为。 

可以通过[使用 Microsoft Graph 安全 API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/security-api-overview) 来访问 Azure信息保护警报，也可以使用 Azure Monitor 将[警报流式传输](https://developer.microsoft.com/graph/docs/concepts/security_siemintegration)到 SIEM 解决方案，例如 Splunk 和 IBM Qradar。

有关 Microsoft Graph 安全 API 的详细信息，请参阅 [Microsoft Graph 安全 API 概述](https://developer.microsoft.com/graph/docs/concepts/security-concept-overview)。

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Windows Server FCI 和 Azure 信息保护扫描程序有何区别？

Windows Server 文件分类基础结构在过去一直都有一个选项：对文档进行分类，然后使用 [Rights Management 连接器](deploy-rms-connector.md)（仅 Office 文档）或 [PowerShell 脚本](./rms-client/configure-fci.md)（所有文件类型）保护文档。 

我们现在建议你使用 [Azure 信息保护扫描程序](deploy-aip-scanner.md)。 扫描程序使用 Azure 信息保护客户端和 Azure 信息保护策略来为文档（所有文件类型）添加标签，然后可以对这些文档进行分类并且还可根据需要保护文档。

这两种解决方案的主要差异是：

|Windows Server FCI|Azure 信息保护扫描程序|
|--------------------------------|-------------------------------------|
|支持的数据存储： <br /><br />- Windows Server 上的本地文件夹|支持的数据存储： <br /><br />- Windows Server 上的本地文件夹<br /><br />- Windows 文件共享和网络连接存储<br /><br />- SharePoint Server 2016 和 SharePoint Server 2013。 对于具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)的客户，还支持 SharePoint Server 2010。|
|操作模式： <br /><br />- 实时|操作模式： <br /><br />- 系统地抓取数据存储，且此周期可以运行一次或多次|
|对文件类型的支持： <br /><br />- 默认保护所有文件类型 <br /><br />- 通过编辑注册表，可以从保护配置中排除特定文件类型|对文件类型的支持： <br /><br />- 默认保护 Office 文件类型和 PDF 文档 <br /><br />- 通过编辑注册表，可以将其他文件类型纳入保护|

目前，在本地文件夹或网络共享上受到保护的文件设置 [Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)方面存在差异。 默认情况下，这两个解决方案的 Rights Management 所有者均设置为保护文件的帐户，但可以替代此设置：

- 对于 Windows Server FCI：可以将所有文件的 Rights Management 所有者设置为单个帐户，也可以为每个文件动态设置 Rights Management 所有者。 若要动态设置 Rights Management 所有者，请使用 -OwnerMail [源文件所有者电子邮件] 参数和值。 此配置使用文件“所有者”属性中的用户帐户名从 Active Directory 检索用户的电子邮件地址。

- 对于 Azure 信息保护扫描程序：对于新受保护的文件，可以将指定数据存储上所有文件的 Rights Management 所有者设置为单个帐户，但不能为每个文件动态设置 Rights Management 所有者。 对先前受保护的文件，不更改 Rights Management 所有者。 若要为新的受保护的文件设置帐户，请在扫描程序配置文件中指定“-默认所有者”设置。 

扫描程序保护 SharePoint 网站和库上的文件时，通过使用 SharePoint 编辑者值来动态地设置每个文件的 Rights Management 所有者。

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>听说很快将发布新版 Azure 信息保护 — 何时发布？

本技术文档不包含即将发布的版本的相关信息。 有关此类信息和发布公告，请查看 [Enterprise Mobility and Security Blog](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services)（企业移动性和安全性博客）并在 Twitter 上从 [MicrosoftMobility@MSFTMobility](https://twitter.com/MSFTMobility) 了解最新更新。 如果你对 Office 版本感兴趣，还请务必查看 [Office 365 博客](https://techcommunity.microsoft.com/t5/Office-365-Blog/bg-p/Office365Blog)和 [Office 应用博客](https://techcommunity.microsoft.com/t5/Office-Apps-Blog/bg-p/OfficeAppsBlog)。

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure 信息保护是否适用于我所在的国家/地区？

不同国家/地区的要求和法规不同。 要帮助你的组织回答此问题，请参阅[针对不同国家/地区的适用性](./compliance.md#suitability-for-different-countries)。

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Azure 信息保护如何帮助你符合 GDPR？

要了解 Azure 信息保护如何帮助你满足一般数据保护条例 (GDPR) 的要求，请参阅包含视频的下列博客文章公告：[Microsoft 365 提供可帮助你符合 GDPR 的信息保护策略](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr)。

## <a name="where-can-i-find-supporting-information-for-azureinformation-protectionsuch-as-legal-compliance-and-slas"></a>在何处可以找到 Azure 信息保护的支持信息 — 例如法律、合规性和 SLA？
请参阅 [Azure 信息保护的合规性和支持信息](./compliance.md)。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>如何针对 Azure 信息保护报告问题或发送反馈？

若要获取技术支持，请使用标准支持渠道或[联系 Microsoft 支持](information-support.md#to-contact-microsoft-support)。

有关改进建议或新功能的反馈，请参阅：在 Office 应用程序中，在“主页”选项卡的“保护”组中单击“保护”，然后单击“帮助和反馈”。 在“Microsoft Azure 信息保护”对话框中，单击“发送反馈”。 选择此选项将打开一封要发送到信息保护团队的电子邮件。

我们还邀请你加入我们的工程团队：[Azure 信息保护 Yammer 站点](https://www.yammer.com/askipteam/)。 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>如果我的问题不在这里，我该如何操作？

首先，查看以下特定于分类和标签，或特定于数据保护的常见问题解答。 Azure Rights Management 服务 (Azure RMS) 为 Azure 信息保护提供数据保护技术。 Azure RMS 可与分类和标签结合使用，也可单独使用。 

- [分类和标签的常见问题解答](faqs-infoprotect.md)

- [数据保护的常见问题解答](faqs-rms.md)

如果问题没有回复，请使用 [Azure 信息保护的信息和支持](information-support.md)中列出的链接和资源。

此外，我们还为最终用户制作了常见问题解答：

- [适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题解答](./rms-client/mobile-app-faq.md)

- [适用于 Mac 计算机的 RMS 共享应用的常见问题解答](https://technet.microsoft.com/dn451248)

