---
title: 类 ClassificationResult
description: 记录 Microsoft 信息保护（MIP） SDK 的 classificationresult：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: b87db224bdd7a571c22de9e382ff9faf3ce656b8
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763524"
---
# <a name="class-classificationresult"></a>类 ClassificationResult 
包含对执行状态进行分类调用的结果的类。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  获取分类策略的 ID。
public std::string GetName() const  |  获取分类策略的名称。
public int GetCount() const  |  获取实例计数。
public int GetConfidenceLevel() const  |  获取结果可信度。
public std：： string GetSensitiveInformationDetections （） const  |  获取敏感信息检测。
  
## <a name="members"></a>成员
  
### <a name="getid-function"></a>GetId 函数
获取分类策略的 ID。

  
**返回**：分类策略的 ID。
  
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

  
**返回**：所有敏感信息检测的 Json 字符串。 如果不为空，则必须为有效的 json 格式。