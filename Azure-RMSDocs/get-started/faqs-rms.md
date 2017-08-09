---
title: "Azure RMS 的常见问题解答 - AIP"
description: "有关 Azure 信息保护中数据保护服务 Azure Rights Management (Azure RMS) 的一些常见问题。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5a9f592584c090d8b0bb62acabd5775238b5e411
ms.sourcegitcommit: 7cd6ff39731c7abe990a72a49bc10d104f47764d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2017
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Azure 信息保护中的有关数据保护的常见问题

>*适用于：Azure 信息保护、Office 365*

是否有关于 Azure 信息保护中数据保护服务 Azure Rights Management 的问题？ 请查看此处是否有答案。 

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>是否必须将文件存放在云中才能受 Azure Rights Management 保护？
否，这是一个常见的误解。 在信息保护过程中，Azure Rights Management 服务（和 Microsoft）不查看或存储数据。 要保护的信息永远不会发送或存储到 Azure 中，除非你显式将其存储在 Azure 中，或者使用其他可用于在 Azure 中存储数据的云服务。 

有关详细信息，请参阅 [How does Azure RMS work? Under the hood（Azure RMS 的工作原理。](../understand-explore/how-does-it-work.md)以了解在本地创建并存储的可乐的秘密配方如何受 Azure Rights Management 服务的保护，并始终保存在本地。

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>Azure Rights Management 加密和其他 Microsoft 云服务中的加密有何区别？

Microsoft 提供了多个加密技术，使你能够保护数据以满足不同的方案，方案之间通常能够互补。 例如，Office 365 为存储在 Office 365 中的数据提供静态加密，而 Azure 信息保护的 Azure Rights Management 服务则独立加密数据，使其不受所在位置和传输方式影响而得到保护。

这些加密技术相互补充，使用它们需要单独对其进行启用和配置。 执行此操作时，可以选择使用自己的密钥进行加密，也称为“BYOK”方案。 为其中一种技术启用 BYOK 不影响其他技术。 例如，可对 Azure 信息保护使用 BYOK，而对其他加密技术不使用 BYOK；反之亦然。 不同技术所用密钥可为相同或不同，具体取决于为每种服务配置的加密选项。

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>BYOK 和 HYOK 之间的区别是什么，应何时使用它们？

Azure 信息保护上下文中出现**自带密钥** (BYOK) 时，则表示应为 Azure Rights Management 保护创建自己的本地密钥。 然后将该密钥传输到 Azure Key Vault 中的硬件安全模块 (HSM)，你可在其中继续拥有并管理你的密钥。 若不执行此操作，Azure Rights Management 保护会使用 Azure 中自动为你创建并进行管理的密钥。 这种默认配置称为“Microsoft 管理”而不是“客户管理”（BYOK 选项）。

有关 BYOK 以及是否应为组织选择此密钥拓扑的详细信息，请参阅[规划和实现 Azure 信息保护租户密钥](../plan-design/plan-implement-tenant-key.md)。 

在 Azure 信息保护的上下文中出现**自留密钥** (HYOK)，则表示少量组织的文档或电子邮件自己无法通过存储在云中的密钥进行保护。 对于这些组织来说，即使使用 BYOK 创建和管理密钥，此限制仍然适用。 此限制通常是由于法规或符合性问题引起的，并且 HYOK 配置应仅应用于“顶级机密”信息，此信息永远不会在组织外部共享、仅会在内部网络中使用，并且无需通过移动设备访问。 

对于这些异常（通常需要保护的内容少于所有内容的 10%），组织可使用本地解决方案 Active Directory Rights Management Services 创建保留在本地的密钥。 通过此解决方案，计算机可从云中获取其 Azure 信息保护策略，但可使用本地密钥来保护此标识的内容。

若要深入了解 HYOK 并确保你了解其局限性和限制及使用指南，请参阅 [AD RMS 保护的自留密钥 (HYOK) 要求和限制](../deploy-use/configure-adrms-restrictions.md)。

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>在哪里可以找到与 Azure RMS 集成的第三方解决方案的相关信息？

