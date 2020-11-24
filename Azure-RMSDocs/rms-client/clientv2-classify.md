---
title: 使用 Azure 信息保护统一标签客户端进行分类
description: 使用 Azure 信息保护适用于 Windows 的统一标签客户端时，如何对文档和电子邮件进行分类的说明。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/03/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 1cb9f1216b8b77b19b8cabb6d884512330221a87
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2020
ms.locfileid: "95565378"
---
# <a name="user-guide-classify-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>用户指南：使用适用于 Windows 的 Azure 信息保护统一标签客户端对文件或电子邮件进行分类

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8*
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP For Windows And office 版本中的扩展支持](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)。*
>
> 说明：[用于 Windows 的 Azure 信息保护统一标记客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

> [!NOTE]
> 借助这些说明，对文档和电子邮件进行分类（但不保护）。 如果还需对文档和电子邮件进行保护，请参阅[分类和保护说明](clientv2-classify-protect.md)。 如果不确定应使用哪组说明，请与管理员或支持人员核实。

在 Office 桌面应用（Word、Excel、PowerPoint、Outlook）中创建和编辑文档和电子邮件时对其进行分类最为简单。 

但是，也可使用文件资源管理器对文件进行分类。 此方法支持其他文件类型，它是一次性对多个文件进行分类的便捷方法。 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>使用 Office 应用对文档和电子邮件进行分类

从 " **主页** " 选项卡上，选择功能区中的 " **敏感度** " 按钮，然后选择一个已为你配置的标签。 例如：

![敏感度按钮示例](../media/sensitivity-not-set-callout.png)

或者，如果选择了 "**敏感度**" 按钮中的 "**显示栏**"，则可以从 Azure 信息保护栏中选择一个标签。 例如：

![Azure 信息保护栏示例](../media/info-protect-barv2-not-set-callout.png)

若要设置标签，例如 "常规"，请选择 " **常规**"。 如果你不确定要将哪种标签应用于当前文档或电子邮件，请使用标签工具提示详细了解每种标签及其应用情况。 

如果已将某种标签应用于文档，并且想要进行更改，可以选择其他标签。 如果已显示 Azure 信息保护栏，并且标签未显示在要选择的栏上，请首先单击当前标签值旁边的 " **编辑标签** " 图标。

除了手动选择标签，还可通过以下方式应用标签：

- 管理员配置了默认标签，你可保留或更改该标签。

- 在检测到敏感信息时，管理员配置的标签将自动设置。

- 在检测到敏感信息时，管理员配置了推荐的标签，并且系统会提示你接受建议 (并且该标签将应用) 或拒绝该标签， (建议的标签未) 应用。

### <a name="exceptions-for-the-sensitivity-button"></a>"敏感度" 按钮的异常

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>在 Office 应用程序中看不到 "敏感度" 按钮？

- 你可能没有 [安装](install-unifiedlabelingclient-app.md)Azure 信息保护统一标签客户端。

- 如果未在功能区上看到 " **敏感度** " 按钮，而是看到带标签的 " **保护** " 按钮，则已安装 azure 信息保护客户端 (经典) ，而不是 azure 信息保护统一标签客户端。 [详细信息](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

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
    
    如果无法选择标签（它们显示为灰色），则所选文件不支持分类。 例如：
    
    ![“分类和保护 - Azure 信息保护”对话框中无可用标签](../media/v2info-protect-dialog-labels-dimmed.png)

3. 如果所选文件不支持分类，请单击“关闭”。 无法对此文件进行分类，也无法对其提供保护。
    
    如果选择标签，请单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。

若要更改所选标签，只需重复此过程，然后选择其他标签即可。

指定的分类会保留在文件中，即使通过电子邮件发送文件或将其保存到其他位置也是如此。 

## <a name="other-instructions"></a>其他说明

有关适用于 Windows 的 Azure 信息保护统一标签客户端的用户指南中的详细操作说明：

- [您希望做什么？](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息

请参阅 [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels)。

