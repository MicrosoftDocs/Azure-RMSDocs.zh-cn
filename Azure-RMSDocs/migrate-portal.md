---
title: 从 Azure 经典门户迁移 - AIP
description: 概览 Azure 门户中的管理任务，这些任务过去在 Azure 经典门户中执行
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 57a1073c-02e0-441b-bf49-c6b72fdba24f
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: be25544e4fc5294491c2e339c496018d5692039a
ms.sourcegitcommit: d0012de76c9156dd9239f7ba09c044a4b42ffc71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/06/2020
ms.locfileid: "75675935"
---
# <a name="tasks-that-you-used-to-do-with-the-azure-classic-portal"></a>曾使用 Azure 经典门户执行的任务

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

> [!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的**Azure 信息保护客户端（经典）** 和**标签管理**将于**2021 年3月31日**被**弃用**。 此时间范围允许所有当前的 Azure 信息保护客户使用 Microsoft 信息保护统一标签平台过渡到我们的统一标签解决方案。 在官方[否决通知](https://aka.ms/aipclassicsunset)中了解详细信息。

习惯了使用 Azure 经典门户管理 Azure Rights Management 服务，并在转移到 Azure 门户时需要一些帮助？

Azure 经典门户已于 2018 年 1 月 8 日停用。 此日期之后，用户将不能通过经典门户管理 Azure Rights Management 服务和自定义模板。 如果尝试访问经典门户，则会看到一个链接，可通过此连接转到新的 Azure 门户。

有关经典门户停用的详细信息，请参阅博客文章公告：[Marching into the future of the Azure AD admin experience: retiring the Azure classic portal](https://cloudblogs.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/)（迈进 Azure AD 管理员体验的未来：告别 Azure 经典门户）。 有关原始停用日期的临时扩展，请参阅 [Update on retirement of Azure AD classic portal experience and migration of conditional access policies](https://cloudblogs.microsoft.com/enterprisemobility/2017/11/29/update-on-retirement-of-azure-ad-classic-portal-experience-and-migration-of-conditional-access-policies/)（关于停用 Azure AD 经典门户体验和迁移条件访问策略的更新）。

## <a name="how-to-do-your-familiar-admin-tasks"></a>如何执行熟悉的管理任务

使用以下信息可帮助你快速过渡到新门户。

|Azure 经典门户|如何在 Azure 门户中执行此任务
|-----------|--------------------|
|首次访问配置设置|1.[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。<br /><br />2. 按照中的说明进行操作，[以首次访问 "Azure 信息保护" 窗格](configure-policy.md#to-access-the-azure-information-protection-pane-for-the-first-time)。
|创建新模板|创建应用保护的标签，并使用“设置权限”来定义权限、有效期限和脱机访问。 <br /><br />此配置会在后台创建一个新的自定义模板，集成了 Rights Management 模板的服务和应用程序都可以访问该模板。<br /><br />有关详细信息，请参阅[创建新模板](configure-policy-templates.md#to-create-a-new-template)。
|编辑模板属性： <br /><br />- 模板名称和描述<br /><br />- 使用权限、内容有效期限和脱机访问设置|如果尚未这样做，请[将模板转换为标签](configure-policy-templates.md#to-convert-templates-to-labels)，然后执行以下操作<br /><br />1. 更改标签名称和说明<br /><br />2. 更改标签上的保护设置，以更新权限、过期时间和脱机访问设置。<br /><br />有关详细信息，请参阅[配置标签以保护设置](configure-policy-protection.md#to-configure-a-label-for-protection-settings)。
|存档模板|将标签状态设置为“禁用”。
|创建作用域内模板|创建作用域内策略，并在作用域内创建应用保护的标签。 <br /><br />有关详细信息，请参阅[如何使用作用域内策略为特定用户配置 Azure 信息保护策略](configure-policy-scope.md)。
|复制模板|无法在 Azure 门户中复制模板。 如果希望两个标签具有相同的保护设置，则必须设置每个标签的权限。 <br /><br />有关详细信息，请参阅[配置标签以保护设置](configure-policy-protection.md#to-configure-a-label-for-protection-settings)。
|删除模板|删除模板可能导致无法访问数据，因此 Azure 门户不支持此操作。 不过，您可以删除标签，然后使用 PowerShell [AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate) cmdlet 删除模板。 <br /><br />有关详细信息，请参阅[如何删除或重排 Azure 信息保护的标签](configure-policy-delete-reorder.md)。
|多语言支持|从“管理”菜单选择中，选择“语言”，导出包含模板名称和描述的可自定义字段。 翻译字符串，然后将这些字符串导入门户。 <br /><br />有关详细信息，请参阅[如何在 Azure 信息保护中配置不同语言的标签和模板](configure-policy-languages.md)。
|Rights Management Web 报表|[Azure 信息保护的集中式报告](reports-aip.md)现已发布预览版。<br /><br />你还可以使用 PowerShell [AipServiceUsageLog](/powershell/module/aipservice/get-aipserviceuserlog) Cmdlet 下载 Azure Rights Management 服务的使用日志。 然后可使用此数据创建自定义报表。 有关详细信息，请参阅[记录和分析 Azure 信息保护中的保护使用情况](log-analyze-usage.md)。
|激活和停用 Rights Management 服务|从“管理”菜单选项中，选择“保护激活”。<br /><br />有关详细信息，请参阅[如何从 Azure 门户激活 Rights Management 保护服务](activate-azure.md)。

在编辑模板或将其转换为 Azure 门户中的标签之前，请参阅[Azure 门户中的模板的注意事项](configure-policy-templates.md#considerations-for-templates-in-the-azure-portal)。


## <a name="what-else-has-changed"></a>其他更改内容

Azure 门户中的新功能：

- 可以编辑为组织自动创建的[默认模板](configure-policy-templates.md#default-templates)。

- 可以将模板转换为标签，以便管理单个对象，而不是独立管理模板和标签。 有关说明，请参阅[将模板转换为标签](configure-policy-templates.md#to-convert-templates-to-labels)。

- 对其他管理员角色的支持：尽管必须以全局管理员身份登录到 Azure 经典门户才能配置 Azure Rights Management，但你可以登录到 Azure 门户，通过使用包含**符合性管理员**和**符合性数据管理员**的许多其他管理角色来管理 Azure 信息保护。 "[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)" 部分包含支持的角色的完整列表。

用于创建和管理模板的 PowerShell cmdlet 以及用于激活或停用该服务的 PowerShell cmdlet 将继续受支持，不会更改。

## <a name="see-also"></a>另请参阅
有关详细信息，请参阅[使用 Azure 信息保护策略配置和管理模板](configure-policy-templates.md)。

