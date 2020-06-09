---
title: 概念-MIP SDK 中的操作理由（c + +）
description: 本文将帮助你了解如何降级或删除需要论证的标签。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: v-anikep
ms.openlocfilehash: 1b0926114dd4d494593bd0d2340fee35edfe5fe6
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548235"
---
# <a name="action-justification-in-mip-sdk-c"></a>MIP SDK 中的操作理由（c + +）

## <a name="overview"></a>概述

安全和合规中心中的标签策略允许管理员要求对标签的删除或降级进行**调整**。 降级定义为应用带有较低敏感度值的标签来替代现有标签。

如前所述，文件 API 提供了易于使用的界面，用于从服务中读取标签、将标签应用于定义的文件类型以及从这些文件类型中读取标签。 它还支持用于删除标签的文件操作，以及更改支持的文件类型上的标签。 对文件标签所做的更改是通过 `mip::FileHandler` 的函数支持的 `SetLabel()` ，它使你能够将新标签设置为不受保护的文件或以前受保护的文件，以及 `mip::FileHandler` `DeleteLabel()` 从以前受保护的文件中删除标签的函数。

对于某些敏感性标签，当用户尝试通过删除标签或通过将标签更改为限制性较低的标签来降级敏感度时，安全管理员可能需要应用更严格的策略。 管理员可以通过选中相应的复选框，使用[安全性和符合性中心](https://sip.compliance.microsoft.com/)中的标签策略配置来配置此设置。

![需要操作理由](./media/justify-action.png)

如果文件具有现有标签，并且如果在敏感度级别降级的情况下，标签策略需要理由，则这些 `SetLabel()` / `DeleteLabel()` 函数将引发 `mip::JustificationRequiredError` 。 在这种情况下，API 提供了记录用户理由的能力。 SDK 使用者应为用户提供应用程序界面，以便提供有关降级原因的输入。 记录对齐后，应用程序可以设置 `isDowngradeJustified` 的属性，以及 `mip::LabelingOptions` 设置 `Justification` 属性。

## <a name="next-steps"></a>后续步骤

- 查看[的操作理由快速入门（c + +）](quick-file-justify-actions-cpp.md)
- 查看[的操作理由快速入门（c #）](quick-file-justify-actions-csharp.md)