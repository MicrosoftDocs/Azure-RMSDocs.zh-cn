---
title: "Azure Rights Management 常见问题 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/30/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b73c83b91a6b00e44ff6c8fe7f8e954bd9713e34
ms.openlocfilehash: a3ed9e8de496741fae8904481edb1177762a12c0


---

# Azure Rights Management 常见问题

*适用于：Azure Rights Management、Office 365*

Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]（也称为 Azure RMS）的某些常见问题：

## 部署 Azure RMS 需要做好哪些准备，如何能够顺利完成部署？
首先，请查看 [Azure Rights Management 要求](requirements-azure-rms.md)，其中包含了有关云订阅选项、如何将本地服务器与 Azure RMS 配合使用、当前不支持的部署方案以及哪些设备、应用程序支持 Azure RMS 的信息以及你需要的防火墙或代理服务器的 IP 地址和域名列表链接。 

你可能还需要查看此**入门**部分以及**了解和探索**部分中的其他文章，以基本了解 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 如何帮助保护组织的数据、如何与应用程序配合工作、它与 Active Directory Rights Management 的本地版本比起来如何，并了解特定于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的术语和缩写。

之后，若要开始部署，请使用 [Azure Rights Management 部署路线图](../plan-design/deployment-roadmap.md)。

## 必须存在于云中的文件是否要受 Azure RMS 保护？
否，这是一个常见的误解。 在信息保护过程中，Azure Rights Management 服务（和 Microsoft）不查看或存储你的数据。 要保护的信息永远不会发送或存储到 Azure 中，除非你显式将其存储在 Azure 中，或者使用其他可用于在 Azure 中存储数据的云服务。 

有关详细信息，请参阅 [How does Azure RMS work? Under the hood（Azure RMS 的工作原理。揭秘）](../understand-explore/how-does-it-work.md)以了解在本地创建和存储的秘密可乐配方如何受 Azure RMS 保护但始终在本地。

## 可以将 Azure RMS 与我的本地服务器集成吗？
是。 Azure RMS 可以与你的本地服务器（如 Exchange Server、SharePoint 和 Windows 文件服务器）集成。 为此，你需要使用 [Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。 或者，如果你只想对 Windows Server 使用文件分类基础结构 (FCI)，则可使用 [RMS 保护 cmdlet](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx)。 你还可以使用 [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)，将 Active Directory 域控制器与 Azure AD 同步和联合，为用户提供更为契合的身份验证体验。

Azure RMS 将根据需要自动生成并管理 XrML 证书，因此它不使用本地 PKI。 有关 Azure RMS 如何使用证书的详细信息，请参阅 [Azure RMS 的工作原理](../understand-explore/how-does-it-work.md)一文中的 [Azure RMS 工作原理演练：首次使用、内容保护、内容使用](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)。

## 在哪里可以找到与 Azure RMS 集成的第三方解决方案的相关信息？

许多软件供应商已有或正在实施与 Azure RMS 集成的解决方案，并且这一数量正在快速增长。 请查看 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)（企业移动性和安全性博客）并从 Twitter 上的 [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) 获取最新更新，这可能会对你有所帮助。 但是，如果你有特定的问题，可以向信息保护团队发送电子邮件：askipteam@microsoft.com。

## RMS 连接器是否有管理包或类似的监视机制？

虽然 Rights Management 连接器会将信息、警告和错误消息记录到事件日志中，但不提供用于监视这些事件的管理包。 不过，[监视 Azure Rights Management 连接器](../deploy-use/monitor-rms-connector.md)中记录了事件及其说明的列表，并提供更多帮助你采取纠正措施的信息。

## 是否必须是全局管理员才能配置 Azure RMS？我可以委派给其他管理员吗？

很显然，Office 365 租户或 Azure AD 租户的全局管理员可以运行 Azure RMS 的所有管理任务。 但是，如果你想为其他用户分配管理权限，则可以通过使用 Azure RMS PowerShell cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) 实现此目的。 你可以按用户帐户或组分配此管理角色。 有两种角色可用：**全局管理员**和**连接器管理员**。 

如这些角色名称所示，第一种角色授权运行 Azure Rights Management 的所有管理任务（而不使其成为其他云服务的全局管理员），第二种角色授权仅运行 Rights Management (RMS) 连接器。

需要注意的事项：

