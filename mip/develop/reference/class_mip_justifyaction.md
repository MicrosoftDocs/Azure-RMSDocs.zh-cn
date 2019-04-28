---
title: class mip::JustifyAction
description: '记录 mip:: justifyaction 类的 Microsoft 信息保护 (MIP) SDK。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: c0968fd019e8c251703a8f23f35ce03e421fffc3
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173994"
---
# <a name="class-mipjustifyaction"></a>class mip::JustifyAction 
Justify[Action](class_mip_action.md) 要求必须合理解释标签降级，并设置执行状态下的响应。
  
另请参阅：[mip::ExecutionState::IsDowngradeJustified](class_mip_executionstate.md#isdowngradejustified-function)
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。

## <a name="members"></a>成員
  
### <a name="gettype-function"></a>GetType 函数
获取[操作](class_mip_action.md)类型。

  
**返回**:ActionType：此基类可以转换成的派生操作类型。
