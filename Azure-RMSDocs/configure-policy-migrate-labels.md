---
title: 将 Azure 信息保护标签迁移到统一敏感度标签-AIP
description: 将 Azure 信息保护标签迁移到支持 Microsoft 信息保护框架的客户端和服务的统一敏感度标签。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: labelmigrate
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1751368b74d6ed2800bfd2e7432a4ce4a5844f0a
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809759"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-unified-sensitivity-labels"></a>如何将 Azure 信息保护标签迁移到统一敏感度标签

> 适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
> *适用 **于** [Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

将 Azure 信息保护标签迁移到统一的标签平台，以便可以将它们用作 [支持统一标签的客户端和服务](#clients-and-services-that-support-unified-labeling)的敏感度标签。

> [!NOTE]
> 如果你的 Azure 信息保护订阅非常新，则可能无需迁移标签，因为你的租户已在统一标签平台上。 有关详细信息，请参阅 [如何确定我的租户是否在统一标签平台上？](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

迁移标签后，你将看不到 Azure 信息保护经典客户端的任何差异，因为此客户端将继续从 Azure 门户中的 Azure 信息保护策略下载标签。 但是，你现在可以将标签用于 Azure 信息保护的统一标签客户端和其他使用敏感度标签的客户端和服务。

在阅读迁移标签说明之前，你可能会发现以下常见问题很有用：

- [Azure 信息保护中 Microsoft 365 和标签之间的标签有何区别？](faqs.md#whats-the-difference-between-labels-in-microsoft-365-and-labels-in-azure-information-protection)

- [何时将标签迁移到正确的时间？](faqs.md#when-is-the-right-time-to-migrate-my-labels)

- [迁移我的标签后，该使用哪个管理门户？](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>支持统一标签平台的管理角色

如果你在组织中使用管理员角色来委派管理，则可能需要对统一标签平台进行一些更改：

统一的标签平台不支持 **Azure 信息保护管理员** **)  (** [Azure AD 角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)。 如果在组织中使用此管理角色来管理 Azure 信息保护，请将具有此角色的用户添加到 **符合性管理员**、 **符合性数据管理员** 或 **安全管理员** 的 Azure AD 角色。 如果需要此步骤的帮助，请参阅 [授予用户访问 Microsoft 365 安全 & 相容性中心的权限](/microsoft-365/security/office-365-security/grant-access-to-the-security-and-compliance-center)。 另外，还可以在 Azure AD 门户、Microsoft 365 安全中心和 Microsoft 365 合规中心分配这些角色。

或者，若要使用角色，可以在管理中心为这些用户创建新角色组，然后向该组中添加“敏感度标签管理员”或“组织配置”角色。

如果未使用其中一个配置向这些用户授予对管理中心的访问权限，则在迁移标签后将无法在 Azure 门户中配置 Azure 信息保护。

迁移标签后，租户的全局管理员可以继续管理 Azure 门户和管理中心中的标签和策略。

## <a name="before-you-begin"></a>开始之前

标签迁移具有很多优点，但不可逆。 在迁移之前，请确保你已了解以下更改和注意事项：

- [统一标签的客户端支持](#client-support-for-unified-labeling)
- [策略配置](#policy-configuration)
- [保护模板](#protection-templates)
- [显示名称](#display-names)
- [标签中的本地化字符串](#localized-strings-in-labels)
- [编辑管理中心中的已迁移标签](#editing-migrated-labels-in-the-admin-centers)
- [管理中心不支持的标签设置](#label-settings-that-are-not-supported-in-the-admin-centers)
- [比较标签保护设置的行为](#comparing-the-behavior-of-protection-settings-for-a-label)

### <a name="client-support-for-unified-labeling"></a>统一标签的客户端支持

请确保你的 [客户端支持统一标签](#clients-and-services-that-support-unified-labeling) ，并且如有必要，请在不支持统一标签的客户端的 Azure 门户 (中做好管理准备，) 和管理中心 (支持统一) 标签的客户端。

### <a name="policy-configuration"></a>策略配置

不会迁移策略，包括策略设置和谁有权访问策略（作用域内策略）以及所有高级客户端设置。 在标签迁移后配置这些设置的选项包括：

- 用于敏感度标签的管理中心。
- [Office 365 Security & 符合性 PowerShell](/powershell/exchange/office-365-scc/office-365-scc-powershell)，你必须使用它来 [配置高级客户端设置](rms-client/clientv2-admin-guide-customizations.md#configuring-advanced-settings-for-the-client-via-powershell)。
    
> [!IMPORTANT]
> 管理中心并不支持已迁移标签中的所有设置。 使用[管理中心不支持的标签设置](#label-settings-that-are-not-supported-in-the-admin-centers)部分中的表，来帮助识别这些设置和建议的操作过程。
> 

### <a name="protection-templates"></a>保护模板

- 使用基于云的密钥和为标签配置的一部分模板也随标签一同迁移。 不迁移其他保护模板。 
    
- 如果你的标签已针对预定义的模板进行了配置，请编辑这些标签，并选择“设置权限”选项，配置模板中具有的相同保护设置。 具有预定义模板的标签不会阻止标签迁移，但管理中心不支持此标签配置。
        
    > [!TIP]
    > 为了帮助您重新配置这些标签，您可能会发现有两个浏览器窗口是非常有用的：一个窗口，您可以在其中选择标签的 " **编辑模板** " 按钮以查看保护设置，另一个窗口用于在选择 " **设置权限**" 时配置相同的设置。
    
- 迁移了包含基于云的保护设置的标签后，保护模板的结果范围是 Azure 门户 (中定义的作用域，或者通过使用 AIPService PowerShell 模块) 和在管理中心定义的作用域。 

### <a name="display-names"></a>显示名称

对于每个标签，Azure 门户仅显示可编辑的标签显示名称。 用户将在其应用中看到此标签名称。 

管理中心显示标签的显示名称和标签名称。 标签名称是首次创建标签时指定的初始名称，后端服务使用此属性进行标识。 迁移标签时，显示名称将保持不变，并且标签名称将重命名为 Azure 门户中的标签 ID。

#### <a name="conflicting-display-names"></a>冲突的显示名称

在迁移之前，请确保在迁移完成后不会有冲突的显示名称。 标签层次结构中同一位置的显示名称必须是唯一的。 

例如，请考虑以下标签列表：

- **公共**
- **常规**
- 机密
    - **Confidential\HR**
    - **Confidential\Finance**
- **机密**
    - **Secret\HR**
    - **Secret\Finance**
    
在此列表中，" **公用**"、" **常规**"、" **机密**" 和 " **机密** " 均为父标签，并且不能有重复的名称。 此外， **Confidential\HR** 和 **Confidential\Finance** 位于层次结构中的同一位置，也不能有重复的名称。

但是，不同父级之间的子标签（例如 **Confidential\HR** 和 **Secret\HR** ）不在层次结构中的同一位置，因此可以具有相同的单个名称。 

### <a name="localized-strings-in-labels"></a>标签中的本地化字符串

不迁移标签的任何本地化字符串。 使用 Office 365 Security & 相容性 PowerShell 为已迁移标签定义新的本地化字符串，并为 [集标签](/powershell/module/exchange/policy-and-compliance/set-label)定义 *LocaleSettings* 参数。

### <a name="editing-migrated-labels-in-the-admin-centers"></a>编辑管理中心中的已迁移标签

迁移之后，当你在 Azure 门户中编辑已迁移的标签时，相同的更改将会自动反映在管理中心。 

但是，当你在某个管理中心内编辑已迁移的标签时，必须返回到 "Azure 门户， **Azure 信息保护-统一标签** " 窗格，然后选择 " **发布**"。 

Azure 信息保护客户端需要执行此附加操作 (经典) 来选取标签更改。

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>管理中心不支持的标签设置

使用下表来确定已迁移的标签的哪些配置设置不受 Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 合规中心的支持。 如果你具有这些设置的标签，则迁移完成后，请先使用最终列中的管理指南，然后再将你的标签发布到一个被引用管理中心。

如果不确定如何配置标签，请在 Azure 门户中查看其设置。 如果需要有关此步骤的帮助，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

Azure 信息保护客户端 (经典) 可以使用列出的所有标签设置而不会出现任何问题，因为它们会继续从 Azure 门户下载标签。

|标签配置|受统一标记客户端的支持| 管理中心指南|
|-------------------|---------------------------------------------|-------------------------|
|**启用或禁用状态**<br /><br />此状态不同步到管理中心 |不适用|等效于是否发布标签。 |
|**从列表中选择的标签颜色或使用 RGB 代码指定的标签颜色** |是|标签颜色没有配置选项。 相反，你可以在 Azure 门户中配置标签颜色，也可以使用 [PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)。|
|**使用预定义模板的基于云的保护或基于 HYOK 的保护** |否|预定义模板没有配置选项。 我们不建议使用此配置发布标签。|
|**使用 Word、Excel 和 PowerPoint 的用户定义权限的基于云的保护** |是|管理中心现在具有用户定义的权限的配置选项。 <br /><br /> 如果使用此配置发布标签，请查看 [下表](#comparing-the-behavior-of-protection-settings-for-a-label)中应用标签的结果。|
|**使用 Outlook (的用户定义权限的基于 HYOK 的保护** 不转发)  |否|HYOK 没有配置选项。 我们不建议使用此配置发布标签。 否则，请在[下表](#comparing-the-behavior-of-protection-settings-for-a-label)中查看应用此标签所带来的后果。|
|**自定义字体名称、大小和自定义字体颜色（由 RGB 代码用于视觉标记** (页眉、页脚、水印)   |是|视觉标记的配置限制为颜色和字体大小列表。 尽管无法看见管理中心中配置的值，仍可以不做任何更改发布此标签。 <br /><br />若要更改这些选项，请使用 [**新的标签**](/powershell/module/exchange/new-label) Office 365 Security & 相容性中心 cmdlet。 为了便于管理，请考虑将颜色更改为管理中心中列出的选项之一。 <br /><br />**注意**：安全 & 相容性中心管理中心支持预定义的字体定义列表。 仅通过 [**新的标签**](/powershell/module/exchange/new-label) Office 365 Security & 相容性中心 cmdlet 支持自定义字体和颜色。 <br><br>如果使用的是经典客户端，请在 Azure 门户中对标签进行这些更改。|
|**视觉对象标记中的变量** (页眉、页脚)  |是|对于 "选择应用"，AIP 客户端和 Office 内置标签支持此标签配置。 <br /><br />如果你使用的是不支持此配置的应用程序的内置标签，并且无需更改即可发布此标签，则变量将在客户端上显示为文本，而不是显示动态值。<br /><br />有关详细信息，请参阅 [Microsoft 365 文档](/microsoft-365/compliance/sensitivity-labels-office-apps#dynamic-markings-with-variables)。 |
|**每个应用的视觉标记**|是|此标签配置仅在 AIP 客户端中受支持，而不受 Office 内置标签支持。 <br /><br />如果使用内置标签，并发布此标签而不进行任何更改，则视觉标记配置将显示为变量文本，而不是已配置为在每个应用中显示的视觉标记。  |
|**"仅限我" 保护**|是|管理中心不允许你保存现在应用的加密设置，而无需指定任何用户。 在 Azure 门户中，此配置会生成一个标签，该标签适用于 ["仅限我" 的保护](configure-policy-protection.md#example-6-label-that-applies-just-for-me-protection)。 <br /><br /> 作为替代方法，可以创建应用加密的标签，并指定具有任何权限的用户，然后使用 PowerShell 编辑关联的保护模板。 首先，使用 [AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) cmdlet (参阅示例 3) ，然后使用 *RightsDefinitions* 参数 [AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty#examples) 。|
|**条件和关联设置** <br /><br /> 包括自动和建议标签及其工具提示|不适用|若要重新配置条件，请将自动标记用作标签设置中的独立配置。|
| | | |

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>比较标签保护设置的行为

使用下表来确定标签的相同保护设置的行为方式不同，具体取决于 Azure 信息保护经典客户端、Azure 信息保护统一标签客户端，还是使用内置标签的 Office 应用 (也称为 "本机办公室标签" ) 。 标签行为的差异可能会改变您决定是否发布标签，特别是在您的组织中有混合的客户端时。

如果你不确定保护设置的配置方式，请在 " **保护** " 窗格的 "Azure 门户中查看其设置。 如果需要有关此步骤的帮助，请参阅[配置保护设置标签](configure-policy-protection.md#to-configure-a-label-for-protection-settings)。

下表未列出具有相同行为的保护设置，以下情形例外：
- 使用具有内置标签的 Office 应用时，除非还安装了 Azure 信息保护统一标签客户端，否则标签在文件资源管理器中不可见。
- 使用具有内置标签的 Office 应用时，如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)。

|标签的保护设置 |Azure 信息保护经典客户端 |Azure 信息保护统一标识客户端| 具有内置标签的 Office 应用
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|带有模板的 HYOK (AD RMS)：| 可在 Word、Excel、PowerPoint、Outlook 和文件资源管理器中查看<br /><br /> 当应用此标签时： <br /><br />- 对文档和电子邮件应用 HYOK 保护 | 可在 Word、Excel、PowerPoint、Outlook 和文件资源管理器中查看  <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前通过标签应用了保护，则去除保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 |可在 Word、Excel、PowerPoint 和 Outlook 中查看 <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前通过标签应用了保护，则去除保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1) |
|HYOK (AD RMS)，其中用户定义的权限适用于 Word、Excel、PowerPoint 和文件资源管理器：| 可在 Word、Excel、PowerPoint 和文件资源管理器中查看<br /><br /> 当应用此标签时：<br /><br /> - 对文档和电子邮件应用 HYOK 保护| 可在 Word、Excel 和 PowerPoint 中查看 <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护|可在 Word、Excel 和 PowerPoint 中查看 <br /><br /> 当应用此标签时： <br /><br />- 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 |
|HYOK (AD RMS)，其中用户定义的权限适用于 Outlook：|可在 Outlook 中查看<br /><br />当应用此标签时：<br /><br />- 通过 HYOK 保护向电子邮件应用“请勿转发”规则|可在 Outlook 中查看<br /><br />当应用此标签时：<br /><br /> - 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护|可在 Outlook 中查看<br /><br />当应用此标签时：<br /><br />- 不应用保护；如果之前已通过标签应用保护，则删除该保护 [[2]](#footnote-2) <br /><br />- 如果之前在未使用标签的情况下实施了保护，则保留保护 [[1]](#footnote-1)|

###### <a name="footnote-1"></a>脚注 1

在 Outlook 中，保留保护，但有一个例外：在使用 "仅加密" 选项保护电子邮件时 (**加密**) ，则会删除该保护。


###### <a name="footnote-2"></a>脚注 2

如果用户具有支持此操作的使用权限或角色，则去掉保护：
- [使用权限](configure-usage-rights.md#usage-rights-and-descriptions) - 导出或完全控制。
- [权限管理颁发者/权限管理所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)角色或者[超级用户](configure-super-users.md)。

如果用户没有上述任一使用权限或角色，则不应用标签且保留原始保护。


## <a name="to-migrate-azure-information-protection-labels"></a>若要迁移 Azure 信息保护标签

使用以下说明将租户和 Azure 信息保护标签迁移到使用统一标签存储。

必须是符合性管理员、合规性数据管理员、安全管理员或全局管理员才能迁移标签。

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到“Azure 信息保护”窗格。
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。

2. 在“管理”菜单选项中，选择“统一标签” 。

3. 在 " **Azure 信息保护-统一标签** " 窗格中，选择 " **激活** "，并按照联机说明进行操作。
    
    如果激活选项不可用，请检查 **统一标签状态**：如果你看到 "已 **激活**"，则你的租户已在使用统一标签存储，并且无需迁移标签。

成功迁移的标签现在可被[支持统一标签的客户端和服务](#clients-and-services-that-support-unified-labeling)使用。 但是，必须首先将 [这些标签发布](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy) 到某个管理中心： Office 365 安全 & 符合性中心、Microsoft 365 安全中心或 Microsoft 365 符合性中心。

> [!IMPORTANT]
> 如果在 Azure 门户之外编辑标签，对于 Azure 信息保护客户端 (经典) ，返回到此 **Azure 信息保护-统一标签** 窗格，然后选择 " **发布**"。

### <a name="copy-policies"></a>复制策略

迁移标签后，可以选择用于复制策略的选项。 如果选择此选项，策略的一次性副本及其 [策略设置](configure-policy-settings.md) 和任何 [高级客户端设置](./rms-client/client-admin-guide-customizations.md#available-advanced-classic-client-settings) 将发送到管理标签的管理中心： Office 365 security & 相容中心、Microsoft 365 安全中心、Microsoft 365 合规中心。 

已成功复制策略及其设置和标签之后，会自动将其发布到分配到 Azure 门户中的策略的用户和组。 请注意，对于全局策略，这意味着所有用户。 如果尚未准备好在要发布的复制策略中迁移的标签，则在复制策略后，你可以从管理员标签中心中的标签策略删除标签。

在 " **Azure 信息保护-统一标签**" 窗格上选择 "**复制策略 (预览")** 选项之前，请注意以下事项：

- 在为租户激活统一标签之前，" **复制策略 (预览")** "选项不可用。

- 你无法有选择地选择要复制的策略和设置。 **全局** 策略 (的所有策略和所有作用域内策略) 会自动选择复制，并会复制支持作为标签策略设置的所有设置。 如果已具有同名的标签策略，则会使用 Azure 门户中的策略设置来覆盖它。

- 不会复制某些高级客户端设置，因为对于 Azure 信息保护统一标签客户端，这些设置支持作为 *标签高级设置* ，而不是策略设置。 可以通过 [Microsoft 365 Security & 相容性中心 PowerShell](rms-client/clientv2-admin-guide-customizations.md#configuring-advanced-settings-for-the-client-via-powershell)配置这些标签高级设置。 未复制的高级客户端设置：
    - [LabelbyCustomProperty](./rms-client/client-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [LabelToSMIME](./rms-client/client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- 不同于标签迁移（对标签的后续更改进行同步），" **复制策略** " 操作不会同步任何对策略或策略设置的后续更改。 在 Azure 门户中进行更改后，你可以重复 "复制策略" 操作，并且将再次覆盖任何现有策略及其设置。 或者，将 Set-LabelPolicy 或 Set-Label cmdlet 与 Office 365 Security & 相容性中心 PowerShell 中的 *AdvancedSettings* 参数一起使用。

- 复制 **策略** 操作在复制每个策略之前验证以下各项：
    
    - 分配给策略的用户和组目前处于 Azure AD。 如果缺少一个或多个帐户，则不会复制此策略。 不检查组成员身份。
    
    - 全局策略包含至少一个标签。 由于管理员标签中心不支持不带标签的标签策略，因此不会复制不带标签的全局策略。

- 如果复制策略，然后将其从管理标签中心删除，请在使用 " **复制策略** " 操作之前至少等待两个小时，以确保有足够的时间来复制删除。

- 从 Azure 信息保护复制的策略不具有相同的名称，而是使用 **AIP_** 的前缀来命名。 以后不能更改策略名称。 

有关为 Azure 信息保护统一标签客户端配置策略设置、高级客户端设置和标签设置的详细信息，请参阅管理员指南中 [的 Azure 信息保护统一标签客户端的自定义配置](./rms-client/clientv2-admin-guide-customizations.md) 。

> [!NOTE]
> Azure 信息保护对复制策略的支持目前以预览版提供。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。 

### <a name="clients-and-services-that-support-unified-labeling"></a>支持统一标签的客户端和服务

若要确认你使用的客户端和服务是否支持统一标签，请参阅其文档，检查它们是否可以使用从某个管理中心发布的敏感度标签： Office 365 Security & 相容性中心、Microsoft 365 安全中心或 Microsoft 365 合规中心。 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>当前支持统一标签的客户端包括：

- **[适用于 Windows 的 Azure 信息保护统一标签客户端](./rms-client/unifiedlabelingclient-version-release-history.md)** 

    有关此客户端与 Azure 信息保护经典客户端的比较，请参阅 [比较适用于 Windows 计算机的标记解决方案](rms-client/use-client.md#compare-the-labeling-solutions-for-windows-computers)。

- **不同可用性阶段中的 Office 应用** 

    有关详细信息，请参阅 Microsoft 365 相容性文档 [中的对应用中的敏感度标签功能的支持](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps) 。
    
- **来自软件供应商和开发人员** 的使用 [MICROSOFT 信息保护 SDK](/information-protection/develop/overview)的应用。

##### <a name="services-that-currently-support-unified-labeling-include"></a>当前支持统一标签的服务包括：

- **[Power BI](/power-bi/admin/service-security-data-protection-overview)**

- **Web 上的 Office Online 和 Outlook**

    有关详细信息，请参阅 [在 SharePoint 和 OneDrive 中启用 Office 文件的敏感度标签](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)。

- **Microsoft SharePoint、OneDrive for work 或 school、OneDrive for home、团队和 Microsoft 365 组**
    
    有关详细信息，请参阅 [使用敏感度标签保护 Microsoft 团队、Microsoft 365 组和 SharePoint 站点中的内容](/microsoft-365/compliance/sensitivity-labels-teams-groups-sites)。

- **Microsoft Defender 高级威胁防护**

- **Microsoft Cloud App Security**
    
    此服务使用以下逻辑支持迁移到统一标签存储之前及之后的标签：
    
    - 如果管理中心具有敏感度标签，则将从管理中心检索这些标签。 若要在 Cloud App Security 中选择这些标签，至少一个标签必须发布到至少一个用户。
    
    - 如果管理中心没有敏感度标签，则从 Azure 门户检索 Azure 信息保护标签。

- **来自软件供应商和开发人员的服务** ，使用 [MICROSOFT 信息保护 SDK](/information-protection/develop/overview)。

## <a name="next-steps"></a>后续步骤

**客户体验团队的指导和提示**：

- 博客文章： [了解统一标签迁移](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Understanding-Unified-Labeling-migration/ba-p/783185)

- 网络研讨会： [记录、卡片组和常见问题解答的统一标签](https://github.com/nihendle/MIP-Comp/tree/master/MIP/Webinars/Unified%20Labeling%20Migration)


**关于敏感度标签**：
- [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels)
- [创建和配置敏感度标签及其策略](/microsoft-365/compliance/create-sensitivity-labels)。

**部署 AIP 统一标签客户端**：

如果尚未这样做，请安装 Azure 信息保护统一标签客户端。 

有关详细信息，请参阅：

- [Azure 信息保护统一标签客户端-版本发行历史记录和支持策略](rms-client/unifiedlabelingclient-version-release-history.md)
- [Azure 信息保护统一标记客户端管理员指南](rms-client/clientv2-admin-guide.md)
- [Azure 信息保护统一标签用户指南](rms-client/clientv2-user-guide.md)
