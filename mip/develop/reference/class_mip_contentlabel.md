---
title: class mip::ContentLabel
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： contentlabel 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f131885572ab5ad3a2664a6b50162a011529bfbb
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490330"
---
# <a name="class-mipcontentlabel"></a>class mip::ContentLabel 
Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
它还包含特定应用标签实例的属性。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public std：： chrono：： time_point\<std：： chrono：： system_clock\> GetCreationTime （） const  |  获取标签的创建时间。
public AssignmentMethod GetAssignmentMethod() const  |  获取标签的分配方法。
public const std：： vector\<std：:p air\<std：： string，std：： string\>\>& GetExtendedProperties （） const  |  获取扩展属性。
public bool IsProtectionAppliedFromLabel() const  |  获取标签是否应用了保护的指示。
public std：： shared_ptr\<Label\> GetLabel （） const  |  获取应用于内容的实际标签对象。
  
## <a name="members"></a>Members
  
### <a name="getcreationtime-function"></a>GetCreationTime 函数
获取标签的创建时间。

  
**返回**：创建时间。
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod 函数
获取标签的分配方法。

  
**返回结果**：AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
  
**另请参阅**： [Mip：： AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
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