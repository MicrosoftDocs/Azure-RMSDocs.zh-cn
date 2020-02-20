---
title: 类 mip：： AuthDelegate
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： authdelegate 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 30907f3bf4a08f72305a59290c8cbd891def44c9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490602"
---
# <a name="class-mipauthdelegate"></a>类 mip：： AuthDelegate 
用于身份验证相关操作的委托。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public virtual bool AcquireOAuth2Token （const mip：： Identity & identity，const OAuth2Challenge & 质询，OAuth2Token & 标记）  |  当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。
public virtual bool AcquireOAuth2Token （const mip：： Identity & identity，const OAuth2Challenge & 质询，const std：： shared_ptr\<void\>& context，OAuth2Token & token）  |  当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。
  
## <a name="members"></a>Members
  
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