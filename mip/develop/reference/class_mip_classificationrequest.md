---
title: '类 mip:: ClassificationRequest'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: classificationrequest 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 1966123c8a0975ea42aa119883cabd47db594bc4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884493"
---
# <a name="class-mipclassificationrequest"></a>类 mip:: ClassificationRequest 
包含执行状态的分类调用请求的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std:: string GetClassificationId () const  |  获取分类策略的 ID。
public std:: string GetRulePackageId () const  |  获取规则包的 ID。
  
## <a name="members"></a>成员
  
### <a name="getclassificationid-function"></a>GetClassificationId 函数
获取分类策略的 ID。

  
**返回**:分类策略的 ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 函数
获取规则包的 ID。

  
**返回**:规则包的 ID。 预生成的分类将设置为空 guid。