---
title: '类 mip:: ServiceDisabledError'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: servicedisablederror 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 6496b2b8967571454c205b84b01a6e4b74456c17
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882914"
---
# <a name="class-mipservicedisablederror"></a>类 mip:: ServiceDisabledError 
由于服务被禁用, 用户无法访问内容。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共区 GetExtent () const  |  获取服务的禁用范围。
枚举范围  |  描述服务的禁用范围。
  
## <a name="members"></a>成员
  
### <a name="getextent-function"></a>GetExtent 函数
获取服务的禁用范围。

  
**返回**:禁用服务的范围
  
### <a name="extent-enum"></a>区枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
用户            | 已为用户禁用服务。
设备            | 设备的服务已禁用。
平台            | 平台已禁用服务。
租户            | 租户的服务已禁用。
描述服务的禁用范围。