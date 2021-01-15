---
title: 类 ClassificationRequest
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 classificationrequest：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 5903c0bcccf7899449d7097c99e79feef038c988
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211934"
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