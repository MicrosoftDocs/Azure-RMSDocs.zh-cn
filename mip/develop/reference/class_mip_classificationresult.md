---
title: 类 mip::ClassificationResult
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： classificationresult 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a245cd4d9505de8adbf3cc1a2de6d2fa20369ce7
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490398"
---
# <a name="class-mipclassificationresult"></a>类 mip::ClassificationResult 
包含对执行状态进行分类调用的结果的类。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  获取分类策略的 ID。
public std::string GetName() const  |  获取分类策略的名称。
public int GetCount() const  |  获取实例计数。
public int GetConfidenceLevel() const  |  获取结果可信度。
public std：： string GetSensitiveInformationDetections （） const  |  获取敏感信息检测。
  
## <a name="members"></a>Members
  
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

  
**返回**：所有敏感信息检测的 Json 字符串。 如果不为空，则必须为有效的 json 格式。