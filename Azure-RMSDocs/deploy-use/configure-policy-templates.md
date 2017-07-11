---
title: "配置并管理 Azure 信息保护策略中的模板"
description: "目前在预览版中，可以通过 Azure 信息保护策略配置和管理权限管理模板。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 1f41aad2d132e087e9122b2683be4b45185527de
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
<a id="configuring-and-managing-templates-in-the-azure-information-protection-policy" class="xliff"></a>

# 在 Azure 信息保护策略中配置和管理模板

>*适用于：Azure 信息保护*

>[!NOTE]
>此功能目前为预览版，可能会进行频繁更改。
>
>使用在 Azure 经典门户中创建的自定义模板测试此预览功能之前，请考虑是否具有模板的最新备份。 可以使用 [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate) PowerShell cmdlet 备份自定义模板，如有必要，使用 [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate) 还原它们。
>
>由于实现方式存在差异，我们不建议你通过 Azure 经典门户和 Azure 门户管理相同的模板。


权限管理模板现已与 Azure 信息保护策略集成。 

**订阅包含分类、设置标签和保护（Azure 信息保护 P1 或 P2）：**

- 设置标签后，租户的权限管理模板显示在新“模板”部分。 你可以将这些模板转换为标签，也可以将其作为单独的模板继续管理，并在为标签配置保护时链接到它们。 

**订阅仅包含保护（包括 Azure 权限管理服务的 Office 365 订阅）：**

- 租户的权限管理模板显示为标签，目前也可以使用特定于分类和设置标签的配置设置。 


<a id="considerations-for-templates-in-the-azure-portal" class="xliff"></a>

## Azure 门户中的模板的注意事项

在 Azure 门户中编辑这些模板或将其转换为标签之前，在 Azure 经典门户中管理模板时，请注意实现过程中的以下更改。 预期会在预览期间解决一些限制问题：

- 编辑或转换模板并保存 Azure 信息保护策略后，将对初始[使用权限](configure-usage-rights.md)进行以下更改。 如有必要，可以使用 PowerShell 的 [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) 和 [Set-AadrmTemplatePropert](/powershell/module/aadrm/new-aadrmrightsdefinition) cmdlet 添加或删除个人使用权限。
    
    - 删除了“另存为”、“导出”（公用名）。 在 Azure 门户中，无法手动指定此使用权限，但它包含在“完全控制”使用权限中，如果适用，可以添加该权限。
    
    - 自动添加了“允许宏”（公用名）。 Office 应用中的 Azure 信息保护栏要求此使用权限。
    
- 目前可以显示默认模板，但无法进行编辑或转换。 

- 无法复制或删除模板。 要删除模板，请使用 PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) cmdlet。 

- 目前，使用 Azure 经典门户或 PowerShell 为语言配置的模板不会显示这些语言的名称和说明，但会保留这些信息。

- “发布”和“已存档”设置在“标签”边栏选项卡上分别显示为“已启用: 打开”和“已启用: 关闭”。

- 在全局策略中显示部门模板（为作用域配置的模板）。 目前，如果编辑并保存部门模板，则会删除作用域配置。 Azure 信息保护策略中的作用域内模板相当于[作用域内策略](configure-policy-scope.md)。 如果将模板转换为标签，则可以选择现有作用域。
    
    此外，目前无法设置部门模板的应用程序兼容性设置。 如有必要，可以使用 PowerShell 的 [Set-aadrmtemplateproperty](/powershell/module/aadrm/set-aadrmtemplateproperty) cmdlet 进行设置。

