---
title: "Azure 信息保护中数据保护服务 Azure Rights Management 的常见问题 | Azure 信息保护"
description: "有关 Azure 信息保护中数据保护服务 Azure Rights Management (Azure RMS) 的一些常见问题。"
author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f17cf257607b0f74ca8bdaef13130da2f62dd587
ms.openlocfilehash: 114dfd2a0f19205432771b5dc17ddcb60f7ec44b


---

# Azure 信息保护中的有关数据保护的常见问题

>*适用于：Azure 信息保护、Office 365*

是否有关于 Azure 信息保护中数据保护服务 Azure Rights Management 的问题？ 请查看此处是否有答案。 

## 是否必须将文件存放在云中才能受 Azure Rights Management 保护？
否，这是一个常见的误解。 在信息保护过程中，Azure Rights Management 服务（和 Microsoft）不查看或存储数据。 要保护的信息永远不会发送或存储到 Azure 中，除非你显式将其存储在 Azure 中，或者使用其他可用于在 Azure 中存储数据的云服务。 

有关详细信息，请参阅 [How does Azure RMS work? Under the hood（Azure RMS 的工作原理。](../understand-explore/how-does-it-work.md)以了解在本地创建并存储的可乐的秘密配方如何受 Azure Rights Management 服务的保护，并始终保存在本地。

## 是否可以将 Azure Rights Management 与本地服务器集成？
是。 Azure Rights Management 可以与本地服务器（如 Exchange Server、SharePoint 和 Windows 文件服务器）集成。 为此，你需要使用 [Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。 或者，如果你只想对 Windows Server 使用文件分类基础结构 (FCI)，则可使用 [RMS 保护 cmdlet](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx)。 你还可以使用 [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)，将 Active Directory 域控制器与 Azure AD 同步和联合，为用户提供更为契合的身份验证体验。

Azure Rights Management 根据需要自动生成并管理 XrML 证书，因此它不使用本地 PKI。 有关 Azure Rights Management 如何使用证书的详细信息，请参阅 [Azure RMS 的工作原理](../understand-explore/how-does-it-work.md)一文中的 [Azure RMS 工作演练：首次使用、内容保护、内容使用](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)。

## 在哪里可以找到与 Azure RMS 集成的第三方解决方案的相关信息？

许多软件供应商已经具备或正在实施与 Azure Rights Management 集成的解决方案 — 并且这一数量正在快速增长。 请查看 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)（企业移动性和安全性博客）并从 Twitter 上的 [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) 获取最新更新，这可能会对你有所帮助。 但是，如果你有特定的问题，可以向信息保护团队发送电子邮件：askipteam@microsoft.com。

## RMS 连接器是否有管理包或类似的监视机制？

虽然 Rights Management 连接器会将信息、警告和错误消息记录到事件日志中，但不提供用于监视这些事件的管理包。 不过，[监视 Azure Rights Management 连接器](../deploy-use/monitor-rms-connector.md)中记录了事件及其说明的列表，并提供更多帮助你采取纠正措施的信息。

## 是否必须是全局管理员才能配置 Azure RMS？我可以委派给其他管理员吗？

显然，Office 365 租户或 Azure AD 租户的全局管理员可以运行 Azure Rights Management 服务的所有管理任务。 但是，如果你想为其他用户分配管理权限，则可以通过使用 Azure RMS PowerShell cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) 实现此目的。 你可以按用户帐户或组分配此管理角色。 有两种角色可用：**全局管理员**和**连接器管理员**。 

如这些角色名称所示，第一种角色授权运行 Azure Rights Management 的所有管理任务（而不使其成为其他云服务的全局管理员），第二种角色授权仅运行 Rights Management (RMS) 连接器。

需要注意的事项：

- 只有 Office 365 的全局管理员和 Azure AD 的全局管理员才能使用管理门户（Office 365 管理中心或 Azure 经典门户）来配置 Azure RMS。 分配有 Azure RMS 全局管理员角色的用户必须使用 Azure RMS PowerShell 命令来配置 Azure RMS。 请参阅[使用 Windows PowerShell 管理 Azure Rights Management](../deploy-use/administer-powershell.md)，以帮助查找特定任务的正确 cmdlet。

