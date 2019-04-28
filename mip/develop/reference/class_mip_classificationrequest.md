---
title: 类 mip::ClassificationRequest
description: 记录 mip::classificationrequest 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3fddd870b6aebb9f5209fc43160c32d87b1d7129
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184750"
---
# <a name="class-mipclassificationrequest"></a>类 mip::ClassificationRequest 
包含请求的执行状态的一个分类调用的类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std:: string GetClassificationId() 常量  |  获取分类策略的 ID。
public std::string GetRulePackageId() const  |  获取规则包的 ID。
  
## <a name="members"></a>成員
  
### <a name="getclassificationid-function"></a>GetClassificationId 函数
获取分类策略的 ID。

  
**返回**:分类策略的 ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 函数
获取规则包的 ID。

  
**返回**:规则包的 ID。 预生成的分类将设置为空 guid。