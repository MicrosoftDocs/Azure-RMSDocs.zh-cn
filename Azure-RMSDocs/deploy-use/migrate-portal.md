---
title: "从 Azure 经典门户迁移 - AIP"
description: "概览 Azure 门户中的管理任务，这些任务过去在 Azure 经典门户中执行"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/08/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 57a1073c-02e0-441b-bf49-c6b72fdba24f
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 367189865266e85df967c398b17153d970241e98
ms.sourcegitcommit: fc789ce08821e031d3a2b22d850b4318302d3585
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="tasks-that-you-used-to-do-with-the-azure-classic-portal"></a>曾使用 Azure 经典门户执行的任务

>*适用于：Azure 信息保护、Office 365*

习惯了使用 Azure 经典门户管理 Azure Rights Management 服务，并在转移到 Azure 门户时需要一些帮助？ 

Azure 经典门户已于 2018 年 1 月 8 日停用。 此日期之后，用户将不能通过经典门户管理 Azure Rights Management 服务和自定义模板。 如果尝试访问经典门户，则会看到一个链接，可通过此连接转到新的 Azure 门户。 

有关经典门户停用的详细信息，请参阅博客文章公告：[Marching into the future of the Azure AD admin experience: retiring the Azure classic portal](https://blogs.technet.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/)（迈进 Azure AD 管理员体验的未来：告别 Azure 经典门户）。 有关原始停用日期的临时扩展，请参阅 [Update on retirement of Azure AD classic portal experience and migration of conditional access policies](https://cloudblogs.microsoft.com/enterprisemobility/2017/11/29/update-on-retirement-of-azure-ad-classic-portal-experience-and-migration-of-conditional-access-policies/)（关于停用 Azure AD 经典门户体验和迁移条件访问策略的更新）。

## <a name="how-to-do-your-familiar-admin-tasks"></a>如何执行熟悉的管理任务

使用以下信息可帮助你快速过渡到新门户。

但是，订阅 Office 365 美国政府版（政府社区云）的客户目前无法使用 Azure 门户，必须改用 [PowerShell](configure-templates-with-powershell.md) 来管理模板。 


|Azure 经典门户|如何在 Azure 门户中执行此任务
|-----------|--------------------|
|首次访问配置设置|1.以租户的全局管理员身份或安全管理员身份登录到 Azure 门户。<br /><br />2.在中心菜单上，单击“新建”，然后从 **MARKETPLACE** 列表中选择“安全 + 标识”。<br /><br />3.在“安全 + 标识”边栏选项卡上，从“特别推荐的应用”列表中选择“Azure 信息保护”。 然后，在“Azure 信息保护”边栏选项卡上，单击“创建”。<br /><br />此操作将创建“Azure 信息保护”边栏选项卡，以便下次登录到门户时，可以从中心的“更多服务”列表中选择该服务。
|创建新模板|创建应用保护的标签，并使用“设置权限”来定义权限、有效期限和脱机访问。 <br /><br />此配置会在后台创建一个新的自定义模板，集成了 Rights Management 模板的服务和应用程序都可以访问该模板。<br /><br />有关详细信息，请参阅[创建新模板](configure-policy-templates.md#to-create-a-new-template)。
|编辑模板属性： <br /><br />- 模板名称和描述<br /><br />- 使用权限、内容有效期限和脱机访问设置|如果尚未这样做，请[将模板转换为标签](configure-policy-templates.md#to-convert-templates-to-labels)，然后执行以下操作<br /><br />1.更改标签名称和描述<br /><br />2.更改标签上的保护设置，以更改权限、有效期限和脱机访问设置。<br /><br />有关详细信息，请参阅[配置标签以进行 Rights Management 保护](configure-policy-protection.md#to-configure-a-label-for-rights-management-protection)。
|存档模板|将标签状态设置为“禁用”。
|创建作用域内模板|创建作用域内策略，并在作用域内创建应用保护的标签。 <br /><br />有关详细信息，请参阅[如何使用作用域内策略为特定用户配置 Azure 信息保护策略](configure-policy-scope.md)。
|复制模板|无法在 Azure 门户中复制模板。 如果希望两个标签具有相同的保护设置，则必须设置每个标签的权限。 <br /><br />有关详细信息，请参阅[配置标签以进行 Rights Management 保护](configure-policy-protection.md#to-configure-a-label-for-rights-management-protection)。
|删除模板|删除模板可能导致无法访问数据，因此 Azure 门户不支持此操作。 但是，可以删除标签，然后使用 PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) cmdlet 来删除模板。 <br /><br />有关详细信息，请参阅[如何删除或重排 Azure 信息保护的标签](configure-policy-delete-reorder.md)。
|多语言支持|从“管理”菜单选择中，选择“语言”，导出包含模板名称和描述的可自定义字段。 翻译字符串，然后将这些字符串导入门户。 <br /><br />有关详细信息，请参阅[如何在 Azure 信息保护中配置不同语言的标签和模板](configure-policy-languages.md)。
|Rights Management Web 报表|使用 PowerShell [Get-AadrmUsageLog ](/powershell/module/aadrm/Get-AadrmUsageLog) cmdlet 下载 Azure Rights Management 服务的使用日志。 然后可使用此数据创建自定义报表。 <br /><br />有关详细信息，请参阅[记录和分析 Azure 权限管理服务的使用情况](log-analyze-usage.md)。<br /><br />提示：查看[企业移动性和安全性博客](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection)上的公告，了解 Azure 信息保护新的集中式解决方案。 
|激活和停用 Rights Management 服务|从“管理”菜单选项中，选择“RMS 设置”或“保护激活”。 此选项正处于重命名的过程中。<br /><br />有关详细信息，请参阅[如何从 Azure 门户激活 Azure 权限管理](activate-azure.md)。

在编辑模板或将其转换为 Azure 门户中的标签之前，请参阅[Azure 门户中的模板的注意事项](configure-policy-templates.md#considerations-for-templates-in-the-azure-portal)。


## <a name="what-else-has-changed"></a>其他更改内容

Azure 门户中的新功能：

- 可以编辑为组织自动创建的[默认模板](configure-policy-templates.md#default-templates)。

- 可以将模板转换为标签，以便管理单个对象，而不是独立管理模板和标签。 有关说明，请参阅[将模板转换为标签](configure-policy-templates.md#to-convert-templates-to-labels)。

支持安全管理员角色：用户必须以 Azure 管理员身份登录 Azure 经典门户才能配置 Azure Rights Management，可以通过使用具有全局管理员或安全管理员角色的帐户登录 Azure 门户来配置 Azure 信息保护。 

用于创建和管理模板的 PowerShell cmdlet 以及激活或停用该服务的 PowerShell cmdlet 将继续受支持，不会更改。


## <a name="see-also"></a>另请参阅
有关详细信息，请参阅[使用 Azure 信息保护策略配置和管理模板](../deploy-use/configure-policy-templates.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]