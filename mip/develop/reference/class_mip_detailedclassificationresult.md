---
title: 类 DetailedClassificationResult
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 detailedclassificationresult：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 9b1921c046867207d6b1d9a67df46f442fb95977
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211629"
---
# <a name="class-detailedclassificationresult"></a>类 DetailedClassificationResult 
包含对执行状态进行分类调用的结果的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public int GetConfidenceLevel() const  |  获取结果可信度。
public int GetCount() const  |  获取实例计数。
  
## <a name="members"></a>成员
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel 函数
获取结果可信度。

  
**返回**：介于0-100 的计数中的数字置信度。
  
### <a name="getcount-function"></a>GetCount 函数
获取实例计数。

  
**返回结果**：实例计数。