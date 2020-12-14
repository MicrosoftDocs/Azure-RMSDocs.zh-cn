---
title: Azure 信息保护策略概述
description: 了解 Azure 信息保护策略中的标签和设置，并将其下载到 Azure 信息保护客户端。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 21efcc84720849b6164a7754cf82c786a7559192
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386417"
---
# <a name="overview-of-the-azure-information-protection-policies"></a>Azure 信息保护策略概述

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标签客户端，请参阅 Microsoft 365 文档中的 " [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels) "。 *

> [!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月31日** 被 **弃用**。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>

Azure 信息保护策略包含以下可配置的元素：
    
- 包含哪些允许管理员和用户对文档和电子邮件进行分类（并选择性地保护）的标签。

- 用户在 Office 应用程序中看到的信息保护栏的标题和工具提示。

- 将默认标签设置为对文档和电子邮件进行分类的起始点的选项。

- 在用户保存文档和发送电子邮件时强制执行分类的选项。

- 当用户选择比原始级别低的敏感度级别时提示用户提供相应原因的选项。

- 用于自动标记电子邮件的选项（基于电子邮件附件）。

- 控制是否将信息保护栏显示在 Office 应用程序中的选项。

- 控制是否在 Outlook 中显示“不转发”按钮的选项。

- 允许用户指定自己文档权限的选项。

- 为用户提供自定义帮助链接的选项。

Azure 信息保护附带[默认策略](configure-policy-default.md)，其中包含五个主要标签。 这些标签中有 2 个包含子标签，可根据需要提供子类别。 

为子标签配置标签时，用户不能选择主标签，但必须选择一个子标签。 在此情况下，支持将主标签仅作为名称和颜色的显示容器。

Azure 信息保护标签可用于组织常规创建和存储的数据，包括从最低等级的个人数据到最高等级的机密数据等各类数据。 

可以使用无更改的默认标签，或者你可以自定义它们，或删除它们，并可以创建新标签。 有关完整说明，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

## <a name="next-steps"></a>后续步骤

有关如何自定义 Azure 信息保护策略以及查看所导致的用户行为的示例，请尝试学习以下教程：

- [编辑 Azure 信息保护策略并创建新标签](infoprotect-quick-start-tutorial.md)

- [配置协同工作的 Azure 信息保护策略设置](infoprotect-settings-tutorial.md)