许多软件供应商已经具备或正在实施与 Azure 权限管理集成的解决方案，并且这一数量正在快速增长。 你可能会发现查看[启用 RMS 的解决方案](requirements-applications.md#rms-enlightened-solutions)列表，并通过 Twitter 上的 [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) 了解最新动态非常有用。 但是，如果有特定的问题，可以向信息保护团队发送电子邮件：askipteam@microsoft.com。

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>RMS 连接器是否有管理包或类似的监视机制？

虽然 Rights Management 连接器会将信息、警告和错误消息记录到事件日志中，但不提供用于监视这些事件的管理包。 不过，[监视 Azure Rights Management 连接器](../deploy-use/monitor-rms-connector.md)中记录了事件及其说明的列表，并提供更多帮助你采取纠正措施的信息。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators"></a>是否必须是全局管理员才能配置 Azure RMS？我可以委派给其他管理员吗？

显然，Office 365 租户或 Azure AD 租户的全局管理员可以运行 Azure Rights Management 服务的所有管理任务。 但是，如果你想为其他用户分配管理权限，则可以通过使用 Azure RMS PowerShell cmdlet [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) 实现此目的。 你可以按用户帐户或组分配此管理角色。 有两种角色可用：**全局管理员**和**连接器管理员**。 

如这些角色名称所示，第一种角色授权运行 Azure Rights Management 的所有管理任务（而不使其成为其他云服务的全局管理员），第二种角色授权仅运行 Rights Management (RMS) 连接器。

需要注意的事项：

- 只有 Office 365 的全局管理员和 Azure AD 的全局管理员才能使用 Office 365 管理中心或 Azure 经典门户来配置 Azure RMS。 如果将 Azure 门户用于 Azure 信息保护，也可以安全管理员身份登录。

- 分配有 Azure RMS 全局管理员角色的用户必须使用 Azure RMS PowerShell 命令来配置 Azure RMS。 请参阅[使用 Windows PowerShell 管理 Azure Rights Management](../deploy-use/administer-powershell.md)，以帮助查找特定任务的正确 cmdlet。

- 如果配置了[加入控制](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，此配置不会影响管理 Azure RMS 的能力，但会影响管理 RMS 连接器的能力。 例如，如果配置了加入控制，以致仅允许“IT 部门”组保护内容，那么，用于安装和配置 RMS 连接器的帐户必须是该组的成员。 

- 任何 Azure RMS 管理员（例如租户全局管理员或 Azure RMS 全局管理员）都不能对受 Azure RMS 保护的文档或电子邮件自动解除保护。 只有在启用了超级用户功能的情况下，分配为 Azure RMS 超级用户的用户才能执行此操作。 但是，租户全局管理员和所有 Azure RMS 全局管理员都可以将用户分配为超级用户，包括其自己的帐户。 他们还可以启用超级用户功能。 这些操作记录在 Azure RMS 管理员日志中。 有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)中的“最佳安全做法”部分。 

>[!NOTE]
> 用于配置 Azure 权限管理保护的模板和新选项已移动到 Azure 门户，除支持全局管理员访问之外，该网站还支持安全管理员访问。 

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>如何在 Azure 门户中创建新的自定义模板？

自定义模板已移动到 Azure 门户，可以在该门户中继续将其作为模板进行管理，或将其转换为标签。 要创建新模板，请创建新标签并为 Azure RMS 配置数据保护设置。 这会在后台创建一个新模板，集成了 Rights Management 模板的服务和应用程序都可以访问该模板。

有关 Azure 门户中的模板的详细信息，请参阅[配置和管理 Azure 信息保护的模板](../deploy-use/configure-policy-templates.md)。

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>我对 Exchange 采用混合部署：Exchange Online 上存在一些用户，而其他用户则在 Exchange Server 上。Azure RMS 支持这种部署吗？
绝对支持，而且很棒的是，用户将受到无缝保护，并可以在两种 Exchange 部署上使用受保护的电子邮件和附件。 对于此配置，[激活 Azure RMS](../deploy-use/activate-service.md) 并[启用适用于 Exchange Online 的 IRM](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)，然后[部署并配置适用于 Exchange Server 的 RMS 连接器](../deploy-use/deploy-rms-connector.md)。

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azure-rms"></a>如果在我的生产环境中使用该保护，那么我的公司是否就只能使用该解决方案？或者是否存在无法访问由 Azure RMS 进行保护的内容的风险？
不会，你可以始终控制并继续访问数据，即使你决定不再使用 Azure Rights Management 服务也是如此。 有关详细信息，请参阅[解除 Azure Rights Management 授权和停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)。

但是，在你解除 Azure RMS 部署授权前，我们希望倾听你的意见，了解你为什么做出这个决定。 如果 Azure Rights Management 保护未能满足你的业务需求，请联系我们，以确认在不久的将来是否会有新的功能，或者是否存在替代功能。 将电子邮件发送到 [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS)，我们将很高兴讨论你的技术和商业要求。

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>是否可以控制哪些用户能够使用 Azure RMS 来保护内容？
是的，Azure Rights Management 服务具有针对这一应用场景的用户载入控制。 有关详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md) 一文中的[为分阶段部署配置加入控制](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)部分。

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>是否可以防止用户与特定的组织共享受保护文档？
在数据保护中使用 Azure Rights Management 服务的最大优势之一在于，它支持企业与企业的协作，同时，无需为每个合作伙伴组织配置显式信任关系，因为 Azure AD 会代你处理好身份验证。

