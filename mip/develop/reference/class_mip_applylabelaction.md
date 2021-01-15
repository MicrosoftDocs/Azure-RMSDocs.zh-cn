---
title: 类 ApplyLabelAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 applylabelaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: a88a913ea5dfd958e5ed073f0dff6f0bac1b527f
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212240"
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