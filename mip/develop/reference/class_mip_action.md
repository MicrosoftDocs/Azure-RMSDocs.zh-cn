---
title: class mip::Action
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： action 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d3cc1aecfb5ca8bf2d78dd9d6c8c280b5541389d
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560415"
---
# <a name="class-mipaction"></a>class mip::Action 
操作的接口。 每个操作都转换为，出于应用标签目的，应用程序需要执行的步骤（如策略所定义）
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public ActionType GetType() const  |  获取操作的类型。
  
## <a name="members"></a>成員
  
### <a name="gettype-function"></a>GetType 函数
获取操作的类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。