- 只有 Office 365 的全局管理员和 Azure AD 的全局管理员才能使用管理门户（Office 365 管理中心或 Azure 经典门户）来配置 Azure RMS。 分配有 Azure RMS 全局管理员角色的用户必须使用 Azure RMS PowerShell 命令来配置 Azure RMS。 请参阅[使用 Windows PowerShell 管理 Azure Rights Management](../deploy-use/administer-powershell.md)，以帮助查找特定任务的正确 cmdlet。

- 如果配置了[加入控制](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，这不会影响管理 Azure RMS 的能力，但会影响管理 RMS 连接器的能力。 例如，如果配置了加入控制，以致仅允许“IT 部门”组保护内容，那么，用于安装和配置 RMS 连接器的帐户必须是该组的成员。 

- 任何 Azure RMS 管理员（租户全局管理员或 Azure RMS 全局管理员）都不能对受 Azure RMS 保护的文档或电子邮件自动解除保护。 只有在启用了超级用户功能的情况下，分配为 Azure RMS 超级用户的用户才能执行此操作。 但是，租户全局管理员和所有 Azure RMS 全局管理员都可以将用户分配为超级用户，包括其自己的帐户。 他们还可以启用超级用户功能。 这些操作记录在 Azure RMS 管理员日志中。 有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)中的“最佳安全做法”部分。 


## 我对 Exchange 采用混合部署：Exchange Online 上存在一些用户，而其他用户则在 Exchange Server 上。Azure RMS 支持这种部署吗？
绝对支持，而且很棒的是，用户将受到无缝保护，并可以在两种 Exchange 部署上使用受保护的电子邮件和附件。 对于此配置，[激活 Azure RMS](../deploy-use/activate-service.md) 并[启用适用于 Exchange Online 的 IRM](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)，然后[部署并配置适用于 Exchange Server 的 RMS 连接器](../deploy-use/deploy-rms-connector.md)。

## 是否有配置 Exchange Online 使用 Azure RMS 的分步指导？

是。 请参阅 [Exchange Online：IRM 配置](../deploy-use/configure-office365.md#exchange-online-irm-configuration)以查看使 Exchange Online 使用 Azure RMS 的一组典型命令，了解为什么 Outlook Web App 不立即显示“设置权限”菜单选项，以及在更改或更新 Azure RMS 模板时要运行的命令。 

## 如果我在生产中部署 Azure RMS，我的公司是否就只能使用该解决方案？或者是否存在无法访问由 Azure RMS 进行保护的内容的风险？
不会，数据始终由你控制，并可以继续访问，即使你决定不再使用 Azure RMS 也是如此。 有关详细信息，请参阅[解除 Azure Rights Management 授权和停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)。

但是，在你解除 Azure RMS 部署授权前，我们希望倾听你的意见，了解你为什么做出这个决定。 如果 Azure RMS 未能满足你的业务要求，请与我们取得联系，或许在不久的将来会计划新功能或存在替代方法。 将电子邮件发送到 [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) ，我们将很高兴讨论你的技术和商业要求。

## 是否可以控制哪些用户能够使用 Azure RMS 来保护内容？
可以，Azure RMS 针对这种情况提供了用户登记控制功能。 有关详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md) 一文中的[为分阶段部署配置加入控制](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)部分。

## 是否可以防止用户与特定的组织共享受保护文档？
Azure RMS 的最大优势之一在于，它支持企业与企业的协作，同时，你无需为每个合作伙伴组织配置显式信任关系，因为 Azure AD 会代你处理好身份验证。

我们未提供相应的管理选项来防止用户与特定的组织安全共享文档。 例如，你想要阻止某家你不信任的或者竞争的组织。 防止 Azure RMS 向该组织的用户发送受保护文档没有任何意义，因为你的用户到时还是会共享未保护的文档，而这也许是你最终希望发生的事情！ 例如，你无法识别谁在与这些组织的用户共享公司机密文档，但是，如果文档（或电子邮件）受 Azure RMS 的保护，则你可以识别。

## 如果我与公司之外的用户共享受保护文档，该用户如何进行身份验证。
Azure RMS 始终使用 Azure Active Directory 帐户和关联的电子邮件地址进行用户身份验证，这为管理员将企业间的协作变得天衣无缝。 如果其他组织使用 Azure 服务，用户将具有 Azure Active Directory 帐户，即使这些帐户是在本地创建和进行管理，然后同步到 Azure。 如果组织具有 Office 365，此服务在后台还会将 Azure Active Directory 用于用户帐户。 如果用户的组织在 Azure 中没有托管帐户，用户可以注册[个人 RMS](../understand-explore/rms-for-individuals.md)，这将为组织创建非托管的 Azure 租户和目录，并为用户创建帐户，以便此用户（和后续用户）进行 Azure RMS 身份验证。

