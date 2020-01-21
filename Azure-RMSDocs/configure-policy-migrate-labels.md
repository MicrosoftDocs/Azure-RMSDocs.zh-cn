---
title: 将 Azure 信息保护标签迁移到统一敏感度标签-AIP
description: 将 Azure 信息保护标签迁移到支持 Microsoft 信息保护框架的客户端和服务的统一敏感度标签。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/18/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: labelmigrate
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 45802279809a73c7338ff622fcd545e6e9eab7e7
ms.sourcegitcommit: 10cefe41b0c888ef237511cddeb23f9a54b3c07d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2020
ms.locfileid: "76281575"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-unified-sensitivity-labels"></a>如何将 Azure 信息保护标签迁移到统一敏感度标签

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
> *适用于[Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*


将 Azure 信息保护标签迁移到统一的标签平台，以便可以将它们用作[支持统一标签的客户端和服务](#clients-and-services-that-support-unified-labeling)的敏感度标签。

> [!NOTE]
> 如果你的 Azure 信息保护订阅非常新，则可能无需迁移标签，因为你的租户已在统一标签平台上。 有关详细信息，请参阅[如何确定我的租户是否在统一标签平台上？](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

迁移标签后，你将看不到 Azure 信息保护客户端（经典）的任何差异，因为此客户端将继续从 Azure 门户中的 Azure 信息保护策略下载标签。 但是，你现在可以将标签用于 Azure 信息保护的统一标签客户端和其他使用敏感度标签的客户端和服务。

在阅读迁移标签说明之前，你可能会发现以下常见问题很有用：

- [Azure 信息保护中的标签与 Office 365 中的标签之间有何区别？](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [何时将标签迁移到正确的时间？](faqs.md#when-is-the-right-time-to-migrate-my-labels)

- [迁移我的标签后，该使用哪个管理门户？](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>支持统一标签平台的管理角色

如果你在组织中使用管理员角色来委派管理，则可能需要对统一标签平台进行一些更改：

统一标签平台不支持**Azure 信息保护管理员**（以前称为**信息保护管理员**）的[Azure AD 角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)。 如果在组织中使用此管理角色来管理 Azure 信息保护，请将具有此角色的用户添加到**符合性管理员**、**符合性数据管理员**或**安全管理员**的 Azure AD 角色。 如果需要有关此步骤的帮助，请参阅[向用户授予对 Office 365 安全与合规中心的访问权限](https://docs.microsoft.com/microsoft-365/security/office-365-security/grant-access-to-the-security-and-compliance-center)。 另外，还可以在 Azure AD 门户、Microsoft 365 安全中心和 Microsoft 365 合规中心分配这些角色。

或者，若要使用角色，可以在管理中心为这些用户创建新角色组，然后向该组中添加“敏感度标签管理员”或“组织配置”角色。

如果未使用其中一个配置向这些用户授予对管理中心的访问权限，则在迁移标签后将无法在 Azure 门户中配置 Azure 信息保护。

迁移标签后，租户的全局管理员可以继续管理 Azure 门户和管理中心中的标签和策略。

## <a name="before-you-begin"></a>在开始之前

标签迁移具有很多优点，但不可逆，因此请确保你已了解以下更改和注意事项：

- 请确保你的[客户端支持统一标签](#clients-and-services-that-support-unified-labeling)，并且如有必要，在 Azure 门户（适用于不支持统一标签的客户端）和管理中心（对于支持统一标签的客户端）进行管理。

- 不会迁移策略，包括策略设置和谁有权访问策略（作用域内策略）以及所有高级客户端设置。 在标签迁移后配置这些设置的选项包括：
    - 用于敏感度标签的管理中心。
    - [Office 365 安全性和符合性 PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps)，你必须使用它来配置[高级客户端设置](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)。
    

- 管理中心并不支持已迁移标签中的所有设置。 使用[管理中心不支持的标签设置](#label-settings-that-are-not-supported-in-the-admin-centers)部分中的表，来帮助识别这些设置和建议的操作过程。

- 保护模板：
    
    - 使用基于云的密钥和为标签配置的一部分模板也随标签一同迁移。 不迁移其他保护模板。 
    
    - 如果你的标签已针对预定义的模板进行了配置，请编辑这些标签，并选择“设置权限”选项，配置模板中具有的相同保护设置。 具有预定义模板的标签不会阻止标签迁移，但管理中心不支持此标签配置。
        
        提示：为了帮助您重新配置这些标签，您可能会发现有两个浏览器窗口很有用：一个窗口，您可以在其中选择标签的 "**编辑模板**" 按钮以查看保护设置，另一个窗口用于在选择 "**设置权限**" 时配置相同的设置。
    
    - 迁移了包含基于云的保护设置的标签后，保护模板的结果范围是在 Azure 门户（或通过使用 AIPService PowerShell 模块）和管理中心定义的作用域中定义的作用域。 

- 对于每个标签，Azure 门户仅显示可编辑的标签显示名称。 用户将在其应用中看到此标签名称。 管理中心显示标签的显示名称和标签名称。 标签名称是首次创建标签时指定的初始名称，后端服务使用此属性进行标识。 迁移标签时，显示名称将保持不变，并且标签名称将重命名为 Azure 门户中的标签 ID。

- 不迁移标签的任何本地化字符串。 使用 Office 365 安全性和符合性 PowerShell 为已迁移标签定义新的本地化字符串，并为[集标签](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)定义*LocaleSettings*参数。

- 迁移之后，当你在 Azure 门户中编辑已迁移的标签时，相同的更改将会自动反映在管理中心。 但是，当你在某个管理中心内编辑已迁移的标签时，必须返回到 "Azure 门户， **Azure 信息保护-统一标签**" 窗格，然后选择 "**发布**"。 Azure 信息保护客户端（经典）需要此额外操作来选取标签更改。

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>管理中心不支持的标签设置

使用下表来确定已迁移的标签的哪些配置设置不受 Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 合规中心的支持。 如果你具有这些设置的标签，则迁移完成后，请先使用最终列中的管理指南，然后再将你的标签发布到一个被引用管理中心。

如果不确定如何配置标签，请在 Azure 门户中查看其设置。 如果需要有关此步骤的帮助，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

Azure 信息保护客户端（经典）可以使用列出的所有标签设置而不会出现任何问题，因为它们会继续从 Azure 门户下载标签。

|标签配置|受统一标记客户端的支持| 管理中心指南|
|-------------------|---------------------------------------------|-------------------------|
|启用或禁用状态<br /><br />此状态不同步到管理中心 |Not applicable|等效于是否发布标签。 |
|从列表中选择的标签颜色或使用 RGB 代码指定的标签颜色 |“是”|标签颜色没有配置选项。 相反，你可以在 Azure 门户中配置标签颜色，也可以使用[PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)。|
|使用预定义模板的基于云的保护或基于 HYOK 的保护 |否|预定义模板没有配置选项。 我们不建议使用此配置发布标签。|
|使用 Word、Excel 和 PowerPoint 的用户定义权限的基于云的保护 |“是”|管理中心现在具有用户定义的权限的配置选项。 <br /><br /> 如果使用此配置发布标签，请查看[下表](#comparing-the-behavior-of-protection-settings-for-a-label)中应用标签的结果。|
|使用 Outlook（不可转发）中用户定义权限的基于 HYOK 的保护 |否|HYOK 没有配置选项。 我们不建议使用此配置发布标签。 否则，请在[下表](#comparing-the-behavior-of-protection-settings-for-a-label)中查看应用此标签所带来的后果。|
|删除保护 |否|没有用于删除保护的配置选项。 我们不建议使用此配置发布标签。<br /><br /> 如果使用此配置发布标签，则在应用该标签时，始终会删除保护，无论是通过标签还是独立于标签对保护进行保护。|
|任何经过身份验证的用户保护设置 |“是”|没有用于选择此保护设置的配置选项。 如果此设置已迁移或在 Azure 门户中进行配置，请使用此配置发布标签。|
|为视觉标记（页眉、页脚、水印）使用 RGB 代码自定义字体和字体颜色|“是”|视觉标记的配置限制为颜色和字体大小列表。 尽管无法看见管理中心中配置的值，仍可以不做任何更改发布此标签。 <br /><br />若要更改这些选项，可以使用 Azure 门户。 但是，请考虑将颜色更改为管理中心中列出的选项之一，以便于管理。|
|视觉标记（页眉、页脚）中的变量|否|如果不做更改就发布此标签，则变量将在客户端上显示为文本而不是显示动态值。 发布标签之前，请编辑字符串以删除变量。|
|每个应用的视觉标记|否|如果不做更改就发布此标签，则在所有应用中应用变量将在客户端上显示为文本，而不是在所选的应用上显示文本字符串。 仅当适用于所有应用时发布此标签，并编辑字符串以删除应用变量。|
|条件和关联设置 <br /><br /> 包括自动和建议标签及其工具提示|Not applicable|若要重新配置条件，请将自动标记用作标签设置中的独立配置。|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>比较标签保护设置的行为

使用下表来确定标签的相同保护设置的行为方式不同，具体取决于 Azure 信息保护客户端（经典）、Azure 信息保护统一标签客户端还是 Office 应用使用它内置标签的（也称为 "本机办公室标签"）。 标签行为的差异可能会改变您决定是否发布标签，特别是在您的组织中有混合的客户端时。

如果你不确定保护设置的配置方式，请在 "**保护**" 窗格的 "Azure 门户中查看其设置。 如果需要有关此步骤的帮助，请参阅[配置保护设置标签](configure-policy-protection.md#to-configure-a-label-for-protection-settings)。

下表未列出具有相同行为的保护设置，以下情形例外：
- 使用具有内置标签的 Office 应用时，除非还安装了 Azure 信息保护统一标签客户端，否则标签在文件资源管理器中不可见。
- 使用具有内置标签的 Office 应用时，如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)。

|标签的保护设置 |Azure 信息保护客户端（经典版） |Azure 信息保护统一标识客户端| 具有内置标签的 Office 应用
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|Azure（云密钥），其中用户定义的权限适用于 Word、Excel、PowerPoint 和文件资源管理器：| 可在 Word、Excel、PowerPoint 和文件资源管理器中查看 <br /><br /> 当应用标签时：<br /><br /> - 提示用户获取自定义权限，这些权限之后通过云端密钥作为保护措施加以应用| 可在 Word、Excel、PowerPoint 和文件资源管理器中查看 <br /><br /> 当应用标签时：<br /><br /> - 提示用户获取自定义权限，这些权限之后通过云端密钥作为保护措施加以应用|可在 Word、Excel、PowerPoint 和 Outlook 中查看： <br /><br /> 当应用标签时：<br /><br /> - 不提示用户获取自定义权限且不应用保护 <br /><br /> - 如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)|
|带有模板的 HYOK (AD RMS)：| 可在 Word、Excel、PowerPoint、Outlook 和文件资源管理器中查看<br /><br /> 当应用此标签时： <br /><br />- 对文档和电子邮件应用 HYOK 保护 | 可在 Word、Excel、PowerPoint、Outlook 和文件资源管理器中查看  <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前通过标签应用了保护，则去除保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 |可在 Word、Excel、PowerPoint 和 Outlook 中查看 <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前通过标签应用了保护，则去除保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1) |
|HYOK (AD RMS)，其中用户定义的权限适用于 Word、Excel、PowerPoint 和文件资源管理器：| 可在 Word、Excel、PowerPoint 和文件资源管理器中查看<br /><br /> 当应用此标签时：<br /><br /> - 对文档和电子邮件应用 HYOK 保护| 可在 Word、Excel 和 PowerPoint 中查看 <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护|可在 Word、Excel 和 PowerPoint 中查看 <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 |
|HYOK (AD RMS)，其中用户定义的权限适用于 Outlook：|可在 Outlook 中查看<br /><br />当应用此标签时：<br /><br />- 通过 HYOK 保护向电子邮件应用“请勿转发”规则|可在 Outlook 中查看<br /><br />当应用此标签时：<br /><br /> - 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护|可在 Outlook 中查看<br /><br />当应用此标签时：<br /><br />- 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)|

###### <a name="footnote-1"></a>脚注 1

在 Outlook 中，保护已保留，但有一个例外：在使用 "仅加密" 选项保护电子邮件时，将删除该保护。


###### <a name="footnote-2"></a>脚注 2

如果用户具有支持此操作的使用权限或角色，则去掉保护：
- [使用权限](configure-usage-rights.md#usage-rights-and-descriptions) - 导出或完全控制。
- [权限管理颁发者/权限管理所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)角色或者[超级用户](configure-super-users.md)。

如果用户没有上述任一使用权限或角色，则不应用标签且保留原始保护。


## <a name="to-migrate-azure-information-protection-labels"></a>若要迁移 Azure 信息保护标签

使用以下说明将租户和 Azure 信息保护标签迁移到使用统一标签存储。

必须是符合性管理员、合规性数据管理员、安全管理员或全局管理员才能迁移标签。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”窗格。
    
    例如，在 "资源"、"服务" 和 "文档" 的 "搜索" 框中，开始键入**信息**并选择 " **Azure 信息保护**"。

2. 从 "**管理**" 菜单选项中，选择 "**统一标签**"。

3. 在 " **Azure 信息保护-统一标签**" 窗格中，选择 "**激活**"，并按照联机说明进行操作。
    
    如果激活选项不可用，请检查**统一标签状态**：如果你看到 "已**激活**"，则你的租户已在使用统一标签存储，并且无需迁移标签。

成功迁移的标签现在可被[支持统一标签的客户端和服务](#clients-and-services-that-support-unified-labeling)使用。 但是，必须先将[这些标签发布](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)到某个管理中心： Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 365 符合性中心。

> [!IMPORTANT]
> 如果在 Azure 门户之外编辑标签，请针对 Azure 信息保护客户端（经典），返回到 " **Azure 信息保护-统一标签**" 窗格，然后选择 "**发布**"。

### <a name="copy-policies"></a>复制策略

> [!NOTE]
> 此选项处于预览阶段，可能会发生更改。

迁移标签后，可以选择用于复制策略的选项。 如果选择此选项，策略的一次性副本及其[策略设置](configure-policy-settings.md)和任何[高级客户端设置](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings)将发送到管理标签的管理中心： Office 365 安全与合规中心、Microsoft 365 安全中心、Microsoft 365 符合性中心。 

已成功复制策略及其设置和标签之后，会自动将其发布到分配到 Azure 门户中的策略的用户和组。 请注意，对于全局策略，这意味着所有用户。 如果尚未准备好在要发布的复制策略中迁移的标签，则在复制策略后，你可以从管理员标签中心中的标签策略删除标签。

在 " **Azure 信息保护-统一标签**" 窗格中选择 "**复制策略（预览）** " 选项之前，请注意以下事项：

- 在为租户激活统一标签之前，"**复制策略（预览版）** " 选项不可用。

- 你无法有选择地选择要复制的策略和设置。 所有策略（**全局**策略和所有作用域内策略）会自动选择进行复制，并且会复制所有受支持的作为标签策略设置的设置。 如果已具有同名的标签策略，则会使用 Azure 门户中的策略设置来覆盖它。

- 不会复制某些高级客户端设置，因为对于 Azure 信息保护统一标签客户端，这些设置支持作为*标签高级设置*，而不是策略设置。 可以通过[Office 365 安全与合规中心 PowerShell](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)配置这些标签高级设置。 未复制的高级客户端设置：
    - [LabelbyCustomProperty](./rms-client/client-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [LabelToSMIME](./rms-client/client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- 不同于标签迁移（对标签的后续更改进行同步），"**复制策略**" 操作不会同步任何对策略或策略设置的后续更改。 在 Azure 门户中进行更改后，你可以重复 "复制策略" 操作，并且将再次覆盖任何现有策略及其设置。 或者，将 LabelPolicy 或设置标签 cmdlet 与 Office 365 安全与合规中心 PowerShell 中的*AdvancedSettings*参数一起使用。

- 复制**策略**操作在复制每个策略之前验证以下各项：
    
    - 分配给策略的用户和组目前处于 Azure AD。 如果缺少一个或多个帐户，则不会复制此策略。 不检查组成员身份。
    
    - 全局策略包含至少一个标签。 由于管理员标签中心不支持不带标签的标签策略，因此不会复制不带标签的全局策略。

- 如果复制策略，然后将其从管理标签中心删除，请在使用 "**复制策略**" 操作之前至少等待两个小时，以确保有足够的时间来复制删除。

有关为 Azure 信息保护统一标签客户端配置策略设置、高级客户端设置和标签设置的详细信息，请参阅管理员指南中[的 Azure 信息保护统一标签客户端的自定义配置](./rms-client/clientv2-admin-guide-customizations.md)。

### <a name="clients-and-services-that-support-unified-labeling"></a>支持统一标签的客户端和服务

若要确认你使用的客户端和服务是否支持统一标签，请参阅其文档，以检查它们是否可以使用从一个管理中心发布的敏感度标签： Office 365 安全与合规中心、Microsoft 365安全中心或 Microsoft 365 相容性中心。 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>当前支持统一标签的客户端包括：

- [适用于 Windows 的 Azure 信息保护统一标签客户端](./rms-client/unifiedlabelingclient-version-release-history.md)。 有关此客户端与 Azure 信息保护客户端（经典）的比较，请参阅[比较 Windows 计算机的标记客户端](./rms-client/use-client.md#compare-the-labeling-clients-for-windows-computers)。

- Office 中处于不同可用性阶段的应用。 有关详细信息，请参阅 Office 文档[中的在应用中支持敏感度标签功能](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)。
    
- 来自软件供应商和开发人员且使用 [Microsoft 信息保护 SDK](https://docs.microsoft.com/information-protection/develop/overview) 的应用。

##### <a name="services-that-currently-support-unified-labeling-include"></a>当前支持统一标签的服务包括：

- [Power BI （预览版）](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview)

- Office Online （预览中）和 Outlook 网页

- SharePoint Online、OneDrive for business、Microsoft 团队和 Office 365 组（预览版）
    
    有关详细信息，请参阅[将敏感度标签与 Microsoft 团队、Office 365 组和 sharepoint 网站（公共预览版）配合使用](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-teams-groups-sites)和[在 SharePoint 和 OneDrive 中启用 Office 文件的敏感性标签（公共预览版）](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)。

- Microsoft Defender 高级威胁防护

- Microsoft Cloud App Security
    
    此服务使用以下逻辑支持迁移到统一标签存储之前及之后的标签：
    
    - 如果管理中心的标签与 Azure 门户中的相同，则将从管理中心检索统一标签。 若要在 Cloud App Security 中选择这些标签，至少一个标签必须发布到至少一个用户。
    
    - 如果管理中心的标签与 Azure 门户中的不同，则不会从管理中心使用统一标签，而是从 Azure 门户检索标签。

- 来自软件供应商和开发人员且使用 [Microsoft 信息保护 SDK](https://docs.microsoft.com/information-protection/develop/overview) 的服务。

## <a name="next-steps"></a>后续步骤

有关我们的客户体验团队的其他指导和技巧，请参阅以下资源：

- 博客文章：[了解统一标签迁移](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Understanding-Unified-Labeling-migration/ba-p/783185)

- 网络研讨会： [AIP 统一标记网络研讨会记录](https://aka.ms/AIP-UL-Webinar-Join1)

若要详细了解现在可以在一个标签管理中心内配置和发布的标签，请参阅[敏感度标签概述](/microsoft-365/compliance/sensitivity-labels)和[创建和配置敏感度标签及其策略](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels)。

如果尚未这样做，请安装 Azure 信息保护统一标签客户端。 有关发布信息、管理员指南和用户指南，请参阅适用[于 Windows 的 Azure 信息保护统一标签客户端](./rms-client/aip-clientv2.md)。
