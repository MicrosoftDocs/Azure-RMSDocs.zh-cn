---
title: 配置和管理 Azure 信息保护的模板 - AIP
description: 在 Azure 门户中配置和管理保护模板，也称为 rights management 模板。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 761927f4815460b5b83b17e7f7481e1ff3a0cf9e
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809704"
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>配置和管理用于 Azure 信息保护的模板

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标记客户端，请参阅 Microsoft 365 文档中的敏感标签中的 " [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels) " 和 ["限制对内容的访问](/microsoft-365/compliance/encryption-sensitivity-labels) "。 *

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>

保护模板（也称为 Rights Management 模板）是 Azure 信息保护的一组管理员定义的保护设置。 这些设置包括为授权用户选择的[使用权限](configure-usage-rights.md)，以及对到期和离线访问的访问控制。 这些模板已与 Azure 信息保护策略集成： 

**如果订阅包含分类、标签和保护 (Azure 信息保护 P1 或 P2)**：

- " **Azure 信息保护-标签**" 窗格中的标签后，"**保护模板**" 部分会显示未与租户的标签集成的模板。 若要导航到此窗格，请选择 "**分类**  >  **标签**" 菜单选项。 可以将这些模板转换为标签，也可以在为标签配置保护时链接到它们。 

**如果订阅仅包含保护 (包含 Azure Rights Management 服务) Microsoft 365 订阅**：

- 租户的模板显示在 " **Azure 信息保护-标签**" 窗格的 "**保护模板**" 部分中。 若要导航到此窗格，请选择 "**分类**  >  **标签**" 菜单选项。 不会显示任何标签。 还可看到特定于分类和标签的配置设置，但这些设置要么对模板没有任何影响，要么无法进行配置。 

>[!NOTE]
>在某些应用程序和服务中，你可能会看到 " [不转发](configure-usage-rights.md#do-not-forward-option-for-emails) " 和 " [仅加密](configure-usage-rights.md#encrypt-only-option-for-emails) " (**加密**) 显示为模板。 这些不是可以编辑或删除的模板，而是默认情况下随 Exchange 服务提供的选项。

## <a name="default-templates"></a>默认模板

当你为 Azure 信息保护或包含 Azure Rights Management 服务的 Microsoft 365 订阅获取订阅时，会为你的租户自动创建两个默认模板。 这些模板限制对你组织中授权用户的访问。 创建这些模板时，它们拥有为 [Azure 信息保护配置使用权限](configure-usage-rights.md#rights-included-in-the-default-templates) 文档中列出的权限。

此外，模板配置为允许为期七天的脱机访问，没有到期日期。

>[!NOTE]
> 可以更改这些设置以及默认模板的名称和说明。 Azure 经典门户曾无法使用此功能，且PowerShell 仍不支持该功能。

通过这些默认模板，你和其他人可立即轻松开始保护组织的敏感数据。 这些模板可与 Azure 信息保护标签一起使用，或通过可使用 Rights Management 模板的[应用程序和服务](applications-support.md)独立使用。

你还可以创建自已的自定义模板。 尽管可能只需要几个模板，但在 Azure 中可最多保存 500 个自定义模板。


### <a name="default-template-names"></a>默认模板名称

如果是最近获得的订阅，则使用以下名称创建默认模板：

- **机密\所有员工**

- **高度机密\所有员工**

如果在一段时间后获取了订阅，则可以创建具有以下名称的默认模板：

- **\<organization name> -机密**

- **\<organization name> -仅限机密查看** 

可以在使用 Azure 门户时重命名（和重新配置）这些默认模板。

>[!NOTE]
>如果未在 " **Azure 信息保护-标签** " 窗格中看到默认模板，则会将其转换为标签或链接到标签。 它们仍作为模板存在，但在 Azure 门户中，你会看到它们属于包含云密钥保护设置的标签配置。 你始终可以通过运行[AIPService PowerShell 模块](administer-powershell.md)中的[AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate) ，来确认你的租户的模板。
>
>可以手动转换模板（如后面部分[将模板转换为标签](#to-convert-templates-to-labels)中所述），然后对其重命名（如果需要）。 或者，如果最近创建了默认 Azure 信息保护策略，并且同时激活了租户的 Azure Rights Management 服务，则将自动转换这些模板。

存档的模板在 " **Azure 信息保护-标签** " 窗格中显示为不可用。 无法为标签选择这些模板，但可以将其转换为标签。

## <a name="considerations-for-templates-in-the-azure-portal"></a>Azure 门户中的模板的注意事项

在编辑这些模板或将其转换为标签之前，请确保了解以下更改和注意事项。 由于实现更改，因此如果你之前在 Azure 经典门户中管理模板，则以下列表尤其重要。

- 编辑或转换模板并保存 Azure 信息保护策略后，将对初始[使用权限](configure-usage-rights.md)进行以下更改。 如果需要，可以使用 Azure 门户添加或删除各个使用权限。 或者，将 PowerShell 与 [AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) 和 [AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) cmdlet 配合使用。
    
    - 自动添加了“允许宏”（公用名）。 Office 应用中的 Azure 信息保护栏需要此使用权限。

- **已发布** 和已 **存档** 的设置显示为 "**已启用** **"** 、"启用" 和 "**已启用**" **：分别在****标签** 窗格上 对于想要保留但对用户或服务不可见的模板，将其设置为“已启用”：“关闭”。

- 无法在 Azure 门户中复制或删除模板。 将模板转换为标签时，可以通过选择“为包含此标签的文档和电子邮件设置权限”选项的“未配置”配置该标签以停止使用该模板。 或者，可以删除标签。 但是，在这两种方案中，模板均不会被删除且模板仍保持已存档状态。
    
    使用 PowerShell [AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate) cmdlet 删除模板是 **永久性** 的。 还可以为未转换为标签的模板使用此 PowerShell cmdlet。 但是，为了确保能够按预期打开和使用以前受到保护的内容，通常建议不要删除模板。 最佳做法是仅当确定模板未用于保护生产中的文档或电子邮件时，才可删除模板。 在使用 PowerShell 永久删除模板之前，请考虑使用 [AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate) cmdlet 将模板导出为备份。 

- 目前，如果编辑并保存部门模板，则会删除作用域配置。 Azure 信息保护策略中的作用域内模板相当于[作用域内策略](configure-policy-scope.md)。 如果将模板转换为标签，则可以选择现有作用域。
    
    此外，无法通过 Azure 门户为部门模板设置应用程序兼容性设置。 如有必要，可以使用 [AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) Cmdlet 和 *EnableInLegacyApps* 参数来设置此应用程序兼容性设置。

- 将模板转换为标签或将模板链接到标签后，其他标签不能再使用该模板。 此外，此模板不再显示在“保护模板”部分中。 

- 不从“保护模板”部分创建新模板。 而是创建一个具有 " **保护** " 设置的标签，并从 " **保护** " 窗格配置使用权限和设置。 有关完整说明，请参阅[创建新模板](#to-create-a-new-template)。

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>在 Azure 信息保护策略中配置模板

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到 " **Azure 信息保护-标签** " 窗格。
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。

2. 从 "**分类**  >  **标签**" 菜单选项：在 " **Azure 信息保护-标签**" 窗格中，展开 "**保护模板**"，然后找到要配置的模板。
    
3. 选择模板，然后在 " **标签** " 窗格中，通过编辑 " **标签显示名称** " 和 " **说明**"，可以根据需要更改模板名称和说明。 然后，选择值为 " **Azure (云密钥)**" 的 "**保护**" 以打开 "**保护**" 窗格。

4. 在 " **保护** " 窗格上，可以更改权限、内容过期和脱机访问设置。 有关配置保护设置的详细信息，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)
    
    单击 **"确定"** 保存更改，然后在 " **标签** " 窗格中单击 " **保存**"。
    
> [!NOTE]
> 如果已将标签配置为使用预定义模板，则还可以使用 "**保护**" 窗格上的 "**编辑模板**" 按钮来编辑模板。 假如没有其他标签也同样使用选定的这一个模板，此按钮将模板转换为标签，并转到步骤 5。 若要深入了解将模板转换为标签时会发生什么情况，请参阅下一部分。

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

可以使用门户或使用 PowerShell 创建模板。 

### <a name="template-creation-using-powershell"></a>使用 PowerShell 创建模板

若要使用具有指定名称、说明、策略和所需状态设置的 PowerShell 创建新的保护模板，请使用 [AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate) cmdlet。 


### <a name="template-creation-using-the-portal"></a>使用门户创建模板

使用具有 **Azure (云密钥)** 的保护设置的门户创建新标签时，此操作将创建新的自定义模板，该模板随后可由与 Rights Management 模板集成的服务和应用程序进行访问。

1. 从 "**分类**  >  **标签**" 菜单选项：在 " **Azure 信息保护-标签**" 窗格中，选择 "**添加新标签**"。

2. 在 " **标签** " 窗格中，保留默认值 " **已启用**： **打开**"，然后输入模板名称和说明的标签名称和说明。

3. 对于“设置包含此标签的文档和电子邮件的权限”，选择“保护”，然后选择“保护”：
    
     ![为 Azure 信息保护标签配置保护](./media/info-protect-protection-bar-configured.png)

4. 在 " **保护** " 窗格上，可以更改权限、内容过期和脱机访问设置。 有关配置这些保护设置的详细信息，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)
    
    单击 **"确定"** 保存更改，然后在 " **标签** " 窗格中单击 " **保存**"。
    
    在 " **Azure 信息保护-标签** " 窗格中，你现在可以看到显示了 " **保护** " 列的新标签，指示它包含保护设置。 这些保护设置显示为支持 Azure Rights Management 服务的应用程序和服务的模板。
    
    虽然标签已启用，但默认情况下，模板已存档。 因此，应用程序和服务可以使用该模板来保护文档和电子邮件，完成发布模板的最后一步。

5. 从 "**分类**  >  **策略**" 菜单选项中，选择要包含新保护设置的策略。 然后选择“添加或删除标签”。 从 " **策略：添加或删除标签** " 窗格中，选择新创建的包含保护设置的标签，选择 **"确定"**，然后选择 " **保存**"。

## <a name="next-steps"></a>后续步骤

对运行 Azure 信息保护客户端的计算机而言，要获取这些更改的设置，可能最多耗时 15 分钟。 若要了解计算机和服务如何下载和刷新模板，请参阅[为用户和服务刷新模板](refresh-templates.md)。

可在 Azure 门户中配置的用于创建和管理模板的所有设置均可通过使用 PowerShell 实现。 此外，PowerShell 还提供了门户中未提供的更多选项。 有关详细信息，请参阅[保护模板的 PowerShell 参考](configure-templates-with-powershell.md)。 

有关配置 Azure 信息保护策略的详细信息，请使用[配置组织的策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。