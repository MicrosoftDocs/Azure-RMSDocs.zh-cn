---
title: 类 mip::ClassificationResult
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: classificationresult 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 83856362e0d0a347f660cb60a64a82e24062c247
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885863"
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