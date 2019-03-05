---
title: class mip::ApplyLabelAction
description: 记录 mip::applylabelaction 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ad1367480497ede6c8efd33d6ebc60c4c6ca34c5
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332219"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
应用标签操作要求，必须调用应用程序，才能应用特定标签。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  获取所需的标签 ID。
public const std:: vector\<std:: string\>& GetClassificationIds() 常量  |  获取的分类 Id 的匹配并导致出现该标签。
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getlabelid-function"></a>GetLabelId 函数
获取所需的标签 ID。

  
**返回**:标签 id。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取的分类 Id 的匹配并导致出现该标签。

  
**返回**:Const std:: vector std:: < string > 和分类导致出现该标签的 Id 的列表。
  
### <a name="gettype-function"></a>GetType 函数
获取[操作](class_mip_action.md)类型。

  
**返回**:ActionType：此基类可以转换成的派生操作类型。
