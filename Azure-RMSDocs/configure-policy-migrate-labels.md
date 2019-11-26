---
title: Migrate Azure Information Protection labels to unified sensitivity labels - AIP
description: Migrate Azure Information Protection labels to unified sensitivity labels for clients and services that support the Microsoft Information Protection framework.
author: cabailey
ms.author: cabailey
manager: rkarlin
ms.date: 11/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: labelmigrate
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bb493943696c5bb349ef66e13891ce4139d904e3
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474274"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-unified-sensitivity-labels"></a>How to migrate Azure Information Protection labels to unified sensitivity labels

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
> *Instructions for: [Azure Information Protection client for Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Migrate Azure Information Protection labels to the unified labeling platform so that you can use them as sensitivity labels by [clients and services that support unified labeling](#clients-and-services-that-support-unified-labeling).

> [!NOTE]
> If your Azure Information Protection subscription is fairly new, you might not need to migrate labels because your tenant is already on the unified labeling platform. For more information, see [How can I determine if my tenant is on the unified labeling platform?](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

After you migrate your labels, you won't see any difference with the Azure Information Protection client (classic) because this client continues to download the labels with the Azure Information Protection policy from the Azure portal. However, you can now use the labels with the Azure Information Protection unified labeling client and other clients and services that use sensitivity labels.

Before you read the instructions to migrate your labels, you might find the following frequently asked questions useful:

- [Azure 信息保护中的标签与 Office 365 中的标签之间有何区别？](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [When is the right time to migrate my labels?](faqs.md#when-is-the-right-time-to-migrate-my-labels)

- [迁移我的标签后，该使用哪个管理门户？](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>Administrative roles that support the unified labeling platform

If you use admin roles for delegated administration in your organization, you might need to do some changes for the unified labeling platform:

The [Azure AD roles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) of **Azure Information Protection administrator** (formerly **Information Protection administrator**), **Security reader**, and **Global reader** are not supported by the unified labeling platform. If any of these administrative roles are used in your organization to manage Azure Information Protection, add the users who have this role to the Azure AD roles of **Compliance administrator**, **Compliance data administrator**, or **Security administrator**. 如果需要有关此步骤的帮助，请参阅[向用户授予对 Office 365 安全与合规中心的访问权限](https://docs.microsoft.com/microsoft-365/security/office-365-security/grant-access-to-the-security-and-compliance-center)。 另外，还可以在 Azure AD 门户、Microsoft 365 安全中心和 Microsoft 365 合规中心分配这些角色。

或者，若要使用角色，可以在管理中心为这些用户创建新角色组，然后向该组中添加“敏感度标签管理员”或“组织配置”角色。

如果未使用其中一个配置向这些用户授予对管理中心的访问权限，则在迁移标签后将无法在 Azure 门户中配置 Azure 信息保护。

迁移标签后，租户的全局管理员可以继续管理 Azure 门户和管理中心中的标签和策略。

## <a name="before-you-begin"></a>在开始之前

Label migration has many benefits but is irreversible, so make sure that you are aware of the following changes and considerations:

- Make sure that you have [clients that support unified labels](#clients-and-services-that-support-unified-labeling) and if necessary, be prepared for administration in both the Azure portal (for clients that don't support unified labels) and the admin centers (for client that do support unified labels).

- 不会迁移策略，包括策略设置和谁有权访问策略（作用域内策略）以及所有高级客户端设置。 Your options to configure these settings after your label migration include the following:
    - Your admin center for sensitivity labels.
    - [Office 365 Security & Compliance PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps), which you must use to configure [advanced client settings](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).
    

- 管理中心并不支持已迁移标签中的所有设置。 使用[管理中心不支持的标签设置](#label-settings-that-are-not-supported-in-the-admin-centers)部分中的表，来帮助识别这些设置和建议的操作过程。

- 保护模板：
    
    - 使用基于云的密钥和为标签配置的一部分模板也随标签一同迁移。 不迁移其他保护模板。 
    
    - 如果你的标签已针对预定义的模板进行了配置，请编辑这些标签，并选择“设置权限”选项，配置模板中具有的相同保护设置。 具有预定义模板的标签不会阻止标签迁移，但管理中心不支持此标签配置。
        
        Tip: To help you reconfigure these labels, you might find it useful to have two browser windows: One window in which you select the **Edit Template** button for the label to view the protection settings, and the other window to configure the same settings when you select **Set permissions**.
    
    - After a label with cloud-based protection settings has been migrated, the resulting scope of the protection template is the scoped that is defined in the Azure portal (or by using the AIPService PowerShell module) and the scope that is defined in the admin centers. 

- 对于每个标签，Azure 门户仅显示可编辑的标签显示名称。 Users see this label name in their apps. 管理中心显示标签的显示名称和标签名称。 The label name is the initial name that you specify when the label is first created and this property is used by the back-end service for identification purposes. When you migrate your labels, the display name remains the same and the label name is renamed to the label ID from the Azure portal.

- 不迁移标签的任何本地化字符串。 Define new localized strings for the migrated labels by using Office 365 Security & Compliance PowerShell and the *LocaleSettings* parameter for [Set-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

- 迁移之后，当你在 Azure 门户中编辑已迁移的标签时，相同的更改将会自动反映在管理中心。 However, when you edit a migrated label in one of the admin centers, you must return to the Azure portal, **Azure Information Protection - Unified labeling** pane, and select **Publish**. This additional action is needed for the Azure Information Protection clients (classic) to pick up the label changes.

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>管理中心不支持的标签设置

使用下表来确定已迁移的标签的哪些配置设置不受 Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 合规中心的支持。 If you have labels with these settings, when the migration is complete, use the administration guidance in the final column before you publish your labels in one of the referenced admin centers.

如果不确定如何配置标签，请在 Azure 门户中查看其设置。 如果需要有关此步骤的帮助，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

Azure Information Protection clients (classic) can use all label settings listed without any problems because they continue to download the labels from the Azure portal.

|标签配置|受统一标记客户端的支持| 管理中心指南|
|-------------------|---------------------------------------------|-------------------------|
|启用或禁用状态<br /><br />This status is not synchronized to the admin centers |“不适用”|等效于是否发布标签。 |
|从列表中选择的标签颜色或使用 RGB 代码指定的标签颜色 |“是”|标签颜色没有配置选项。 Instead, you can configure label colors in the Azure portal or use [PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).|
|使用预定义模板的基于云的保护或基于 HYOK 的保护 |否|预定义模板没有配置选项。 我们不建议使用此配置发布标签。|
|使用 Word、Excel 和 PowerPoint 的用户定义权限的基于云的保护 |“是”|The admin centers now have a configuration option for user-defined permissions. <br /><br /> If you publish a label with this configuration, check the results of applying the label from the [following table](#comparing-the-behavior-of-protection-settings-for-a-label).|
|使用 Outlook（不可转发）中用户定义权限的基于 HYOK 的保护 |否|HYOK 没有配置选项。 我们不建议使用此配置发布标签。 否则，请在[下表](#comparing-the-behavior-of-protection-settings-for-a-label)中查看应用此标签所带来的后果。|
|删除保护 |否|没有用于删除保护的配置选项。 我们不建议使用此配置发布标签。<br /><br /> If you do publish a label with this configuration, when it is applied, protection is always removed, whether the protection was previously applied by a label or independently from a label.|
|Any authenticated user protection setting |“是”|No configuration option to select this protection setting. Publish a label with this configuration when this setting has been migrated or you configure it in the Azure portal.|
|为视觉标记（页眉、页脚、水印）使用 RGB 代码自定义字体和字体颜色|“是”|视觉标记的配置限制为颜色和字体大小列表。 尽管无法看见管理中心中配置的值，仍可以不做任何更改发布此标签。 <br /><br />若要更改这些选项，可以使用 Azure 门户。 但是，请考虑将颜色更改为管理中心中列出的选项之一，以便于管理。|
|视觉标记（页眉、页脚）中的变量|否|如果不做更改就发布此标签，则变量将在客户端上显示为文本而不是显示动态值。 发布标签之前，请编辑字符串以删除变量。|
|每个应用的视觉标记|否|如果不做更改就发布此标签，则在所有应用中应用变量将在客户端上显示为文本，而不是在所选的应用上显示文本字符串。 仅当适用于所有应用时发布此标签，并编辑字符串以删除应用变量。|
|条件和关联设置 <br /><br /> 包括自动和建议标签及其工具提示|“不适用”|若要重新配置条件，请将自动标记用作标签设置中的独立配置。|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>比较标签保护设置的行为

Use the following table to identify how the same protection setting for a label behaves differently, depending on whether it's used by the Azure Information Protection client (classic), the Azure Information Protection unified labeling client, or by Office apps that have labeling built in (also known as "native Office labeling"). The differences in label behavior might change your decision whether to publish the labels, especially when you have a mix of clients in your organization.

If you are not sure how your protection settings are configured, view their settings in the **Protection** pane, in the Azure portal. 如果需要有关此步骤的帮助，请参阅[配置保护设置标签](configure-policy-protection.md#to-configure-a-label-for-protection-settings)。

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

In Outlook, protection is preserved with one exception: When an email has been protected with the Encrypt-Only option, that protection is removed.


###### <a name="footnote-2"></a>脚注 2

如果用户具有支持此操作的使用权限或角色，则去掉保护：
- [使用权限](configure-usage-rights.md#usage-rights-and-descriptions) - 导出或完全控制。
- [权限管理颁发者/权限管理所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)角色或者[超级用户](configure-super-users.md)。

如果用户没有上述任一使用权限或角色，则不应用标签且保留原始保护。


## <a name="to-migrate-azure-information-protection-labels"></a>若要迁移 Azure 信息保护标签

Use the following instructions to migrate your tenant and Azure Information Protection labels to use the unified labeling store.

You must be a Compliance administrator, Compliance data administrator, Security administrator, or Global administrator to migrate your labels.

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”窗格。
    
    For example, in the search box for resources, services, and docs: Start typing **Information** and select **Azure Information Protection**.

2. From the **Manage** menu option, select **Unified labeling**.

3. On the **Azure Information Protection - Unified labeling** pane, select **Activate** and follow the online instructions.
    
    If the option to activate is not available, check the **Unified labeling status**: If you see **Activated**, your tenant is already using the unified labeling store and there is no need to migrate your labels.

成功迁移的标签现在可被[支持统一标签的客户端和服务](#clients-and-services-that-support-unified-labeling)使用。 However, you must first publish these labels in one of the admin centers: Office 365 Security & Compliance Center, Microsoft 365 security center, or Microsoft 365 compliance center.

> [!IMPORTANT]
> If you edit the labels outside the Azure portal, for Azure Information Protection clients (classic), return to this **Azure Information Protection - Unified labeling** pane, and select **Publish**.

### <a name="copy-policies"></a>Copy policies

> [!NOTE]
> This option is in preview and subject to change.

After you have migrated your labels, you can select an option to copy policies. If you select this option, a one-time copy of your policies with their [policy settings](configure-policy-settings.md) and any [advanced client settings](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings) is sent to the admin center where you manage your labels: Office 365 Security & Compliance Center, Microsoft 365 security center, Microsoft 365 compliance center.

Before you select the **Copy policies (preview)** option on the **Azure Information Protection - Unified labeling** pane, be aware of the following:

- You cannot selectively choose policies and settings to copy. All policies (the **Global** policy and any scoped policies) are copied, and all settings that are supported as label policy settings are copied. If you already have a label policy with the same name, it will be overwritten with the policy settings in the Azure portal.

- Some advanced client settings are not copied because for the Azure Information Protection unified labeling client, these are supported as *label advanced settings* rather than policy settings. You can configure these label advanced settings with [Office 365 Security & Compliance Center PowerShell](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell). The advanced client settings that are not copied:
    - [LabelbyCustomProperty](./rms-client/client-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [LabelToSMIME](./rms-client/client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- Unlike label migration where subsequent changes to labels are synchronized, the copy policies action doesn't synchronize any subsequent changes to your policies or policy settings. You can repeat the copy policy action after making changes in the Azure portal, and any existing policies and their settings will be overwritten again. Or, use the Set-LabelPolicy or Set-Label cmdlets with the *AdvancedSettings* parameter from Office 365 Security & Compliance Center PowerShell.

- The **Copy policies (Preview)** option is not available until unified labeling is activated for your tenant.

For more information about configuring the policy settings, advanced client settings, and label settings for the Azure Information Protection unified labeling client, see [Custom configurations for the Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide-customizations.md) from the admin guide.

### <a name="clients-and-services-that-support-unified-labeling"></a>支持统一标签的客户端和服务

To confirm whether the clients and services you use support unified labeling, refer to their documentation to check whether they can use sensitivity labels that are published from one of the admin centers: Office 365 Security & Compliance Center, Microsoft 365 security center, or Microsoft 365 compliance center. 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>当前支持统一标签的客户端包括：

- The [Azure Information Protection unified labeling client for Windows](./rms-client/unifiedlabelingclient-version-release-history.md). For a comparison of this client with the Azure Information Protection client (classic), see [Compare the labeling clients for Windows computers](./rms-client/use-client.md#compare-the-labeling-clients-for-windows-computers).

- Office 中处于不同可用性阶段的应用。 For more information, see [What sensitivity label capabilities are supported in Office today?](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#what-sensitivity-label-capabilities-are-supported-in-office-today) from the Office documentation.
    
- 来自软件供应商和开发人员且使用 [Microsoft 信息保护 SDK](https://docs.microsoft.com/information-protection/develop/overview) 的应用。

##### <a name="services-that-currently-support-unified-labeling-include"></a>当前支持统一标签的服务包括：

- [Power BI (in preview)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview)

- Office Online (in preview) and Outlook on the web

- SharePoint Online, OneDrive for Business, Microsoft Teams, and Office 365 groups (in preview)
    
    For more information, see [Use sensitivity labels with Microsoft Teams, Office 365 groups, and SharePoint sites (public preview)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-teams-groups-sites) and [Enable sensitivity labels for Office files in SharePoint and OneDrive (public preview)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

- Microsoft Defender Advanced Threat Protection

- Microsoft Cloud App Security
    
    此服务使用以下逻辑支持迁移到统一标签存储之前及之后的标签：
    
    - If the admin centers have the same labels as those in the Azure portal: Unified labels are retrieved from the admin centers. 若要在 Cloud App Security 中选择这些标签，至少一个标签必须发布到至少一个用户。
    
    - If the admin centers don't have the same labels as those in the Azure portal: Unified labels are not used from the admin centers, and instead, labels are retrieved from the Azure portal.

- 来自软件供应商和开发人员且使用 [Microsoft 信息保护 SDK](https://docs.microsoft.com/information-protection/develop/overview) 的服务。

## <a name="next-steps"></a>后续步骤

For additional guidance and tips from our Customer Experience team, see the following blog post: [Understanding Unified Labeling Migration](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Understanding-Unified-Labeling-migration/ba-p/783185).

有关现在可以配置并在其中一个管理中心发布的已迁移标签的详细信息，请参阅[敏感度标签的概述](/microsoft-365/compliance/sensitivity-labels)。

If you haven't already done so, install the Azure Information Protection unified labeling client. For release information, an admin guide, and user guide, see [Azure Information Protection unified labeling client for Windows](./rms-client/aip-clientv2.md).