我们未提供相应的管理选项来防止用户与特定的组织安全共享文档。 例如，你想要阻止某家你不信任的或者竞争的组织。 阻止 Azure 权限管理服务向这些组织的用户发送受保护文档没有任何意义，因为你的用户之后还是会共享未保护的文档，而这也许是你最不希望发生的事情。 例如，你无法识别谁在与这些组织的用户共享公司机密文档，但是，如果文档（或电子邮件）受 Azure Rights Management 服务的保护，则可以识别。

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>如果我与公司之外的用户共享受保护文档，该用户如何进行身份验证。
Azure Rights Management 服务始终使用 Azure Active Directory 帐户和关联的电子邮件地址进行用户身份验证，这可以为管理员建立企业间的无缝协作。 如果其他组织使用 Azure 服务，用户已具有 Azure Active Directory 帐户，即使这些帐户是在本地创建和进行管理，然后同步到 Azure。 如果组织具有 Office 365，此服务在后台还会将 Azure Active Directory 用于用户帐户。 如果用户的组织在 Azure 中没有托管帐户，用户可以注册[个人 RMS](../understand-explore/rms-for-individuals.md)，并使用该用户帐户为组织创建非托管的 Azure 租户和目录，以便可以在 Azure Rights Management 服务中对此用户（和后续用户）进行身份验证。

这些帐户的身份验证方法各不相同，具体取决于其他组织中的管理员如何配置 Azure Active Directory 帐户。 例如，他们可以使用为这些帐户、多重身份验证 (MFA)、联合身份验证创建的密码，或在 Active Directory 域服务中创建、然后同步到 Azure Active Directory 的密码。

## <a name="can-i-add-external-users-people-from-outside-my-company-to-templates"></a>能否将外部用户（公司外部人员）添加到模板？
是。 创建最终用户（和管理员）可以从应用程序中选择的模板，可使用户使用你指定的预定义策略应用信息保护变得简单快捷。 该模板中的设置之一是哪些用户能够访问内容，而且你可以指定组织中的用户和组以及组织外部的用户和组。 甚至可以指定另一组织中的所有用户。

配置[保护设置](../deploy-use/configure-policy-protection.md)时，可以使用 Azure 门户来执行此配置。 或者，可以使用 PowerShell 来执行此配置。 若要使用 PowerShell：

