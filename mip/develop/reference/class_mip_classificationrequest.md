---
title: 类 ClassificationRequest
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 classificationrequest：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2e509950bad2d219843c2d45ebd3922a19bef7f4
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565215"
---
# <a name="class-classificationrequest"></a>类 ClassificationRequest 
包含执行状态的分类调用请求的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string GetClassificationId ( # A1 const  |  获取分类策略的 ID。
public std：： string GetRulePackageId ( # A1 const  |  获取规则包的 ID。
  
## <a name="members"></a>成员
  
### <a name="getclassificationid-function"></a>GetClassificationId 函数
获取分类策略的 ID。

  
**返回**：分类策略的 ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 函数
获取规则包的 ID。

  
**返回**：规则包的 ID。 预生成的分类将设置为空 guid。