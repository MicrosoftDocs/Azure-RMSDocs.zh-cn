---
title: 类 DetailedClassificationResult
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 detailedclassificationresult：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d43b75c232d6bfe60f1b7124c66c007d021dd2ee
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565153"
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