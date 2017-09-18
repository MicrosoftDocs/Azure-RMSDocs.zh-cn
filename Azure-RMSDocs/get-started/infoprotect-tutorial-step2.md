---
title: "快速入门教程步骤 2 - AIP"
description: "快速试用 Azure 信息保护入门教程步骤 2 - 配置策略。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/12/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
ms.openlocfilehash: cf84cef5d6bc4d3df32a4e3c8bc3a6ac7380655c
ms.sourcegitcommit: 94a9b6714c555b95f6064088e77ed94f08224a15
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2017
---
# <a name="step-2-configure-and-publish-the-azure-information-protection-policy"></a>步骤 2：配置并发布 Azure 信息保护策略

>适用于：Azure 信息保护

尽管 Azure 信息保护附带了你无需进行配置的默认策略，我们仍然要看一下该策略并进行一些更改。

1. 仍然在 Azure 门户中，选择“全局策略”，打开“策略: 全局”边栏选项卡。 此边栏选项卡将自动打开，以便执行后续连接到服务的操作，它将显示为租户创建的默认信息保护策略。

2. 花几分钟时间了解显示的标签：
    
    - 用于分类的标签：“个人”、“公共”、“常规”、“机密”和“高度机密”。 最后两个标签展开可显示子标签，这提供了有关如何使分类具有子类别的示例：
    
       > [!NOTE]
       > 你的默认策略可能与本教程中的默认策略稍有不同。 例如，你有名为“内部”的标签，而没有“常规”标签，有“秘密”标签而没有“高度机密”标签。 也许没有名为“仅收件人”的子标签，或者根本没有任何标签。 这些变化是因为存在不同版本的默认策略，具体取决于为租户创建默认策略的时间。 或者在开始本教程之前，已自行对其进行编辑。
       > 
       > 如果你的默认策略不同，仍可使用本教程，但使用其中的说明和图片时，应注意这些更改。 如果要修改自己默认策略以符合当前的默认策略，请参阅[默认 Azure 信息保护策略](../deploy-use/configure-policy-default.md)。
    
    - 在默认配置中，某些标签未配置视觉标记。 视觉标记即页脚、页眉和水印。 某些标签可能设置了保护，具体取决于默认策略。 例如： 
    
    ![Azure 信息保护快速入门教程步骤 3 - 默认策略](../media/info-protect-policy-default-labelsv2.png)
    
3. 还看到并未设置某些策略设置。 并非所有文档和电子邮件都需要标签，没有默认标签，用户更改标签时无需提供理由：
    
    ![Azure 信息保护快速入门教程步骤 3 - 默认策略](../media/info-protect-policy-default-settings.png)

## <a name="changing-the-settings-for-a-default-label-and-prompt-for-justification"></a>更改默认标签和有关提示用户提供理由的设置

在本教程中，将更改几个策略设置，以便可以看到它们的工作原理：

1. 对于“选择默认标签”，请选择“常规”。 

    如果因使用旧版本的策略而不具有此标签，请选择“内部”作为等效标签。

2. 对于“用户必须提供设置较低分类标签、删除标签或删除保护的理由”，请将此选项设置为“开”。

## <a name="creating-a-new-label-for-protection-visual-markers-and-a-condition-to-prompt-for-classification"></a>创建新标签，设置保护、视觉标记和分类提示条件

现在，将为“机密”创建一个新的子标签。

1. 右键单击“机密”标签，然后选择“添加子标签”。
    
    如果没有名为“机密”的标签，可以选择另一个标签，或者可以创建一个新标签，具体操作步骤仍与本教程相同，只存在细微差异。

2. 在“子标签”边栏选项卡上，指定标签名称“财务”，并添加以下说明：“机密数据，包含仅限于员工的财务信息”。
    
    此文本说明应如何使用所选标签，并显示为一个工具提示，帮助用户确定要选择的标签。

3. 对于“设置包含此标签的文档和电子邮件的权限”，选择“保护”，然后选择“保护”：
    
    ![为 Azure 信息保护标签配置的保护](../media/info-protect-protection-bar-configured.png) 
    
4. 在“保护”边栏选项卡中，确保选中“Azure RMS”或“Azure (云密钥)”。 此选项正处于重命名的过程中。 此外，请确保也选中“设置权限”。 然后选择“添加权限”。

5. 在“添加权限”边栏选项卡上，选择“添加 \<组织名称> - 所有成员”。 例如，如果组织名称为 VanArsdel Ltd，则会看到以下选项可供选择：
    
    ![为所有成员授予 Azure 信息保护标签保护权限](../media/info-protect-protection-all-members.png) 
    
    此选项会自动选择组织中可以被授予权限的所有用户。 但是，可通过其他选项了解到，能浏览并搜索租户中的组或用户。 或者，选择“输入详细信息”选项时，可以指定单个电子邮件地址，甚至可指定来自另一个组织的所有用户。

