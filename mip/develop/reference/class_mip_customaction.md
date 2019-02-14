---
title: class mip::CustomAction
description: 记录 mip::customaction 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: a0e58673b39f8f68ec19ad7a8be407fa93ad8ea9
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254911"
---
# <a name="class-mipcustomaction"></a>class mip::CustomAction 
[CustomAction](class_mip_customaction.md) 是一个泛型操作类，它捕获操作的所有子属性作为一个属性包。 调用方负责理解操作的含义。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  获取操作名称。
public const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& GetProperties() 常量  |  获取属性键值对列表。
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getname-function"></a>GetName 函数
获取操作名称。

  
**返回**:如果将操作名称存在，否则为空字符串。
  
### <a name="getproperties-function"></a>GetProperties 函数
获取属性键值对列表。

  
**返回**:键值对列表。
  
### <a name="gettype-function"></a>GetType 函数
获取[操作](class_mip_action.md)类型。

  
**返回**:ActionType：此基类可以转换成的派生操作类型。
