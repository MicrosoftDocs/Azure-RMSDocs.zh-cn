---
title: 类 mip::RecommendLabelAction
description: 记录 mip::recommendlabelaction 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 085bcd9438c1a4753cde6a9c99036cc7cb53e440
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332610"
---
# <a name="class-miprecommendlabelaction"></a>类 mip::RecommendLabelAction 
建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  获取建议的标签 ID。
public const std:: vector\<std:: string\>& GetClassificationIds() 常量  |  获取的分类 Id 的匹配并导致出现该标签。
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getlabelid-function"></a>GetLabelId 函数
获取建议的标签 ID。

  
**返回**:标签 id。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取的分类 Id 的匹配并导致出现该标签。

  
**返回**:Const std:: vector std:: < string > 和分类导致出现该标签的 Id 的列表。
  
### <a name="gettype-function"></a>GetType 函数
获取[操作](class_mip_action.md)类型。

  
**返回**:ActionType：此基类可以转换成的派生操作类型。
