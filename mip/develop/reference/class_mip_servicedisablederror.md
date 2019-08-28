---
title: '类 mip:: ServiceDisabledError'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: servicedisablederror 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2fb7968ee2443d208ef3370308056eee4832e385
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057022"
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