---
title: class mip::ApplyLabelAction
description: 记录 mip::applylabelaction 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ce813a544504ce18b382cdb86bd31d89b6626fad
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650487"
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