-   **使用权限定义对象创建或更新模板**。  在权限定义对象中指定外部电子邮件地址及其权限，然后你将使用该地址创建或更新模板。 指定权限定义对象时，可使用 [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition) cmdlet 来创建一个变量，然后通过 [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate) cmdlet（如果是新模板）或 [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) cmdlet（如果需要修改现有模板）将该变量提供给 RightsDefinition 参数。 但是，如果你是将这些用户添加到现有模板中，则需要在模板中为现有组定义权限定义对象，不仅仅只需为外部用户执行此类操作。

有关模板的详细信息，请参阅[配置和管理 Azure 信息保护的模板](../deploy-use/configure-policy-templates.md)。

## <a name="does-azure-rms-work-with-dynamic-groups-in-azure-ad"></a>Azure RMS 是否适用于 Azure AD 中的动态组？
借助 Azure AD Premium 功能，你可以通过指定[基于属性的规则](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/)为安全组配置动态成员资格。 此组类型不支持电子邮件地址，因此不能与 Azure 权限管理服务一起使用。 但是，Office 365 组支持动态组成员资格并已启用邮件。 由于此组启用了邮件，可以将其用于 Azure Rights Management 保护。

有关可用于 Azure 权限管理服务的用户和组的要求详细信息，请参阅[准备用户和组以用于 Azure 信息保护](../plan-design/prepare.md)。

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>如何向 Gmail 或 Hotmail 帐户发送受保护的电子邮件？