- 如果配置了[加入控制](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，这不会影响管理 Azure RMS 的能力，但会影响管理 RMS 连接器的能力。 例如，如果配置了加入控制，以致仅允许“IT 部门”组保护内容，那么，用于安装和配置 RMS 连接器的帐户必须是该组的成员。 

- 任何 Azure RMS 管理员（租户全局管理员或 Azure RMS 全局管理员）都不能对受 Azure RMS 保护的文档或电子邮件自动解除保护。 只有在启用了超级用户功能的情况下，分配为 Azure RMS 超级用户的用户才能执行此操作。 但是，租户全局管理员和所有 Azure RMS 全局管理员都可以将用户分配为超级用户，包括其自己的帐户。 他们还可以启用超级用户功能。 这些操作记录在 Azure RMS 管理员日志中。 有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)中的“最佳安全做法”部分。 


## 我对 Exchange 采用混合部署：Exchange Online 上存在一些用户，而其他用户则在 Exchange Server 上。Azure RMS 支持这种部署吗？
绝对支持，而且很棒的是，用户将受到无缝保护，并可以在两种 Exchange 部署上使用受保护的电子邮件和附件。 对于此配置，[激活 Azure RMS](../deploy-use/activate-service.md) 并[启用适用于 Exchange Online 的 IRM](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)，然后[部署并配置适用于 Exchange Server 的 RMS 连接器](../deploy-use/deploy-rms-connector.md)。

## 如果在我的生产环境中使用该保护，那么我的公司是否就只能使用该解决方案？或者是否存在无法访问由 Azure RMS 进行保护的内容的风险？
不会，你可以始终控制并继续访问数据，即使你决定不再使用 Azure Rights Management 服务也是如此。 有关详细信息，请参阅[解除 Azure Rights Management 授权和停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)。

但是，在你解除 Azure RMS 部署授权前，我们希望倾听你的意见，了解你为什么做出这个决定。 如果 Azure Rights Management 保护未能满足你的业务需求，请联系我们，以确认在不久的将来是否会有新的功能，或者是否存在替代功能。 将电子邮件发送到 [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) ，我们将很高兴讨论你的技术和商业要求。

## 是否可以控制哪些用户能够使用 Azure RMS 来保护内容？
是的，Azure Rights Management 服务具有针对这一应用场景的用户载入控制。 有关详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md) 一文中的[为分阶段部署配置加入控制](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)部分。

## 是否可以防止用户与特定的组织共享受保护文档？
在数据保护中使用 Azure Rights Management 服务的最大优势之一在于，它支持企业与企业的协作，同时，无需为每个合作伙伴组织配置显式信任关系，因为 Azure AD 会代你处理好身份验证。

我们未提供相应的管理选项来防止用户与特定的组织安全共享文档。 例如，你想要阻止某家你不信任的或者竞争的组织。 防止 Azure Rights Management 服务向这些组织的用户发送受保护文档没有任何意义，因为你的用户之后还是会共享未保护的文档，而这也许是你最不希望发生的事情！ 例如，你无法识别谁在与这些组织的用户共享公司机密文档，但是，如果文档（或电子邮件）受 Azure Rights Management 服务的保护，则可以识别。

## 如果我与公司之外的用户共享受保护文档，该用户如何进行身份验证。
Azure Rights Management 服务始终使用 Azure Active Directory 帐户和关联的电子邮件地址进行用户身份验证，这可以为管理员建立企业间的无缝协作。 如果其他组织使用 Azure 服务，用户将具有 Azure Active Directory 帐户，即使这些帐户是在本地创建和进行管理，然后同步到 Azure。 如果组织具有 Office 365，此服务在后台还会将 Azure Active Directory 用于用户帐户。 如果用户的组织在 Azure 中没有托管帐户，用户可以注册[个人 RMS](../understand-explore/rms-for-individuals.md)，并使用该用户帐户为组织创建非托管的 Azure 租户和目录，以便可以在 Azure Rights Management 服务中对此用户（和后续用户）进行身份验证。

这些帐户的身份验证方法各不相同，具体取决于其他组织中的管理员如何配置 Azure Active Directory 帐户。 例如，他们可以使用为这些帐户、多重身份验证 (MFA)、联合身份验证创建的密码，或在 Active Directory 域服务中创建、然后同步到 Azure Active Directory 的密码。

## 我可以将公司之外的用户添加到自定义模板吗？
是。 创建最终用户（和管理员）可以从应用程序中选择的自定义模板，可使用户使用你指定的预定义策略应用信息保护变得简单快捷。 该模板中的设置之一是哪些用户能够访问内容，而且你可以指定组织中的用户和组以及组织之外的用户。

