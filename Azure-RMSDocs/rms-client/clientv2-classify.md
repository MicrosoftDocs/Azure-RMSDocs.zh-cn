---
title: 通过用于 Windows 的 Azure 信息保护统一标记客户端进行分类
description: 有关如何进行分类的文档和电子邮件时使用 Azure 信息保护统一标记适用于 Windows 的客户端的说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 630959840574c0441719d317dda254242cad3b3d
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60182970"
---
# <a name="user-guide-classify-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>用户指南：通过使用 Windows Azure 信息保护统一标记客户端中对文件或电子邮件进行分类

>适用范围：*[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）*
>
> *说明：[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> 借助这些说明，对文档和电子邮件进行分类（但不保护）。 如果还需对文档和电子邮件进行保护，请参阅[分类和保护说明](clientv2-classify-protect.md)。 如果不确定应使用哪组说明，请与管理员或支持人员核实。

对文档和电子邮件进行分类的最简单方式是在如下 Office 桌面应用中创建和编辑它们：Word、Excel、PowerPoint、Outlook。 

但是，也可使用文件资源管理器对文件进行分类。 此方法支持其他文件类型，它是一次性对多个文件进行分类的便捷方法。 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>使用 Office 应用对文档和电子邮件进行分类

从**主页**选项卡上，选择**敏感度**功能区中，按钮，然后选择一个已为你配置的标签。 例如：

![敏感度按钮示例](../media/sensitivity-not-set-callout.png)

或者，如果所选**显示数据条**从**敏感度**按钮，您可以从 Azure 信息保护栏选择标签。 例如：

![Azure 信息保护栏示例](../media/info-protect-barv2-not-set-callout.png)

若要设置标签，例如"常规"，选择**常规**。 如果你不确定要将哪种标签应用于当前文档或电子邮件，请使用标签工具提示详细了解每种标签及其应用情况。 

如果已将某种标签应用于文档，并且想要进行更改，可以选择其他标签。 如果已经显示了 Azure 信息保护栏中，并且不为您进行选择，首先单击栏上显示标签，则**编辑标签**图标，当前标签值旁边。

除了手动选择标签，还可通过以下方式应用标签：

- 管理员配置了默认标签，你可保留或更改该标签。

- 您的管理员配置标签以检测到敏感信息时自动设置。

- 管理员配置时，建议使用标签检测到敏感信息时，系统会提示你接受此建议 （和应用标签），或拒绝它 （不应用建议的标签）。

### <a name="exceptions-for-the-sensitivity-button"></a>敏感度按钮的异常

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>看不到 Office 应用程序中的敏感度按钮？

- 您可能不具有 Azure 信息保护统一标记客户端[安装](install-unifiedlabelingclient-app.md)。

- 如果没有看到**敏感度**按钮在功能区上，但看**保护**按钮与标签，则必须安装了 Azure 信息保护客户端并不在 Azure 信息保护统一标记的客户端。 [详细信息](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>没有显示希望看到的标签？ 

- 如果管理员最近为你配置了新标签，请尝试关闭 Office 应用程序的所有实例，然后重新打开。 此操作将检查对你的标签所做的更改。

- 此标签采用的作用域策略可能不包括你的帐户。 请与你的技术支持或管理员一起检查。


## <a name="using-file-explorer-to-classify-files"></a>使用文件资源管理器对文件进行分类

使用文件资源管理器时，可快速对单个文件、多个文件或文件夹进行分类。 

选择文件夹时，将自动为你设置的分类选项选择该文件夹及其所有子文件夹中的所有文件。 但不会自动对在该文件夹或子文件夹中创建的新文件进行分类。

使用文件资源管理器对文件进行分类时，如果一个或多个标签显示为灰色，则所选文件不支持分类，也不会对其进行保护。

管理员指南包含支持分类但不保护的文件类型完整列表：[仅分类支持的文件类型](clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only)。

### <a name="to-classify-a-file-by-using-file-explorer"></a>使用文件资源管理器对文件进行分类

1. 在文件资源管理器中，选择你的文件、多个文件或文件夹。 右键单击，然后选择“分类和保护”。 例如：
    
    ![在文件资源管理器中，右键单击“使用 Azure 信息保护进行分类和保护”](../media/right-click-classify-protect-folder.png)

2. 在“分类和保护 - Azure信息保护”对话框中，请像在 Office 应用程序中那样使用标签，这样可以按管理员定义的方式设置分类。 
    
    如果没有标签可以选择（它们呈灰显状态）：所选的文件不支持分类。 例如：
    
    ![“分类和保护 - Azure 信息保护”对话框中无可用标签](../media/v2info-protect-dialog-labels-dimmed.png)

3. 如果所选文件不支持分类，请单击“关闭”。 无法对此文件进行分类，也无法对其提供保护。
    
    如果选择标签，请单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。

若要更改所选标签，只需重复此过程，然后选择其他标签即可。

指定的分类会保留在文件中，即使通过电子邮件发送文件或将其保存到其他位置也是如此。 

## <a name="other-instructions"></a>其他说明

有关 Windows 的 Azure 信息保护统一标记客户的用户从多个操作说明指南：

- [要执行什么操作？](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息

请参阅[概述的敏感度标签](/Office365/SecurityCompliance/sensitivity-labels)。

