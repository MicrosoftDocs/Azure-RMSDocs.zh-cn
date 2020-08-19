---
title: 类 ServiceDisabledError
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 servicedisablederror：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3dc6d73f12dc1512d1850d465a966e99d13b52c9
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564447"
---
# <a name="class-servicedisablederror"></a>类 ServiceDisabledError

由于服务被禁用，用户无法访问内容。
  
## <a name="summary"></a>总结

| 成员                          | 说明
|----------------------------------|--------------------------------------------------------
| 公共区 GetExtent ( # A1 const  | 获取服务的禁用范围。
| 枚举范围                      | 描述服务的禁用范围。
  
## <a name="members"></a>成员
  
### <a name="getextent-function"></a>GetExtent 函数
获取服务的禁用范围。

**返回**：禁用服务的范围
  
### <a name="extent-enum"></a>区枚举

描述服务的禁用范围。

| 值   | 说明
|----------|---------------------------------------
| 用户     | 已为用户禁用服务。
| 设备   | 设备的服务已禁用。
| 平台 | 平台已禁用服务。
| 租户   | 租户的服务已禁用。
