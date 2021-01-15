---
title: 类 TelemetryEvent
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 telemetryevent：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8776eff24a889a1132fc71d11c38b02c49822263
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224906"
---
# <a name="class-telemetryevent"></a>类 TelemetryEvent 
单个遥测事件。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  获取事件名称。
public EventLevel GetLevel ( # A1 const  |  获取事件级别，指示是否将其视为必需的服务数据 (NSD) 。
public const std：： chrono：： steady_clock：： time_point& GetStartTime ( # A2 常量  |  获取事件开始时间。
public void AddProperty (const std：： shared_ptr \<EventProperty\>& 的内容)   |  将属性添加到事件。
public void AddProperty (const std：： string& name，bool 值)   |  向事件添加一个布尔属性。
public void AddProperty (const std：： string& name、double value、Pii pii)   |  向事件添加一个双精度属性。
public void AddProperty (const std：： string& name、int64_t value、Pii pii)   |  将 int64 属性添加到事件。
public void AddProperty (const std：： string& name，const std：： string& 值，Pii pii)   |  将字符串属性添加到事件。
public void AddAuditOnlyProperty (const std：： string& name，const std：： string& 值)   |  向事件添加只审核的字符串属性。
public std：： vector \<std::shared_ptr\<EventProperty\> \> GetProperties ( # A1 const  |  获取所有事件属性。
public std：： shared_ptr \<EventProperty\> GetProperty (const std：： string& 名称)   |  获取具有给定名称的属性（如果有）。
  
## <a name="members"></a>成员
  
### <a name="getname-function"></a>GetName 函数
获取事件名称。

  
**返回**：事件名称
  
### <a name="getlevel-function"></a>GetLevel 函数
获取事件级别，指示是否将其视为必需的服务数据 (NSD) 。

  
**返回**：事件级别
  
### <a name="getstarttime-function"></a>GetStartTime 函数
获取事件开始时间。

  
**返回**：事件开始时间
  
### <a name="addproperty-function"></a>AddProperty 函数
将属性添加到事件。

参数：  
* 属性 **：要** 添加的属性


  
### <a name="addproperty-function"></a>AddProperty 函数
向事件添加一个布尔属性。

参数：  
* **名称**：属性名称 


* **值**：属性值


  
### <a name="addproperty-function"></a>AddProperty 函数
向事件添加一个双精度属性。

参数：  
* **名称**：属性名称 


* **值**：属性值 


* **pii**： pii 分类


  
### <a name="addproperty-function"></a>AddProperty 函数
将 int64 属性添加到事件。

参数：  
* **名称**：属性名称 


* **值**：属性值 


* **pii**： pii 分类


  
### <a name="addproperty-function"></a>AddProperty 函数
将字符串属性添加到事件。

参数：  
* **名称**：属性名称 


* **值**：属性值 


* **pii**： pii 分类


  
### <a name="addauditonlyproperty-function"></a>AddAuditOnlyProperty 函数
向事件添加只审核的字符串属性。

参数：  
* **名称**：属性名称 


* **值**：属性值


仅审核属性包含敏感信息，并且不得写入文件日志或任何管道（审核除外），直到手动对其进行审核。
  
### <a name="getproperties-function"></a>GetProperties 函数
获取所有事件属性。

  
**返回**：事件属性
  
### <a name="getproperty-function"></a>GetProperty 函数
获取具有给定名称的属性（如果有）。

参数：  
* **name**：要获取的属性的名称



  
**返回**：具有给定名称的属性; 如果没有，则返回 nullptr