你可能已查看关于 Azure 信息保护如何向 Gmail 或 Hotmail 帐户发送受保护的电子邮件的参考资料或演示。 此功能仍处于个人预览阶段，所以在完全发布前，无法在本文档中找到有关此功能的详细信息。

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Azure RMS 支持哪些设备和哪种文件类型？
有关支持 Azure Rights Management 服务的设备的列表，请参阅[支持 Azure Rights Management 数据保护的客户端设备](../get-started/requirements-client-devices.md)。 由于并非所有受支持的设备目前都能支持全部的 Rights Management 功能，因此，还请务必查看[启用 RMS 的应用程序](../get-started/requirements-applications.md#rms-enlightened-applications)表。

Azure Rights Management 服务支持所有文件类型。 对于文字、图像、Microsoft Office（Word、Excel、PowerPoint）文件、.pdf 文件和一些其他应用程序文件类型，Azure Rights Management 提供的本地保护包括对权利（权限）的加密和执行。 对于其他应用程序和文件类型，通用保护提供文件封装和验证以确认用户是否授权打开文件。

有关 Azure 权限管理本机支持的文件扩展名列表，请参阅 [Azure 信息保护客户端支持的文件类型](../rms-client/client-admin-guide-file-types.md)。 Azure 信息保护客户端支持未列出的文件扩展名，该客户端可自动对这些文件应用常规保护。

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>如何配置 Mac 计算机以保护和跟踪文档？

首先，请确保已使用 https://portal.office.com 上的软件安装链接安装了 Office for Mac。 有关完整说明，请参阅[在电脑或 Mac 上下载并安装或重新安装 Office 365 或 Office 2016](https://support.office.com/en-us/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658)。

打开 Outlook 并使用 Office 365 工作或学校帐户创建配置文件。 然后，创建新邮件，并执行以下操作来配置 Office，使其可以使用 Azure 权限管理服务来保护文档和电子邮件：

1. 在新邮件的“选项”选项卡上，单击“权限”，然后单击“验证凭据”。

2. 出现提示时，再次指定你的 Office 365 工作或学校帐户详细信息，然后选择“登录”。 
    
    这将下载 Azure 权限管理模板，“验证凭据”选项将替换为包括“无限制”、“不要转发”以及为租户发布任何 Azure 权限管理模板的选项。 现在可以取消此新邮件。

保护电子邮件或文档：在“选项”选项卡上，单击“权限”，然后选择用于保护电子邮件或文档的选项或模板。

在保护文档之后跟踪文档：在安装了 Azure 信息保护客户端的 Windows 计算机上，使用 Office 应用程序或文件资源管理器将文档注册到文档跟踪站点。 有关说明，请参阅[跟踪和撤销文档](../rms-client/client-track-revoke.md)。 现在可以从 Mac 计算机使用 Web 浏览器访问文档跟踪站点 (https://track.azurerms.com) 来跟踪和撤销此文档。

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>当我打开受 RMS 保护的 Office 文档时，关联的临时文件是否也将受 RMS 保护？
否。 在此方案中，关联的临时文件不包含原始文档中的数据，而仅包含该文件打开时用户输入的内容。 与原始文件不同，临时文件明显不适合共享，将保留在设备上，受本地安全控件（例如 BitLocker 和 EFS）保护。

## <a name="we-really-want-to-use-byok-with-azure-information-protection-but-learned-that-this-isnt-compatible-with-exchange-onlinewhats-your-advice"></a>我们确实很想将 BYOK 和 Azure 信息保护结合使用，但是 BYOK 与 Exchange Online 不兼容 — 你有什么建议呢？
不要因目前这种限制而推迟使用 Azure 信息保护的 Azure Rights Management 服务。 如果具有 Exchange Online 并想要使用自带密钥 (BYOK)，我们建议暂时以默认密钥管理模式部署 Azure 信息保护，该模式由 Microsoft 生成和管理密钥。 如此一来，你现在可以获取保护重要文件和电子邮件的所有好处，并可以选择以后移动到 BYOK（例如，当 Exchange Online 不支持 BYOK 时）。 移动到 BYOK 时，以前受保护的文档和电子邮件仍然能够通过使用存档的密钥进行访问。

但是，如果公司策略要求使用硬件安全模块 (HSM)，而这会阻止 Azure 信息保护的部署，那么另一种选择是将 Azure 信息保护和 BYOK 一起部署，只不过 Exchange 的 Rights Management 保护功能会减弱。 有关详细信息，请参阅[计划和实施 Azure 信息保护租户密钥](../plan-design/plan-implement-tenant-key.md)中的 [BYOK 定价和限制](../plan-design/byok-price-restrictions.md)。

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>我正在寻找的一项功能看起来不适用于 SharePoint 保护的库。是否计划了针对此功能的支持？
目前，SharePoint 通过使用受 IRM 保护的库来支持受 RMS 保护的文档，但是该库不支持 Rights Management 模板、文档跟踪和一些其他功能。 有关详细信息，请参阅 [Office 应用程序和服务](../understand-explore/office-apps-services-support.md)一文中的 [SharePoint Online 和 SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server)部分。

如果对尚不支持的某项特定功能感兴趣，请务必关注 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)（企业移动性和安全性博客）上的公告。

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>如何在 SharePoint Online 中配置 OneDrive for Business，以便用户可以安全地与公司内外的人员共享他们的文件？
默认情况下，作为 Office 365 管理员，你不用执行此配置，用户会进行配置。

正如 SharePoint 站点管理员为其拥有的 SharePoint 库启用并配置 IRM 一样，根据 OneDrive for Business 的设计，用户也需要为自己的 OneDrive for Business 库启用并配置 IRM。 不过，你可以使用 PowerShell 为他们执行此类操作。 有关说明，请参阅 [Office 365：客户端和联机服务的配置](../deploy-use/configure-office365.md)一文中的 [SharePoint Online 和 OneDrive for Business：IRM 配置](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)部分。

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>对于成功部署，是否有任何提示或窍门？
在考察大量的部署并聆听客户、合作伙伴、顾问和支持工程师的意见后，结合自身的经验，我们很乐意与你分享下面这个极其有效的诀窍：“设计并部署简单策略”。

由于 Azure 信息保护支持与任何人安全共享，因此，你完全有理由相信自己的数据保护措施的覆盖面。 但是，对权限策略应持保守态度。 对于许多组织而言，对业务产生的最大影响来自于通过应用默认权限策略模板防止数据泄漏，将其访问权限限制给组织中的人员。 当然，你可以根据需要采取粒度级比这高得多的措施 - 例如，防止人员打印、编辑，等等。但是，对于确实需要高级安全性的文档，请将更高粒度级的限制保留为例外措施，并且不要一开始就实施这些限制性更强的策略，而是计划采取分阶段的实施方案。

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>我们如何重新获取对由已离职员工保护的文件的访问权限？
使用[超级用户功能](../deploy-use/configure-super-users.md)，它可以让授权用户对组织租户授予的所有使用许可证行使使用权限。 根据需要，此相同功能可以让授权服务编写文件索引和检查文件。

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>在文档跟踪站点中测试吊销时，显式的消息提示人们仍可在 30 天内访问此文档—该时间段是否可配置？

是。 该消息反映了此特定文件的使用许可证。 使用许可证是为打开受保护文件或电子邮件消息的用户所授予的每个文档证书。 该证书包含此用户对文件或电子邮件消息所具有的权限、用于加密内容的加密密钥，以及文档策略中定义的其他访问限制。 该使用许可证的有效期已过期，当某用户尝试打开该文件或电子邮件消息时，必须向 Azure Rights Management 服务重新提交其用户凭据。 

如果撤销文件，仅在用户对 Azure Rights Management 服务进行身份验证时才会强制执行此操作。 因此，如果文件的使用许可证有效期为 30 天，且用户已经打开过文档，则该用户在使用许可证期间仍继续拥有该文档的访问权限。 使用许可证过期时，用户必须重新进行身份验证，此时由于文件被撤销，因此会拒绝用户访问。

保护文档的用户，即 [Rights Management 颁发者](../deploy-use/configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)不受此撤销的限制，始终能够访问其文档。 

租户使用许可证有效期默认值为 30 天，可使用 PowerShell cmdlet **Set-AadrmMaxUseLicenseValidityTime** 配置该值。 可在模板中使用更严格的设置替代此设置。 

有关使用许可证的工作原理的详细信息和示例，请参阅 [Set-AadrmMaxUseLicenseValidityTime](/powershell/module/aadrm/set-aadrmmaxuselicensevaliditytime) 的详细说明。

## <a name="can-rights-management-prevent-screen-captures"></a>Rights Management 可以防止屏幕截图吗？
通过不授予复制[使用权限](../deploy-use/configure-usage-rights.md)，Rights Management 可以阻止许多常用屏幕捕获工具在 Windows 平台（Windows 7、Windows 8.1、Windows 10、Windows Phone）和 Android 上进行屏幕捕获。 但是，iOS 和 Mac 设备不允许任何应用阻止屏幕捕获，而浏览器（例如，与 Outlook Web App 和 Office Online 一起使用时）也不能阻止屏幕捕获。

阻止屏幕捕获可帮助避免意外或疏忽披露机密或敏感信息。 不过，用户可以通过多种方式来共享显示在屏幕上的数据，进行屏幕截图只是其中一种方法。 例如，如果想要共享所显示的信息，用户可以使用带相机的手机拍照，可以重新键入相关数据，还可以直接通过口头方式将其传达给某人。

如这些例子所示，即使支持 Rights Management API 的所有平台和所有软件都阻止屏幕捕获，仅靠技术并非始终能够阻止用户共享他们不应该共享的数据。 Rights Management 可以通过授权和使用策略来确保重要数据的安全性，但在使用此企业权限管理解决方案时还应加入其他控制手段。 例如，可以实施物理安全措施，可以仔细盘查和监视有权访问组织数据的人员，还可以进行用户教育，让用户了解哪些数据是不应共享的。

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>用户通过“不得转发”和不包括“转发”权限的模板来保护电子邮件有什么区别？

除名称和外观外，“不转发”既不是“转发”权限的相反权限，也不是模板。 它实际上是一组权限，包括限制复制、打印和保存附件以及限制转发电子邮件。 这些权限通过所选收件人动态应用于用户，而不由管理员静态分配。 有关详细信息，请参阅[为 Azure Rights Management 配置使用权限](../deploy-use/configure-usage-rights.md)中的[电子邮件的“不得转发”选项](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails)部分。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


