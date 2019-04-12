---
title: 将 Azure 信息保护标签迁移到 Office 365 - AIP
description: 为支持统一标签的客户端和服务将 Azure 信息保护标签迁移到 Office 365 敏感度标签。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/09/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 0cc09e58d49fe9515de0109c726af08e12937dd1
ms.sourcegitcommit: 729b12e1219c6dbf1bb2a6cfa7239f24d1d13cc5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59364566"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-office-365-sensitivity-labels"></a>如何将 Azure 信息保护标签迁移到 Office 365 敏感度标签

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

> [!IMPORTANT]
> 此功能处于预览状态，并且将租户迁移到新平台。 迁移不可撤消。 新平台支持统一标签，因此你创建和管理的标签可以由支持 [Microsoft 信息保护解决方案](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)的客户端和服务使用。

如果想要将标签作为 Office 365 敏感度标签使用，请迁移标签，并由[支持统一标签的客户端和服务](#clients-and-services-that-support-unified-labeling)使用。 管理和发布 Office 365 安全与合规中心或 Microsoft 365 安全中心以及 Microsoft 365 合规中心中的这些标签。 迁移完成后，Azure 信息保护客户端将继续从 Azure 门户下载带有其 Azure 信息保护策略的标签。 

在阅读有关如何迁移标签的详细说明之前，你可能会发现以下常见问题非常有用：

- [Azure 信息保护中的标签与 Office 365 中的标签之间有何区别？](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [何时将我的标签迁移到 Office 365？](faqs.md#when-is-the-right-time-to-migrate-my-labels-to-office-365)

- [迁移我的标签后，该使用哪个管理门户？](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="important-information-about-administrative-roles"></a>有关管理角色的重要信息

统一标记平台不支持 [Azure AD 角色“](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)信息保护管理员”。 如果在迁移标签之前在组织中使用此管理角色，请将具有此角色的用户添加到 Azure AD 角色“安全管理员”或“合规性管理员”。 如果需要有关此步骤的帮助，请参阅[向用户授予对 Office 365 安全与合规中心的访问权限](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center)。 另外，还可以在 Azure AD 门户、Microsoft 365 安全中心和 Microsoft 365 合规中心分配这些角色。

或者，若要使用角色，可以在管理中心为这些用户创建新角色组，然后向该组中添加“敏感度标签管理员”或“组织配置”角色。

如果未使用其中一个配置向这些用户授予对管理中心的访问权限，则在迁移标签后将无法在 Azure 门户中配置 Azure 信息保护。

迁移标签后，租户的全局管理员可以继续管理 Azure 门户和管理中心中的标签和策略。


## <a name="considerations-for-unified-labels"></a>统一标签注意事项

在迁移标签之前，请确保了解以下更改和注意事项：

- 并非所有客户端目前都支持统一标签。 请确保你拥有[支持的客户端](#clients-and-services-that-support-unified-labeling)并准备好在 Azure 门户（适用于不支持统一标签的客户端）和管理中心（适用于支持统一标签的客户端）进行管理。

- 如果你正在定义和配置你想要使用的标签，建议使用 Azure 门户来完成此过程，然后迁移标签。 此策略可以避免在迁移过程中重复标签，然后需要在管理中心进行编辑。

- 不会迁移策略，包括策略设置和谁有权访问策略（作用域内策略）以及所有高级客户端设置。 对于这些不会迁移的更改，需要在迁移标签后在管理中心配置相关选项。
    
    为了获得更一致的用户体验，建议在管理中心的相同范围内发布相同标签。

- 管理中心并不支持已迁移标签中的所有设置。 使用[管理中心不支持的标签设置](#label-settings-that-are-not-supported-in-the-admin-centers)部分中的表，来帮助识别这些设置和建议的操作过程。

- 保护模板：
    
    - 使用基于云的密钥和为标签配置的一部分模板也随标签一同迁移。 不迁移其他保护模板。 
    
    - 如果你的标签已针对预定义的模板进行了配置，请编辑这些标签，并选择“设置权限”选项，配置模板中具有的相同保护设置。 具有预定义模板的标签不会阻止标签迁移，但管理中心不支持此标签配置。
        
        提示：在重新配置这些标签的过程中，你可能发现用两个浏览器窗口很有用：在一个窗口中为标签选择“编辑模板”按钮，查看保护设置；在另一个窗口中配置在选择“设置权限”时使用的相同设置。
    
    - 迁移具有基于云保护设置的标签之后，生成的保护模板范围是在 Azure 门户中定义的范围（或通过使用 AADRM PowerShell 模块），以及在管理中心定义的范围。 

- 迁移标签时，将看到迁移结果显示标签是否创建、更新，或因重复而重命名：

    - 创建标签时，必须在其中一个管理中心发布，以将其提供给应用程序和服务。
    
    - 重命名标签时，必须对其进行编辑，可以在其中一个管理中心或 Azure 门户执行此操作。 

- 对于每个标签，Azure 门户仅显示可编辑的标签显示名称。 管理中心显示标签的显示名称和标签名称。 标签名称是在首次创建标签时指定的初始名称，此属性由后端服务用于标识目的。

- 不迁移标签的任何本地化字符串。 必须在管理中心为已迁移的标签定义新的本地化字符串。

- 迁移之后，当你在 Azure 门户中编辑已迁移的标签时，相同的更改将会自动反映在管理中心。 但是，当在其中一个管理中心编辑已迁移的标签时，必须返回到 Azure 门户的“Azure 信息保护 - 统一标签”边栏选项卡，并选择“发布”。 Azure 信息保护客户端需要通过此附加操作来获取标签更改。

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>管理中心不支持的标签设置

使用下表来确定已迁移的标签的哪些配置设置不受 Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 合规中心的支持。 如果有使用这些设置的标签，迁移完成时，请在其中一个管理中心发布标签前使用最后一列中的管理员指南。

如果不确定如何配置标签，请在 Azure 门户中查看其设置。 如果需要有关此步骤的帮助，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

Azure 信息保护客户端可以使用列出的所有标签设置，而不会出现任何问题，因为它们继续从 Azure 门户下载标签。

|标签配置|受统一标记客户端的支持| 管理中心指南|
|-------------------|---------------------------------------------|-------------------------|
|启用或禁用状态<br /><br />注意：不会同步到管理中心 |“不适用”|等效于是否发布标签。 |
|从列表中选择的标签颜色或使用 RGB 代码指定的标签颜色 |是|标签颜色没有配置选项。 相反，可以在 Azure 门户中配置标签颜色。|
|使用预定义模板的基于云的保护或基于 HYOK 的保护 |否|预定义模板没有配置选项。 我们不建议使用此配置发布标签。|
|使用 Word、Excel 和 PowerPoint 的用户定义权限的基于云的保护 |否|这些 Office 应用的用户定义权限没有配置选项。 我们不建议使用此配置发布标签。 否则，请在[下表](#comparing-the-behavior-of-protection-settings-for-a-label)中查看应用此标签所带来的后果。|
|使用 Outlook（不可转发）中用户定义权限的基于 HYOK 的保护 |否|HYOK 没有配置选项。 我们不建议使用此配置发布标签。 否则，请在[下表](#comparing-the-behavior-of-protection-settings-for-a-label)中查看应用此标签所带来的后果。|
|删除保护 |否|没有用于删除保护的配置选项。 我们不建议使用此配置发布标签。<br /><br /> 如果确实发布了此标签，如果标签之前应用了保护，则应用该标签时，将删除保护。 如果之前从标签中独立应用了保护，则将保留保护。|
|为视觉标记（页眉、页脚、水印）使用 RGB 代码自定义字体和字体颜色|是|视觉标记的配置限制为颜色和字体大小列表。 尽管无法看见管理中心中配置的值，仍可以不做任何更改发布此标签。 <br /><br />若要更改这些选项，可以使用 Azure 门户。 但是，请考虑将颜色更改为管理中心中列出的选项之一，以便于管理。|
|视觉标记（页眉、页脚）中的变量|否|如果不做更改就发布此标签，则变量将在客户端上显示为文本而不是显示动态值。 发布标签之前，请编辑字符串以删除变量。|
|每个应用的视觉标记|否|如果不做更改就发布此标签，则在所有应用中应用变量将在客户端上显示为文本，而不是在所选的应用上显示文本字符串。 仅当适用于所有应用时发布此标签，并编辑字符串以删除应用变量。|
|条件和关联设置 <br /><br />注意：包括自动和建议标签及其工具提示|“不适用”|若要重新配置条件，请将自动标记用作标签设置中的独立配置。|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>比较标签保护设置的行为

使用下表来确定标签的同一保护设置如何表现出不同的行为，这些行为具体取决于使用标签的是 Azure 信息保护客户端（正式发布版或当前预览版）、Azure 信息保护统一标签客户端的当前预览版，还是内置有标签（也称为“本机 Office 标签”）的 Office 应用。

如果不确定如何配置保护设置，请在 Azure 门户中的“保护”边栏选项卡上查看其设置。 如果需要有关此步骤的帮助，请参阅[配置保护设置标签](configure-policy-protection.md#to-configure-a-label-for-protection-settings)。

下表未列出具有相同行为的保护设置，以下情形例外：
- 使用具有内置标签的 Office 应用时，除非还安装了 Azure 信息保护统一标签客户端，否则标签在文件资源管理器中不可见。
- 使用具有内置标签的 Office 应用时，如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)。

|标签的保护设置 |Azure 信息保护客户端|Azure 信息保护统一标识客户端| 具有内置标签的 Office 应用
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|Azure（云密钥），其中用户定义的权限适用于 Word、Excel、PowerPoint 和文件资源管理器：| 可在 Word、Excel、PowerPoint 和文件资源管理器中查看 <br /><br /> 当应用标签时：<br /><br /> - 提示用户获取自定义权限，这些权限之后通过云端密钥作为保护措施加以应用| 不可见 |可在 Word、Excel、PowerPoint 和 Outlook 中查看： <br /><br /> 当应用标签时：<br /><br /> - 不提示用户获取自定义权限且不应用保护 <br /><br /> - 如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)|
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

你必须是全局管理员才能迁移标记。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“管理”菜单选项，选择“统一标记(预览)”。

3. 在“Azure 信息保护 - 统一标签”边栏选项卡上，选择“激活”并按照联机说明进行操作。
    
    如果用于激活的选项不可用，请检查“统一标记状态”：如果看到“已激活”，表明租户已在使用统一标记存储，且无需迁移标签。

成功迁移的标签现在可被[支持统一标签的客户端和服务](#clients-and-services-that-support-unified-labeling)使用。 但必须先在以下其中一个管理中心发布这些标签：Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 365 合规中心。

> [!IMPORTANT]
> 在 Azure 信息保护客户端的 Azure 门户外部编辑标签时，请返回该“Azure 信息保护 - 统一标记”边栏选项卡，并选择“发布”。

### <a name="clients-and-services-that-support-unified-labeling"></a>支持统一标签的客户端和服务

若要确认使用的客户端和服务是否支持统一标签，请参阅其文档以查看它们是否可以使用以下其中一个管理中心发布的敏感度标签：Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 365 合规中心。 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>当前支持统一标签的客户端包括：

- [适用于 Windows 的 Azure 信息保护统一标记客户端](./rms-client/unifiedlabelingclient-version-release-history.md) - 预览版

- Office 中处于不同可用性阶段的应用。 有关详细信息，请参阅 Office 文档中的[将敏感标签应用于 Office 中的文档和电子邮件](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9)中的**现在可从何处获取功能？**。
    
- 来自软件供应商和开发人员且使用 [Microsoft 信息保护 SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview) 的应用。

##### <a name="services-that-currently-support-unified-labeling-include"></a>当前支持统一标签的服务包括：

- Windows Defender Azure 高级威胁防护

- Microsoft Cloud App Security
    
    此服务使用以下逻辑支持迁移到统一标签存储之前及之后的标签：
    
    - 如果管理中心具有的标签与 Azure 门户中的标签相同：从管理中心检索统一标签。 若要在 Cloud App Security 中选择这些标签，至少一个标签必须发布到至少一个用户。
    
    - 如果管理中心具有的标签与 Azure 门户中的标签不同：管理中心不使用统一标签，而是从 Azure 门户检索标签。

- 来自软件供应商和开发人员且使用 [Microsoft 信息保护 SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview) 的服务。

## <a name="next-steps"></a>后续步骤

有关现在可以配置并在其中一个管理中心发布的已迁移标签的详细信息，请参阅[敏感度标签的概述](/Office365/SecurityCompliance/sensitivity-labels)。

阅读博客通告文章：[宣布推出安全与合规中心的统一标记管理](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)。
