---
title: "删除或重排 Azure 信息保护标签"
description: "可以删除或重排用户在信息保护栏看到的标签，方法是在 Azure 信息保护策略中对此进行配置。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.openlocfilehash: 85d8e612d95358ce7f5d883450dc207e54549828
ms.sourcegitcommit: 67750454f8fa86d12772a0075a1d01a69f167bcb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>如何删除或重排 Azure 信息保护的标签

>适用于：Azure 信息保护

可以删除或重排用户在信息保护栏看到的标签，方法是在 Azure 信息保护策略中选择这些操作。

![在 Azure 信息保护策略中删除或重排标签](../media/info-protect-contextmenu.png)

删除应用于文档和电子邮件的标签并发布 Azure 信息保护策略时，该标签在下次由 Azure 信息保护客户端打开时会自动从这些文档或电子邮件中删除。

但是，如果标签已应用保护，该标签则不会被删除。 标签中的保护设置将保留并显示在“保护模板”中。 现在可以将此模板转换为新的标签或链接到标签。 此模板存在时，无法创建与已删除标签的名称相同的新标签。 如果想那么做，有如下选项可供选择：

- 将模板转换为标签。 
    
    建议采用此操作，因为随后可以按需更改此模板的名称并修改保护设置。

- 使用 PowerShell 重命名模板或将它删除。
    
    在执行这些操作前，请考虑其他的管理员或服务是否正在使用此模板，并按其当前名称对其进行标识。 仅在无需打开由模板保护的文档或电子邮件时才删除此模板。

有关管理保护模板的详细信息，请参阅[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)。

删除标签前，请考虑是否要将其改为禁用。 禁用已应用到文档和电子邮件的标签时，将不会从这些文档和电子邮件中删除已应用的标签，但此标签将不再显示为“信息保护”栏上用户可以选择的标签。 通过禁用此标签，可保持原始配置，以供希望用户以后选择此标签时使用，在此情况下，只需重新启用此标签即可。

对标签进行排序，以便用户在信息保护栏中的逻辑进度中就可以看到它们。 例如，以敏感度递增的方式排列标签，以便用户先看到最不敏感的标签，最后看到最敏感的标签。 [默认策略](configure-policy-default.md)使用此配置，并在标签名中反映出逐渐递增的敏感级别。

> [!IMPORTANT]
>如果为标签配置的 [条件](configure-policy-classification.md)(#条件) 可能会应用于多个标签，必须从最不敏感到最敏感排列标签。 这一顺序可确保当并评估条件时，应用最敏感的标签。


按照以下说明进行这些更改。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 如果要配置的标签将应用于所有用户，请选择“Azure 信息保护 - 全局策略”边栏选项卡。
    
    如果要配置的标签位于[作用域内策略](configure-policy-scope.md)中，仅应用于所选用户，请从“策略”菜单选项中选择“作用域内策略”。 然后从“Azure 信息保护 - 作用域内策略”边栏选项卡选择作用域内策略。

3. 从“Azure 信息保护 - 全局策略”边栏选项卡或“策略: \<名称>”边栏选项卡中，执行以下一种或多种操作： 

    - 删除标签：对于你想要删除的标签，右键单击或选择上下文菜单 (**...**)，单击“**删除此标签**”，然后单击“**是**”以确认。 然后，单击“**保存**”。 

    - 禁用标签：选择你想要禁用的标签。 在“**标签**”边栏选项卡上，针对“**启用**”，单击“**关闭**”，然后单击“**保存**”。

    - 重排标签：针对想要重排的标签，右键单击或选择上下文菜单 (**...**)，然后单击“**上移**”或“**下移**”直到标签位于所需的顺序。 然后，单击“**保存**”。 

4. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

