---
title: 更改 Azure 信息保护标签 - AIP
description: 可以更改或细化用户在“信息保护”栏上看到的标签，方法是在 Azure 信息保护策略中对其进行配置。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 4f8a58ccb9d237a5a3d784a9f92c57e07b6ac21f
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806799"
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>如何更改或自定义 Azure 信息保护的现有标签

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标签客户端，请参阅 Microsoft 365 文档中的 " [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels) "。 *

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

通过在 Azure 门户中配置标签，可以更改或优化用户在“信息保护”栏或从 Office 功能区的“保护”按钮看到的任何标签。

例如，可以更改标签或子标签名称、工具提示、颜色和顺序。 可以更改标签是否适用于页脚或水印等视觉标记。 还可以更改标签是否适用于保护、建议的分类或自动分类。

若要更改标签，请按照以下说明进行操作：

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到“Azure 信息保护”窗格。 
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。

2. 从 "**分类**  >  **标签**" 菜单选项：在 " **Azure 信息保护-标签**" 窗格中，选择要更改的标签。

    除非你想要对标签进行重新排序：右键单击标签或选择标签的上下文菜单（而不是选择标签）。 然后，选择“上移”或“下移”选项。

3. 无论何时在新窗格中进行更改，如果想要保留所做的更改，请单击该窗格上的 " **保存** "。
    
    单击“保存”时，更改将会自动提供给用户和服务。 不再提供单独发布选项。

4. 如果已更改标签显示名称或说明并已为其他语言配置了这些项：请重新导出 Azure 信息保护策略，提供新的翻译，然后导入所做的更改。 有关详细信息，请参阅[如何为不同语言配置标签](configure-policy-languages.md)。

> [!TIP]
>如果要将某个默认标签恢复为默认值，请使用[默认信息保护策略](configure-policy-default.md)中的信息。

## <a name="next-steps"></a>后续步骤

有关配置可以为标签生成的选项以及 Azure 信息保护策略的其他设置的详细信息，请使用[配置组织的策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。