这些帐户的身份验证方法各不相同，具体取决于其他组织中的管理员如何配置 Azure Active Directory 帐户。 例如，他们可以使用为这些帐户、多重身份验证 (MFA)、联合身份验证创建的密码，或在 Active Directory 域服务中创建、然后同步到 Azure Active Directory 的密码。

## 我可以将公司之外的用户添加到自定义模板吗？
适用。 创建最终用户（和管理员）可以从应用程序中选择的自定义模板，可使用户使用你指定的预定义策略应用信息保护变得简单快捷。 该模板中的设置之一是哪些用户能够访问内容，而且你可以指定组织中的用户和组以及组织之外的用户。

若要从组织外部指定用户，请在配置模板时在 Azure 经典门户中将用户添加为所选组的联系人。 或者使用[适用于 Azure Rights Management 的 Windows PowerShell 模块](../deploy-use/install-powershell.md)：

-   **使用权限定义对象创建或更新模板**。    在权限定义对象中指定外部电子邮件地址及其权限，然后你将使用该地址创建或更新模板。 指定权限定义对象时，可使用 [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) cmdlet 来创建一个变量，然后将该变量提供给 -RightsDefinition 参数，并可使用 [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) cmdlet（如果是新模板）或 [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) cmdlet（如果需要修改现有模板）。 但是，如果你是将这些用户添加到现有模板中，则需要在模板中为现有组定义权限定义对象，不仅仅只需为外部用户进行此类操作。

有关自定义模板的详细信息，请参阅[为 Azure Rights Management 配置自定义模板](../deploy-use/configure-custom-templates.md)。

## Azure RMS 是否适用于 Azure AD 中的动态组？
Azure AD Premium 功能可让你通过指定[基于属性的规则](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/)为组配置动态成员资格。 在 Azure AD 中创建安全组时，这种组类型支持动态成员资格，但不支持电子邮件地址，因此不能与 Azure RMS 配合使用。 但是，现在可以在 Azure AD 中创建支持动态成员身份并启用了邮件的新组类型。 当在 Azure 经典门户中添加新组时，你可以选择 **Office 365“预览版”**的**组类型**。 由于此组启用了邮件，你可以将它与 Azure RMS 配合使用。

正如选项名清楚显示的一样，此新组类型仍为预览版，预期后续将推出其他功能和新文档。 在此期间，我们想要确认你可以将此新组类型与 Azure RMS 配合使用。


## Azure RMS 支持哪些设备和哪种文件类型？
有关受支持设备的列表，请参阅 [Azure RMS 要求：支持 Azure RMS 的客户端设备](../get-started/requirements-client-devices.md)。 由于并非所有受支持的设备目前都能支持所有 RMS 功能，因此，还请务必查看 [Azure RMS 要求：应用程序](../get-started/requirements-applications.md)中的表。

Azure RMS 能够支持所有文件类型。 对于文字、图像、Microsoft Office (Word、Excel、PowerPoint) 文件、.pdf 文件和一些其他应用程序文件类型，Azure RMS 提供的本地保护包括对权利（权限）的加密和执行。 对于其他应用程序和文件类型，通用保护提供文件封装和验证以确认用户是否授权打开文件。

对于 Azure RMS 以本机方式支持的文件扩展名列表，请参阅 [Rights Management 共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)中的[支持的文件类型和文件扩展名](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)部分。 未列出的文件扩展名支持使用 RMS 共享应用程序，可自动提供通用保护保护这些文件。

## 当我打开受 RMS 保护的 Office 文档时，关联的临时文件是否也将受 RMS 保护？

否。 在此方案中，关联的临时文件不包含原始文档中的数据，而仅包含该文件打开时用户输入的内容。 与原始文件不同，临时文件明显不适合共享，将保留在设备上，受本地安全控件（例如 BitLocker 和 EFS）保护。

## 你们何时支持从 AD RMS 迁移？
最初，Azure RMS 不支持从本地部署的 Rights Management（如 AD RMS）迁移。 但是，现在支持这种迁移。

