---
title: 概念-MIP SDK 中的操作理由
description: 本文可帮助你了解如何降级或删除需要理由的标签。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: mbaldwin
ms.openlocfilehash: b6f5ebaa08a2726671f891c583d46f310952d1d2
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864934"
---
# <a name="action-justification-in-mip-sdk"></a>MIP SDK 中的操作理由

## <a name="overview"></a>概述

安全和合规中心中的标签策略允许管理员要求对标签的删除或降级进行 **调整** 。 降级定义为应用带有较低敏感度值的标签来替代现有标签。

如前所述，文件 API 提供了易于使用的界面，用于从服务中读取标签、将标签应用于定义的文件类型以及从这些文件类型中读取标签。 它还支持用于删除和更改支持的文件类型的标签的文件操作。 对文件标签所做的更改是通过 `mip::FileHandler` 的函数支持的 `SetLabel()` ，它使你能够将新标签设置为不受保护的文件或以前受保护的文件，以及 `mip::FileHandler` `DeleteLabel()` 从以前受保护的文件中删除标签的函数。

对于某些敏感性标签，当用户尝试通过删除标签或通过将标签更改为限制性较低的标签来降级敏感度时，安全管理员可能需要应用更严格的策略。 管理员可以通过选中相应的复选框，使用 [安全性和符合性中心](https://sip.compliance.microsoft.com/) 中的标签策略配置来配置此设置。

![需要操作理由](./media/justify-action.png)

如果文件具有现有标签，并且标签策略要求在对标签进行降级时进行调整，则这些 `SetLabel()` / `DeleteLabel()` 函数将引发 `mip::JustificationRequiredError` 。 应用程序必须捕获此异常，并为用户提供应用程序接口，以提供有关降级原因的输入。 记录对齐后，应用程序可以设置 `isDowngradeJustified` 的属性，以及 `mip::LabelingOptions` 设置 `Justification` 属性。

## <a name="next-steps"></a>后续步骤

- 查看 [ (c + +) 的操作理由快速入门 ](quick-file-justify-actions-cpp.md)
- 查看 [ (c # ) 的操作理由快速入门 ](quick-file-justify-actions-csharp.md)