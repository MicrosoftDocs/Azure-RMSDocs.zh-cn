---
title: 类 ApplyLabelAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 applylabelaction：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 1de755d141cd86441ef3eb756d1f46dbdd73f2c4
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565231"
---
# <a name="class-applylabelaction"></a>类 ApplyLabelAction 
应用标签操作要求，必须调用应用程序，才能应用特定标签。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： shared_ptr \<Label\>& GetLabel ( # A2 const  |  获取所需的标签。
public const std：： vector \<std::string\>& GetClassificationIds ( # A2 const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>成员
  
### <a name="getlabel-function"></a>GetLabel 函数
获取所需的标签。

  
**返回**：标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**： Const std：： vector<std：： string>& 导致此标签出现的分类 id 列表。