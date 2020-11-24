---
title: 类 RecommendLabelAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 recommendlabelaction：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2a0318c0da7bfc3a2be72c1139754da1f7142d71
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565021"
---
# <a name="class-recommendlabelaction"></a>类 RecommendLabelAction 
建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： shared_ptr \<Label\>& GetLabel ( # A2 const  |  获取建议的标签。
public const std：： vector \<std::string\>& GetClassificationIds ( # A2 const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>成员
  
### <a name="getlabel-function"></a>GetLabel 函数
获取建议的标签。

  
**返回**：标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**： Const std：： vector<std：： string>& 导致此标签出现的分类 id 列表。