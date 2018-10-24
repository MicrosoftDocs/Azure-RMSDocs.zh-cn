---
title: 类 mip ContentLabel
description: 类 mip ContentLabel 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c105f620ed2cd3d6f1427f2543784ea66ce2c4d7
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446016"
---
# <a name="class-mipcontentlabel"></a>class mip::ContentLabel 
Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
它还包含特定应用标签实例的属性。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const std::string& GetCreationTime() const  |  获取标签的创建时间。
 public AssignmentMethod GetAssignmentMethod() const  |  获取标签的分配方法。
public const std::vector<std::pair<std::string, std::string>>& GetExtendedProperties() const  |  获取扩展属性。
 public bool IsProtectionAppliedFromLabel() const  |  获取标签是否应用了保护的指示。
public std::shared_ptr<Label> GetLabel() const  |  获取应用于内容的实际标签对象。
  
## <a name="members"></a>成員
  
### <a name="getcreationtime"></a>GetCreationTime
获取标签的创建时间。

  
**返回结果**：GMT 字符串形式的创建时间。
  
### <a name="getassignmentmethod"></a>GetAssignmentMethod
获取标签的分配方法。

  
**返回结果**：AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
  
另请参阅：mip::AssignmentMethod
  
### <a name="getextendedproperties"></a>GetExtendedProperties
获取扩展属性。

  
**返回结果**：扩展属性。
  
### <a name="isprotectionappliedfromlabel"></a>IsProtectionAppliedFromLabel
获取标签是否应用了保护的指示。

  
**返回结果**：如果有模板保护并且由此标签提供，则返回 true；否则返回 false。
  
### <a name="label"></a>Label
获取应用于内容的实际标签对象。

  
**返回结果**：应用于内容的标签对象。 
  
另请参阅：[mip::Label](class_mip_label.md)