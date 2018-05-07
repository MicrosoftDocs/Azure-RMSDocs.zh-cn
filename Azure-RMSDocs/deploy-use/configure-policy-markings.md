---
title: 为 Azure 信息保护标签配置可视标记
description: 当文档或电子邮件中分配一个标签时，可以选择几个选项，以便方便地显示所选的分类。 这些可视标记是页眉、页脚和水印。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/22/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: 0b8bef6acd02abb664b274bc04fe77eea06de356
ms.sourcegitcommit: 94d1c7c795e305444e9fde17ad73e46f242bcfa9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2018
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>如何配置 Azure 信息保护可视标记的标签

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

>[!NOTE]
> 本文反映了 Azure 门户的最新更新，它允许你独立于全局策略或限定范围的策略来创建标签。 还将删除发布策略的选项。 如果租户尚未更新这些更改，例如，你仍看到 Azure 信息保护的“发布”选项，而没有看到“分类”菜单选项，请等待几天，然后再返回查看这些说明。

当文档或电子邮件中分配一个标签时，可以选择几个选项，以便方便地显示所选的分类。 这些可视标记是页眉、页脚和水印。

有关这些可视标记的其他信息：

- 页眉和页脚适用于 Word、Excel、PowerPoint 和 Outlook。

- 水印适用于 Word、Excel 和 PowerPoint：

    - Excel：水印仅在页面布局和打印预览模式及打印后可见。
    
    - PowerPoint：水印应用于母板幻灯片，作为背景图像。
    
    - 支持多行文本。

- 你可以简单地指定文本字符串，也可以使用[变量](#using-variables-in-the-text-string)在应用页眉、页脚或水印时动态创建文本字符串。

- 视觉标记仅支持一种语言。

## <a name="when-visual-markings-are-applied"></a>应用视觉标记的情况

对于电子邮件，从 Outlook 发送电子邮件时会应用可视标记。

对于文档，视觉标记应用如下所示：

- 在 Office 应用中，会在应用标签时应用来自标签的视觉标记。 打开标记的文档以及首次保存该文档时，也会应用视觉标记。  

- 当使用文件资源管理器或 PowerShell 标记文档时，不会立即应用视觉标记，但在 Office 应用中打开文档以及首次保存文档时都会应用视觉标记。

## <a name="to-configure-visual-markings-for-a-label"></a>配置标签的视觉标记

请按照以下说明来配置标签的可视标记。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“分类” > “标签”菜单选项：在“Azure 信息保护 - 标签”边栏选项卡上，选择包含要添加或更改的视觉标记的标签。

3. 在“**标签**”边栏选项卡的“**设置可视标记（如页眉或页脚）**”部分中，配置所需可视标记的设置，然后单击设置“**保存**”：
    
    - 配置一个页眉：针对“**文档的此标签具有页眉**”，选择“**打开**”（如果希望具有页眉），或“**关闭**”（如果不希望这样做）。 如果选择“打开”，则指定页眉的文本、大小、[字体](#setting-the-font-name)、[颜色](#setting-the-font-color)和对齐方式。
    
    - 配置一个页脚：针对**文档的此标签具有页脚**，选择“**打开**”（如果希望具有页脚），或“**关闭**”（如果不希望这样做）。 如果选择“打开”，则指定页脚的文本、大小、[字体](#setting-the-font-name)、[颜色](#setting-the-font-color)和对齐方式。
    
    - 配置一个水印：针对**文档的此标签具有水印**，选择“**打开**”（如果希望具有水印），或“**关闭**”（如果不希望这样做）。 如果选择“打开”，则指定水印的文本、大小、[字体](#setting-the-font-name)、[颜色](#setting-the-font-color)和对齐方式。
    
单击“保存”时，更改将会自动提供给用户和服务。 不再提供单独发布选项。


## <a name="using-variables-in-the-text-string"></a>在文本字符串中使用变量

你可以在文本字符串中为页眉、页脚或水印使用以下变量：

- `${Item.Label}`，针对所选标签。 例如：Internal

- `${Item.Name}`，针对文件名或电子邮件主题。 例如：JulySales.docx

- `${Item.Location}`，针对文档的路径和文件名，以及电子邮件的主题。 例如：\\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}`，针对文档或电子邮件的所有者（按 Windows 登录用户名）。 例如：rsimone

- `${User.PrincipalName}`，针对文档或电子邮件的所有者（按 Azure 信息保护客户端登录电子邮件地址 (UPN)）。 例如：rsimone@vanarsdelltd.com

- `${Event.DateTime}`，针对设置所选标签时的日期和时间。 例如：2016/8/16 下午 1:30

示例：如果为“常规”标签页脚指定字符串 `Document: ${item.name}  Classification: ${item.label}`，则应用于名为 project.docx 的文档的页脚文本将为 **Document: project.docx  Classification: General**。

## <a name="setting-different-visual-markings-for-word-excel-powerpoint-and-outlook"></a>为 Word、Excel、PowerPoint 和 Outlook 设置不同的视觉标记

默认情况下，指定的视觉标记将应用于 Word、Excel、PowerPoint 和 Outlook。 但是，在文本字符串中使用“If.App”变量语句并使用值 **Word**、**Excel**、**PowerPoint** 或 **Outlook** 标识应用程序类型时，可以为每个 Office 应用程序类型指定视觉标记。 还可以简化这些值，当想要在同一 If.App 语句中指定多个值时，这很有必要。

使用以下语法：

    ${If.App.<application type>}<your visual markings text> ${If.End}

此语句中的该语法区分大小写。

例如：

- **仅为 Word 文档设置页眉文本：**
    
    `${If.App.Word}This Word document is sensitive ${If.End}`
    
    仅在 Word 文档页眉中，标签应用页眉文本“此 Word 文档包含敏感内容”。 没有页眉文本应用于其他 Office 应用程序。

- **为 Word、Excel 和 Outlook 设置页脚文本，为 PowerPoint 设置不同的页脚文本：**
    
    `${If.App.WXO}This content is confidential. ${If.End}${If.App.PowerPoint}This presentation is confidential. ${If.End}`
    
    在 Word、Excel 和 Outlook 中，标签应用页脚文本“此内容是机密的”。 在 PowerPoint 中，标签应用页脚文本“此演示文稿是机密的”。

- **为 Word 和 PowerPoint 设置特定的水印文本，然后为 Word、Excel 和 PowerPoint 设置水印文本：**
    
    `${If.App.WP}This content is ${If.End}Confidential`
    
    在 Word 和 PointPoint 中，标签应用水印文本“此内容是机密的”。 在 Excel 中，标签应用水印文本“机密”。 在 Outlook 中，标签不应用任何水印文本，因为 Outlook 不支持将水印作为视觉标记。

### <a name="setting-the-font-name"></a>设置字体名称

Calibri 是页眉、页脚和水印文字的默认字体。 如果指定替代字体名称，请确保它在将应用视觉对象标记的客户端设备上可用。 

如果指定字体不可用，客户端将回退使用 Calibri 字体。

### <a name="setting-the-font-color"></a>设置字体颜色

可从可用颜色列表中进行选择，或输入颜色的红绿蓝 (RGB) 组成的十六进制三元色代码来指定自定义颜色。 例如，#DAA520。 

如果需要引用这些代码，请参阅 MSDN 文档中的 [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85\).aspx)（按名称分类的颜色），这是一个有用的起点。 也可在许多可编辑图片的应用程序中找到这些代码。 例如，通过 Microsoft 画图，从调色板中选择自定义颜色，系统将自动显示 RGB 值，该值可供复制。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
