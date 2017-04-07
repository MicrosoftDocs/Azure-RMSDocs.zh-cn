---
title: "删除或重排 Azure 信息保护标签"
description: "可以删除或重排用户可以在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对此进行配置。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.openlocfilehash: 8cb5c6270c90b7d012607da9aa9e4e6172d33a7b
ms.sourcegitcommit: f0402cf14506b4c61a156a2baf7e69b7b16883a1
translationtype: HT
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>如何删除或重排 Azure 信息保护的标签

>*适用于：Azure 信息保护*

可以删除或重排用户可以在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对此进行配置。

![在 Azure 信息保护策略中删除或重排标签](../media/info-protect-contextmenu.png)

删除应用于文档和电子邮件的标签并发布 Azure 信息保护策略时，该标签在下次由 Azure 信息保护客户端打开时会自动从这些文档或电子邮件中删除。

删除标签前，请考虑是否要将其改为禁用。 禁用已应用到文档和电子邮件的标签时，将不会从这些文档和电子邮件中删除已应用的标签，但此标签将不再显示为“信息保护”栏上用户可以选择的标签。 通过禁用此标签，可保持原始配置，以供希望用户以后选择此标签时使用，在此情况下，只需重新启用此标签即可。

对标签进行排序，以便用户在信息保护栏中的逻辑进度中就可以看到它们。 例如，以敏感度递增的方式排列标签，以便用户先看到最不敏感的标签，最后看到最敏感的标签。 [默认策略](configure-policy-default.md)使用此配置，并在标签名中反映出逐渐递增的敏感级别。

> [!IMPORTANT]
>如果为标签配置的 [条件](configure-policy-classification.md)(#条件) 可能会应用于多个标签，必须从最不敏感到最敏感排列标签。 这一顺序可确保当并评估条件时，应用最敏感的标签。


按照以下说明进行这些更改。

1. 如果尚未这样做，请在新的浏览器窗口中以全局管理员的身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果要删除、禁用或重新排序的标签会应用于所有用户，请在“策略: 全局”边栏选项卡中执行以下操作之一。 

    - 删除标签：对于你想要删除的标签，右键单击或选择上下文菜单 (**...**)，单击“**删除此标签**”，然后单击“**是**”以确认。 然后，单击“**保存**”。 

    - 禁用标签：选择你想要禁用的标签。 在“**标签**”边栏选项卡上，针对“**启用**”，单击“**关闭**”，然后单击“**保存**”。

    - 重排标签：针对想要重排的标签，右键单击或选择上下文菜单 (**...**)，你，单击“**上移**”或“**下移**”直到标签位于所需的顺序。 然后，单击“**保存**”。 

     如果要删除、禁用或重新排序的标签位于[作用域内策略](configure-policy-scope.md)中，以便仅应用于所选用户，请首先从初始的“Azure 信息保护”边栏选项卡中选择作用域内策略。

3. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