若要从组织外部指定用户，请在配置模板时在 Azure 经典门户中将用户添加为所选组的联系人。 或者使用[适用于 Azure Rights Management 的 Windows PowerShell 模块](../deploy-use/install-powershell.md)：

-   **使用权限定义对象创建或更新模板**。    在权限定义对象中指定外部电子邮件地址及其权限，然后你将使用该地址创建或更新模板。 指定权限定义对象时，可使用 [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) cmdlet 来创建一个变量，然后将该变量提供给 -RightsDefinition 参数，并可使用 [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) cmdlet（如果是新模板）或 [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) cmdlet（如果需要修改现有模板）。 但是，如果你是将这些用户添加到现有模板中，则需要在模板中为现有组定义权限定义对象，不仅仅只需为外部用户进行此类操作。

有关自定义模板的详细信息，请参阅[为 Azure 权限管理服务配置自定义模板](../deploy-use/configure-custom-templates.md)。

## Azure RMS 是否适用于 Azure AD 中的动态组？
Azure AD Premium 功能可让你通过指定[基于属性的规则](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/)为组配置动态成员资格。 在 Azure AD 中创建安全组时，该组类型支持动态成员资格，但不支持电子邮件地址，因此不能用于Azure Rights Management 服务。 但是，现在可以在 Azure AD 中创建支持动态成员身份并启用了邮件的新组类型。 当在 Azure 经典门户中添加新组时，你可以选择 **Office 365“预览版”**的**组类型**。 由于此组启用了邮件，可以将其用于 Azure Rights Management 保护。

正如选项名清楚显示的一样，此新组类型仍为预览版，预期后续将推出其他功能和新文档。 在此期间，我们想要确认是否可以将此新组类型用于 Azure Rights Management 保护。


## Azure RMS 支持哪些设备和哪种文件类型？
有关支持 Azure Rights Management 服务的设备的列表，请参阅 [Azure RMS 要求：支持 Azure RMS 的客户端设备](../get-started/requirements-client-devices.md)。 由于并非所有受支持的设备目前都能支持所有 Rights Management 功能，因此，还请务必查看 [Azure RMS 要求：应用程序](../get-started/requirements-applications.md)中的表。

Azure Rights Management 服务支持所有文件类型。 对于文字、图像、Microsoft Office（Word、Excel、PowerPoint）文件、.pdf 文件和一些其他应用程序文件类型，Azure Rights Management 提供的本地保护包括对权利（权限）的加密和执行。 对于其他应用程序和文件类型，通用保护提供文件封装和验证以确认用户是否授权打开文件。

对于 Azure Rights Management 直接支持的文件扩展名列表，请参阅 [Rights Management 共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)中的[支持的文件类型和文件扩展名](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)部分。 未列出的文件扩展名支持使用 RMS 共享应用程序，可自动提供通用保护保护这些文件。

## 当我打开受 RMS 保护的 Office 文档时，关联的临时文件是否也将受 RMS 保护？

否。 在此方案中，关联的临时文件不包含原始文档中的数据，而仅包含该文件打开时用户输入的内容。 与原始文件不同，临时文件明显不适合共享，将保留在设备上，受本地安全控件（例如 BitLocker 和 EFS）保护。

## 我们确实很想将 BYOK 和 Azure 信息保护结合使用，但是 BYOK 与 Exchange Online 不兼容 — 你有什么建议呢？
不要因目前这种限制而推迟使用 Azure 信息保护的 Azure Rights Management 服务。 如果具有 Exchange Online 并想要使用自带密钥 (BYOK)，我们建议暂时以默认密钥管理模式部署 Azure 信息保护，该模式由 Microsoft 生成和管理密钥。 如此一来，你现在可以获取保护重要文件和电子邮件的所有好处，并可以选择以后移动到 BYOK（例如，当 Exchange Online 不支持 BYOK 时）。 移动到 BYOK 时，以前受保护的文档和电子邮件将仍然能够通过使用存档的密钥进行访问。

但是，如果公司策略要求使用硬件安全模块 (HSM)，而这会阻止 Azure 信息保护的部署，那么另一种选择是将 Azure 信息保护和 BYOK 一起部署，只不过 Exchange 的 Rights Management 保护功能会减弱。 有关详细信息，请参阅[计划和实施你的 Azure Rights Management 租户密钥](../plan-design/plan-implement-tenant-key.md)中的 [BYOK 定价和限制](../plan-design/byok-price-restrictions.md)。

