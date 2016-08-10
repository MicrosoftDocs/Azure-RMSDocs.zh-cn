---
title: "如何配置 Azure 信息保护可视标记的标签 | Azure 权限管理"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 9f2d28e4f162891497a7b0518322338628118b9d


---

# 如何配置 Azure 信息保护可视标记的标签

>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

当文档或电子邮件中分配一个标签时，可以选择几个选项，以便方便地显示所选的分类。 这些可视标记是页眉、页脚和水印：

应用标签和保存文档时，可视标记将应用于 Word、Excel 和 PowerPoint 文档。 对于电子邮件，发送电子邮件时应用可视标记。

有关这些可视标记的其他信息：

- 页眉和页脚适用于 Word、Excel、PowerPoint 和 Outlook。

- 水印适用于 Word、Excel 和 PowerPoint：

    - Excel：水印仅在页面布局和打印预览模式及打印后可见。

    - PowerPoint：水印应用于母板幻灯片，作为背景图像。

请按照以下说明来配置标签的可视标记。

1. 登录到 [Azure 门户](https://portal.azure.com)。
 
2. 在中心菜单上单击“浏览”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

3. 在“**Azure 信息保护**”边栏选项卡上，选择要配置为可视标记的标签。

4. 在“**标签**”边栏选项卡的“**设置可视标记（如页眉或页脚）**”部分中，配置所需可视标记的设置，然后单击设置“**保存**”：

    - 配置一个页眉：针对“**文档的此标签具有页眉**”，选择“**打开**”（如果希望具有页眉），或“**关闭**”（如果不希望这样做）。 如果选择“**打开**”，然后指定页眉的文本、大小、颜色和对齐方式。

    - 配置一个页脚：针对**文档的此标签具有页脚**，选择“**打开**”（如果希望具有页脚），或“**关闭**”（如果不希望这样做）。 如果选择“**打开**”，然后指定页脚的文本、大小、颜色和对齐方式。

    - 配置一个水印：针对**文档的此标签具有水印**，选择“**打开**”（如果希望具有水印），或“**关闭**”（如果不希望这样做）。 如果选择“**打开**”，然后指定页眉的水印文本、大小、颜色和布局。

5. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## 后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organization-s-policy)(#配置组织的策略) 部分中的链接。  





<!--HONumber=Jul16_HO5-->


