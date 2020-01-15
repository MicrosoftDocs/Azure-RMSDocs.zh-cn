---
title: 教程 - 使用 Azure 信息保护策略设置进行数据分类
description: 本入门教程介绍如何配置 Azure 信息保护策略设置，从而帮助对组织的文档和电子邮件进行分类。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 0c1e008185fb279964c56f508ee9daa6822718e4
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2020
ms.locfileid: "75743520"
---
# <a name="tutorial-configure-azure-information-protection-policy-settings-that-work-together"></a>教程：配置协同工作的 Azure 信息保护策略设置

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：  [适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

在本教程中，你将了解如何：
> [!div class="checklist"]
> * 配置协同工作的策略设置
> * 在实际操作中查看设置


与其依赖用户手动标记其文档和电子邮件，不如使用 Azure 信息保护策略设置来实现以下目的：

- 确保新内容和已编辑内容具有基本级别的分类

- 让用户了解标签并且能够轻松地应用正确的标签

完成本教程需要 15 分钟。

## <a name="prerequisites"></a>必备条件 

若要完成本教程，你需要：

1. 包含 Azure 信息保护计划 1 或计划 2 的订阅。
    
    如果没有包含此计划的订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

2. “Azure 信息保护”窗格已添加到 Azure 门户，并在 Azure 信息保护全局策略中发布了一个或多个标签。
    
    有关这些步骤，请参阅[快速入门：将 Azure 信息保护添加到 Azure 门户和查看策略](quickstart-viewpolicy.md)。

3. Azure 信息保护客户端（经典）安装在 Windows 计算机上（最低版本为 Windows 7 Service Pack 1）。 
    
    若要安装经典客户端，可以转到 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)，然后从“Azure 信息保护”页下载 AzInfoProtection.exe  。 
    
    如果对经典客户端使用了不同的标签客户端，请参阅 Office 文档，以了解有关敏感度标签的策略设置信息。 例如，[敏感度标签概述](/microsoft-365/compliance/sensitivity-labels)。

4. 你已从下列类别之一登录到 Office 应用：
    
    - Office 应用最低版本 1805，Office 365 商业版或 Microsoft 365 商业版中的内部版本 9330.2078，前提是已为你分配了 Azure Rights Management（亦称为“适用于 Office 365 的 Azure 信息保护”）许可证。
    
    - Office 365 专业增强版。
    
    - Office 专业增强版 2019。
    
    - Office Professional Plus 2016。
    
    - Office Professional Plus 2013 Service Pack 1。
    
    - Office Professional Plus 2010 Service Pack 2。

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。

让我们开始吧。

## <a name="edit-the-azure-information-protection-policy"></a>编辑 Azure 信息保护策略

与其依赖用户手动标记其文档和电子邮件，不如使用部分策略设置来确保基本级别的分类。 

我们将使用 Azure 门户编辑全局策略以更改所有用户的策略设置。

1. 打开新的浏览器窗口，以全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。然后导航到“Azure 信息保护”  。 
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”  并选择“Azure 信息保护”  。
    
    如果你不是全局管理员，请使用以下链接获取替代角色：[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)

2. 选择“分类”   > “策略”   > “全局”  ，打开“策略: 全局”边栏选项卡  。 

3. 在“配置要对信息保护最终用户显示和应用的设置”  部分中，找到位于标签后面的策略设置。 你的设置中的值可能与显示的值不同：
    
    ![Azure 信息保护教程 - 默认设置](./media/defaultsettings-aip.png)

