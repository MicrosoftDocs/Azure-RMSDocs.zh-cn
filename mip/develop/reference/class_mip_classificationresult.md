---
title: 类 mip::ClassificationResult
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： classificationresult 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6f4b1147ef6831ca622d095c0cada67b9f0cf023
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559396"
---
# <a name="class-mipclassificationresult"></a>类 mip::ClassificationResult 
包含对执行状态进行分类调用的结果的类。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  获取分类策略的 ID。
public std::string GetName() const  |  获取分类策略的名称。
public int GetCount() const  |  获取实例计数。
public int GetConfidenceLevel() const  |  获取结果可信度。
public std：： string GetSensitiveInformationDetections （） const  |  获取敏感信息检测。
  
## <a name="members"></a>成員
  
### <a name="getid-function"></a>GetId 函数
获取分类策略的 ID。

  
返回结果：分类策略的 ID。
  
### <a name="getname-function"></a>GetName 函数
获取分类策略的名称。

  
**返回**：分类策略的名称。
  
### <a name="getcount-function"></a>GetCount 函数
获取实例计数。

  
**返回结果**：实例计数。
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel 函数
获取结果可信度。
  
### <a name="getsensitiveinformationdetections-function"></a>GetSensitiveInformationDetections 函数
获取敏感信息检测。

  
**返回**：所有敏感信息检测的 Json 字符串。