---
title: 类 ServiceDisabledError
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 servicedisablederror：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: b4ccba889ce025f343293d458f76ae7d63457f4f
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565160"
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

 值                         | 说明                                
--------------------------------|---------------------------------------------
用户            | 已为用户禁用服务。
设备            | 设备的服务已禁用。
平台            | 平台已禁用服务。
租户            | 租户的服务已禁用。

描述服务的禁用范围。