---
title: Azure 信息保护的常见问题解答
description: 有关 Azure 信息保护及其数据保护服务 Azure Rights Management (Azure RMS) 的一些常见问题。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/03/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 37619ad71fea842617556219c1684a3e837c3cc7
ms.sourcegitcommit: 3af39b88d321d75038caad266e906f6e622011d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Azure 信息保护的常见问题

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

是否有关于 Azure 信息保护或 Azure Rights Management 服务 (Azure RMS) 的问题？ 请查看此处是否有答案。

这些常见问题页将定期更新，其中新添加的内容将在 [Azure 信息保护技术博客](https://aka.ms/AIPblog)上的每月文档更新公告中列出。

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure 信息保护和 Azure Rights Management 之间有何不同？

Azure 信息保护对组织的文档和电子邮件进行分类、标记和保护。 该保护技术使用 Azure Rights Management 服务；现在该服务是 Azure 信息保护的一个组件。

## <a name="what-is-the-role-of-identity-management-for-azure-information-protection"></a>Azure 信息保护的身份管理的角色是什么？

用户必须具有有效的用户名和密码才能访问受 Azure 信息保护保护的内容。 要详细了解 Azure 信息保护如何帮助保护数据，请参阅 [Azure 信息保护在保护数据方面的角色](/enterprise-mobility-security/solutions/azure-information-protection-securing-data)。 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>需要为 Azure 信息保护准备哪个订阅，以及它包括哪些功能？
请参阅 [Azure 信息保护](https://azure.microsoft.com/en-us/pricing/details/information-protection)页面上的订阅信息和功能列表。 

如果你的 Office 365 订阅包含 Azure Rights Management 数据保护，请下载 [Azure 信息保护许可数据表](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)，其中还包含一些有关许可的常见问题解答。

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Azure 信息保护客户端是否只适用于包含分类和标记的订阅？

不能。 尽管你所参阅的关于 Azure 信息保护客户端的大部分演示文稿和演示都指出此类客户端支持分类和标记，但它还可以与只包含 Azure Rights Management Service 的订阅结合使用来共同保护数据。

如果安装了适用于 Windows 的 Azure 信息保护客户端，但没有 Azure 信息保护策略，那么客户端会在[仅保护模式](../rms-client/client-protection-only-mode.md)下自动运行。 在这种模式下，用户可以轻松应用 Rights Management 模板和自定义权限。 如果以后购买确实包含分类和标记的订阅，客户端会在下载 Azure 信息保护策略后自动切换到标准模式。

如果当前使用 Windows 版 Rights Management 共享应用程序，建议使用 Azure 信息保护客户端替换此应用程序。 将于 2019 年 1 月 31 日停止提供对共享应用程序的支持。 若要顺利过渡，请参阅[用于操作 RMS 共享应用程序的任务](../rms-client/upgrade-client-app.md)。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>是否必须是全局管理员才能配置 Azure 信息保护？我可以委派给其他管理员吗？

很显然，Office 365 租户或 Azure AD 租户的全局管理员可以运行 Azure 信息保护的所有管理任务。 但是，如果想要将管理权限分配给其他用户，可以使用以下选项：

- 信息保护管理员：此 Azure Active Directory 管理员角色允许管理员配置 Azure 信息保护的所有方面，但不能配置其他服务。 具有此角色的管理员可以激活和停用 Azure Rights Management 保护服务，配置保护设置和标签，并配置 Azure 信息保护策略。 此外，具有此角色的管理员可以运行针对 [Azure 信息保护客户端](../rms-client/client-admin-guide-powershell.md)以及来自 [AADRM 模块](../deploy-use/administer-powershell.md)的所有 PowerShell cmdlet。 
    
    若要将用户分配到此管理角色，请参阅[将用户分配到 Azure Active Directory 中的管理员角色](/azure/active-directory/active-directory-users-assign-role-azure-portal)。

- **安全管理员**：此 Azure Active Directory 管理员角色允许管理员在 Azure 门户中配置 Azure 信息保护的所有方面，同时还可以配置其他 Azure 服务的某些方面。 具有此角色的管理员无法运行任何[来自 AADRM 模块的 PowerShell cmdlet](../deploy-use/administer-powershell.md)。
    
    若要将用户分配到此管理角色，请参阅[将用户分配到 Azure Active Directory 中的管理员角色](/azure/active-directory/active-directory-users-assign-role-azure-portal)。 若要查看具有此角色的用户还拥有哪些其他权限，请参阅 Azure Active Directory 文档的[可用角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles)部分。

- Azure Rights Management **全局管理员**和**连接器管理员**：对于这些 Azure Rights Management 管理员角色，第一个可授予用户权限以运行所有[来自 AADRM 模块的 PowerShell cmdlet](../deploy-use/administer-powershell.md) 而不使其成为其他云服务的全局管理员，第二个角色授予权限来仅运行 Rights Management (RMS) 连接器。 这些管理角色都不会授予对管理控制台的权限。

    若要分配其中任一管理角色，请使用 AADRM PowerShell cmdlet [Add-aadrmrolebasedadministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator)。

需要注意的事项：

- 如果配置了[加入控制](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，此配置不会影响管理 Azure 信息保护的能力（RMS 连接器除外）。 例如，如果配置了加入控制，以致仅允许“IT 部门”组保护内容，那么，用于安装和配置 RMS 连接器的帐户必须是该组的成员。 

- 分配了管理角色的用户无法从受 Azure 信息保护保护的文档或电子邮件中自动删除保护。 只有在启用了超级用户功能的情况下，分配为超级用户的用户才能执行此操作。 但是，你将管理权限分配给 Azure 信息保护的任何用户可以将用户分配为超级用户，包括其自己的帐户。 他们还可以启用超级用户功能。 这些操作记录在管理员日志中。 有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)中的“最佳安全做法”部分。 


## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure 信息保护是否支持本地和混合方案？

是。 尽管 Azure 信息保护是基于云的解决方案，但它可对存储在本地和云中的文档和电子邮件进行分类、标签设置和保护。

如果具有 Exchange Server、SharePoint Server 和 Windows 文件服务器，则可部署[权限管理连接器](../deploy-use/deploy-rms-connector.md)，便于这些本地服务器可使用 Azure 权限管理服务保护电子邮件和文档。 你还可以使用 [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)，将 Active Directory 域控制器与 Azure AD 同步和联合，为用户提供更为契合的身份验证体验。

Azure 权限管理服务根据需要自动生成并管理 XrML 证书，因此它不使用本地 PKI。 有关 Azure Rights Management 如何使用证书的详细信息，请参阅 [Azure RMS 的工作原理](../understand-explore/how-does-it-work.md)一文中的 [Azure RMS 工作演练：首次使用、内容保护、内容使用](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)。

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Azure 信息保护可以分类和保护哪些类型的数据？

Azure 信息保护可以分类和保护电子邮件和文档，无论它们是位于本地还是云中。 这些文档包括 Word 文档、Excel 电子表格，PowerPoint 演示文稿、PDF 文档、基于文本的文件和图像文件。 有关支持的文档类型的列表，请参阅管理员指南中的[支持文件类型](../rms-client/client-admin-guide-file-types.md)列表。

Azure 信息保护不能分类和保护结构化数据，如数据库文件、日历项、PowerBI 报表、Yammer 帖子、Sway 内容和 OneNote 笔记本。

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>我看到 Azure 信息保护被列为可用于条件访问的云应用 - 工作原理是什么？

是，作为公共预览版产品/服务，现可为 Azure 信息保护配置 Azure AD 条件访问。

当用户打开受 Azure 信息保护保护的文档时，管理员现可基于标准条件访问控制，阻止其租户中用户的访问或授予他们访问权限。 最常见的请求条件之一是需要多重身份验证 (MFA)。 另一常见请求条件是，设备必须[遵守 Intune 策略](/intune/conditional-access-intune-common-ways-use)（以便移动设备满足密码要求和最低操作系统版本），并且计算机必须已加入域。

有关详细信息和演练示例，请参阅以下博客文章：[Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/)（Azure 信息保护的条件访问策略）。

其他信息:

- Windows 计算机：对于当前预览版本，[初始化用户环境](../understand-explore/how-does-it-work.md#initializing-the-user-environment)时会对 Azure 信息保护的条件访问策略进行评估（此过程也称为引导），之后每 30 天评估一次。

- 建议对条件访问策略的评估频率进行微调。 可通过配置令牌生存期来执行此操作。 有关详细信息，请参阅 [Azure Active Directory 中的可配置令牌生存期](/azure/active-directory/active-directory-configurable-token-lifetimes)。

- 建议不要将管理员帐户添加到条件访问策略，因为这些帐户无法访问 Azure 门户中的“Azure 信息保护”边栏选项卡。

- 如果针对条件访问使用许多云应用，则列表中可能不会显示“Microsoft Azure 信息保护”选项，因此无法进行选择。 在这种情况下，可使用列表顶部的搜索框。 开始键入“Microsoft Azure 信息保护”，筛选可用应用。 如果已有受支持的订阅，则可以看到“Microsoft Azure 信息保护”选项，可进行选择。 

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Azure 信息保护中的标签和 Office 365 中的标签之间有何不同？

通过 Azure 信息保护中的标签，可对文档和电子邮件应用一致分类和保护策略，无论它们在本地还是在云中。 此分类和保护与内容的存储位置或其移动方式无关。 通过 [Office 365 中标签的安全性和符合性](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30)，可在内容处于 Office 365 服务中时，对文档和电子邮件进行分类以供审核和保留。 

当前，用户需单独应用和管理这些标签，但 Microsoft 致力于推出针对多个服务（包括 Azure 信息保护、Office 365、Microsoft Cloud App Security 和 Windows 信息保护）的全面且统一的标记策略。 你可能听说过此策略，它称为“Microsoft 信息保护”(MIP)。 这一相同的标记架构和存储也可用于软件供应商。 有关详细信息，请参阅博客文章 [Consistent labeling and protection policies coming to Office 365 and Azure Information Protection](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Consistent-labeling-and-protection-policies-coming-to-Office-365/ba-p/161553)（Office 365 和 Azure 即将推出一致的标签和保护策略）。

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Windows Server FCI 和 Azure 信息保护扫描程序有何区别？

在一段时间内，已可以使用 Windows Server 文件分类基础结构对文档进行分类，然后使用 [Rights Management 连接器](../deploy-use/deploy-rms-connector.md)（仅 Office 文档）或 [PowerShell脚本](../rms-client/configure-fci.md)（所有文件类型）保护文档。 

现在可以使用 [Azure 信息保护扫描程序](../deploy-use/deploy-aip-scanner.md)。 扫描程序使用 Azure 信息保护客户端和 Azure 信息保护策略来为文档（所有文件类型）添加标签，然后可以对这些文档进行分类并且还可根据需要保护文档。

这两种解决方案的主要差异是：

|Windows Server FCI|Azure 信息保护扫描程序|
|--------------------------------|-------------------------------------|
|支持的数据存储： <br /><br />- Windows Server 上的本地文件夹|支持的数据存储： <br /><br />- Windows Server 上的本地文件夹<br /><br />- Windows 文件共享和网络连接存储<br /><br />- SharePoint Server 2016 和 SharePoint Server 2013|
|操作模式： <br /><br />- 实时|操作模式： <br /><br />- 系统地抓取数据存储，且此周期可以运行一次或多次|

目前，在本地文件夹或网络共享上受到保护的文件设置 [Rights Management 所有者](../deploy-use/configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)方面存在差异。 默认情况下，这两个解决方案的 Rights Management 所有者均设置为保护文件的帐户，但可以替代此设置：

- 对于 Windows Server FCI：可以将所有文件的 Rights Management 所有者设置为单个帐户，也可以为每个文件动态设置 Rights Management 所有者。 若要动态设置 Rights Management 所有者，请使用 -OwnerMail [源文件所有者电子邮件] 参数和值。 此配置使用文件“所有者”属性中的用户帐户名从 Active Directory 检索用户的电子邮件地址。

- 对于 Azure 信息保护扫描程序：可以将指定数据存储上所有文件的 Rights Management 所有者设置为单个帐户，但不能为每个文件动态设置 Rights Management 所有者。 若要设置帐户，请为[数据存储库配置文件](/powershell/module/azureinformationprotection/Set-AIPScannerRepository?view=azureipps#optional-parameters)指定 **-DefaultOwner** 参数。

扫描程序保护 SharePoint 网站和库上的文件时，通过使用 SharePoint 创建者值来动态地设置每个文件的 Rights Management 所有者。

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>听说很快将发布新版 Azure 信息保护 — 何时发布？

本技术文档不包含即将发布的版本的相关信息。 有关此类信息和发布公告，请查看 [Enterprise Mobility and Security Blog](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services)（企业移动性和安全性博客）并在 Twitter 上从 [MicrosoftMobility@MSFTMobility](https://twitter.com/MSFTMobility) 了解最新更新。 如果你对 Office 版本感兴趣，还请务必查看 [Office 博客](https://blogs.office.com/)。

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure 信息保护是否适用于我所在的国家/地区？

不同国家/地区的要求和法规不同。 要帮助你的组织回答此问题，请参阅[针对不同国家/地区的适用性](../understand-explore/compliance.md#suitability-for-different-countries)。

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Azure 信息保护如何帮助你符合 GDPR？

要了解 Azure 信息保护如何帮助你满足一般数据保护条例 (GDPR)，请参阅包含视频的下列博客文章公告：[Microsoft 365 提供可帮助你符合 GDPR 的信息保护策略](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr)。

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>在何处可以找到 Azure 信息保护的支持信息 — 例如法律、合规性和 SLA？
请参阅 [Azure 信息保护的合规性和支持信息](../understand-explore/compliance.md)。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>如何针对 Azure 信息保护报告问题或发送反馈？

若要获取技术支持，请使用标准支持渠道或[联系 Microsoft 支持](information-support.md#to-contact-microsoft-support)。

若要提供反馈（例如，针对改进功能或新功能提出建议）：请在 Office 应用程序的“开始”选项卡的“保护”组中，单击“保护”，然后单击“帮助和反馈”。 在“Microsoft Azure 信息保护”对话框中，单击“发送反馈”。 选择此选项将打开一封要发送到信息保护团队的电子邮件。

我们还邀请你加入我们的工程团队：[Azure 信息保护 Yammer 站点](https://www.yammer.com/askipteam/)。 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>如果我的问题不在这里，我该如何操作？

首先，查看以下特定于分类和标签，或特定于数据保护的常见问题解答。 Azure Rights Management 服务 (Azure RMS) 为 Azure 信息保护提供数据保护技术。 Azure RMS 可与分类和标签结合使用，也可单独使用。 

- [分类和标签的常见问题解答](faqs-infoprotect.md)

- [数据保护的常见问题解答](faqs-rms.md)

如果问题没有回复，请使用 [Azure 信息保护的信息和支持](information-support.md)中列出的链接和资源。

此外，我们还为最终用户制作了常见问题解答：

- [适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题解答](../rms-client/mobile-app-faq.md)

- [适用于 Mac 计算机和 Windows Phone 的 RMS 共享应用常见问题解答](https://technet.microsoft.com/dn451248)

- [FAQ for Rights Management Sharing Application for Windows](https://technet.microsoft.com/dn467883)（适用于 Windows 的 Rights Management 共享应用程序常见问题解答）


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

