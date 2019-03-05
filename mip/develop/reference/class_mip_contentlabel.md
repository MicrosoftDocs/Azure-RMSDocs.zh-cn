---
title: class mip::ContentLabel
description: '记录 mip:: contentlabel 类的 Microsoft 信息保护 (MIP) SDK。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 34e4395858713219361e4e2ccf8308d89bc5f29d
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330485"
---
# <a name="class-mipcontentlabel"></a>class mip::ContentLabel 
Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
它还包含特定应用标签实例的属性。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetCreationTime() const  |  获取标签的创建时间。
public AssignmentMethod GetAssignmentMethod() const  |  获取标签的分配方法。
public const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& GetExtendedProperties() 常量  |  获取扩展属性。
public bool IsProtectionAppliedFromLabel() const  |  获取标签是否应用了保护的指示。
public std::shared_ptr\<Label\> GetLabel() const  |  获取应用于内容的实际标签对象。
  
## <a name="members"></a>成員
  
### <a name="getcreationtime-function"></a>GetCreationTime 函数
获取标签的创建时间。

  
**返回**:GMT 字符串形式的创建时间。
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod 函数
获取标签的分配方法。

  
**返回**:AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
  
**另请参阅**: [mip::AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties 函数
获取扩展属性。

  
**返回**:扩展的属性。
  
### <a name="isprotectionappliedfromlabel-function"></a>IsProtectionAppliedFromLabel 函数
获取标签是否应用了保护的指示。

  
**返回**:如果没有模板保护措施，并且它是通过此标签，否则为 false，则为 true。
  
### <a name="getlabel-function"></a>GetLabel 函数
获取应用于内容的实际标签对象。

  
**返回**:应用于内容的标签对象。 
  
另请参阅：[mip::Label](class_mip_label.md)
