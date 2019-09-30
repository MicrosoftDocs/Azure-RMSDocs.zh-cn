---
title: 在 Azure 信息保护中配置不同语言标签
description: 可以为用户在信息保护栏上看到的标签以及用户看到的任意模板添加对不同语言的支持，方法是在 Azure 信息保护策略中指定语言，并导入翻译。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: e1f5b3c05ae7e8c0717ef4d0227eacda8eeade3e
ms.sourcegitcommit: f14ec329cef1967d2d66b0d550501449ee55abf9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2019
ms.locfileid: "71673899"
---
# <a name="how-to-configure-labels-and-templates-for-different-languages-in-azure-information-protection"></a>如何在 Azure 信息保护中配置不同语言的标签和模板

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

> [!NOTE]
> 这些说明适用于 Azure 信息保护客户端（经典），而不是 Azure 信息保护统一标签客户端。 不确定这些客户端之间有何区别？ 请参见[常见问题解答](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)。
> 
> 如果要查找有关为敏感度标签配置不同语言的信息，请使用 Office 365 安全性和符合性 PowerShell，并使用*LocaleSettings*参数[设置标签](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)。

虽然 Azure 信息保护的默认标签支持多种语言，但必须配置对指定标签名称和说明的支持。 此配置要求执行以下操作：

1. 选择用户使用的语言。 

2. 将当前标签名称和说明导出到一个文件。

3. 编辑该文件，提供你的翻译。

4. 将该文件导入回 Azure 信息保护策略。

以下任一条件适用时，还可配置不同语言的模板。 如果用户或管理员需要以其已本地化的语言查看当前模板名称和说明，则此配置适用。

- 该模板是通过 Azure 经典门户或使用 PowerShell 创建的，它未使用“选择预定义的模板”保护设置链接到标签。

- 由于没有支持标签的订阅，因此只能在 Azure 门户中创建和管理模板。

为 Office 和 Windows 选择与用户的语言设置相匹配的语言。 这些标签名称和说明随后会分别显示在 Office 应用中的“Azure 信息保护”栏，以及“分类和保护 - Azure 信息保护”对话框中。 有关所选语言的详细信息，请参阅此页上的 [Azure 信息保护客户端如何确定要显示的语言](#how-the-azure-information-protection-client-determines-the-language-to- display)部分。 

## <a name="to-configure-labels-and-templates-for-different-languages"></a>配置不同语言的标签和模板

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“管理” > “语言”菜单选项中：在“Azure 信息保护 - 语言”边栏选项卡中，选择“添加新语言以进行翻译”。 选择要添加的语言，然后选择“确定”。 可以在搜索框中键入语言名称，也可以滚动浏览可用语言列表进行选择

3. 现在，所选语言显示在“Azure 信息保护 - 语言”边栏选项卡上：
    
    - 要添加其他语言，请选择“添加新语言以进行翻译”并重复执行上一步骤。 
        
        > [!NOTE]
        > 请务必选择用户所有的适用于 Office 和 Windows 的语言。 在某些情况下，可能需要为每台计算机配置两种不同的选择。
        
    - 如果要更改已添加的任何语言，从列表中选择该条目，然后单击“删除”。

4. 列出你想要支持的所有语言后，选中“语言名称”旁边的复选框以选中所有条目（或者选择单个条目），然后单击“导出”，将现有标签名称和说明的本地副本保存到文件。 
    
    下载的文件名为“exported localization.zip”，保存在本地“下载”文件夹中。 此外，还可以通过在 Azure 门户的状态栏上选择此文件名对其进行访问。

5. 从“exported localization.zip”中提取文件，这样，你所选的每种语言都有可供下载的 .xml 文件。 

6. 编辑每个 .xml 文件：对于 `<LocalizedText>` 标记中的每个字符串，为每种所选语言提供你想要的翻译。 

7. 编辑每个 .xml 文件后，创建一个新的压缩 (zipped) 文件夹来包含这些文件。 压缩文件夹可以具有任何名称，但必须具有 .zip 扩展名。
    
    提示：不必等到编辑完已下载的每个语言文件。 相反，可以通过将已下载的所有文件中的一部分文件包括在 .zip 文件中来分阶段推出不同语言。 完成多种语言的翻译后，重复步骤 7 和 8。

8. 返回到“Azure 信息保护 - 语言”边栏选项卡，然后选择“导入”。 请注意，如果此选项不可用，则首先清除“语言名称”复选框或单独选择的语言对应的复选框。
    
    完成导入后，将为用户下载本地化名称和说明。

如果需要支持一种新语言、创建新标签，或在 Azure 门户中更改标签的名称或说明，则必须重复此过程。

## <a name="how-the-azure-information-protection-client-determines-the-language-to-display"></a>Azure 信息保护客户端如何确定要显示的语言

当用户下载可支持不同语言的 Azure 信息保护策略时，用户看到的标签名称和工具提示的语言由以下逻辑决定：

**对于用户在 Office 应用的 Azure 信息保护栏上看到的标签和工具提示：**

- 如果 Office 应用的语言具有一个直接匹配项，标签名称和说明会以该语言显示。

- 如果 Office 应用的语言无匹配项，标签名称和说明会以你默认为所有用户指定的语言显示。 此语言通常是英语，它是默认策略中使用的语言。

**对于用户在使用右键单击对文件或文件夹进行分类和保护时看到的标签和工具提示：**

- 如果操作系统的语言具有一个直接匹配项，标签名称和说明会以该语言显示。

- 如果操作系统的语言无匹配项，标签名称和说明会以你默认为所有用户指定的语言显示。 此语言通常是英语，它是默认策略中使用的语言。

## <a name="when-localized-label-names-are-not-used"></a>不使用本地化标签名称

在以下情况下，不使用本地化标签（和子标签）名称。 为了保持租户的一致性，始终将默认语言用于以下项：

- 客户端使用情况日志

- PowerShell（从 Get-AIPFileStatus 输出）

- 文档元数据和电子邮件标头


## <a name="next-steps"></a>后续步骤

若要详细了解可针对标签配置的选项以及可针对 Azure 信息保护策略配置的其他设置，请使用[配置组织策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。



