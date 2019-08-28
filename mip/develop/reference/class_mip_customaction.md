---
title: class mip::CustomAction
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: customaction 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 7e78d11cc85af5550a4d6ab235b3754d72b2c012
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055177"
---
# <a name="class-mipcustomaction"></a>class mip::CustomAction 
[CustomAction](class_mip_customaction.md) 是一个泛型操作类，它捕获操作的所有子属性作为一个属性包。 调用方负责理解操作的含义。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  获取操作名称。
public const std:: vector\<std::p air\<std:: string, std:: string\>\>& GetProperties () const  |  获取属性键值对列表。
  
## <a name="members"></a>成员
  
### <a name="getname-function"></a>GetName 函数
获取操作名称。

  
**返回**:操作名称 (如果存在), 否则为空字符串。
  
### <a name="getproperties-function"></a>GetProperties 函数
获取属性键值对列表。

  
**返回**:键值对列表。