有关详细信息，请参阅[从 AD RMS 迁移到 Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。

## 我们很想将 BYOK 和 Azure RMS 一起使用，但却了解到这与 Exchange Online 不兼容，你有什么建议呢？
不要让此当前限制延迟 Azure RMS 部署。 如果你具有 Exchange Online 并想要使用自带密钥 (BYOK)，我们建议你暂时以默认密钥管理模式部署 Azure RMS，即由 Microsoft 生成和管理你的密钥。 如此一来，你现在可以获取保护重要文件和电子邮件的所有好处，并可以选择以后移动到 BYOK（例如，当 Exchange Online 不支持 BYOK 时）。

但是，如果你的公司策略要求你使用硬件安全模块 (HSM)，但这将阻止你的 Azure RMS 部署，可以另作选择，将 Azure RMS 和 BYOK 一起部署，只不过 Exchange 的 RMS 功能会减弱。 有关详细信息，请参阅[计划和实施你的 Azure Rights Management 租户密钥](../plan-design/plan-implement-tenant-key.md)中的 [BYOK 定价和限制](../plan-design/byok-price-restrictions.md)。

## 我正在寻找的一项功能看起来不适用于 SharePoint 保护的库。是否计划了针对此功能的支持？
当前，SharePoint 通过使用 IRM 保护的库，支持 RMS 保护的文档，但不支持自定义模板、文档跟踪和一些其他功能。 有关详细信息，请参阅 [Office 应用程序和服务](../understand-explore/office-apps-services-support.md)一文中的 [SharePoint Online 和 SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server)部分。

如果你对当前不支持的某项特定功能感兴趣，请务必关注 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)（企业移动性和安全性博客）上的公告。

## 如何在 SharePoint Online 中配置 OneDrive for Business，以便用户可以安全地与公司内外的人员共享他们的文件？
默认情况下，作为 Office 365 管理员，你不用执行此配置，用户会进行配置。

正如 SharePoint 站点管理员为其拥有的 SharePoint 库启用并配置 IRM 一样，根据 OneDrive for Business 的设计，用户也需要为自己的 OneDrive for Business 库启用并配置 IRM。  不过，你可以使用 PowerShell 为他们执行此类操作。 有关说明，请参阅 [Office 365：客户端和联机服务的配置](../deploy-use/configure-office365.md)一文中的 [SharePoint Online 和 OneDrive for Business：IRM 配置](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)部分。

## 是否能够提供有关成功部署 RMS 的任何诀窍或技巧？
在考察大量的部署并聆听客户、合作伙伴、顾问和支持工程师的意见后，结合自身的经验，我们很乐意与你分享下面这个极其有效的诀窃： **设计并部署简单的权限策略**。

由于 Azure RMS 支持与任何人安全共享，因此，你完全有理由相信自己的信息保护措施的覆盖面。 但是，对权限策略应持保守态度。 对于许多组织而言，对业务产生的最大影响来自于通过应用默认权限策略模板防止数据泄漏，将其访问权限限制给组织中的人员。 当然，你可以根据需要采取粒度级比这高得多的措施 - 例如，防止人员打印、编辑，等等。但是，对于确实需要高级安全性的文档，请将更高粒度级的限制保留为例外措施，并且不要一开始就实施这些限制性更强的策略，而是计划采取分阶段的实施方案。

## 哪些功能可以或不可以用于 Azure RMS 的不同订阅？
对于支持 Azure RMS 的付费订阅（Office 365、Azure RMS Premium 和企业移动性套件），在支持的 RMS 功能方面存在一些差异。 有关列表，请参阅 [Rights Management 服务 (RMS) 产品比较](http://technet.microsoft.com/dn858608)。

支持 Azure RMS（个人 RMS）的免费订阅支持使用受 Azure RMS 保护的内容。 有关详细信息，请参阅[个人 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)。

## 我在哪里可以获取有关 Azure RMS（个人 RMS）免费订阅的技术信息 — 例如它的工作原理、如何控制帐户、哪些域名不可用？
你会在[个人 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)及相关文章中找到这些问题的解答。

## 我们如何重新获取对由已离职员工保护的文件的访问权限？
使用 Azure RMS 的超级用户功能，它可以让授权用户对组织的 RMS 租户授予的所有使用许可证行使所有者权限。 根据需要，此相同功能可以让授权服务编写文件索引和检查文件。

有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)。

