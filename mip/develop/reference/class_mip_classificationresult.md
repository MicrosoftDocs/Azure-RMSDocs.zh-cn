---
title: 类 ClassificationResult
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 classificationresult：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: c1f4154bbc12613726aac8f56a322cb6cd4d5a53
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211866"
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