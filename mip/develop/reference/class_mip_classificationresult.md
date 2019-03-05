---
title: 类 mip::ClassificationResult
description: 记录 mip::classificationresult 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 716bc18031b5b67b080281b76c42df296f3d72fa
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332508"
---
# <a name="class-mipclassificationresult"></a>类 mip::ClassificationResult 
包含对执行状态进行分类调用的结果的类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  获取分类策略的 ID。
public int GetCount() const  |  获取实例计数。
public int GetConfidenceLevel() const  |  获取结果可信度。
  
## <a name="members"></a>成員
  
### <a name="getid-function"></a>GetId 函数
获取分类策略的 ID。

  
**返回**:分类策略的 ID。
  
### <a name="getcount-function"></a>GetCount 函数
获取实例计数。

  
**返回**:实例计数。
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel 函数
获取结果可信度。