## Rights Management 可以防止屏幕截图吗？
通过不授予**复制**[使用权限](../deploy-use/configure-usage-rights.md)，Rights Management 可以阻止许多常用屏幕捕获工具在 Windows 平台（Windows 7、Windows 8.1、Windows 10、Windows Phone）和 Android 上进行屏幕捕获。 但是，iOS 和 Mac 设备不允许任何应用阻止屏幕捕获，而浏览器（例如，与 Outlook Web App 和 Office Online 一起使用时）也不能阻止屏幕捕获。

阻止屏幕捕获可帮助避免意外或疏忽披露机密或敏感信息。 不过，用户可以通过多种方式来共享显示在屏幕上的数据，进行屏幕截图只是其中一种方法。 例如，如果想要共享所显示的信息，用户可以使用带相机的手机拍照，可以重新键入相关数据，还可以直接通过口头方式将其传达给某人。

如这些例子所示，即使支持 Rights Management API 的所有平台和所有软件都阻止屏幕捕获，仅靠技术并非始终能够阻止用户共享他们不应该共享的数据。 Rights Management 可以通过授权和使用策略来确保重要数据的安全性，但在使用此企业权限管理解决方案时还应加入其他控制手段。 例如，可以实施物理安全措施，可以仔细盘查和监视有权访问组织数据的人员，还可以进行用户教育，让用户了解哪些数据是不应共享的。

## 用户通过“不得转发”和不包括“转发”权限的模板来保护电子邮件有什么区别？

除名称和外观外，**不得转发**既不是“转发”权限的对立面，也不是模板。 它实际上是一组权限，包括限制复制、打印和保存附件以及限制转发电子邮件。 这些权限通过所选收件人动态应用于用户，而不由管理员静态分配。 有关详细信息，请参阅[为 Azure Rights Management 配置使用权限](../deploy-use/configure-usage-rights.md)中的[电子邮件的“不得转发”选项](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails)部分。

## 我在何处可以找到 Azure RMS 的支持信息，例如法律、合规性和 SLA？
Azure RMS 支持其他服务，也依赖于其他服务。 如果你寻找的信息与 Azure RMS 相关，但与如何使用 Azure RMS 服务无关，请查看以下资源：

**法律和隐私：**

-   对于 Microsoft Azure 协议信息： [Microsoft Azure 协议](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   对于 Microsoft Azure 隐私信息： [Microsoft Azure 隐私声明](http://azure.microsoft.com/support/legal/privacy-statement/)

**安全、相容性和审核：**

请参阅 [Azure RMS 解决了哪些问题？](../understand-explore/azure-rms-problems-it-solves.md)一文中的[安全、合规性和法规要求](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements) 此外：

-   对于 Azure RMS 的外部认证： [Microsoft Azure 信任中心](http://azure.microsoft.com/support/trust-center/)

-   对于 FIPS 140 信息： [FIPS 140 验证](https://technet.microsoft.com/library/security/cc750357.aspx)

**服务级别协议：**

-   按所选区域的 Azure RMS 服务级别协议：[从产品许可搜索页下载](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

    - 例如，单击 **OnlineSvcsConsolidatedSLA(WW)(English)(March2016)** 以下载适用于北美的 2016 年 3 月服务级别协议。

-   Azure Active Directory 的服务级别协议： [服务级别协议](http://azure.microsoft.com/support/legal/sla/)

**文档：**

-   Azure Active Directory 文档站点： [Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Azure Active Directory 库：[Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx)

-   Office 365 库：[Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## 听说很快将发布新版 Azure RMS，何时发布？

本技术文档不包含即将发布的版本的相关信息。 有关此类信息和发布公告，请查看 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)（企业移动性和安全性博客）并从 Twitter 上的 [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) 获取最新更新。 如果你对 Office 版本感兴趣，还请务必查看 [Office 博客[(https://blogs.office.com/)。

## 如果我的问题不在这里，我该如何操作？
使用 [Azure Rights Management 的信息和支持](information-support.md)中列出的链接和资源。

此外，我们还为最终用户制作了常见问题解答：

-   [适用于 Windows 的 Rights Management 共享应用程序常见问题](https://technet.microsoft.com/dn467883)

-   [适用于移动平台和 Mac 平台的 Rights Management 共享应用程序的常见问题](https://technet.microsoft.com/dn451248)

-   [文档跟踪常见问题](http://go.microsoft.com/fwlink/?LinkId=523977)

此常见问题页将定期更新，其中新添加的内容将在 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)（企业移动性和安全性博客）上的每月文档更新公告中列出。





<!--HONumber=Jul16_HO1-->


