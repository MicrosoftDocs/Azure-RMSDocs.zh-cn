---
title: 类 mip::ClassificationResult
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: classificationresult 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2744e2d5fe188667ff7c1c93a7f98719f200aecd
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056224"
---
# <a name="class-mipclassificationresult"></a>类 mip::ClassificationResult 
包含对执行状态进行分类调用的结果的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  获取分类策略的 ID。
public int GetCount() const  |  获取实例计数。
public int GetConfidenceLevel() const  |  获取结果可信度。
public std:: string GetSensitiveInformationDetections () const  |  获取敏感信息检测。
  
## <a name="members"></a>成员
  
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