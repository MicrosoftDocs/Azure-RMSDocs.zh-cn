---
title: "如何配置 Azure 信息保护可视标记的标签 | Azure 权限管理"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: b5e7fecca7aeb61221dc1f61aa3e202936b8c042
ms.openlocfilehash: 2b4f464fa51e0743cb1ce0726c7feb31146b5128


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

- 你可以简单地指定文本字符串，也可以使用[变量](#using-variables-in-the-text-string)在应用页眉、页脚或水印时动态创建文本字符串。 

请按照以下说明来配置标签的可视标记。

1. 如果尚未这样做，请登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“浏览”，然后在“筛选”框中开始键入**信息**。 选择“Azure 信息保护”。

2. 在“**Azure 信息保护**”边栏选项卡上，选择要配置为可视标记的标签。

3. 在“**标签**”边栏选项卡的“**设置可视标记（如页眉或页脚）**”部分中，配置所需可视标记的设置，然后单击设置“**保存**”：

    - 配置一个页眉：针对“**文档的此标签具有页眉**”，选择“**打开**”（如果希望具有页眉），或“**关闭**”（如果不希望这样做）。 如果选择“**打开**”，然后指定页眉的文本、大小、颜色和对齐方式。
    
    - 配置一个页脚：针对**文档的此标签具有页脚**，选择“**打开**”（如果希望具有页脚），或“**关闭**”（如果不希望这样做）。 如果选择“**打开**”，然后指定页脚的文本、大小、颜色和对齐方式。
    
    - 配置一个水印：针对**文档的此标签具有水印**，选择“**打开**”（如果希望具有水印），或“**关闭**”（如果不希望这样做）。 如果选择“**打开**”，然后指定页眉的水印文本、大小、颜色和布局。 

4. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## 在文本字符串中使用变量

你可以在文本字符串中为页眉、页脚或水印使用以下变量：

- `${Item.Label}` 针对所选标签。 例如：Internal

- `${Item.Name}` 针对文件名或电子邮件主题。 例如：JulySales.docx

- `${Item.Location}` 针对文档的路径和文件名，以及电子邮件的电子邮件主题。 例如：\\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}` 针对文档或电子邮件的所有者，通过使用用户名登录的 Windows。 例如：rsimone

- `${User.PrincipalName}` 针对文档或电子邮件的所有者，通过使用电子邮件地址 (UPN) 登录的 Azure 信息保护客户端。 例如：rsimone@vanarsdelltd.com

- `${Event.DateTime}` 针对设置所选标签时的日期和时间。 例如：2016/8/16 下午 1:30
    
示例：如果为 Secret 标签页脚指定字符串 `Document: ${item.name}  Classification: ${item.label}`，则应用于名为 project.docx 的文档的页脚文本将为 **Document: project.docx  Classification: Secret**。

## 后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organization-s-policy)(#配置组织的策略) 部分中的链接。  





<!--HONumber=Aug16_HO3-->


