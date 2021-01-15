---
title: 类 DelegationLicense
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 delegationlicense：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: cfb719a68650b2159574dd6f8d92fb3d0c15a2c1
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224917"
---
# <a name="class-delegationlicense"></a>类 DelegationLicense 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector \<uint8_t\>& GetSerializedDelegationJsonLicense ( # A2  |  获取委派许可证。
public const std：： vector \<uint8_t\>& GetSerializedUserLicense (ProtectionHandler：:P relicenseformat 格式)   |  获取用户许可证（如果请求）。
public const std：： string& GetUser ( # A2  |  获取为其创建此许可证的用户。
  
## <a name="members"></a>成员
  
### <a name="getserializeddelegationjsonlicense-function"></a>GetSerializedDelegationJsonLicense 函数
获取委派许可证。

  
**返回**：序列化的许可证此许可证绑定到发出请求的用户的标识
  
### <a name="getserializeduserlicense-function"></a>GetSerializedUserLicense 函数
获取用户许可证（如果请求）。

参数：  
* **格式**：许可证格式



  
**返回**：如果请求，则为序列化用户许可证，否则为空矢量。此许可证绑定到请求中的委托用户
  
### <a name="getuser-function"></a>GetUser 函数
获取为其创建此许可证的用户。

  
**返回**：用户