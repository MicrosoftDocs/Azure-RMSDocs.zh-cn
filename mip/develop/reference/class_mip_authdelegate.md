---
title: 类 mip：： AuthDelegate
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： authdelegate 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 3dc5679893c0de02eb9b9cb4f197c5ea39bf356f
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560334"
---
# <a name="class-mipauthdelegate"></a>类 mip：： AuthDelegate 
用于身份验证相关操作的委托。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public virtual bool AcquireOAuth2Token （const mip：： Identity & identity，const OAuth2Challenge & 质询，OAuth2Token & 标记）  |  当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。
public virtual bool AcquireOAuth2Token （const mip：： Identity & identity，const OAuth2Challenge & 质询，const std：： shared_ptr\<void\>& context，OAuth2Token & token）  |  当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。
  
## <a name="members"></a>成員
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 函数
当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。

参数：  
* **标识**： 


* **挑战**： 


* token： 


> 弃用：此方法将很快弃用，以接受接受上下文参数的一个。 如果已实现新版本，则无需实现此版本。
  
### <a name="acquireoauth2token-function"></a>AcquireOAuth2Token 函数
当策略引擎需要具有给定标识和给定质询的身份验证令牌时，将调用此方法。 客户端应返回获取令牌是否成功。 如果成功，则它应初始化给定的标记对象。

参数：  
* **标识**：请求令牌的用户 


* **挑战**： OAuth2 挑战 


* **上下文**：主机应用程序传递到 MIP API 的不透明上下文 


* **令牌**： [Output] Base64 编码的 OAuth2 令牌

