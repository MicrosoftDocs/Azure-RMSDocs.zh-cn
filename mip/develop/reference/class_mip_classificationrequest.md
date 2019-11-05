---
title: 类 mip：： ClassificationRequest
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： classificationrequest 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 62b600a377d195c693c94dff7a0472305b53b3f2
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558979"
---
# <a name="class-mipclassificationrequest"></a>类 mip：： ClassificationRequest 
包含执行状态的分类调用请求的类。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string GetClassificationId （） const  |  获取分类策略的 ID。
public std：： string GetRulePackageId （） const  |  获取规则包的 ID。
  
## <a name="members"></a>成員
  
### <a name="getclassificationid-function"></a>GetClassificationId 函数
获取分类策略的 ID。

  
返回结果：分类策略的 ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 函数
获取规则包的 ID。

  
**返回**：规则包的 ID。 预生成的分类将设置为空 guid。