4. 更改设置以匹配下表中的值。 记下更改的设置，以便在完成本教程后再次将它更改回来。 

    |设置|值|信息|
    |-------|-----|-----|
    |**选择默认标签**|**常规**|“常规”  标签是 Azure 信息保护可为你创建的默认标签之一。 [创建和发布标签](quickstart-viewpolicy.md#create-and-publish-labels)快速入门中介绍了此步骤。 如果没有名为“常规”  的标签，可以从下拉列表中选择另一个标签。 未标记的文档和电子邮件将自动应用此标签作为基本分类。 不过，用户可以将所选标签更改为其他标签。|
    |**强制所有文档和电子邮件都具有标签**|**开**|此设置通常称为强制标记，因为它可以防止用户保存文档或发送未标记的电子邮件。 连同默认标签，文档和电子邮件将具有你设置的默认标签或它们选择的标签。
    |**对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签**|推荐 |如果用户附加的文档的分类级别高于所选默认标签，此设置会提示用户为其电子邮件选择更高级别的分类标签。
    |**在 Office 应用程序中显示“信息保护”栏**|**开**|显示“信息保护”栏后，用户可以更轻松地查看和更改默认标签。
    
    设置现在应如下所示：
    
    ![Azure 信息保护教程 - 更改的默认设置](./media/defaultsettings-aip-changed.png)

5. 选择此“策略: 全局”  边栏选项卡上的“保存”  ，如果系统提示你确认操作，请选择“确定”  。 

## <a name="see-your-policy-settings-in-action"></a>在实际操作中查看策略设置 

在本教程中，我们将在实际操作中使用 Word 和 Outlook 查看你的策略更改。 如果在更改策略设置之前已加载这些应用，请重新启动它们以下载更改。

### <a name="default-label-and-the-information-protection-bar"></a>默认标签和“信息保护”栏

在 Word 中打开一个新文档。 你会看到文档自动标记为“常规”  ，而不是依赖用户选择标签。 

显示“信息保护”栏并显示可用标签后，用户可以轻松地查看当前选定的标签，如果默认标签不合适，还可以更改标签：

![Azure 信息保护教程 - 使用默认标签的新文档](./media/defaultlabel-word.png)

如果未显示该栏，无需更改标签，关闭“信息保护”栏即可比较体验：

![Azure 信息保护教程 - 关闭栏](./media/infoprotect-bar-close.png)

“常规”  标签仍处于选中状态，但不太明显。 选择不同标签的选项也不太明显。 为此，用户必须选择“保护”  按钮：

![Azure 信息保护教程 - 已选择“保护”按钮](./media/infoprotect-protectbutton-pulldown.png)

现在，在下拉菜单中可以看到已选中“常规”  标签，因为它旁边有一个复选标记。 要更改当前选定的标签，用户可以从列表中选择其他标签。 如果用户不熟悉标记操作，他们可能不记得每次都要选择“保护”  按钮。 他们也可能没有意识到可以选择另一个标签。

若要再次显示“信息保护”栏，请从下拉菜单选择“显示栏”  。

> [!TIP]
> 可以配置[高级客户端设置](./rms-client/client-admin-guide-customizations.md#set-a-different-default-label-for-outlook)，为 Outlook 选择其他默认标签。

### <a name="mandatory-labeling"></a>强制标记

可以将当前选定的“常规”  标签更改为其他标签，但不能将其删除。 由于我们已将“强制所有文档和电子邮件都具有标签”  设置为“开”  ，因此，“信息保护”栏上的“删除标签”  图标不可用。 

如果我们没有更改该设置，“信息保护”栏会显示以下图标：

![Azure 信息保护教程 - 关闭栏](./media/infoprotect-deletelabel-icon.png)

连同默认标签一起，强制标记可确保新文档和已编辑的文档（和电子邮件）具有所选的基本分类。 

如果我们没有通过强制标记设置来设置默认标签，系统会始终提示用户在保存未标记文档或发送未标记电子邮件时选择标签。 对于许多用户而言，系统持续发出的提示可能会令人沮丧，并且还会导致标记不够准确。 对于那些在完成处理文档或电子邮件后系统提示选择标签的用户，他们的工作流程会中断，然后随机选择任何标签，以便可以转移到需要执行的下一项操作。

### <a name="recommendations-for-emails-with-attachments"></a>带附件的电子邮件的建议

对于打开的 Word 文档，请选择一个分类级别高于“常规”  的标签。 例如，“保密”  下的任一子标签，如“保密 - 所有人(未保护)”  。 在本地保存文档并为其提供任何名称。 

启动 Outlook 并创建新的电子邮件。 正如我们在 Word 中看到的那样，新电子邮件会自动标记为“常规”  ，并显示“信息保护”栏。

将刚刚标记为附件的 Word 文档添加到电子邮件。 你会看到提示将电子邮件标签更改为与 Word 附件匹配的“保密”  标签。 可接受或忽略该建议：

![Azure 信息保护教程 - 提示重新标记电子邮件以匹配已标记附件](./media/infoprotect-matchemail-label.png)

如果单击“忽略”  ，则不会应用新标签，但会看到电子邮件仍然使用已配置的默认标签“常规”  进行标记。 仍然显示可用标签以供选择。

如果选择“立即更改”  ，则电子邮件重新标记为“保密”  子标签。 但是，用户仍然可以在发送电子邮件之前更改标签，方法是选择“编辑”标签图标：

![Azure 信息保护教程 -“编辑标签”图标](./media/infoprotect-editlabel-icon.png)

“信息保护”栏会再次显示，供用户选择替代标签。

由于在发送电子邮件之前选择了标签，因此无需实际发送电子邮件以查看此策略设置的工作方式。 可以关闭电子邮件（无需发送或保存）。

不过，如果希望尝试重复此练习，还要附加具有更高分类级别的另一个文档（“高度保密”  标签中的子标签）。 然后，可以看到提示如何更改为应用更高分类级别标签。 如果使用具有相同父标签的子标签测试多个附件，必须配置[高级客户端设置](./rms-client/client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)以支持其在 Azure 门户中的排序。

## <a name="clean-up-resources"></a>清理资源

如果你不想保留在本教程中所做的更改，请执行以下操作：

1. 选择“分类”   > “策略”   > “全局”  ，打开“策略: 全局”边栏选项卡  。

2. 将策略设置恢复为你记下的原始值，然后选择“保存”  。

重新启动 Word 和 Outlook 应用以下载这些更改。

## <a name="next-steps"></a>后续步骤

若要详细了解如何编辑 Azure 信息保护策略设置，请参阅[如何配置 Azure 信息保护的策略设置](configure-policy-settings.md)。

我们更改的策略设置有助于确保基本级别的分类，并鼓励用户选择适当的标签。 下一步是通过检查文档和电子邮件的内容，然后推荐或自动应用适当的标签来增强此策略。 可以通过为标签配置条件的方式来执行此操作。 有关详细信息，请参阅[如何配置 Azure 信息保护的自动和建议分类条件](configure-policy-classification.md)。
