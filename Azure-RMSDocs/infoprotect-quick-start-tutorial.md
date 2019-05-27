---
title: 教程 - 编辑 Azure 信息保护策略 - AIP
description: 介绍如何为组织编辑 Azure 信息保护策略的入门教程，大概需要 15 分钟完成。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/20/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 10fa599831a57291d6e89574b2d57a1db025b2ac
ms.sourcegitcommit: fe23bc3e24eb09b7450548dc32b4ef09c8970615
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2019
ms.locfileid: "65934815"
---
# <a name="tutorial-configure-azure-information-protection-policy-settings-and-create-a-new-label"></a>教程：配置 Azure 信息保护策略设置并创建新标签

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：  [适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

在本教程中，你将了解如何执行以下操作：
> [!div class="checklist"]
> * 配置策略设置
> * 创建新标签 
> * 配置视觉标记、建议分类和保护的标签
> * 在实际操作中查看设置和标签

完成此配置后，用户在创建新文档或电子邮件时会看到应用的默认标签。 但是，当检测到信用卡信息时，系统会提示用户应用新标签。 应用新标签时，内容将重新分类并受到保护，还会带有相应的页脚和水印。 

完成本教程需要 15 分钟。

## <a name="prerequisites"></a>必备条件 

若要完成本教程，你需要：

1. 包含 Azure 信息保护计划 2 的订阅。
    
    如果没有包含 Azure 信息保护计划 2 的订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

2. 已将“Azure 信息保护”边栏选项卡添加到 Azure 门户，并确认已激活保护服务。

    如果在执行这些操作时需要帮助，请参阅[快速入门：将 Azure 信息保护添加到 Azure 门户和查看策略](quickstart-viewpolicy.md)

3. 计算机上已安装 Azure 信息保护客户端。 
    
    可以转到 [Microsoft下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)，然后从“Azure 信息保护”页下载 AzInfoProtection.exe  ，安装客户端。

4. 一台运行 Windows（最低配置为 Windows 7 Service Pack 1）的计算机，并在此计算机上，从以下类别之一登录到 Office 应用程序：
    
    - Office 应用最低版本 1805，Office 365 商业版或 Microsoft 365 商业版中的内部版本 9330.2078，前提是已为你分配了 Azure Rights Management（亦称为“适用于 Office 365 的 Azure 信息保护”）许可证。
    
    - Office 365 专业增强版。
    
    - Office 专业增强版 2019。
    
    - Office Professional Plus 2016。
    
    - Office Professional Plus 2013 Service Pack 1。
    
    - Office Professional Plus 2010 Service Pack 2。

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。

让我们开始吧。

## <a name="edit-the-azure-information-protection-policy"></a>编辑 Azure 信息保护策略

使用 Azure 门户，首先更改几项策略设置，然后创建一个新标签。

### <a name="edit-the-policy-settings"></a>编辑策略设置

1. 打开新的浏览器窗口，以全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。然后导航到“Azure 信息保护”  。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”   。 选择“Azure 信息保护”。 
    
    如果你不是全局管理员，请使用以下链接获取替代角色：[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)

2. 选择“分类”   > “策略”   > “全局”  ，打开“策略: 全局”边栏选项卡  。 

3. 在“配置要对信息保护最终用户显示和应用的设置”  部分中，找到位于标签后面的策略设置。 
    
    记下设置的当前配置方式。 具体来说，是“选择默认标签”  和“用户必须提供设置较低分类标签、删除标签或删除保护的理由”  这两项设置。 例如：
    
    ![Azure 信息保护教程 - 要更改的策略设置](./media/info-protect-policy-default-settings.png)
    
    我们会在本教程后面使用这些策略设置，你将在实际操作看到相应设置。

4. 对于“选择默认标签”，请选择“常规”   。 

    如果因使用旧版本的策略而不具有此标签，请选择“内部”  作为等效标签。

5. 对于“用户必须提供设置较低分类标签、删除标签或删除保护的理由”  ，请将此选项设置为“开”  （如果还不是此设置）。

6. 另外，请务必将“在 Office 应用程序中显示信息保护栏”这一项  设置为“开”  。

7. 选择此“策略: 全局”边栏选项卡上的“保存”  ，  如果系统提示你确认操作，请选择“确定”  。 关闭此边栏选项卡。

### <a name="create-a-new-label-for-protection-visual-markers-and-a-condition-to-prompt-for-classification"></a>创建保护新标签、视觉标记和分类提示条件

现在，将为“机密”  创建一个新的子标签。

1. 从“分类” > “标签”菜单选项中   ：右键单击“机密”标签，然后选择“添加子标签”   。
    
    如果没有名为“机密”  的标签，可以选择另一个标签，也可以创建一个新标签，具体操作步骤仍与本教程相同，只存在细微差异。

2. 在“子标签”  边栏选项卡上，指定“财务”  的标签名称，并添加以下说明：包含财务信息的机密数据仅限员工使用  。
    
    此文本说明应如何使用所选标签，并显示为一个工具提示，帮助用户确定要选择的标签。

3. 对于“为包含此标签的文档和电子邮件设置权限”  ，选择“保护”  ，这会在为你选择“保护”选项时，自动打开“保护”  边栏选项卡  ：
    
    ![配置 Azure 信息保护标签以进行保护](./media/info-protect-protection-bar-configured.png) 
    
4. 在“保护”边栏选项卡中，确保选中“Azure (云密钥)”   。 此选项使用 Azure Rights Management 服务保护文档和电子邮件。 还请务必选择“设置权限”选项  。 然后选择“添加权限”  。

5. 在“添加权限”边栏选项卡上，选择“添加 \<组织名称> - 所有成员”   。 例如，如果组织名称为 VanArsdel Ltd，则会看到以下选项可供选择：
    
    ![为所有成员授予 Azure 信息保护标签保护权限](./media/info-protect-protection-all-members.png) 
    
    此选项会自动选择组织中可以被授予权限的所有用户。 但是，可通过其他选项了解到，能浏览并搜索租户中的组或用户。 或者，选择“输入详细信息”选项时，可以指定单个电子邮件地址，甚至可指定来自另一个组织的所有用户  。

6. 对于权限，请在预设选项中选择“审阅者”  。 可了解此权限级别如何自动授予部分列出的权限而不是所有权限：
    
    ![为合著者授予 Azure 信息保护标签保护权限](./media/info-protect-protection-reviewer.png)
    
    使用“自定义”选项，可选择不同的权限级别或指定个人使用权限  。 但对于本教程，请保持选中“审阅者”选项  。 稍后可以尝试不同的权限，并了解它们如何限制指定用户对受保护文档或电子邮件可执行的操作。

7. 单击“确定”关闭“添加权限”边栏选项卡，可看到“保护”边栏选项卡如何更新以反映配置    。 例如：
    
     ![显示 Azure 信息保护标签权限配置的“保护”边栏选项卡](./media/info-protect-protection-configured.png)
    
    如果选择“添加权限”  ，此操作会再次打开“添加权限”  边栏选项卡，以方便添加更多用户，并向他们授予不同的权限。 例如，为特定组授予仅查看访问权限。 但对于本教程，将为所有用户保留一组权限。

8. 查看并保留内容有效期限和脱机访问的默认值，然后单击“确定”，保存并关闭此“保护”边栏选项卡   。

8. 返回“子标签”边栏选项卡，找到“设置视觉标记”部分   ：
    
    对于“包含此标签的文档具有页脚”设置，请单击“开”，然后在“文本”框中键入“分类为机密”     。 
    
    对于“使用该标签的文档具有一个水印”  设置：单击“开”  ，然后在“文本”  框中键入你的组织名称。 例如，VanArsdel, Ltd  
    
    尽管可以更改视觉标记的外观，但是我们将暂时使用这些设置的默认值。
    
9. 定位到“配置条件以自动应用该标签”  部分：
    
    单击“添加新条件”，然后在“条件”边栏选项卡中选择以下选项   ：
    
    a. **选择条件类型**：保留默认值“信息类型”  。
    
    b. 对于“选择行业”  ：保留默认值“全部”  。
    
    c. 在“选择信息类型”  搜索框中：键入“信用卡卡号”  。 然后，从搜索结果中选择“信用卡号”  。
    
    d. **最少出现次数**：保留默认值“1”  。
    
    e. **仅计算唯一值的发生次数**：保留默认值“关闭”  。
    
    ![Azure 信息保护教程 - 配置信用卡条件](./media/step2-configure-condition.png)
    
    单击“保存”返回到“子标签”边栏选项卡   。

10. 在“子标签”边栏选项卡中，会看到“信用卡号”显示为“条件名称”，“出现次数”为“1”      ：
    
    ![Azure 信息保护教程 - 信用卡条件摘要](./media/step2-see-condition.png)

11. 对于**选择应用此标签的方式**：保留默认设置“推荐”  ，并且不要更改默认策略提示。 

12. 在“添加备注以供管理员使用”  框中，键入“仅用于测试目的”  。

13. 在此“子标签”边栏选项卡上单击“保存”   。 如果系统提示你确认，请单击“确定”  。 将创建和保存新标签，但尚未将其添加到策略。

14. 从“分类” > “策略”菜单选项中   ：再次选择“全局”  ，然后选择标签后的“添加或删除标签”  链接。

15. 从“策略:  添加或删除标签”边栏选项卡中，选择刚刚创建的标签（名为“财务”  的子标签），然后单击“确定”  。

16. 在“策略:**全局”** 边栏选项卡上，现在可以在全局策略中看到针对视觉标记和保护配置的新子标签。 例如：

    ![Azure 信息保护教程 - 新建子标签](./media/info-protect-policy-configuredv2.png)
    
    还可以看到对默认标签和理由配置的设置：
    
    ![Azure 信息保护教程 - 配置的设置](./media/info-protect-settings-configuredv2.png)
    

17. 单击此“策略: 全局”边栏选项卡上的“保存”   。 如果系统提示你确认此操作，请单击“确定”  。

完成本教程后，可以关闭 Azure 门户，也可以将其保留为打开状态以尝试其他配置选项。

你已准备好尝试更改结果。

## <a name="see-classification-labeling-and-protection-in-action"></a>在实际操作中查看分类、标签设置和保护 

你所做的策略更改以及你创建的新标签适用于 Word、Excel、PowerPoint 和 Outlook。 我们在本教程中使用 Word 进行实际操作。 

在 Word 中打开一个新文档。 由于已安装 Azure 信息保护客户端，可以看到以下视图：

![Azure 信息保护教程 - 客户端已安装](./media/word2016-calloutsv2.png)

- 在“主页”  选项卡上，有一个“保护”  组，其中有一个名为“保护”  的按钮。
    
    依次单击“**保护**” > “**帮助和反馈**”，然后在“**Microsoft Azure 信息保护**”对话框中，确认客户端状态。 它应显示“连接为”  和你的用户名。 此外，还应该看到上次连接的最近时间和日期以及信息保护策略的下载时间。 验证对于租户显示的用户名是否正确。

- 功能区下方有一个新栏：信息保护栏。 其显示“敏感度”  的标题及我们在 Azure 门户中看到的标签。

### <a name="to-manually-change-our-default-label"></a>手动更改默认标签

1. 在信息保护栏上，选择最后一个标签，然后可看到子标签是如何排列的：
    
    ![Azure 信息保护教程 - 查看子标签](./media/info-protect-sub-labelsv2.png)

2. 选择其中任一子标签，将看到其他标签如何不再显示在栏上，因为已为本文档选择标签。 “敏感级别”  值将更改，以显示标签和子标签名称，标签颜色也会相应更改。 例如：
    
    ![Azure 信息保护教程 - 已选择子标签](./media/info-protect-sub-label-selectedv2.png)

3. 在信息保护栏上，单击当前所选标签值旁边的“编辑标签”  图标：
    
    ![Azure 信息保护教程 -“编辑标签”图标](./media/info-protect-edit-label-selectedv2.png)
    
    此操作将再次显示可用的标签。

4. 现在，选择第一个标签：“个人”  。 由于所选标签的分类低于之前为此文档选择的标签分类，因此将会看到阐明为什么要降低分类级别的提示：
    
    ![Azure 信息保护教程 - 确认降低理由的提示](./media/info-protect-lower-justification.png)
    
    选择“不再应用以前的标签”  ，然后单击“确认”  。 “敏感度”  值将更改为“个人”  ，其他标签将再次隐藏。

### <a name="to-remove-the-classification-completely"></a>完全删除分类

1. 在信息保护栏上，再次单击“编辑标签”  图标。 不要选择某个标签，而是单击“删除标签”图标  ：
    
    ![Azure 信息保护教程 -“删除”图标](./media/delete-icon-from-personalv2.png)
    
2. 系统提示时，这一次请键入“此文档不需要分类”，然后单击“确认”  。  
    
    可看到“敏感度”  值显示为“未设置”（这是在未将默认标签设置为策略设置时用户最初看到的新文档设置）  。

### <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>查看标签和自动保护的推荐提示

1. 在 Word 文档中，键入有效的信用卡号，例如：**4242-4242-4242-4242**。 

2. 使用任意文件名在本地保存文档。 

3. 现在，检测到信用卡卡号时，将看到一条提示，提示用户使用针对保护配置的标签。 如果不同意这条建议，可通过选择“忽略”  来拒绝这一建议。 提供建议同时允许用户重写，可帮助减少使用自动分类时的误报。 在本教程中，请单击“立即更改”  。

    ![Azure 信息保护教程 - 推荐提示](./media/change-nowv2.png)

    此时，除了表明已应用所配置标签（例如“机密\财务”）的文档外，还可立即在整个页面上看到组织名称的水印，并且还应用了页脚“分类为机密”   。 

    该文档还受到为此标签指定的权限的保护。 单击“文件”选项卡可以确认文档是否处于受保护状态，然后查看“保护文档”的信息   。 看到该文档受“机密\财务”的保护以及标签说明  。 
    
    由于标签的保护配置，只有员工可以打开该文档，且其某些操作受限。 例如，由于他们没有打印、复制和提取内容权限，因此，无法打印文档或从中复制内容。 这样的限制有助于防止数据丢失。 作为文档所有者，你可以打印它并从中进行复制。 但是，如果你将该文档以电子邮件的形式发送给组织中的其他用户，他们将无法执行这些操作。

4. 现在可以关闭此文档。

## <a name="clean-up-resources"></a>清理资源

如果你不想保留在本教程中所做的更改，请执行以下操作：

1. 选择“分类”   > “策略”   > “全局”  ，打开“策略: 全局”边栏选项卡  。

2. 将策略设置恢复为你记下的原始值，然后选择“保存”  。 

3. 从“分类”   > “标签”  菜单选项中：在“Azure 信息保护 - 标签”  边栏选项卡上，选择创建的“财务”  标签的上下文菜单 (...  )。

4. 选择“删除此标签”  ，如果系统提示你进行确认，请选择“确定”  。

重新启动 Word，下载这些更改。

## <a name="next-steps"></a>后续步骤

若要详细了解如何编辑 Azure 信息保护策略，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

若要详细了解记录标签活动的位置，请参阅 [Azure 信息保护客户端的使用日志记录](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)。

