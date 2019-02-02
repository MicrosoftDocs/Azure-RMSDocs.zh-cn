---
title: class mip::JustifyAction
description: '记录 mip:: justifyaction 类的 Microsoft 信息保护 (MIP) SDK。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: e52a38f8ca25ecb8cc8ae470cb77164abb2b6ec8
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650675"
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