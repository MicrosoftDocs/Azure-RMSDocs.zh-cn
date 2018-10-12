---
title: class mip ClassificationResult
description: class mip ClassificationResult 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ea312330c656b6daefbc1bcba690f53ebfbf419f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446288"
---
# <a name="class-mipclassificationresult"></a>类 mip::ClassificationResult 
包含对执行状态进行分类调用的结果的类。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public std::string GetId() const  |  获取分类策略的 ID。
 public int GetCount() const  |  获取实例计数。
 public int GetConfidenceLevel() const  |  获取结果可信度。
  
## <a name="members"></a>成員
  
### <a name="getid"></a>GetId
获取分类策略的 ID。

  
返回结果：分类策略的 ID。
  
### <a name="getcount"></a>GetCount
获取实例计数。

  
**返回结果**：实例计数。
  
### <a name="getconfidencelevel"></a>GetConfidenceLevel
获取结果可信度。