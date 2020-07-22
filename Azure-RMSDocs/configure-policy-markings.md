---
title: 为 Azure 信息保护标签配置可视标记 - AIP
description: 当文档或电子邮件中分配一个标签时，可以选择几个选项，以便方便地显示所选的分类。 这些可视标记是页眉、页脚和水印。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 5ff7dc706d272228892b238da99a008ed626e522
ms.sourcegitcommit: 16d2c7477b96c5e8f6e4328a61fe1dc3d12c878d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86927363"
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>如何配置 Azure 信息保护可视标记的标签

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
>[!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

当文档或电子邮件中分配一个标签时，可以选择几个选项，以便方便地显示所选的分类。 这些可视标记是页眉、页脚和水印。

有关这些视觉标记的其他信息：

- 页眉和页脚适用于 Word、Excel、PowerPoint 和 Outlook。

- 水印适用于 Word、Excel 和 PowerPoint：

    - Excel：水印仅在页面布局和打印预览模式及打印后可见。

    - PowerPoint：水印应用于母板幻灯片，作为背景图像。 在“视图”**** 选项卡上的“幻灯片母版”**** 中，确保未选中“隐藏背景图形”**** 复选框。

- Word、Excel 和 PowerPoint 中的水印、页眉和页脚支持多行。 如果为 Outlook 中应用的标签页眉或页脚指定多行，这些行就会连接到一起。 在这种情况下，请考虑使用配置来[为 Word、Excel、PowerPoint 和 Outlook 设置不同的视觉标记](#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)。

- 最大字符串长度：

    - 页眉和页脚可以输入的最大字符串长度为 1024 个字符。 但是，Excel 的页眉和页脚的总数限制为 255 个字符。 此限制包括 Excel 中不可见的字符，例如格式代码。 如果达到该限制，则输入的字符串不在 Excel 中显示。

    - 可以输入的水印的最大字符串长度为 255 个字符。

- 你可以简单地指定文本字符串，也可以使用[变量](#using-variables-in-the-text-string)在应用页眉、页脚或水印时动态创建文本字符串。

- Word、PowerPoint 和 Outlook 支持使用不同颜色的视觉标记，现在 Excel 也不例外。

- 视觉标记仅支持一种语言。

## <a name="when-visual-markings-are-applied"></a>应用视觉标记的情况

对于电子邮件，从 Outlook 发送电子邮件时会应用视觉标记。 如果通过更改标签来转发或回复该电子邮件，则始终保留原始视觉标记。

对于文档，视觉标记应用如下所示：

- 在 Office 应用中，会在应用标签时应用来自标签的视觉标记。 打开标记的文档以及首次保存该文档时，也会应用视觉标记。  

- 当使用文件资源管理器、PowerShell 或 Azure 信息保护扫描程序标记文档时，不会立即应用视觉标记，但在 Office 应用中打开文档以及首次保存文档时会通过 Azure 信息保护客户端应用视觉标记。

    当你对保存在 Microsoft SharePoint、OneDrive for work 或 school 或 OneDrive for home 中的文件使用 "[自动保存](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5)" 时，不会应用可视标记，除非你将 "[高级客户端" 设置](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)配置为启用分类以在后台连续运行。

## <a name="to-configure-visual-markings-for-a-label"></a>配置标签的视觉标记

请按照以下说明来配置标签的可视标记。

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到“Azure 信息保护”窗格。

    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。

2. 从 "**分类**  >  **标签**" 菜单选项：在 " **Azure 信息保护-标签**" 窗格中，选择包含要添加或更改的视觉标记的标签。

3. 在 "**标签**" 窗格中，在 "**设置视觉标记（如页眉或页脚）** " 部分中，为所需的视觉标记配置设置，然后单击 "**保存**"：

    - 配置一个页眉：针对“**文档的此标签具有页眉**”，选择“**打开**”（如果希望具有页眉），或“**关闭**”（如果不希望这样做）。 如果选择“打开”，则指定页眉的文本、大小、[字体](#setting-the-font-name)、[颜色](#setting-the-font-color)和对齐方式****。

    - 配置一个页脚：针对**文档的此标签具有页脚**，选择“**打开**”（如果希望具有页脚），或“**关闭**”（如果不希望这样做）。 如果选择“打开”，则指定页脚的文本、大小、[字体](#setting-the-font-name)、[颜色](#setting-the-font-color)和对齐方式****。

    - 配置一个水印：针对**文档的此标签具有水印**，选择“**打开**”（如果希望具有水印），或“**关闭**”（如果不希望这样做）。 如果选择“打开”，则指定水印的文本、大小、[字体](#setting-the-font-name)、[颜色](#setting-the-font-color)和对齐方式****。

单击“保存”**** 时，更改将会自动提供给用户和服务。 不再提供单独发布选项。

## <a name="using-variables-in-the-text-string"></a>在文本字符串中使用变量

你可以在文本字符串中为页眉、页脚或水印使用以下变量：

- `${Item.Label}`，针对所选标签。 例如：“常规”

- `${Item.Name}`，针对文件名或电子邮件主题。 例如：JulySales.docx

- `${Item.Location}`，针对文档的路径和文件名，以及电子邮件的主题。 例如：\\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}`，针对文档或电子邮件的所有者（按 Windows 登录用户名）。 例如：rsimone

- `${User.PrincipalName}`，针对文档或电子邮件的所有者（按 Azure 信息保护客户端登录电子邮件地址 (UPN)）。 例如： rsimone@vanarsdelltd.com

- `${Event.DateTime}`，针对设置所选标签时的日期和时间。 例如：2016/8/16 下午 1:30

> [!NOTE]
>此语法区分大小写。 例如，如果为 `Document: ${Item.Name}  Classification: ${Item.Label}` "**常规**" 标签页脚指定字符串，则应用于名为 project.docx 的文档的页脚文本将为 "**文档： project.docx 分类：常规**"。

<!-- REMOVED w JUNE 2020 RELEASE> [!NOTE]
> Use of either the `${User.Name}` and/or `${User.PrincipalName}` variable are currently not supported by the Azure Information Protection unified labeling client. 
-->
>[!TIP]
> 还可以使用[字段代码将标签名称插入](faqs-infoprotect.md#can-i-create-a-document-template-that-automatically-includes-the-classification)到文档或模板中。

## <a name="setting-different-visual-markings-for-word-excel-powerpoint-and-outlook"></a>为 Word、Excel、PowerPoint 和 Outlook 设置不同的视觉标记

默认情况下，指定的视觉标记将应用于 Word、Excel、PowerPoint 和 Outlook。 但是，在文本字符串中使用“If.App”变量语句并使用值 **Word**、**Excel**、**PowerPoint** 或 **Outlook** 标识应用程序类型时，可以为每个 Office 应用程序类型指定视觉标记。 还可以简化这些值，当想要在同一 If.App 语句中指定多个值时，这很有必要。

使用以下语法：

```ps
${If.App.<application type>}<your visual markings text> ${If.End}
```

> [!NOTE]
>此语句中的该语法区分大小写。

示例：

- **仅为 Word 文档设置页眉文本：**

    `${If.App.Word}This Word document is sensitive ${If.End}`

    仅在 Word 文档页眉中，标签应用页眉文本“此 Word 文档包含敏感内容”。 没有页眉文本应用于其他 Office 应用程序。

- **为 Word、Excel 和 Outlook 设置页脚文本，为 PowerPoint 设置不同的页脚文本：**

    `${If.App.WXO}This content is confidential. ${If.End}${If.App.PowerPoint}This presentation is confidential. ${If.End}`

    在 Word、Excel 和 Outlook 中，标签应用页脚文本“此内容是机密的”。 在 PowerPoint 中，标签应用页脚文本“此演示文稿是机密的”。

- **为 Word 和 PowerPoint 设置特定的水印文本，然后为 Word、Excel 和 PowerPoint 设置水印文本：**

    `${If.App.WP}This content is ${If.End}Confidential`

    在 Word 和 PowerPoint 中，标签应用水印文本“此内容保密”。 在 Excel 中，标签应用水印文本“机密”。 在 Outlook 中，标签不应用任何水印文本，因为 Outlook 不支持水印视觉标记。

> [!NOTE]
> 使用 Azure 信息保护统一标签客户端时，仅可使用 Azure 信息保护门户设置**字体名称**的值。 当设置**字体颜色**值超出五个默认值之一时，还可以使用 Azure 信息保护门户。

### <a name="setting-the-font-name"></a>设置字体名称

Calibri 是页眉、页脚和水印文字的默认字体。 如果指定替代字体名称，请确保它在将应用视觉标记的客户端设备上可用。
如果指定字体不可用，客户端将回退使用 Calibri 字体。

### <a name="setting-the-font-color"></a>设置字体颜色

可从可用颜色列表中进行选择，或输入颜色的红绿蓝 (RGB) 组成的十六进制三元色代码来指定自定义颜色。 例如， **#40e0d0**为青绿色的 RGB 十六进制值。

如果需要这些代码的参考，可从 MSDN web 文档的页面找到一个有用的表格 [\<color>](https://developer.mozilla.org/docs/Web/CSS/color_value) 。你还可以在许多应用程序中找到这些代码，以便你编辑图片。 例如，通过 Microsoft 画图，从调色板中选择自定义颜色，系统将自动显示 RGB 值，该值可供复制。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用[配置组织的策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。  