- 不会从“模板”容器创建新模板；而是创建一个具有保护设置的标签，并从“保护”边栏选项卡配置使用权限和设置。 有关完整说明，请参阅[创建新模板](#to-create-a-new-template)。

<a id="to-configure-the-templates-in-the-azure-information-protection-policy" class="xliff"></a>

## 在 Azure 信息保护策略中配置模板

1. 在新浏览器窗口中，以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。

2. 导航到“Azure 信息保护”边栏选项卡：例如，在中心菜单上，单击“更多服务”并在“筛选”框中开始键入**信息保护**。 在结果中选择“Azure 信息保护”。 

2. 如果要配置的模板将应用于所有用户，请选择“Azure 信息保护”边栏选项卡中的“全局”。 不过，如果要配置的模板包含在[作用域内策略](configure-policy-scope.md)中，以便仅应用于选定用户，请改为选择作用域内策略。

3. 在策略边栏选项卡上，找到想要配置的模板：
    
    - 如果订阅包含分类、设置标签和保护：在设置标签后展开模板。
    
    - 如果订阅仅包含保护：模板显示为标签。

4. 选择模板，在“标签”边栏选项卡上，通过编辑“标签名称”和“说明”，可以根据需要更改模板名称和说明。 然后，选择值为 Azure RMS 的保护，打开“保护”边栏选项卡。

5. 在“保护”边栏选项卡上，可以更改权限、内容有效期限和脱机访问设置。 有关配置保护设置的详细信息，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)
    
    单击“确定”保留所做更改，然后在“标签”边栏选项卡上单击“保存”。

6. 若要使所做的更改适用于用户应用程序和服务，在“Azure 信息保护”边栏选项卡上单击“发布”。

<a id="to-convert-templates-to-labels" class="xliff"></a>

## 将模板转换为标签

如果订阅包含分类、设置标签和保护，可将模板转换为标签。 执行此操作时，将保留原始模板，但在 Azure 门户中，它现在显示为新标签的一部分。

例如，如果你要转换一个名为“市场营销”的标签（该标签向市场营销组授予使用权限），那么在 Azure 门户中，它将显示为具有相同保护设置的名为“市场营销”的标签。 可以在模板中更改新创建标签的保护设置，使用此模板的任何用户或服务在下一次模板刷新时都会获取新保护设置。 

不要求将所有模板都转换为标签，但当你执行此操作时，保护设置会与标签的完整功能完全集成，这样你就不必单独维护设置。

若要将模板转换为标签，右键单击相应模板，然后选择“转换为标签”。 或者使用上下文菜单选择此选项。

将模板转换为标签时：

- 模板的名称转换为新的标签名称，并且模板说明转换为标签工具提示。 

- 如果模板的状态已发布，此设置会映射到标签的“已启用: 打开”，当你下次发布 Azure 信息保护策略时，该设置向用户显示为此标签。 如果模板的状态已存档，则此设置映射到标签的“已启用: 关闭”，不会显示为用户可用的标签。

- 会保留保护设置，你可以根据需要进行编辑，还可以添加其他标签设置，如视觉对象标记和条件。

- 原始模板不再显示在“模板”下，要在 Azure 门户中进行编辑，现在可以编辑已创建的标签。 该模板仍可用于 Azure 权限管理服务，仍然可以使用 [PowerShell 命令](administer-powershell.md)进行管理。  

<a id="to-create-a-new-template" class="xliff"></a>

## 创建新模板

创建一个具有 Azure RMS 保护设置的新标签时，它会在后台创建一个新的自定义模板，集成了 Rights Management 模板的服务和应用程序都可以访问该模板。

1. 如果要将创建的新模板应用于所有用户，请在“策略: 全局”边栏选项卡上单击“添加新标签”。
    
     如果要创建的新模板是部门模板，并且要使其仅适用于所选用户，请首先从初始“Azure 信息保护”边栏选项卡中选择或创建作用域内策略。

2. 在“标签”边栏选项卡上，保留默认值“已启用: 打开”以发布此新模板，或将此设置更改为“关闭”，创建该模板作为已存档模板。 然后输入标签名称和说明用作模板名称和说明。

3. 对于“设置包含此标签的文档和电子邮件的权限”，选择“保护”，然后选择“保护”：
    
     ![为 Azure 信息保护标签配置保护权限](../media/info-protect-protection-bar.png)

4. 在“保护”边栏选项卡上，可以更改权限、内容有效期限和脱机访问设置。 有关配置这些保护设置的详细信息，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)
    
    单击“确定”保留所做更改，然后在“标签”边栏选项卡上单击“保存”。

5. 若要使这些模板适用于用户应用程序和服务，在“Azure 信息保护”边栏选项卡上单击“发布”。


<a id="next-steps" class="xliff"></a>

## 后续步骤

与 Azure 信息保护策略的所有更改一样，运行 Azure 信息保护客户端的计算机可能需要 15 分钟才能完成下载这些模板的操作。 有关计算机和服务如何下载并刷新模板的信息，请参阅[为用户和服务刷新模板](refresh-templates.md)。

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
