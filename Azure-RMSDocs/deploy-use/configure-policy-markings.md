---
title: "为 Azure 信息保护标签配置可视标记"
description: "当文档或电子邮件中分配一个标签时，可以选择几个选项，以便方便地显示所选的分类。 这些可视标记是页眉、页脚和水印。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: aacdeeb9185755af90f4aa6144c47e3a9771b4e2
ms.sourcegitcommit: f0402cf14506b4c61a156a2baf7e69b7b16883a1
translationtype: HT
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>如何配置 Azure 信息保护可视标记的标签

>*适用于：Azure 信息保护*

当文档或电子邮件中分配一个标签时，可以选择几个选项，以便方便地显示所选的分类。 这些可视标记是页眉、页脚和水印：

在这些 Office 应用程序中应用标签和保存文档时，会将可视标记应用于 Word、Excel 和 PowerPoint 文档。 对于电子邮件，从 Outlook 发送电子邮件时会应用可视标记。

在以下情况下不会将可视标记应用于文档：使用文件资源管理器和右键单击操作应用标签时。 或者，使用 PowerShell 对文档进行分类时。

有关这些可视标记的其他信息：

- 页眉和页脚适用于 Word、Excel、PowerPoint 和 Outlook。

- 水印适用于 Word、Excel 和 PowerPoint：

    - Excel：水印仅在页面布局和打印预览模式及打印后可见。

    - PowerPoint：水印应用于母板幻灯片，作为背景图像。

- 你可以简单地指定文本字符串，也可以使用[变量](#using-variables-in-the-text-string)在应用页眉、页脚或水印时动态创建文本字符串。

请按照以下说明来配置标签的可视标记。

1. 如果尚未这样做，请在新的浏览器窗口中以全局管理员的身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。

    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果为视觉标记配置的标签将应用于所有用户，请从“策略: 全局”边栏选项卡中选择要更改的标签。

     如果要配置的标签位于[作用域内策略](configure-policy-scope.md)中，以便仅应用于所选用户，请首先从初始的“Azure 信息保护”边栏选项卡中选择作用域内策略。

3. 在“**标签**”边栏选项卡的“**设置可视标记（如页眉或页脚）**”部分中，配置所需可视标记的设置，然后单击设置“**保存**”：

    - 配置一个页眉：针对“**文档的此标签具有页眉**”，选择“**打开**”（如果希望具有页眉），或“**关闭**”（如果不希望这样做）。 如果选择“**打开**”，然后指定页眉的文本、大小、颜色和对齐方式。

    - 配置一个页脚：针对**文档的此标签具有页脚**，选择“**打开**”（如果希望具有页脚），或“**关闭**”（如果不希望这样做）。 如果选择“**打开**”，然后指定页脚的文本、大小、颜色和对齐方式。

    - 配置一个水印：针对**文档的此标签具有水印**，选择“**打开**”（如果希望具有水印），或“**关闭**”（如果不希望这样做）。 如果选择“**打开**”，然后指定页眉的水印文本、大小、颜色和布局。

4. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## <a name="using-variables-in-the-text-string"></a>在文本字符串中使用变量

你可以在文本字符串中为页眉、页脚或水印使用以下变量：

- `${Item.Label}`，针对所选标签。 例如：Internal

- `${Item.Name}`，针对文件名或电子邮件主题。 例如：JulySales.docx

- `${Item.Location}`，针对文档的路径和文件名，以及电子邮件的主题。 例如：\\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}`，针对文档或电子邮件的所有者（按 Windows 登录用户名）。 例如：rsimone

- `${User.PrincipalName}`，针对文档或电子邮件的所有者（按 Azure 信息保护客户端登录电子邮件地址 (UPN)）。 例如：rsimone@vanarsdelltd.com

- `${Event.DateTime}`，针对设置所选标签时的日期和时间。 例如：2016/8/16 下午 1:30

示例：如果为“常规”标签页脚指定字符串 `Document: ${item.name}  Classification: ${item.label}`，则应用于名为 project.docx 的文档的页脚文本将为 **Document: project.docx  Classification: General**。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
