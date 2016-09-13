---
title: "如何创建 Azure 信息保护的新标签 | Azure 信息保护"
description: "尽管 Azure 信息保护附带了可以自定义的默认标签，你还可以创建用户可在信息保护栏中看到的自己的标签。"
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: b02c3e602a8178c0837104a88b360d041ecddc4d


---

# 如何创建 Azure 信息保护的标签

>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

尽管 Azure 信息保护附带了可以自定义的默认标签，你还可以创建用户可在信息保护栏中看到的自己的标签。

可以添加新标签，或在需要更高级别的分类时将新子标签添加到现有标签。 例如，属于 [默认策略](configure-policy-default.md)(#默认策略) 的“**秘密**”标签包含子标签。

使用以下说明将一个新标签添加到 Azure 的信息保护策略。

1. 如果尚未这样做，请登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“浏览”，然后在“筛选”框中开始键入**信息**。 选择“Azure 信息保护”。

2. 在“**Azure 信息保护**”边栏选项卡上，执行以下操作之一：

    - 创建新的标签：单击“**添加新的标签**”。

    - 创建新的子标签：对于要创建子标签的标签，右键单击或选择上下文菜单 (**...**)，然后单击“**添加子标签**”。

3. 在“**标签**”或“**子标签**”边栏选项卡上，选择要应用于此新标签的选项，然后单击“**保存**”。

    > [!NOTE]
    >有关设置保护的信息，请参阅 [如何配置标签以应用保护](configure-policy-protection.md)(#如何配置标签以应用保护)。

4. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## 后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organization-s-policy)(#配置组织的策略) 部分中的链接。  





<!--HONumber=Sep16_HO1-->


