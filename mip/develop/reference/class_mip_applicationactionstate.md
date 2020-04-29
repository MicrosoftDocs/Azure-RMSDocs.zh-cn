---
title: 类 ApplicationActionState
description: 记录 Microsoft 信息保护（MIP） SDK 的 applicationactionstate：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 389fd02b47153c6953fefad3ba068add6ff431ee
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763672"
---
# <a name="class-applicationactionstate"></a>类 ApplicationActionState 
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public LabelState GetNewLabelState （） const  |  获取新标签状态。
public std：： shared_ptr\<标签\> GetNewLabel （） const  |  获取应在文档上应用的敏感度标签 ID。
公共 std：:p air\<bool，std：： string\> IsDowngradeJustified （） const  |  实现应传递是否提供了降级现有标签的合理理由。
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  获取新标签的分配方法。
public virtual std：： vector\<std：:p 风\<std：： string、std：： string\> \> GetNewLabelExtendedProperties （） const  |  返回新标签的扩展属性。
public ActionType GetSupportedActions() const  |  获取描述所有受支持操作类型的掩码枚举。
public bool IsRecommendationEnabled （） const  |  获取一个布尔值，表示建议的操作将返回。 默认情况下，除非用户指定 else，否则应为 true。
  
## <a name="members"></a>成员
  
### <a name="getnewlabelstate-function"></a>GetNewLabelState 函数
获取新标签状态。

  
**返回**：新的标签状态。 
  
**另请参阅**： mip：： LabelState
  
### <a name="getnewlabel-function"></a>GetNewLabel 函数
获取应在文档上应用的敏感度标签 ID。

  
**返回结果**：如果存在，则返回要应用于内容的敏感度标签 ID；否则为空以删除标签。
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified 函数
实现应传递是否提供了降级现有标签的合理理由。

  
**返回结果**：如果降级合理并提供了合理理由消息，则返回 true；否则返回 false 
  
**另请参阅**： mip：： JustifyAction
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod 函数
获取新标签的分配方法。

  
**返回结果**：分配方法 STANDARD、PRIVILEGED、AUTO。 
  
**** 另请参阅：mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties 函数
返回新标签的扩展属性。

  
**返回结果**：应用于内容的扩展属性。
  
### <a name="getsupportedactions-function"></a>GetSupportedActions 函数
获取描述所有受支持操作类型的掩码枚举。

  
**返回结果**：描述所有受支持操作类型的掩码枚举。
必须支持 ActionType::Justify。 当策略和标签更改需要合理理由时，将始终返回合理理由操作。
  
### <a name="isrecommendationenabled-function"></a>IsRecommendationEnabled 函数
获取一个布尔值，表示建议的操作将返回。 默认情况下，除非用户指定 else，否则应为 true。

  
**返回**：表示建议操作的布尔值将返回。
要使此字段生效，必须启用 ActionType：： RecommendLabel。