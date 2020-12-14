---
title: 分类-Azure 信息保护经典客户端
description: 有关使用适用于 Windows 的 Azure 信息保护经典客户端时如何对文档和电子邮件进行分类的说明。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/09/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d65c7690-fab7-4823-845c-8c73903e9c79
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 0b96e2680239c87a350e4dee7dbf75db75cd8340
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385941"
---
# <a name="user-guide-classify-a-file-or-email-with-the-azure-information-protection-classic-client"></a>用户指南：使用 Azure 信息保护经典客户端对文件或电子邮件进行分类

>***适用于**： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月31日** 被 **弃用**。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

> [!TIP]
> 借助这些说明，对文档和电子邮件进行分类（但不保护）。 如果还需对文档和电子邮件进行保护，请参阅[分类和保护说明](client-classify-protect.md)。 如果不确定应使用哪组说明，请与管理员或支持人员核实。

在 Office 桌面应用（Word、Excel、PowerPoint、Outlook）中创建和编辑文档和电子邮件时对其进行分类最为简单。 

但是，也可使用文件资源管理器对文件进行分类。 此方法支持其他文件类型，它是一次性对多个文件进行分类的便捷方法。 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>使用 Office 应用对文档和电子邮件进行分类

使用 Azure 信息保护栏并选择其中一个已为你配置的标签。 

例如，在下图中，因为“敏感度”显示“未设置”，因此尚未标记文档。 要设置标签，例如“常规”，请单击“常规”。 如果你不确定要将哪种标签应用于当前文档或电子邮件，请使用标签工具提示详细了解每种标签及其应用情况。 

![Azure 信息保护栏示例](../media/info-protect-bar-not-set-callout.png)

如果已将某种标签应用于文档，并且想要进行更改，可以选择其他标签。 如果标签没有显示在栏上，请首先单击当前标签值旁边的“编辑标签”图标。

> [!TIP]
> 还可从“文件”选项卡上的“保护”按钮中选择标签。

除了手动选择标签，还可通过以下方式应用标签：

- 管理员配置了默认标签，你可保留或更改该标签。

- 管理员配置了建议提示，当检测到敏感数据时将提示选择特定标签。 你可以接受此建议（应用标签），或拒绝建议（不应用建议标签）。

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Azure 信息保护栏的异常 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>你的 Office 应用程序中看不到此信息保护栏？

- 可能未[安装](install-client-app.md) Azure 信息保护客户端。

- 安装了客户端，但管理员配置的设置不显示信息保护栏。 可改为从 Office 功能区“文件”选项卡上的“保护”按钮选择标签。 

##### <a name="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar"></a>你希望看到的标签没有显示在栏上？ 

- 如果管理员最近为你配置了新标签，请尝试关闭 Office 应用程序的所有实例，然后重新打开。 此操作将检查对你的标签所做的更改。

- 此标签采用的作用域策略可能不包括你的帐户。 请与你的技术支持或管理员一起检查。


## <a name="using-file-explorer-to-classify-files"></a>使用文件资源管理器对文件进行分类

使用文件资源管理器时，可快速对单个文件、多个文件或文件夹进行分类。 

选择文件夹时，将自动为你设置的分类选项选择该文件夹及其所有子文件夹中的所有文件。 但不会自动对在该文件夹或子文件夹中创建的新文件进行分类。

使用文件资源管理器对文件进行分类时，如果一个或多个标签显示为灰色，则所选文件不支持分类，也不会对其进行保护。

管理员指南包含支持分类但不保护的文件类型完整列表：[仅分类支持的文件类型](client-admin-guide-file-types.md#file-types-supported-for-classification-only)。

### <a name="to-classify-a-file-by-using-file-explorer"></a>使用文件资源管理器对文件进行分类

1. 在文件资源管理器中，选择你的文件、多个文件或文件夹。 右键单击，然后选择“分类和保护”。 例如：
    
    ![在文件资源管理器中，右键单击“使用 Azure 信息保护进行分类和保护”](../media/right-click-classify-protect-folder.png)

2. 在“分类和保护 - Azure信息保护”对话框中，请像在 Office 应用程序中那样使用标签，这样可以按管理员定义的方式设置分类。 
    
    如果无法选择标签（它们显示为灰色），则所选文件不支持分类。 例如：
    
    ![“分类和保护 - Azure 信息保护”对话框中无可用标签](../media/info-protect-dialog-labels-dimmed.png)

3. 如果所选文件不支持分类，请单击“关闭”。 无法对此文件进行分类，也无法对其提供保护。
    
    如果选择标签，请单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。

若要更改所选标签，只需重复此过程，然后选择其他标签即可。

指定的分类会保留在文件中，即使通过电子邮件发送文件或将其保存到其他位置也是如此。 
## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [您希望做什么？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
请参阅[配置 Azure 信息保护策略](../configure-policy.md)。

