---
title: '类 mip:: ApplicationActionState'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: applicationactionstate 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 308918e57cf5495e3da2102ee8caca910c11f670
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893610"
---
# <a name="class-mipapplicationactionstate"></a>类 mip:: ApplicationActionState 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public LabelState GetNewLabelState () const  |  获取新标签状态。
public std:: shared_ptr\<Label\> GetNewLabel () const  |  获取应在文档上应用的敏感度标签 ID。
公共 std::p air\<bool, std:: string\> IsDowngradeJustified () const  |  实现应传递是否提供了降级现有标签的合理理由。
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  获取新标签的分配方法。
public virtual std:: vector\<std::p 风\<std:: string、std:: string\> \> GetNewLabelExtendedProperties () const  |  返回新标签的扩展属性。
public ActionType GetSupportedActions() const  |  获取描述所有受支持操作类型的掩码枚举。
public bool IsRecommendationEnabled () const  |  获取一个布尔值, 表示建议的操作将返回。 默认情况下, 除非用户指定 else, 否则应为 true。
  
## <a name="members"></a>成员
  
### <a name="getnewlabelstate-function"></a>GetNewLabelState 函数
获取新标签状态。

  
**返回**:新标签状态。 
  
**另请参阅**: mip:: LabelState
  
### <a name="getnewlabel-function"></a>GetNewLabel 函数
获取应在文档上应用的敏感度标签 ID。

  
**返回**:如果存在, 则为要应用于内容的敏感度标签 ID, 否则为空以删除标签。
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified 函数
实现应传递是否提供了降级现有标签的合理理由。

  
**返回**:如果降级为 justifiedalong, 则为 True; 否则为 messageelse false 
  
另请参阅：[mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod 函数
获取新标签的分配方法。

  
**返回**:分配方法标准、特权、自动。 
  
**另请参阅**: [Mip:: AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties 函数
返回新标签的扩展属性。

  
**返回**:应用于内容的扩展属性。
  
### <a name="getsupportedactions-function"></a>GetSupportedActions 函数
获取描述所有受支持操作类型的掩码枚举。

  
**返回**:描述所有支持的操作类型的屏蔽枚举。
必须支持 ActionType::Justify。 当策略和标签更改需要合理理由时，将始终返回合理理由操作。
  
### <a name="isrecommendationenabled-function"></a>IsRecommendationEnabled 函数
获取一个布尔值, 表示建议的操作将返回。 默认情况下, 除非用户指定 else, 否则应为 true。

  
**返回**:表示建议操作的布尔值将返回。
要使此字段生效, 必须启用 ActionType:: RecommendLabel。