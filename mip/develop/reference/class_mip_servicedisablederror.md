---
title: 类 ServiceDisabledError
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 servicedisablederror：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: e7f3ec6e3e02047607f696acd0a14cd632b5b0e9
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214280"
---
# <a name="class-servicedisablederror"></a>类 ServiceDisabledError 
由于服务被禁用，用户无法访问内容。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共区 GetExtent ( # A1 const  |  获取服务的禁用范围。
枚举范围  |  描述服务的禁用范围。
  
## <a name="members"></a>成员
  
### <a name="getextent-function"></a>GetExtent 函数
获取服务的禁用范围。

  
**返回**：禁用服务的范围
  
### <a name="extent-enum"></a>区枚举

描述服务的禁用范围。

 值                         | 说明                                
--------------------------------|---------------------------------------------
用户            | 已为用户禁用服务。
设备            | 设备的服务已禁用。
平台            | 平台已禁用服务。
租户            | 租户的服务已禁用。
