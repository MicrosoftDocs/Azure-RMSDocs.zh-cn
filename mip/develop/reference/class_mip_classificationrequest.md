---
title: 类 ClassificationRequest
description: 记录 Microsoft 信息保护（MIP） SDK 的 classificationrequest：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 0d4b8d3ed5e12698c0044975516b017d1c9376b0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763541"
---
# <a name="class-classificationrequest"></a>类 ClassificationRequest 
包含执行状态的分类调用请求的类。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string GetClassificationId （） const  |  获取分类策略的 ID。
public std：： string GetRulePackageId （） const  |  获取规则包的 ID。
  
## <a name="members"></a>成员
  
### <a name="getclassificationid-function"></a>GetClassificationId 函数
获取分类策略的 ID。

  
**返回**：分类策略的 ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 函数
获取规则包的 ID。

  
**返回**：规则包的 ID。 预生成的分类将设置为空 guid。