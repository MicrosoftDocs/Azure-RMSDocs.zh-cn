---
title: 类 mip::RecommendLabelAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： recommendlabelaction 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 629e6410657fcb799e3f71c0ccb3752b82437428
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560028"
---
# <a name="class-miprecommendlabelaction"></a>类 mip::RecommendLabelAction 
建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： shared_ptr\<标签\>& GetLabel （） const  |  获取建议的标签。
public const std：： vector\<std：： string\>& GetClassificationIds （） const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>成員
  
### <a name="getlabel-function"></a>GetLabel 函数
获取建议的标签。

  
**返回**：标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**： Const std：： vector < std：： string > & 导致此标签出现的分类 id 的列表。