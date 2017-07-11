---
title: "在 Azure 信息保护中配置不同语言标签"
description: "可以为用户在信息保护栏上看到的标签添加对不同语言的支持，方法是在 Azure 信息保护策略中指定语言，并将其导入你的翻译。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.openlocfilehash: ec99bf36e8904a7304a9d33c32d17ba92e2e22d2
ms.sourcegitcommit: 8b768e7e249e124f24acdf630d165eaf743f9c21
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2017
---
<a id="how-to-configure-labels-for-different-languages-in-azure-information-protection" class="xliff"></a>

# 如何在 Azure 信息保护中配置不同语言标签

>适用于：Azure 信息保护

>[!NOTE]
>此功能目前处于预览状态，将与 Azure 信息保护客户端的**预览**版本（可从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载）结合使用。

默认情况下，标签的名称和说明支持向组织中所有用户显示的一种语言。 可以通过选择需要的语言来添加对不同语言的支持，将当前标签名称和说明导出到一个文件中，编辑该文件以提供你的翻译，然后将该文件导入回 Azure 信息保护策略。

为 Office 和 Windows 选择与用户的语言设置相匹配的语言。 这些标签名称和说明随后会分别显示在 Office 应用中的 Azure 信息保护栏，以及“分类和保护 - Azure 信息保护”对话框中。 有关所选语言的详细信息，请参阅此页上的 [Azure 信息保护客户端如何确定要显示的语言](#how-the-azure-information-protection-client-determines-the-language-to- display)部分。 

<a id="to-configure-labels-to-display-in-different-languages" class="xliff"></a>

## 配置标签以显示不同语言

1. 如果尚未执行此操作，请在新的浏览器窗口中以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 在初始“Azure 信息保护”边栏选项卡上，找到“管理”，然后选择“语言（预览）”。

3. 在“Azure 信息保护 - 语言（预览）”边栏选项卡上，通过在搜索框中输入键入名称，或通过滚动浏览可用语言列表，找到你希望添加的第一种语言。 

4. 选择语言，然后选择“确定”。

5. 在下一个边栏选项卡上，可以看到添加到列表的所选语言：
    
    - 若要添加其他语言，请选择“为翻译添加新语言”并重复执行步骤 3 和步骤 4。 
        
        > [!NOTE]
        > 请务必选择用户所有的适用于 Office 和 Windows 的语言。 在某些情况下，可能需要为每台计算机配置两种不同的选择。
        
    - 如果要更改已添加的任何语言，从列表中选择该条目，然后单击“删除”。

6. 列出你想要支持的所有语言后，选中“语言名称”旁边的复选框以选中所有条目（或者选择单个条目），然后单击“导出”，将现有标签名称和说明的本地副本保存到文件。 
    
    下载的文件名为“exported localization.zip”，保存在本地“下载”文件夹中。 此外，还可以通过在 Azure 门户的状态栏上选择此文件名对其进行访问。

7. 从“exported localization.zip”中提取文件，这样，你所选的每种语言都有可供下载的 .xml 文件。 

8. 编辑每个 .xml 文件：对于 `<LocalizedText>` 标签中的每个字符串，为每种所选语言提供你想要的翻译。 

9. 编辑每个 .xml 文件后，创建一个新的压缩 (zipped) 文件夹来包含这些文件。 压缩文件夹可以具有任何名称，但必须具有 .zip 扩展名。

10. 返回到 Azure 门户边栏选项卡并选择“导入”。 请注意，如果此选项不可用，则首先清除“语言名称”复选框或单独选择的语言对应的复选框。
    
    导入完成后，本地化的标签名称和说明将在你下次发布 Azure 信息保护策略后为用户下载。 可以单击“全局策略”或“范围策略”边栏选项卡中的“发布”。

<a id="how-the-azure-information-protection-client-determines-the-language-to-display" class="xliff"></a>

## Azure 信息保护客户端如何确定要显示的语言

当用户下载可支持不同语言的 Azure 信息保护策略时，用户看到的标签名称和工具提示的语言由以下逻辑决定：

**对于用户在 Office 应用的 Azure 信息保护栏上看到的标签和工具提示：**

- 如果 Office 应用的语言具有一个直接匹配项，标签名称和说明会以该语言显示。

- 如果 Office 应用的语言无匹配项，标签名称和说明会以你默认为所有用户指定的语言显示。 此语言通常是英语，它是默认策略中使用的语言。

**对于用户在使用右键单击对文件或文件夹进行分类和保护时看到的标签和工具提示：**

- 如果操作系统的语言具有一个直接匹配项，标签名称和说明会以该语言显示。

- 如果操作系统的语言无匹配项，标签名称和说明会以你默认为所有用户指定的语言显示。 此语言通常是英语，它是默认策略中使用的语言。

<a id="when-localized-label-names-are-not-used" class="xliff"></a>

## 不使用本地化标签名称

在以下情况下，不使用本地化标签（和子标签）名称。 为了保持租户的一致性，始终将默认语言用于以下项：

- 客户端使用情况日志

- PowerShell（从 Get-AIPFileStatus 输出）

- 文档元数据和电子邮件标头


<a id="next-steps" class="xliff"></a>

## 后续步骤

若要详细了解可针对标签配置的选项以及可针对 Azure 信息保护策略配置的其他设置，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


