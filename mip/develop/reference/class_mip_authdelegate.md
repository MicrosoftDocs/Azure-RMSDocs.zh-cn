---
title: 类 AuthDelegate
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 authdelegate：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: afe0dd79217942a767211f7959c898e098bd8f38
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212155"
---
# <a name="class-authdelegate"></a>类 AuthDelegate 
用于身份验证相关操作的委托。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual bool AcquireOAuth2Token (const Identity& Identity、const OAuth2Challenge& 质询、OAuth2Token& 令牌)   |  当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。
public virtual bool AcquireOAuth2Token (const Identity& Identity，const OAuth2Challenge& 质询，const std：： shared_ptr \<void\>& context，OAuth2Token& 令牌)   |  当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。
  
## <a name="members"></a>成员
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 函数
当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。

参数：  
* **标识**：请求令牌的用户 


* **挑战**： OAuth2 挑战 


* **令牌**： [Output] Base64 编码的 OAuth2 令牌



  
**返回**：如果已成功获取令牌，则为 True; 否则为 false，如果 token output 参数包含错误消息，则会将其包含在 NoAuthTokenError 异常中，稍后会将其引发到应用程序。
> 弃用：此方法将很快弃用，以接受接受上下文参数的一个。 如果已实现新版本，则无需实现此版本。
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 函数
当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。

参数：  
* **标识**：请求令牌的用户 


* **挑战**： OAuth2 挑战 


* **上下文**：主机应用程序传递到 MIP API 的不透明上下文 


* **令牌**： [Output] Base64 编码的 OAuth2 令牌



  
**返回**：如果已成功获取令牌，则为 True; 否则为 false，如果 token output 参数包含错误消息，则会将其包含在 NoAuthTokenError 异常中，稍后会将其引发到应用程序。