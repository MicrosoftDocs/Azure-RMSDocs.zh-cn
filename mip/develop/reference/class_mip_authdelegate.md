---
title: 类 mip::AuthDelegate
description: 记录 mip::authdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: cf6ea43b36518f2eec74b9ed0f8682466aa6b64d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258005"
---
# <a name="class-mipauthdelegate"></a>类 mip::AuthDelegate 
委托身份验证相关的操作。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共 bool AcquireOAuth2Token (const mip::Identity 标识，const OAuth2Challenge & 挑战，OAuth2Token 和令牌)  |  具有提供的标识和给定的质询的策略引擎需要身份验证令牌时，调用此方法。 客户端应返回获取令牌是否成功。 如果成功，它应初始化给定的令牌对象。
  
## <a name="members"></a>成員
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 函数
具有提供的标识和给定的质询的策略引擎需要身份验证令牌时，调用此方法。 客户端应返回获取令牌是否成功。 如果成功，它应初始化给定的令牌对象。

参数：  
* **标识**: 


* **质询**: 


* **令牌**:

