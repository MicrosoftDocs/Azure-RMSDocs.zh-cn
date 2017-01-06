---
title: "快速入门教程步骤 4 | Azure Rights Management"
description: "入门教程第 3 步，该教程用于快速试用适合你组织的 Microsoft Azure 信息保护，所需时间大概 30 分钟。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: bcf1e9ee7a2d6cf8fb264533f150b350ce0a9e56


---

# <a name="step-4-see-classification-labeling-and-protection-in-action"></a>步骤 4：查看分类、设置标签和保护的实际操作 

>适用于：Azure 信息保护

既然已安装 Azure 信息保护客户端，并打开了 Word 文档，就可以知道使用我们配置的策略开始为文档设置标签并保护文档有多么简单。

分类和保护在保存文档后进行，但在保存文档之前，我们将使用未保存的文档来看应用并更改标签是多么容易。

## <a name="to-manually-change-our-default-label"></a>手动更改默认标签

在信息保护栏上，选择“个人”标签，此时系统会提示你输入降低分类级别的理由：

![Azure 信息保护快速入门教程步骤 4 - 确认降低理由的提示](../media/info-protect-lower-justification.png)

选择“不再应用以前的标签”，然后单击“确认”。 你将看到“敏感度”的值变为“个人”。

## <a name="to-remove-the-classification-completely"></a>完全删除分类

在信息保护栏上，单击“个人”旁边的“编辑标签”图标。 将显示可用的标签。 但这一次不是选择某个标签，而是单击“删除标签”图标。 单击“确定”确认删除，然后提供该操作的理由。  

你将看到“敏感度”的值显示为“未设置”，即未设置默认标签时，用户看到的最初内容：

![Azure 信息保护快速入门教程步骤 4 - 删除分类](../media/sensitivity-not-set.png)


## <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>查看标签和自动保护的推荐提示

1. 在 Word 文档中，键入有效的信用卡号，例如：**4242-4242-4242-4242**。 

2. 保存文档（使用任何文件名、任何位置）。 

3. 现在你会看到提示：**建议将该文件标记为“机密”**。 单击“立即更改”。

    ![Azure 信息保护快速入门教程步骤 4 - 推荐提示](../media/change-now.png)

    除了标签设置为“机密”的文档外，你可以立即在页面上看到你的组织名称的水印，并且还应用了页脚**敏感度：机密**。 

    该文档仍使用你指定的 Azure Rights Management 模板进行保护，你可以单击“文件”选项卡并查看“保护文档”的信息来确认。 如果你使用默认的机密模板，将看到以下信息：该文档仅供内部用户使用（组织外部的用户将无法打开该文档），并且文档的内容不可复制或打印。 作为文档的所有者，你可以复制和打印该文档，但是如果将其通过电子邮件发送给组织中的其他用户，那么他们将无法执行这些操作。

现在你已经在实际操作中了解了分类、标记和保护，我们来看看已在另一组织中与其他人共享你的文档的情况下，如何保护你的文档。 你甚至可以跟踪它们的使用方式，并撤销对它们的访问权限。

>[!div class="step-by-step"]
[« 步骤 3](infoprotect-tutorial-step3.md)
[步骤 5 »](infoprotect-tutorial-step5.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


