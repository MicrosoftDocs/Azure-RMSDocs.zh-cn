---
title: 类 RecommendLabelAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 recommendlabelaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3990d6de9d78002d9c240e621f96351cd337aabb
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764540"
---
# <a name="class-recommendlabelaction"></a>类 RecommendLabelAction 
建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： shared_ptr\<标签\>& GetLabel （） const  |  获取建议的标签。
public const std：： vector\<std：： String\>& GetClassificationIds （） const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>成员
  
### <a name="getlabel-function"></a>GetLabel 函数
获取建议的标签。

  
**返回**：标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**： Const std：： vector<std：： string>& 导致此标签出现的分类 id 列表。