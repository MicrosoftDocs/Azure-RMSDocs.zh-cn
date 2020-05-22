---
title: Azure RMS 的常见问题解答 - AIP
description: 有关 Azure 信息保护中数据保护服务 Azure Rights Management (Azure RMS) 的一些常见问题。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 25ad77fb68f6d26891eaae62318388ce21fe54b4
ms.sourcegitcommit: 8499602fba94fbfa28d7682da2027eeed6583c61
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83746783"
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Azure 信息保护中的有关数据保护的常见问题

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）**** 和标签管理**** 将于 2021 年 3 月 31 日**** 弃用****。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

是否有关于 Azure 信息保护中数据保护服务 Azure Rights Management 的问题？ 请查看此处是否有答案。

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>是否必须将文件存放在云中才能受 Azure Rights Management 保护？
否，这是一个常见的误解。 在信息保护过程中，Azure Rights Management 服务（和 Microsoft）不查看或存储数据。 要保护的信息永远不会发送或存储到 Azure 中，除非显式将其存储在 Azure 中，或者使用其他可用于在 Azure 中存储数据的云服务。

有关详细信息，请参阅[Azure RMS 如何工作？在](./how-does-it-work.md)这种情况下，要了解在本地创建和存储的机密可乐配方公式如何受 Azure Rights Management 服务保护，但仍保留在本地。

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>Azure Rights Management 其他 Microsoft 云服务中的加密和加密之间的区别是什么？

Microsoft 提供了多个加密技术，用于保护数据以满足不同的方案，方案之间通常能够互补。 例如，Office 365 为存储在 Office 365 中的数据提供静态加密，而 Azure 信息保护的 Azure Rights Management 服务则独立加密数据，使其不受所在位置和传输方式影响而得到保护。

这些加密技术相互补充，使用它们需要单独对其进行启用和配置。 执行此操作时，可以选择使用自己的密钥进行加密，也称为“BYOK”方案。 为其中一种技术启用 BYOK 不影响其他技术。 例如，可对 Azure 信息保护使用 BYOK，而对其他加密技术不使用 BYOK；反之亦然。 不同技术所用密钥可为相同或不同，具体取决于为每种服务配置的加密选项。

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>BYOK 和 HYOK 之间的区别是什么，应何时使用它们？

Azure 信息保护上下文中出现**自带密钥** (BYOK) 时，则表示应为 Azure Rights Management 保护创建自己的本地密钥。 然后将该密钥传输到 Azure Key Vault 中的硬件安全模块 (HSM)，可在其中继续拥有并管理密钥。 若不执行此操作，Azure Rights Management 保护会使用 Azure 中自动创建并进行管理的密钥。 这种默认配置称为“Microsoft 管理”而不是“客户管理”（BYOK 选项）。

