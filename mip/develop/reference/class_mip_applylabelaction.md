---
title: 类 ApplyLabelAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 applylabelaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: df208a53f6cd6ec3806e91c28901a3005b801742
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763716"
---
# <a name="class-applylabelaction"></a>类 ApplyLabelAction 
应用标签操作要求，必须调用应用程序，才能应用特定标签。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： shared_ptr\<标签\>& GetLabel （） const  |  获取所需的标签。
public const std：： vector\<std：： String\>& GetClassificationIds （） const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>成员
  
### <a name="getlabel-function"></a>GetLabel 函数
获取所需的标签。

  
**返回**：标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**： Const std：： vector<std：： string>& 导致此标签出现的分类 id 列表。