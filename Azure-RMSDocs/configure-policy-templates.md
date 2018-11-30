---
title: 配置和管理 Azure 信息保护的模板
description: 通过 Azure 门户配置和管理 Rights Management 模板。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/29/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6e6200849a5d62001317708e000fbb7da4a7ac6d
ms.sourcegitcommit: e72c89e35cae6a19dca060f688838d78dc8f0448
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/29/2018
ms.locfileid: "52585969"
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>配置和管理 Azure 信息保护的模板

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

保护模板（也称为 Rights Management 模板）是 Azure 信息保护的一组管理员定义的保护设置。 这些设置包括为授权用户选择的[使用权限](configure-usage-rights.md)，以及对到期和离线访问的访问控制。 这些模板已与 Azure 信息保护策略集成： 

**订阅包含分类、设置标签和保护（Azure 信息保护 P1 或 P2）：**

- 未与租户的标签集成的模板显示在“Azure 信息保护 - 标签”边栏选项卡上标签后的“保护模板”部分。 要导航到此边栏选项卡，请选择“分类” > “标签”菜单选项。 可以将这些模板转换为标签，也可以在为标签配置保护时链接到它们。 

**订阅仅包含保护（包括 Azure 权限管理服务的 Office 365 订阅）：**

- 租户的模板显示在“Azure 信息保护 - 标签”边栏选项卡上的“保护模板”部分。 要导航到此边栏选项卡，请选择“分类” > “标签”菜单选项。 不显示任何标签。 还可看到特定于分类和标签的配置设置，但这些设置要么对模板没有任何影响，要么无法进行配置。 

