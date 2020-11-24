---
title: 类 CustomAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 customaction：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: fc67920b517f3a9f75c395b42350cec9d75b23b3
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565194"
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