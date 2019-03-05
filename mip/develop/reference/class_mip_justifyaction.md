---
title: class mip::JustifyAction
description: '记录 mip:: justifyaction 类的 Microsoft 信息保护 (MIP) SDK。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: cf0500aa9d7c6a0422e5846edda23515319c1efc
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333205"
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
