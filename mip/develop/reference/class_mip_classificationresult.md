---
title: 类 mip::ClassificationResult
description: 记录 mip::classificationresult 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6a048dd7902e8148e4f32f8cc9e62d63110b2b4a
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60174215"
---
# <a name="class-mipclassificationresult"></a>类 mip::ClassificationResult 
包含对执行状态进行分类调用的结果的类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  获取分类策略的 ID。
public int GetCount() const  |  获取实例计数。
public int GetConfidenceLevel() const  |  获取结果可信度。
public std:: string GetSensitiveInformationDetections() 常量  |  获取敏感信息检测。
  
## <a name="members"></a>成員
  
### <a name="getid-function"></a>GetId 函数
获取分类策略的 ID。

  
**返回**:分类策略的 ID。
  
### <a name="getcount-function"></a>GetCount 函数
获取实例计数。

  
**返回**:实例计数。
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel 函数
获取结果可信度。
  
### <a name="getsensitiveinformationdetections-function"></a>GetSensitiveInformationDetections 函数
获取敏感信息检测。

  
**返回**:所有敏感信息检测的 Json 字符串。