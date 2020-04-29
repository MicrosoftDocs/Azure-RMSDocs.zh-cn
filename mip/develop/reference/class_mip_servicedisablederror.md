---
title: 类 ServiceDisabledError
description: 记录 Microsoft 信息保护（MIP） SDK 的 servicedisablederror：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: ef521d9330df410bc14ad6ae856b837fc615cfbb
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760678"
---
# <a name="class-servicedisablederror"></a>类 ServiceDisabledError 
由于服务被禁用，用户无法访问内容。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共区 GetExtent （） const  |  获取服务的禁用范围。
枚举范围  |  描述服务的禁用范围。
  
## <a name="members"></a>成员
  
### <a name="getextent-function"></a>GetExtent 函数
获取服务的禁用范围。

  
**返回**：禁用服务的范围
  
### <a name="extent-enum"></a>区枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
User            | 已为用户禁用服务。
设备            | 设备的服务已禁用。
平台            | 平台已禁用服务。
租户            | 租户的服务已禁用。
描述服务的禁用范围。