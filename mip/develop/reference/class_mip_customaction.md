---
title: 类 CustomAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 customaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 82f6ccc0e44fc5d055a1b4785c33d473dbedabf6
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763385"
---
# <a name="class-customaction"></a>类 CustomAction 
CustomAction 是一个通用操作类，它捕获操作的所有子属性作为属性包。 调用方负责理解操作的含义。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  获取操作名称。
public const std：： vector\<std：:p air\<std：： string，std：： string\> \>& GetProperties （） const  |  获取属性键值对列表。
  
## <a name="members"></a>成员
  
### <a name="getname-function"></a>GetName 函数
获取操作名称。

  
返回结果**** 操作名称（如果存在），否则为空字符串。
  
### <a name="getproperties-function"></a>GetProperties 函数
获取属性键值对列表。

  
**返回结果**：键值对列表。