## 我正在寻找的一项功能看起来不适用于 SharePoint 保护的库。是否计划了针对此功能的支持？
当前，SharePoint 通过使用 IRM 保护的库来支持 Rights Management 保护的文档，但是该库不支持自定义模板、文档跟踪和其他一些功能。 有关详细信息，请参阅 [Office 应用程序和服务](../understand-explore/office-apps-services-support.md)一文中的 [SharePoint Online 和 SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server)部分。

如果对尚不支持的某项特定功能感兴趣，请务必关注 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)（企业移动性和安全性博客）上的公告。

## 如何在 SharePoint Online 中配置 OneDrive for Business，以便用户可以安全地与公司内外的人员共享他们的文件？
默认情况下，作为 Office 365 管理员，你不用执行此配置，用户会进行配置。

正如 SharePoint 站点管理员为其拥有的 SharePoint 库启用并配置 IRM 一样，根据 OneDrive for Business 的设计，用户也需要为自己的 OneDrive for Business 库启用并配置 IRM。  不过，你可以使用 PowerShell 为他们执行此类操作。 有关说明，请参阅 [Office 365：客户端和联机服务的配置](../deploy-use/configure-office365.md)一文中的 [SharePoint Online 和 OneDrive for Business：IRM 配置](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)部分。

## 对于成功部署，是否有任何提示或窍门？
在考察大量的部署并聆听客户、合作伙伴、顾问和支持工程师的意见后，结合自身的经验，我们很乐意与你分享下面这个极其有效的诀窃： **设计并部署简单的权限策略**。

由于 Azure 信息保护支持与任何人安全共享，因此，你完全有理由相信自己的数据保护措施的覆盖面。 但是，对权限策略应持保守态度。 对于许多组织而言，对业务产生的最大影响来自于通过应用默认权限策略模板防止数据泄漏，将其访问权限限制给组织中的人员。 当然，你可以根据需要采取粒度级比这高得多的措施 - 例如，防止人员打印、编辑，等等。但是，对于确实需要高级安全性的文档，请将更高粒度级的限制保留为例外措施，并且不要一开始就实施这些限制性更强的策略，而是计划采取分阶段的实施方案。

## 我们如何重新获取对由已离职员工保护的文件的访问权限？
使用 Azure RMS 的超级用户功能，它可以让授权用户对组织的 RMS 租户授予的所有使用许可证行使所有者权限。 根据需要，此相同功能可以让授权服务编写文件索引和检查文件。

有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)。

## Rights Management 可以防止屏幕截图吗？
通过不授予**复制**[使用权限](../deploy-use/configure-usage-rights.md)，Rights Management 可以阻止许多常用屏幕捕获工具在 Windows 平台（Windows 7、Windows 8.1、Windows 10、Windows Phone）和 Android 上进行屏幕捕获。 但是，iOS 和 Mac 设备不允许任何应用阻止屏幕捕获，而浏览器（例如，与 Outlook Web App 和 Office Online 一起使用时）也不能阻止屏幕捕获。

阻止屏幕捕获可帮助避免意外或疏忽披露机密或敏感信息。 不过，用户可以通过多种方式来共享显示在屏幕上的数据，进行屏幕截图只是其中一种方法。 例如，如果想要共享所显示的信息，用户可以使用带相机的手机拍照，可以重新键入相关数据，还可以直接通过口头方式将其传达给某人。

如这些例子所示，即使支持 Rights Management API 的所有平台和所有软件都阻止屏幕捕获，仅靠技术并非始终能够阻止用户共享他们不应该共享的数据。 Rights Management 可以通过授权和使用策略来确保重要数据的安全性，但在使用此企业权限管理解决方案时还应加入其他控制手段。 例如，可以实施物理安全措施，可以仔细盘查和监视有权访问组织数据的人员，还可以进行用户教育，让用户了解哪些数据是不应共享的。

## 用户通过“不得转发”和不包括“转发”权限的模板来保护电子邮件有什么区别？

除名称和外观外，**不得转发**既不是“转发”权限的对立面，也不是模板。 它实际上是一组权限，包括限制复制、打印和保存附件以及限制转发电子邮件。 这些权限通过所选收件人动态应用于用户，而不由管理员静态分配。 有关详细信息，请参阅[为 Azure Rights Management 配置使用权限](../deploy-use/configure-usage-rights.md)中的[电子邮件的“不得转发”选项](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails)部分。






<!--HONumber=Oct16_HO1-->


