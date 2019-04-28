---
title: 类 mip::AuthDelegate
description: 记录 mip::authdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: bcc38bf4b55ca99cf926138279223a4140f7bbf4
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184835"
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

