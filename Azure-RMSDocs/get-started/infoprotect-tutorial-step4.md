---
title: "快速入门教程步骤 4 - AIP"
description: "快速试用 Azure 信息保护入门教程步骤 4 - 查看设置标签与保护的实际操作。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
ms.openlocfilehash: 56ecd7b99f81a3b2399e166c1ca6a50797e65fa3
ms.sourcegitcommit: f0402cf14506b4c61a156a2baf7e69b7b16883a1
translationtype: HT
---
# <a name="step-4-see-classification-labeling-and-protection-in-action"></a>步骤 4：查看分类、设置标签和保护的实际操作 

>适用于：Azure 信息保护

既然已安装 Azure 信息保护客户端，并打开了 Word 文档，就可以知道使用我们配置的策略开始为文档设置标签并保护文档有多么简单。

分类和保护在保存文档后进行，但在保存文档之前，我们将使用未保存的文档来看应用并更改标签是多么容易。

## <a name="to-manually-change-our-default-label"></a>手动更改默认标签

在信息保护栏上，选择最后一个标签，然后可看到子标签是如何排列的：

![Azure 信息保护快速入门教程步骤 4 - 选择子标签](../media/info-protect-sub-labelsv2.png)

选择其中任一子标签，将看到其他标签如何不再显示在栏上，因为已为本文档选择标签。 “敏感级别”值将更改，以显示标签和子标签名称，标签颜色也会相应更改。 例如：

![Azure 信息保护快速入门教程步骤 4 - 已选择子标签](../media/info-protect-sub-label-selectedv2.png)

在信息保护栏上，单击当前所选标签值旁边的“编辑标签”图标：

![Azure 信息保护快速入门教程步骤 4 -“编辑标签”图标](../media/info-protect-edit-label-selectedv2.png)

将再次显示可用的标签。

现在，选择第一个标签：“个人”。 所选标签的分类低于之前为本文档选择的标签，因此系统将提示你确认降低分类级别的原因：

![Azure 信息保护快速入门教程步骤 4 - 确认降低理由的提示](../media/info-protect-lower-justification.png)

选择“不再应用以前的标签”，然后单击“确认”。 “敏感度”值将更改为“个人”，其他标签将再次隐藏。

## <a name="to-remove-the-classification-completely"></a>完全删除分类

在信息保护栏上，再次单击“编辑标签”图标。 不要选择某个标签，而是单击“删除标签”图标：

![Azure 信息保护快速入门教程步骤 4 -“删除”图标](../media/delete-icon-from-personalv2.png)

系统提示时，这一次请键入“此文档不需要分类”，然后单击“确认”。  

你将看到“敏感度”的值显示为“未设置”，即未设置默认标签时，用户看到的最初内容：

![Azure 信息保护快速入门教程步骤 4 - 删除分类](../media/sensitivity-not-setv2.png)


## <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>查看标签和自动保护的推荐提示

1. 在 Word 文档中，键入有效的信用卡号，例如：**4242-4242-4242-4242**。 

2. 保存文档（使用任何文件名、任何位置）。 

3. 现在，检测到信用卡卡号时，将看到一条提示，提示用户使用针对保护配置的标签。 如果不同意这条建议，可通过选择“忽略”来拒绝这一建议。 提供建议同时允许用户重写，可帮助减少使用自动分类时的误报。 在本教程中，请单击“立即更改”。

    ![Azure 信息保护快速入门教程步骤 4 - 推荐提示](../media/change-nowv2.png)

    除了可看到一个文档，显示已应用配置的标签（例如，**机密\所有员工**），还可立即在页面上看到组织名称的水印，并且还应用了页脚**归类为机密**。 

    该文档仍使用你指定的 Azure Rights Management 模板进行保护，你可以单击“文件”选项卡并查看“保护文档”的信息来确认。 如果你使用默认的机密模板，将看到以下信息：该文档仅供内部用户使用（组织外部的用户将无法打开该文档），并且文档的内容不可复制或打印。 作为文档的所有者，你可以复制和打印该文档，但是如果将其通过电子邮件发送给组织中的其他用户，那么他们将无法执行这些操作。

4. 现在可以关闭此文档。

现在你已经在实际操作中了解了分类、标记和保护，我们来看看已在另一组织中与其他人共享你的文档的情况下，如何保护你的文档。 你甚至可以跟踪它们的使用方式，并撤销对它们的访问权限。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|有关标记和保护文件的完整说明 |[对文件或电子邮件进行分类和保护](../rms-client/client-classify-protect.md)|





>[!div class="step-by-step"]
[« 步骤 3](infoprotect-tutorial-step3.md)
[步骤 5 »](infoprotect-tutorial-step5.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]