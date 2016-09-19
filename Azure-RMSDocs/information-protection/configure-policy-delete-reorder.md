---
title: "如何删除或重排 Azure 信息保护的标签 | Azure 信息保护"
description: "可以删除或重排用户可以在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对此进行配置。"
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
translationtype: Human Translation
ms.sourcegitcommit: 801ca11da602d4acb9c398c9a89aeb33e45cb0f4
ms.openlocfilehash: 0283706733a61e2ccf88552b23ec67a7f755b8da


---

# 如何删除或重排 Azure 信息保护的标签

>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

可以删除或重排用户可以在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对此进行配置。

![在 Azure 信息保护策略中删除或重排标签](../media/info-protect-contextmenu.png)

如果你想要保留标签配置但防止它显示在信息保护栏中，你可能只是想禁用它，而不是删除标签。

对标签进行排序，以便用户在信息保护栏中的逻辑进度中就可以看到它们。 例如，以敏感度递增的方式排列标签，以便用户先看到最不敏感的标签，最后看到最敏感的标签。 [默认策略](configure-policy-default.md)使用此配置。

> [!IMPORTANT]
>如果为标签配置的 [条件](configure-policy-classification.md)(#条件) 可能会应用于多个标签，必须从最不敏感到最敏感排列标签。 这一顺序可确保当并评估条件时，应用最敏感的标签。


按照以下说明进行这些更改。

1. 如果尚未这样做，请在新的浏览器窗口中登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在“筛选”框中开始键入**信息**。 选择“Azure 信息保护”。

2. 在“**Azure 信息保护**”边栏选项卡上，执行以下操作之一，具体取决于是否想要删除、禁用或重排标签：

    - 删除标签：对于你想要删除的标签，右键单击或选择上下文菜单 (**...**)，单击“**删除此标签**”，然后单击“**是**”以确认。 然后，单击“**保存**”。 

    - 禁用标签：选择你想要禁用的标签。 在“**标签**”边栏选项卡上，针对“**启用**”，单击“**关闭**”，然后单击“**保存**”。

    - 重排标签：针对想要重排的标签，右键单击或选择上下文菜单 (**...**)，你，单击“**上移**”或“**下移**”直到标签位于所需的顺序。 然后，单击“**保存**”。 

3. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## 后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organization-s-policy)(#配置组织的策略) 部分中的链接。  





<!--HONumber=Sep16_HO3-->


