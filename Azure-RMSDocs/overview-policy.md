---
title: Azure 信息保护策略概述
description: 了解 Azure 信息保护策略中的标签和设置。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/27/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 29f573ae997431d621a616eccb9591c830ae8e9c
ms.sourcegitcommit: 1fe9720526a2ff814cd5d353249b16497cfcaadc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425923"
---
# <a name="overview-of-the-azure-information-protection-policy"></a>Azure 信息保护策略概述

>适用范围：*[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*

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
