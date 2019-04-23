---
title: 类 mip::RecommendLabelAction
description: 记录 mip::recommendlabelaction 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: eeab9022b257ff327e2c83b1d8860662355180e5
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173216"
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