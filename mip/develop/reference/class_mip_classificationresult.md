---
title: 类 ClassificationResult
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 classificationresult：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 4e64abc1cca11f11b19238282c9061dc26b29290
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565213"
---
# <a name="class-classificationresult"></a>类 ClassificationResult 
包含对执行状态进行分类调用的结果的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  获取分类策略的 ID。
public std::string GetName() const  |  获取分类策略的名称。
public int GetCount() const  |  获取实例计数。
public int GetConfidenceLevel() const  |  获取结果可信度。
public std：： string GetSensitiveInformationDetections ( # A1 const  |  获取敏感信息检测。
public virtual std：： vector \<std::shared_ptr\<mip::DetailedClassificationResult\> \> GetDetailedClassificationAttributes ( # A1 const  |  如果启用了增强分类，请获取特定检测带区。
  
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
  
### <a name="getdetailedclassificationattributes-function"></a>GetDetailedClassificationAttributes 函数
如果启用了增强分类，请获取特定检测带区。

  
**返回**：实例的向量在不同的置信度阈值