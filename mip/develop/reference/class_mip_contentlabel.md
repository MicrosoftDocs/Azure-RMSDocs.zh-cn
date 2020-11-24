---
title: 类 ContentLabel
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 contentlabel：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a60244b9db9b3087dde71cbdbcf63ba170cb06c3
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565202"
---
# <a name="class-contentlabel"></a>类 ContentLabel 
Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
它还包含特定应用标签实例的属性。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std：： chrono：： time_point \<std::chrono::system_clock\> GetCreationTime ( # A1 const  |  获取标签的创建时间。
public AssignmentMethod GetAssignmentMethod() const  |  获取标签的分配方法。
public const std：： vector \<MetadataEntry\>& GetExtendedProperties ( # A2 const  |  获取扩展属性。
public bool IsProtectionAppliedFromLabel() const  |  获取标签是否应用了保护的指示。
public std::shared_ptr\<Label\> GetLabel() const  |  获取应用于内容的实际标签对象。
  
## <a name="members"></a>成员
  
### <a name="getcreationtime-function"></a>GetCreationTime 函数
获取标签的创建时间。

  
**返回**：创建时间。
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod 函数
获取标签的分配方法。

  
**返回结果**：AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
  
另请参阅：mip::AssignmentMethod
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties 函数
获取扩展属性。

  
**返回结果**：扩展属性。
  
### <a name="isprotectionappliedfromlabel-function"></a>IsProtectionAppliedFromLabel 函数
获取标签是否应用了保护的指示。

  
**返回结果**：如果有模板保护并且由此标签提供，则返回 true；否则返回 false。
  
### <a name="getlabel-function"></a>GetLabel 函数
获取应用于内容的实际标签对象。

  
**返回结果**：应用于内容的标签对象。 
  
**另请参阅**： mip：： Label