6. 对于权限，请在预设选项中选择“审阅者”。 可了解此权限级别如何自动授予部分列出的权限而不是所有权限：
    
    ![为合著者授予 Azure 信息保护标签保护权限](../media/info-protect-protection-reviewer.png)
    
    使用“自定义”选项，可选择不同的权限级别或指定个人使用权限。 但对于本教程，请保持选中“审阅者”选项。 稍后可以尝试不同的权限，并了解它们如何限制指定用户对受保护文档或电子邮件可执行的操作。

7. 单击“确定”关闭“添加权限”边栏选项卡，可看到“保护”边栏选项卡如何更新以反映配置。 例如：
    
     ![显示 Azure 信息保护标签权限配置的“保护”边栏选项卡](../media/info-protect-protection-configured.png)
    
    如果选择“添加权限”，则会再次打开“添加权限”边栏选项卡，以便可以添加更多用户并向他们授予不同的权限。 例如，为特定组授予仅查看访问权限。 但对于本教程，将为所有用户保留一组权限。

8. 查看并保留内容有效期限和脱机访问的默认值，然后单击“确定”，保存并关闭此“保护”边栏选项卡。

8. 返回“子标签”边栏选项卡，找到“设置视觉标记”部分：
    
    对于“包含此标签的文档具有页脚”设置，请单击“开”，然后在“文本”框中键入“分类为机密”。 
    
    对于“使用该标签的文档具有一个水印”设置：单击“开”，然后在“文本”框中键入你的组织名称。 例如，VanArsdel, Ltd 
    
    尽管可以更改视觉标记的外观，但是我们将暂时使用这些设置的默认值。
    
9. 定位到“配置条件以自动应用该标签”部分：
    
    单击“添加新条件”，然后在“条件”边栏选项卡中选择以下选项：
    
    a. “选择条件类型”：保留默认设置“信息类型”。
    
    b。 在“选择信息类型”搜索框中：键入“信用卡号”。 然后，从搜索结果中选择“信用卡号”。
    
    c. “最小出现次数” ：保留默认值“1”。
    
    d. “仅计算唯一值的发生次数”：保留默认设置“关闭”。
    
    ![Azure 信息保护快速入门教程步骤 3 - 配置信用卡条件](../media/step2-configure-condition.png)
    
    单击“保存”返回到“子标签”边栏选项卡。

10. 在“子标签”边栏选项卡中，会看到“信用卡号”显示为“条件名称”，“出现次数”为“1”：
    
    ![Azure 信息保护快速入门教程步骤 3 - 配置信用卡条件](../media/step2-see-condition.png)

11. 对于“选择应用此标签的方式”：保留默认设置“推荐”，并且不要更改默认策略提示。 

12. 在“输入内部管理的注释”框中，键入“仅用于测试”。

13. 在此“子标签”边栏选项卡上单击“保存”。 然后在“策略: 全局”边栏选项卡上，再次单击“保存”。
    
    现在看到新的子标签，它配置了视觉标记和保护。 例如：

    ![Azure 信息保护快速入门教程步骤 3 - 已配置默认策略](../media/info-protect-policy-configuredv2.png)
    
    还可以看到已根据对默认标签的更改和更改理由配置设置：
    
    ![Azure 信息保护快速入门教程步骤 3 - 配置设置](../media/info-protect-settings-configuredv2.png)
    
14. 现在已做出更改并进行了保存，希望将更改提供给用户，因此请单击“发布”，然后单击“是”确认发布。

    ![Azure 信息保护快速入门教程步骤 3 - 发布配置的策略](../media/info-protect-publish.png)

完成本教程后你可以关闭 Azure 门户，或将其保留为打开状态以尝试其他配置选项。

现在你已经了解了默认策略并进行了一些更改，下一步是安装 Azure 信息保护客户端。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于默认策略和不同版本|[默认 Azure 信息保护策略](../deploy-use/configure-policy-default.md)|
|有关策略的配置选项|[配置 Azure 信息保护策略](../deploy-use/configure-policy.md)|
|配置标签以进行保护的详细说明|[如何配置标签以进行 Rights Management 保护](../deploy-use/configure-policy-protection.md)|
|有关权限的详细信息|[为 Azure Rights Management 配置使用权限](../deploy-use/configure-usage-rights.md)|



>[!div class="step-by-step"]
[&#171; 步骤 1](infoprotect-tutorial-step1.md)
[步骤 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]