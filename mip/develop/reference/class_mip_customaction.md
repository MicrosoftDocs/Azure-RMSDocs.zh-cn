---
title: 类 CustomAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 customaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: d1fb231d76ba2b5f076d42bbeeff95618c7386f3
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211696"
---
# <a name="class-customaction"></a>类 CustomAction 
CustomAction 是一个通用操作类，它捕获操作的所有子属性作为属性包。 调用方负责理解操作的含义。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  获取操作名称。
public const std：： vector \<std::pair\<std::string, std::string\> \>& GetProperties ( # A2 const  |  获取属性键值对列表。
  
## <a name="members"></a>成员
  
### <a name="getname-function"></a>GetName 函数
获取操作名称。

  
返回结果操作名称（如果存在），否则为空字符串。
  
### <a name="getproperties-function"></a>GetProperties 函数
获取属性键值对列表。

  
**返回结果**：键值对列表。