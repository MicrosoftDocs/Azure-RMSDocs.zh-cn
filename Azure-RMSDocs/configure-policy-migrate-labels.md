---
title: 将 Azure 信息保护标签迁移到 Office 365 - AIP
description: 为支持统一标签的客户端和服务将 Azure 信息保护标签迁移到 Office 365 敏感度标签。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: labelmigrate
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4a00d85ea5669a5a81a7380796888edff939e310
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68791751"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-office-365-sensitivity-labels"></a>如何将 Azure 信息保护标签迁移到 Office 365 敏感度标签

>适用对象：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

在 Azure 信息保护中迁移标签, 以便可以将它们用作支持统一标签的[客户端和服务](#clients-and-services-that-support-unified-labeling)的敏感度标签。

然后, Azure 信息保护统一标签客户端可以使用这些标签。 如果继续使用 Azure 信息保护客户端 (经典), 此客户端将继续使用 Azure 门户中的 Azure 信息保护策略下载标签。

在阅读迁移标签说明之前, 你可能会发现以下常见问题很有用:

- [Azure 信息保护中的标签与 Office 365 中的标签之间有何区别？](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [何时将我的标签迁移到 Office 365？](faqs.md#when-is-the-right-time-to-migrate-my-labels-to-office-365)

- [迁移我的标签后，该使用哪个管理门户？](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>支持统一标签平台的管理角色

如果你在组织中使用管理员角色来委派管理, 则可能需要对统一标签平台进行一些更改:

统一标签平台不支持**Azure 信息保护管理员**(以前称为**信息保护管理员**) 的[Azure AD 角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)。 如果在组织中使用此管理角色, 请将具有此角色的用户添加到**符合性管理员**、**符合性数据管理员**或**安全管理员**的 Azure AD 角色中。 如果需要有关此步骤的帮助，请参阅[向用户授予对 Office 365 安全与合规中心的访问权限](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center)。 另外，还可以在 Azure AD 门户、Microsoft 365 安全中心和 Microsoft 365 合规中心分配这些角色。

或者，若要使用角色，可以在管理中心为这些用户创建新角色组，然后向该组中添加“敏感度标签管理员”或“组织配置”角色。

如果未使用其中一个配置向这些用户授予对管理中心的访问权限，则在迁移标签后将无法在 Azure 门户中配置 Azure 信息保护。

迁移标签后，租户的全局管理员可以继续管理 Azure 门户和管理中心中的标签和策略。

## <a name="before-you-begin"></a>在开始之前

标签迁移具有很多优点, 但不可逆, 因此请确保你已了解以下更改和注意事项:

- 请确保你的[客户端支持统一标签](#clients-and-services-that-support-unified-labeling), 并且如有必要, 在 Azure 门户 (适用于不支持统一标签的客户端) 和管理中心 (对于支持统一标签的客户端) 进行管理。

- 不会迁移策略，包括策略设置和谁有权访问策略（作用域内策略）以及所有高级客户端设置。 在标签迁移后配置这些设置的选项包括:
    - 用于敏感度标签的管理中心。
    - [Office 365 安全性和符合性 PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps), 你必须使用它来配置[高级客户端设置](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)。
    

- 管理中心并不支持已迁移标签中的所有设置。 使用[管理中心不支持的标签设置](#label-settings-that-are-not-supported-in-the-admin-centers)部分中的表，来帮助识别这些设置和建议的操作过程。

- 保护模板：
    
    - 使用基于云的密钥和为标签配置的一部分模板也随标签一同迁移。 不迁移其他保护模板。 
    
    - 如果你的标签已针对预定义的模板进行了配置，请编辑这些标签，并选择“设置权限”选项，配置模板中具有的相同保护设置。 具有预定义模板的标签不会阻止标签迁移，但管理中心不支持此标签配置。
        
        提示：在重新配置这些标签的过程中，你可能发现用两个浏览器窗口很有用：在一个窗口中为标签选择“编辑模板”按钮，查看保护设置；在另一个窗口中配置在选择“设置权限”时使用的相同设置。
    
    - 迁移了包含基于云的保护设置的标签后, 保护模板的结果范围是在 Azure 门户 (或通过使用 AIPService PowerShell 模块) 和管理中心定义的作用域中定义的作用域。 

- 对于每个标签，Azure 门户仅显示可编辑的标签显示名称。 用户将在其应用中看到此标签名称。 管理中心显示标签的显示名称和标签名称。 标签名称是首次创建标签时指定的初始名称, 后端服务使用此属性进行标识。 迁移标签时, 显示名称将保持不变, 并且标签名称将重命名为 Azure 门户中的标签 ID。

- 不迁移标签的任何本地化字符串。 使用 Office 365 安全性和符合性 PowerShell 为已迁移标签定义新的本地化字符串, 并为[集标签](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)定义*LocaleSettings*参数。

- 迁移之后，当你在 Azure 门户中编辑已迁移的标签时，相同的更改将会自动反映在管理中心。 但是，当在其中一个管理中心编辑已迁移的标签时，必须返回到 Azure 门户的“Azure 信息保护 - 统一标签”边栏选项卡，并选择“发布”。 Azure 信息保护客户端 (经典) 需要此额外操作来选取标签更改。

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>管理中心不支持的标签设置

使用下表来确定已迁移的标签的哪些配置设置不受 Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 合规中心的支持。 如果你具有这些设置的标签, 则迁移完成后, 请先使用最终列中的管理指南, 然后再将你的标签发布到一个被引用管理中心。

如果不确定如何配置标签，请在 Azure 门户中查看其设置。 如果需要有关此步骤的帮助，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

Azure 信息保护客户端 (经典) 可以使用列出的所有标签设置而不会出现任何问题, 因为它们会继续从 Azure 门户下载标签。

|标签配置|受统一标记客户端的支持| 管理中心指南|
|-------------------|---------------------------------------------|-------------------------|
|启用或禁用状态<br /><br />此状态不同步到管理中心 |“不适用”|等效于是否发布标签。 |
|从列表中选择的标签颜色或使用 RGB 代码指定的标签颜色 |是|标签颜色没有配置选项。 相反, 你可以在 Azure 门户中配置标签颜色, 也可以使用[PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)。|
|使用预定义模板的基于云的保护或基于 HYOK 的保护 |否|预定义模板没有配置选项。 我们不建议使用此配置发布标签。|
|使用 Word、Excel 和 PowerPoint 的用户定义权限的基于云的保护 |是|对于这些 Office 应用, 管理中心没有用户定义的权限的配置选项。 但是, 如果您使用此配置迁移标签, 或者使用 Azure 门户在迁移之后配置标签, 则支持此设置。 <br /><br /> 如果使用此配置发布标签, 请查看[下表](#comparing-the-behavior-of-protection-settings-for-a-label)中应用标签的结果。|
|使用 Outlook（不可转发）中用户定义权限的基于 HYOK 的保护 |否|HYOK 没有配置选项。 我们不建议使用此配置发布标签。 否则，请在[下表](#comparing-the-behavior-of-protection-settings-for-a-label)中查看应用此标签所带来的后果。|
|删除保护 |否|没有用于删除保护的配置选项。 我们不建议使用此配置发布标签。<br /><br /> 如果使用此配置发布标签, 则在应用该标签时, 如果该标签之前已由标签应用, 则会将其删除。 如果之前从标签中独立应用了保护，则将保留保护。|
|为视觉标记（页眉、页脚、水印）使用 RGB 代码自定义字体和字体颜色|是|视觉标记的配置限制为颜色和字体大小列表。 尽管无法看见管理中心中配置的值，仍可以不做任何更改发布此标签。 <br /><br />若要更改这些选项，可以使用 Azure 门户。 但是，请考虑将颜色更改为管理中心中列出的选项之一，以便于管理。|
|视觉标记（页眉、页脚）中的变量|否|如果不做更改就发布此标签，则变量将在客户端上显示为文本而不是显示动态值。 发布标签之前，请编辑字符串以删除变量。|
|每个应用的视觉标记|否|如果不做更改就发布此标签，则在所有应用中应用变量将在客户端上显示为文本，而不是在所选的应用上显示文本字符串。 仅当适用于所有应用时发布此标签，并编辑字符串以删除应用变量。|
|条件和关联设置 <br /><br /> 包括自动和建议标签及其工具提示|“不适用”|若要重新配置条件，请将自动标记用作标签设置中的独立配置。|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>比较标签保护设置的行为

使用下表来确定标签的相同保护设置的行为方式不同, 具体取决于 Azure 信息保护客户端 (经典)、Azure 信息保护统一标签客户端还是 Office 应用使用它内置标签的 (也称为 "本机办公室标签")。 标签行为的差异可能会改变您决定是否发布标签, 特别是在您的组织中有混合的客户端时。

如果不确定如何配置保护设置，请在 Azure 门户中的“保护”边栏选项卡上查看其设置。 如果需要有关此步骤的帮助，请参阅[配置保护设置标签](configure-policy-protection.md#to-configure-a-label-for-protection-settings)。

下表未列出具有相同行为的保护设置，以下情形例外：
- 使用具有内置标签的 Office 应用时，除非还安装了 Azure 信息保护统一标签客户端，否则标签在文件资源管理器中不可见。
- 使用具有内置标签的 Office 应用时，如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)。

|标签的保护设置 |Azure 信息保护客户端 (经典) |Azure 信息保护统一标识客户端| 具有内置标签的 Office 应用
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|Azure（云密钥），其中用户定义的权限适用于 Word、Excel、PowerPoint 和文件资源管理器：| 可在 Word、Excel、PowerPoint 和文件资源管理器中查看 <br /><br /> 当应用标签时：<br /><br /> - 提示用户获取自定义权限，这些权限之后通过云端密钥作为保护措施加以应用| 可在 Word、Excel、PowerPoint 和文件资源管理器中查看 <br /><br /> 当应用标签时：<br /><br /> - 提示用户获取自定义权限，这些权限之后通过云端密钥作为保护措施加以应用|可在 Word、Excel、PowerPoint 和 Outlook 中查看： <br /><br /> 当应用标签时：<br /><br /> - 不提示用户获取自定义权限且不应用保护 <br /><br /> - 如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)|
|带有模板的 HYOK (AD RMS)：| 可在 Word、Excel、PowerPoint、Outlook 和文件资源管理器中查看<br /><br /> 当应用此标签时： <br /><br />- 对文档和电子邮件应用 HYOK 保护 | 可在 Word、Excel、PowerPoint、Outlook 和文件资源管理器中查看  <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前通过标签应用了保护，则去除保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 |可在 Word、Excel、PowerPoint 和 Outlook 中查看 <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前通过标签应用了保护，则去除保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1) |
|HYOK (AD RMS)，其中用户定义的权限适用于 Word、Excel、PowerPoint 和文件资源管理器：| 可在 Word、Excel、PowerPoint 和文件资源管理器中查看<br /><br /> 当应用此标签时：<br /><br /> - 对文档和电子邮件应用 HYOK 保护| 可在 Word、Excel 和 PowerPoint 中查看 <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护|可在 Word、Excel 和 PowerPoint 中查看 <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 |
|HYOK (AD RMS)，其中用户定义的权限适用于 Outlook：|可在 Outlook 中查看<br /><br />当应用此标签时：<br /><br />- 通过 HYOK 保护向电子邮件应用“请勿转发”规则|可在 Outlook 中查看<br /><br />当应用此标签时：<br /><br /> - 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护|可在 Outlook 中查看<br /><br />当应用此标签时：<br /><br />- 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)|

###### <a name="footnote-1"></a>脚注 1

在 Outlook for Mac 中保留保护，但以下情形除外：如果已通过“仅加密”选项保护电子邮件，则去掉保护。


###### <a name="footnote-2"></a>脚注 2

如果用户具有支持此操作的使用权限或角色，则去掉保护：
- [使用权限](configure-usage-rights.md#usage-rights-and-descriptions) - 导出或完全控制。
- [权限管理颁发者/权限管理所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)角色或者[超级用户](configure-super-users.md)。

如果用户没有上述任一使用权限或角色，则不应用标签且保留原始保护。


## <a name="to-migrate-azure-information-protection-labels"></a>若要迁移 Azure 信息保护标签

请使用以下说明迁移租户和 Azure 信息保护标签，来使用新的统一标记存储。

必须是符合性管理员、合规性数据管理员、安全管理员或全局管理员才能迁移标签。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从 "**管理**" 菜单选项中, 选择 "**统一标签**"。

3. 在“Azure 信息保护 - 统一标签”边栏选项卡上，选择“激活”并按照联机说明进行操作。
    
    如果用于激活的选项不可用，请检查“统一标记状态”：如果看到“已激活”，表明租户已在使用统一标记存储，且无需迁移标签。

成功迁移的标签现在可被[支持统一标签的客户端和服务](#clients-and-services-that-support-unified-labeling)使用。 但必须先在以下其中一个管理中心发布这些标签：Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 365 合规中心。

> [!IMPORTANT]
> 如果在 Azure 门户之外编辑标签, 则对于 Azure 信息保护客户端 (经典), 返回到 " **Azure 信息保护-统一标签**" 边栏选项卡, 然后选择 "**发布**"。

### <a name="clients-and-services-that-support-unified-labeling"></a>支持统一标签的客户端和服务

若要确认使用的客户端和服务是否支持统一标签，请参阅其文档以查看它们是否可以使用以下其中一个管理中心发布的敏感度标签：Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 365 合规中心。 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>当前支持统一标签的客户端包括：

- [适用于 Windows 的 Azure 信息保护统一标签客户端](./rms-client/unifiedlabelingclient-version-release-history.md)。 有关此客户端与 Azure 信息保护客户端 (经典) 的比较, 请参阅[比较客户端](./rms-client/use-client.md#compare-the-clients)。

- Office 中处于不同可用性阶段的应用。 有关详细信息，请参阅 Office 文档中的[将敏感标签应用于 Office 中的文档和电子邮件](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9)中的**现在可从何处获取功能？** 。
    
- 来自软件供应商和开发人员且使用 [Microsoft 信息保护 SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview) 的应用。

##### <a name="services-that-currently-support-unified-labeling-include"></a>当前支持统一标签的服务包括：

- Microsoft Defender 高级威胁防护

- Microsoft Cloud App Security
    
    此服务使用以下逻辑支持迁移到统一标签存储之前及之后的标签：
    
    - 如果管理中心具有的标签与 Azure 门户中的标签相同：从管理中心检索统一标签。 若要在 Cloud App Security 中选择这些标签，至少一个标签必须发布到至少一个用户。
    
    - 如果管理中心具有的标签与 Azure 门户中的标签不同：管理中心不使用统一标签，而是从 Azure 门户检索标签。

- 来自软件供应商和开发人员且使用 [Microsoft 信息保护 SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview) 的服务。

## <a name="next-steps"></a>后续步骤

有关我们的客户体验团队的其他指导和技巧, 请参阅以下博客文章:[了解统一标签迁移](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Understanding-Unified-Labeling-migration/ba-p/783185)。

有关现在可以配置并在其中一个管理中心发布的已迁移标签的详细信息，请参阅[敏感度标签的概述](/Office365/SecurityCompliance/sensitivity-labels)。

如果尚未这样做, 请安装 Azure 信息保护统一标签客户端。 有关发布信息、管理员指南和用户指南, 请参阅适用[于 Windows 的 Azure 信息保护统一标签客户端](./rms-client/aip-clientv2.md)。
