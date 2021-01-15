---
title: 类 EventProperty
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 eventproperty：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 5ee28e454aa5d7854c572df8ef6e4642482c1104
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224915"
---
# <a name="class-eventproperty"></a>类 EventProperty 
单个审核/遥测属性。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public EventPropertyType GetPropertyType ( # A1 const  |  获取此属性的基础数据类型。
public const std::string& GetName() const  |  获取属性的名称。
公有 Pii GetPii ( # A1 const  |  获取个人身份信息 (PII) 分类（如果有）。
public bool IsAuditOnly ( # A1 const  |  获取此属性是否限制为审核管道。
public double GetDouble ( # A1 const  |   (双精度值获取属性值) 
public int64_t GetInt64 ( # A1 const  |  获取属性值 (int64) 
public const std：： string& GetString ( # A2 const  |  获取属性值 (字符串) 
  
## <a name="members"></a>成员
  
### <a name="getpropertytype-function"></a>GetPropertyType 函数
获取此属性的基础数据类型。

  
**返回**：基础数据类型
  
### <a name="getname-function"></a>GetName 函数
获取属性的名称。

  
**返回**：属性的名称
  
### <a name="getpii-function"></a>GetPii 函数
获取个人身份信息 (PII) 分类（如果有）。

  
**返回**： PII 分类
  
### <a name="isauditonly-function"></a>IsAuditOnly 函数
获取此属性是否限制为审核管道。

  
**返回**：如果此值为 true，则此属性是否限制为审核管道，属性包含敏感信息，并且不得写入文件日志或除审核之外的任何管道，直到手动进行了审核。
  
### <a name="getdouble-function"></a>GetDouble 函数
 (双精度值获取属性值) 

  
**返回**：属性值
  
### <a name="getint64-function"></a>GetInt64 函数
获取属性值 (int64) 

  
**返回**：属性值
  
### <a name="getstring-function"></a>GetString 函数
获取属性值 (字符串) 

  
**返回**：属性值