有关 BYOK 以及是否应为组织选择此密钥拓扑的详细信息，请参阅[规划和实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

在 Azure 信息保护的上下文中出现**自留密钥** (HYOK)，则表示少量组织的文档或电子邮件自己无法通过存储在云中的密钥进行保护。 对于这些组织来说，即使使用 BYOK 创建和管理密钥，此限制仍然适用。 此限制通常是由于法规或符合性问题引起的，并且 HYOK 配置应仅应用于“顶级机密”信息，此信息永远不会在组织外部共享、仅会在内部网络中使用，并且无需通过移动设备访问。

对于这些异常（通常需要保护的内容少于所有内容的 10%），组织可使用本地解决方案 Active Directory Rights Management Services 创建保留在本地的密钥。 通过此解决方案，计算机可从云中获取其 Azure 信息保护策略，但可使用本地密钥来保护此标识的内容。

若要深入了解 HYOK 并确保了解其局限性和限制及使用指南，请参阅 [AD RMS 保护的自留密钥 (HYOK) 要求和限制](configure-adrms-restrictions.md)。

## <a name="can-i-now-use-byok-with-exchange-online"></a>现在我是否可以结合使用 BYOK 和 Exchange Online？

可以，在按照 [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)（设置构建在 Azure 信息保护之上新的 Office 365 邮件加密功能）中的说明进行操作时，现在可以结合使用 BYOK 和 Exchange Online。 这些说明介绍如何启用 Exchange Online 中的新功能，这些功能支持将 BYOK 用于 Azure 信息保护和新的 Office 365 邮件加密。

有关此更改的详细信息，请参阅博客公告：[具有新功能的 Office 365 邮件加密](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>在哪里可以找到与 Azure RMS 集成的第三方解决方案的相关信息？

许多软件供应商已经具备或正在实施与 Azure Rights Management 集成的解决方案，并且这一数量正在快速增长。 你可能会发现，查看[启用 RMS 的解决方案](requirements-applications.md#rms-enlightened-solutions)列表，并在 Twitter 上从 [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) 了解最新更新非常有用。 此外，请查看[开发人员指南](./develop/developers-guide.md)并在 Azure 信息保护 [Yammer 网站](https://www.yammer.com/AskIPTeam)上发布任何特定的集成问题。

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>RMS 连接器是否有管理包或类似的监视机制？

尽管 Rights Management 连接器会将信息、警告和错误消息记录到事件日志中，但没有管理包包含对这些事件的监视。 不过，[监视 Azure Rights Management 连接器](monitor-rms-connector.md)中记录了事件及其说明的列表，并提供更多帮助你采取纠正措施的信息。

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>如何在 Azure 门户中创建新的自定义模板？

自定义模板已移动到 Azure 门户，可以在该门户中继续将其作为模板进行管理，或将其转换为标签。 要创建新模板，请创建新标签并为 Azure RMS 配置数据保护设置。 这会在后台创建一个新模板，集成了 Rights Management 模板的服务和应用程序都可以访问该模板。

有关 Azure 门户中的模板的详细信息，请参阅[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)。

## <a name="ive-protected-a-document-and-now-want-to-change-the-usage-rights-or-add-usersdo-i-need-to-reprotect-the-document"></a>我已保护一个文档，但现在想要更改使用权限或添加用户，是否需要重新保护该文档？

如果该文档使用的是标签或模板进行保护，则无需重新保护该文档。 通过更改使用权限来修改标签或模板或者添加新组（或用户），然后保存这些更改：

- 如果用户在你进行更改之前没有访问过该文档，则更改会在他们打开该文档时立即生效。

- 如果用户已访问过文档，则所做的更改将在他们的[使用许可证](configure-usage-rights.md#rights-management-use-license)过期时生效。 只有在等不及使用许可证过期时才需要重新保护文档。 重新保护操作会有效地创建一个新的文档版本，并因此为用户创建新的使用许可证。

或者，如果已为所需权限配置了一个组，则可更改组成员身份以包含或排除用户，而无需更改标签或模板。 更改生效前可能稍有延迟，因为组成员身份由 Azure Rights Management 服务[缓存](prepare.md#group-membership-caching-by-azure-information-protection)。

如果文档通过自定义权限保护，则无法更改现有文档的权限。 必须再次保护文档，并指定这一新的文档版本所需的所有用户和所有使用权限。 若要重新保护受保护的文档，必须具有“完全控制”使用权限。

提示：要检查文档是受模板保护还是受自定义权限保护，请使用 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell cmdlet。 如果是自定义权限，则始终能看到访问受限的模板说明，以及运行 [Get-RMSTemplate](/powershell/module/azureinformationprotection/get-rmstemplate) 时不会显示的唯一模板 ID****。

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>我对 Exchange 采用混合部署：Exchange Online 上存在一些用户，而其他用户则在 Exchange Server 上。Azure RMS 支持这种部署吗？
绝对支持，而且很棒的是，用户能够在两种 Exchange 部署上无缝保护并使用受保护的电子邮件和附件。 对于此配置，[激活 Azure RMS](activate-service.md) 并[启用适用于 Exchange Online 的 IRM](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)，然后[部署并配置适用于 Exchange Server 的 RMS 连接器](deploy-rms-connector.md)。

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azurerms"></a>如果在我的生产环境中使用该保护，那么我的公司是否就只能使用该解决方案？或者是否存在无法访问由 Azure RMS 进行保护的内容的风险？
不会，你可以始终控制并继续访问数据，即使你决定不再使用 Azure Rights Management 服务也是如此。 有关详细信息，请参阅[解除 Azure Rights Management 授权和停用 Azure Rights Management](decommission-deactivate.md)。

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>是否可以控制哪些用户能够使用 Azure RMS 来保护内容？
是的，Azure Rights Management 服务具有针对这一应用场景的用户载入控制。 有关详细信息，请参阅[从 Azure 信息保护中激活保护服务](activate-service.md)一文中的为[分阶段部署配置加入控制](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)部分。

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>是否可以防止用户与特定的组织共享受保护文档？
在数据保护中使用 Azure Rights Management 服务的最大优势之一在于，它支持企业与企业的协作，同时，无需为每个合作伙伴组织配置显式信任关系，因为 Azure AD 会代你处理好身份验证。

我们未提供相应的管理选项来防止用户与特定的组织安全共享文档。 例如，你想要阻止你不信任或具有竞争性业务的组织。 阻止 Azure Rights Management 服务向这些组织的用户发送受保护文档没有任何意义，因为你的用户会共享其文档不受保护，这可能是你在此方案中的最后一件事。 例如，你无法识别谁在与这些组织的用户共享公司机密文档，如果文档（或电子邮件）受 Azure Rights Management 服务的保护，则可以执行此操作。

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>如果我与公司之外的用户共享受保护文档，该用户如何进行身份验证。

默认情况下，Azure Rights Management 服务使用 Azure Active Directory 帐户和关联的电子邮件地址进行用户身份验证，这可以为管理员建立企业到企业的无缝协作。 如果其他组织使用 Azure 服务，用户已具有 Azure Active Directory 帐户，即使这些帐户是在本地创建和进行管理，然后同步到 Azure。 如果组织具有 Office 365，此服务在后台还会将 Azure Active Directory 用于用户帐户。 如果用户的组织在 Azure 中没有托管帐户，用户可以注册[个人 RMS](./rms-for-individuals.md)，这将为组织创建非托管的 azure 租户和目录，并为组织提供用户帐户，以便随后可以为此用户（和后续用户）提供针对 Azure Rights Management 服务的身份验证。

这些帐户的身份验证方法各不相同，具体取决于其他组织中的管理员如何配置 Azure Active Directory 帐户。 例如，他们可以使用为这些帐户、联合身份验证创建的密码，或在 Active Directory 域服务中创建、然后同步到 Azure Active Directory 的密码。

其他身份验证方法：

- 如果针对在 Azure AD 中没有帐户的用户保护含有 Office 文档附件的电子邮件，身份验证方法则会发生改变。 Azure Rights Management 服务会通过一些常用社交标识提供者进行身份验证，例如 Gmail。 如果用户的电子邮件提供商受支持，用户可登录到该服务，其电子邮件提供商负责对其进行身份验证。 如果用户的电子邮件提供商不受支持，或者作为首选项，用户可申请用于对他们进行身份验证的一次性密码，并在 Web 浏览器中显示含有受保护文档的电子邮件。

- Azure 信息保护可以将 Microsoft 帐户用于支持的应用程序。 目前，并非所有应用程序都可以在使用 Microsoft 帐户进行身份验证时打开受保护的内容。 [详细信息](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>能否将外部用户（公司外部人员）添加到自定义模板？

是。 利用[保护设置](configure-policy-protection.md)（可在 Azure 门户中配置），可为组织外的用户和组甚至其他组织中的所有用户添加权限。 你可能会发现引用分步示例，[使用 Azure 信息保护保护文档协作](secure-collaboration-documents.md)很有用。 

注意，如果具有 Azure 信息保护标签，必须先将自定义模板转换为标签，然后再在 Azure 门户中配置这些保护设置。 有关详细信息，请参阅[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)。

此外，也可使用 PowerShell 将外部用户添加到自定义模板和标签。 此配置要求使用权限定义对象（用于更新模板）：

1. 通过使用[AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) cmdlet 创建变量，在权限定义对象中指定外部电子邮件地址及其权限。

2. 将此变量提供给[AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) Cmdlet 的 RightsDefinition 参数。

    如果将用户添加到现有模板，除新用户以外，还须在模板中为现有用户定义权限定义对象。 对于此方案，建议查看[示例](/powershell/module/aipservice/set-aipservicetemplateproperty#examples)部分的“示例 3：将新用户和权限添加到自定义模板”，这可帮助你了解相关 cmdlet****。

## <a name="what-type-of-groups-can-i-use-with-azure-rms"></a>我可以对 Azure RMS 使用什么类型的组？
大多数情况下，可以使用具有电子邮件地址的 Azure AD 中的任何组类型。 尽管分配使用权限时此经验法则始终适用，但在管理 Azure Rights Management 服务时存在一些例外。 有关详细信息，请参阅[组帐户 Azure 信息保护要求](prepare.md#azure-information-protection-requirements-for-group-accounts)。

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>如何向 Gmail 或 Hotmail 帐户发送受保护的电子邮件？

使用 Exchange Online 和 Azure Rights Management 服务时，必须将电子邮件作为受保护的邮件发送给用户。 例如，可在 Outlook 网页版的命令栏中选择新的“保护”按钮，使用 Outlook“不要转发”按钮或菜单选项********。 或者，可选择 Azure 信息保护标签，自动应用“不要转发”功能，并对电子邮件进行分类。

收件人会看见一个登录到他们的 Gmail、Yahoo 或 Microsoft 帐户的选项，然后可以阅读受保护的邮件。 或者，他们可选择一次性密码选项在浏览器中阅读此电子邮件。

若要支持此方案，必须为 Azure Rights Management 服务和 Office 365 邮件加密中的新功能启用 Exchange Online。 有关此配置的详细信息，请参阅 [Exchange Online：IRM 配置](configure-office365.md#exchangeonline-irm-configuration)。

若要详细了解新功能（包括在所有设备上支持所有电子邮件帐户），请参阅以下博客文章：[Announcing new capabilities available in Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)（宣布在 Office 365 邮件加密中推出新功能）。

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Azure RMS 支持哪些设备和哪种文件类型？
有关支持 Azure Rights Management 服务的设备的列表，请参阅[支持 Azure Rights Management 数据保护的客户端设备](./requirements-client-devices.md)。 由于并非所有受支持的设备目前都能支持全部的 Rights Management 功能，因此，还请务必查看[启用 RMS 的应用程序](./requirements-applications.md#rms-enlightened-applications)表。

Azure Rights Management 服务支持所有文件类型。 对于文字、图像、Microsoft Office（Word、Excel、PowerPoint）文件、.pdf 文件和一些其他应用程序文件类型，Azure Rights Management 提供的本地保护包括对权利（权限）的加密和执行。 对于其他应用程序和文件类型，通用保护提供文件封装和验证以确认用户是否授权打开文件。

有关 Azure Rights Management 本机支持的文件扩展名列表，请参阅 [Azure 信息保护客户端支持的文件类型](./rms-client/client-admin-guide-file-types.md)。 Azure 信息保护客户端支持未列出的文件扩展名，该客户端可自动对这些文件应用常规保护。

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>如何配置 Mac 计算机以保护和跟踪文档？

首先，请确保已使用 https://admin.microsoft.com 上的软件安装链接安装了 Office for Mac。 有关完整说明，请参阅[在电脑或 Mac 上下载并安装或重新安装 Office 365 或 Office 2019](https://support.office.com/en-us/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658)。

打开 Outlook 并使用 Office 365 工作或学校帐户创建配置文件。 然后，创建新邮件，并执行以下操作来配置 Office，使其可以使用 Azure Rights Management 服务来保护文档和电子邮件：

1. 在新邮件的“选项”**** 选项卡上，单击“权限”****，然后单击“验证凭据”****。

2. 出现提示时，再次指定 Office 365 工作或学校帐户详细信息，然后选择“登录”****。

    这将下载 Azure Rights Management 模板，“验证凭据”**** 选项将替换为包括“无限制”****、“不要转发”**** 以及为租户发布任何 Azure Rights Management 模板的选项。 现在可以取消此新邮件。

保护电子邮件或文档：在“选项”**** 选项卡上，单击“权限”****，然后选择用于保护电子邮件或文档的选项或模板。

在保护文档之后跟踪文档：在安装了 Azure 信息保护客户端的 Windows 计算机上，使用 Office 应用程序或文件资源管理器将文档注册到文档跟踪站点。 有关说明，请参阅[跟踪和撤销文档](./rms-client/client-track-revoke.md)。 现在可以从 Mac 计算机使用 Web 浏览器访问文档跟踪站点 (https://track.azurerms.com) 来跟踪和撤销此文档。

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>当我打开受 RMS 保护的 Office 文档时，关联的临时文件是否也将受 RMS 保护？
否。 在此方案中，关联的临时文件不包含原始文档中的数据，而只包含文件打开时用户输入的内容。 与原始文件不同，临时文件明显不适合共享，将保留在设备上，受本地安全控件（例如 BitLocker 和 EFS）保护。

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>我正在寻找的一项功能似乎不适用于 SharePoint 受保护的库，是否支持对我的功能进行计划？
目前，Microsoft SharePoint 通过使用受 IRM 保护的库来支持受 RMS 保护的文档，这些库不支持 Rights Management 模板、文档跟踪和一些其他功能。 有关详细信息，请参阅[Office 应用程序和服务](./office-apps-services-support.md)一文[中 Microsoft 365 和 sharepoint Server 中的 sharepoint](./office-apps-services-support.md#sharepoint-in-microsoft-365-and-sharepoint-server)部分。

如果对尚不支持的某项特定功能感兴趣，请务必关注 [Enterprise Mobility and Security Blog](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-rights-management-services)（企业移动性和安全性博客）上的公告。

## <a name="how-do-i-configure-one-drive-in-sharepoint-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>如何实现在 SharePoint 中配置一个驱动器，以便用户可以安全地与公司内外的人员共享其文件？
默认情况下，作为 Office 365 管理员，你未配置此设置;用户执行的操作。

正如 SharePoint 站点管理员为其拥有的 SharePoint 库启用并配置 IRM 一样，OneDrive 旨在使用户为其自己的 OneDrive 库启用并配置 IRM。 不过，可以使用 PowerShell 为他们执行此类操作。 有关说明，请参阅[Office 365：客户端的配置和联机服务](configure-office365.md)一文[中 Microsoft 365 和 OneDrive： IRM 配置](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration)部分中的 SharePoint。

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>对于成功部署，是否有任何提示或窍门？

在考察大量的部署并聆听客户、合作伙伴、顾问和支持工程师的意见后，结合自身的经验，我们很乐意与你分享下面这个极其有效的诀窍：设计并部署简单策略****。

由于 Azure 信息保护支持与任何人安全共享，因此，你完全有理由相信自己的数据保护措施的覆盖面。 但是在配置权限使用限制时请保守一点。 对许多组织而言，最大的业务影响来自于通过将访问权限限制为组织内部人员的方式来防止数据泄露。 当然，如果需要，您可以获得更精细的粒度：阻止用户打印、编辑等。但是，对于确实需要高级安全性的文档，请保持更细致的限制，但不要在第一天实现这些限制更强的使用权限，而是计划更分阶段的方法。

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>我们如何重新获取对由已离职员工保护的文件的访问权限？
请使用[超级用户功能](configure-super-users.md)，对于受租户保护的所有文档和电子邮件，此功能会向授权用户授予完全控制使用权限。 超级用户可始终阅读此受保护的内容，并可根据需要移除保护或针对不同的用户进行重新保护。 根据需要，此相同功能可以让授权服务编写文件索引和检查文件。

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>在文档跟踪站点中测试吊销时，显式的消息提示人们仍可在 30 天内访问此文档—该时间段是否可配置？

是。 该消息反映了此特定文件的[使用许可证](configure-usage-rights.md#rights-management-use-license)。

如果撤销文件，仅在用户对 Azure Rights Management 服务进行身份验证时才会强制执行此操作。 因此，如果文件的使用许可证有效期为 30 天，且用户已经打开过文档，则该用户在使用许可证期间仍继续拥有该文档的访问权限。 使用许可证过期时，用户必须重新进行身份验证，此时由于文件被撤销，因此会拒绝用户访问。

保护文档的用户，即 [Rights Management 颁发者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)不受此撤销的限制，始终能够访问其文档。

租户使用许可证有效期的默认值为 30 天，此设置可通过标签或模板中限制性更强的设置进行替代。 若要详细了解使用许可证以及如何对其进行配置，请参阅 [Rights Management 使用许可证](configure-usage-rights.md#rights-management-use-license)文档。

## <a name="can-rights-management-prevent-screen-captures"></a>Rights Management 可以防止屏幕截图吗？
通过不授予复制**** [使用权限](configure-usage-rights.md)，Rights Management 可以阻止许多常用屏幕捕获工具在 Windows 平台（Windows 7、Windows 8.1、Windows 10、Windows 10 移动版）和 Android 上进行屏幕捕获。 不过，iOS 和 Mac 设备不允许任何应用阻止屏幕截图。 此外，任何设备上的浏览器也都不能阻止屏幕截图。 浏览器使用包括 web 上的 Outlook 和 web 上的 Office。

阻止屏幕捕获可帮助避免意外或疏忽披露机密或敏感信息。 但是，用户可以通过多种方式来共享显示在屏幕上的数据，拍摄屏幕截图只是一种方法。 例如，如果想要共享所显示的信息，用户可以使用带相机的手机拍照，可以重新键入相关数据，还可以直接通过口头方式将其传达给某人。

如这些例子所示，即使支持 Rights Management API 的所有平台和所有软件都阻止屏幕捕获，仅靠技术并非始终能够阻止用户共享他们不应该共享的数据。 Rights Management 可以通过授权和使用策略来确保重要数据的安全性，但在使用此企业权限管理解决方案时还应加入其他控制手段。 例如，可以实施物理安全措施，可以仔细盘查和监视有权访问组织数据的人员，还可以进行用户教育，让用户了解哪些数据是不应共享的。

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>用户通过“不得转发”和不包括“转发”权限的模板来保护电子邮件有什么区别？

除名称和外观外，“不转发”**** 既不是“转发”权限的相反权限，也不是模板。 它实际上是一组权限，包括限制在邮箱外复制、打印和保存电子邮件，以及限制电子邮件的转发。 这些权限通过所选收件人动态应用于用户，而不由管理员静态分配。 有关详细信息，请参阅为[Azure 信息保护配置使用权限](configure-usage-rights.md)中的[电子邮件](configure-usage-rights.md#do-not-forward-option-for-emails)的 "不转发" 选项部分。