>[!NOTE]
>在某些应用程序和服务中，你可能会看到[不转发](configure-usage-rights.md#do-not-forward-option-for-emails)和[仅加密](configure-usage-rights.md#encrypt-only-option-for-emails)（或加密）显示为模板。 这些不是可以编辑或删除的模板，而是默认情况下随 Exchange 服务提供的选项。

## <a name="default-templates"></a>默认模板

当你获得 Azure 信息保护订阅或获得包含 Azure Rights Management 服务的 Office 365 订阅时，会为你的租户自动创建两个默认模板。 这些模板限制对你组织中授权用户的访问。 创建这些模板时，它们拥有[为 Azure Rights Management 配置使用权限](configure-usage-rights.md#rights-included-in-the-default-templates)文档中列出的权限。

此外，模板配置为允许为期七天的脱机访问，没有到期日期。

>[!NOTE]
> 可以更改这些设置以及默认模板的名称和说明。 Azure 经典门户曾无法使用此功能，且PowerShell 仍不支持该功能。

通过这些默认模板，你和其他人可立即轻松开始保护组织的敏感数据。 这些模板可与 Azure 信息保护标签一起使用，或通过可使用 Rights Management 模板的[应用程序和服务](applications-support.md)独立使用。

你还可以创建自已的自定义模板。 尽管可能只需要几个模板，但在 Azure 中可最多保存 500 个自定义模板。


### <a name="default-template-names"></a>默认模板名称

如果是最近获得的订阅，则使用以下名称创建默认模板：

- 机密\所有员工，授予受保护内容的读取或修改权限。

- 高度机密\所有员工，授予受保护内容的只读权限。

如果是不久前获得的订阅，则使用以下名称创建默认模板：

- \<组织名称> - 机密，授予受保护内容的读取或修改权限。

- \<组织名称> - 机密（仅供查阅），授予受保护内容的只读权限。 

可以在使用 Azure 门户时重命名（和重新配置）这些默认模板。

>[!NOTE]
>如果没有在“Azure 信息保护 - 标签”边栏选项卡中看到默认模板，则这些模板已转换为标签或链接到标签。 它们仍作为模板存在，但在 Azure 门户中，你会看到它们属于包含云密钥保护设置的标签配置。 可以始终通过从 [AADRM PowerShell 模块](administer-powershell.md)运行 [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) 来确认租户具有哪些模板。
>
>可以手动转换模板（如后面部分[将模板转换为标签](#to-convert-templates-to-labels)中所述），然后对其重命名（如果需要）。 或者，如果最近创建了默认 Azure 信息保护策略，并且同时激活了租户的 Azure Rights Management 服务，则将自动转换这些模板。

存档的模板在“Azure 信息保护 - 标签”边栏选项卡中显示为不可用。 无法为标签选择这些模板，但可以将其转换为标签。

## <a name="considerations-for-templates-in-the-azure-portal"></a>Azure 门户中的模板的注意事项

在编辑这些模板或将其转换为标签之前，请确保了解以下更改和注意事项。 由于实现更改，因此如果你之前在 Azure 经典门户中管理模板，则以下列表尤其重要。

- 编辑或转换模板并保存 Azure 信息保护策略后，将对初始[使用权限](configure-usage-rights.md)进行以下更改。 如果需要，可以通过使用 Azure 门户来添加或删除各使用权限。 或者，在 PowerShell 中使用 [New-aadrmrightsdefinition](/powershell/module/aadrm/new-aadrmrightsdefinition) 和 [Set-aadrmtemplateproperty](/powershell/module/aadrm/set-aadrmtemplateproperty) cmdlet。
    
    - 自动添加了“允许宏”（公用名）。 Office 应用中的 Azure 信息保护栏要求此使用权限。

- “发布”和“已存档”设置在“标签”边栏选项卡上分别显示为“已启用: 打开”和“已启用: 关闭”。 对于想要保留但对用户或服务不可见的模板，将其设置为“已启用”：“关闭”。

- 无法在 Azure 门户中复制或删除模板。 将模板转换为标签时，可以通过选择“为包含此标签的文档和电子邮件设置权限”选项的“未配置”配置该标签以停止使用该模板。 或者，可以删除标签。 但是，在这两种方案中，模板均不会被删除且模板仍保持已存档状态。
    
    现在可以通过使用 PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) cmdlet 删除模板。 还可以为未转换为标签的模板使用此 PowerShell cmdlet。 但是，如果删除已用于保护内容的模板，则不能再打开该内容。 仅当确定模板未用于保护生产中的文档或电子邮件时，才可删除模板。 作为一种预防措施，建议考虑首先使用 [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate) cmdlet 将模板作为备份导出。 

- 目前，如果编辑并保存部门模板，则会删除作用域配置。 Azure 信息保护策略中的作用域内模板相当于[作用域内策略](configure-policy-scope.md)。 如果将模板转换为标签，则可以选择现有作用域。
    
    此外，无法通过 Azure 门户为部门模板设置应用程序兼容性设置。 如有必要，可以使用 [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) cmdlet 和 EnableInLegacyApps 参数来设置应用程序兼容性设置。

- 将模板转换为标签或将模板链接到标签后，其他标签不能再使用该模板。 此外，此模板不再显示在“保护模板”部分中。 

- 不从“保护模板”部分创建新模板。 而是创建一个具有“保护”设置的标签，并从“保护”边栏选项卡配置使用权限和设置。 有关完整说明，请参阅[创建新模板](#to-create-a-new-template)。

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>在 Azure 信息保护策略中配置模板

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护 - 标签”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“分类” > “标签”菜单选项：在“Azure 信息保护 - 标签”边栏选项卡上，展开“保护模板”，然后找到要配置的模板。
    
3. 选择模板，在“标签”边栏选项卡上，通过编辑“标签显示名称”和“说明”，可以根据需要更改模板名称和说明。 然后，选择值为“Azure (云密钥)”的“保护”，打开“保护”边栏选项卡。

4. 在“保护”边栏选项卡上，可以更改权限、内容有效期限和脱机访问设置。 有关配置保护设置的详细信息，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)
    
    单击“确定”保留所做更改，然后在“标签”边栏选项卡上单击“保存”。
    
> [!NOTE]
> 如果已将某个标签配置为使用预定义模板，则也可以使用“保护”边栏选项卡上的“编辑模板”按钮来编辑模板。 假如没有其它标签也同样使用选定的这一个模板，此按钮将模板转换为标签，并转到步骤 5。 若要深入了解将模板转换为标签时会发生什么情况，请参阅下一节。

## <a name="to-convert-templates-to-labels"></a>将模板转换为标签

如果订阅包含分类、设置标签和保护，可将模板转换为标签。 转换模板时，将保留原始模板，但在 Azure 门户中，它现在会显示为新标签的一部分。

例如，如果你要转换一个名为“市场营销”的标签（该标签向市场营销组授予使用权限），那么在 Azure 门户中，它将显示为具有相同保护设置的名为“市场营销”的标签。 可以在模板中更改新创建标签的保护设置，使用此模板的任何用户或服务在下一次模板刷新时都会获取新保护设置。 

不要求将所有模板都转换为标签，但当你执行此操作时，保护设置会与标签的完整功能完全集成，这样你就不必单独维护设置。

若要将模板转换为标签，右键单击相应模板，然后选择“转换为标签”。 或者使用上下文菜单选择此选项。 

使用“编辑模板”按钮还可在配置保护标签和预定义模板时将模板转换为标签。 

将模板转换为标签时：

- 模板的名称转换为新的标签名称，并且模板说明转换为标签工具提示。 

- 如果模板的状态已发布，此设置会映射到标签的“已启用: 打开”，当你下次发布 Azure 信息保护策略时，该设置向用户显示为此标签。 如果模板的状态已存档，则此设置映射到标签的“已启用: 关闭”，不会显示为用户可用的标签。

- 会保留保护设置，你可以根据需要进行编辑，还可以添加其他标签设置，如视觉对象标记和条件。

- 为标签配置保护时，原始模板不再显示在“保护模板”中，且不能选择为预定义模板。 若要在 Azure 门户中编辑此模板，现在编辑在转换模板时创建的标签。 该模板仍可用于 Azure 权限管理服务，仍然可以使用 [PowerShell 命令](administer-powershell.md)进行管理。  

## <a name="to-create-a-new-template"></a>创建新模板

创建一个具有 Azure（云密钥）保护设置的新标签时，此操作会在后台创建一个新的自定义模板，集成了 Rights Management 模板的服务和应用程序都可以访问该模板。

1. 从“分类” > “标签”菜单选项：在“Azure 信息保护 - 标签”边栏选项卡上，选择“添加新标签”。

2. 在“标签”边栏选项卡中，保持默认值“已启用: 打开”，然后输入标签名称和说明用作模板名称和说明。

3. 对于“设置包含此标签的文档和电子邮件的权限”，选择“保护”，然后选择“保护”：
    
     ![为 Azure 信息保护标签配置保护权限](./media/info-protect-protection-bar-configured.png)

4. 在“保护”边栏选项卡上，可以更改权限、内容有效期限和脱机访问设置。 有关配置这些保护设置的详细信息，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)
    
    单击“确定”保留所做更改，然后在“标签”边栏选项卡上单击“保存”。
    
    在“Azure 信息保护 - 标签”边栏选项卡上，现在会看到在“保护”列中显示的新标签，指明它包含保护设置。 这些保护设置显示为支持 Azure Rights Management 服务的应用程序和服务的模板。
    
    虽然标签已启用，但默认情况下，模板已存档。 因此，应用程序和服务可以使用该模板来保护文档和电子邮件，完成发布模板的最后一步。

5. 从“分类” > “策略”菜单选项中，选择要包含新保护设置的策略。 然后选择“添加或删除标签”。 从“策略: 添加或删除标签”边栏选项卡上，选择新创建的标签，其中包含你的保护设置，单击“确定”，然后选择“保存”。

## <a name="next-steps"></a>后续步骤

对运行 Azure 信息保护客户端的计算机而言，要获取这些更改的设置，可能最多耗时 15 分钟。 有关计算机和服务如何下载并刷新模板的信息，请参阅[为用户和服务刷新模板](refresh-templates.md)。

可在 Azure 门户中配置的用于创建和管理模板的所有设置均可通过使用 PowerShell 实现。 此外，PowerShell 还提供了门户中未提供的更多选项。 有关详细信息，请参阅[保护模板的 PowerShell 参考](configure-templates-with-powershell.md)。 

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

