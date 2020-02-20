---
title: 类 mip：： ClassificationRequest
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： classificationrequest 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 27c6e01eea2dae3735ce5cc3e5cd618b6223d2eb
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489021"
---
# <a name="class-mipclassificationrequest"></a>类 mip：： ClassificationRequest 
包含执行状态的分类调用请求的类。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string GetClassificationId （） const  |  获取分类策略的 ID。
public std：： string GetRulePackageId （） const  |  获取规则包的 ID。
  
## <a name="members"></a>Members
  
### <a name="getclassificationid-function"></a>GetClassificationId 函数
获取分类策略的 ID。

  
返回结果：分类策略的 ID。
  
### <a name="getrulepackageid-function"></a>GetRulePackageId 函数
获取规则包的 ID。

  
**返回**：规则包的 ID。 预生成的分类将设置为空 guid。