---
title: 类 AuthDelegate：： OAuth2Challenge
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 authdelegate：： oauth2challenge 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: f422b99674213904316eab622bfc915f128228ec
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565227"
---
# <a name="class-authdelegateoauth2challenge"></a>类 AuthDelegate：： OAuth2Challenge 
一个类，其中包含调用应用程序所需的所有信息，以便生成 oauth2 标记。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public OAuth2Challenge (const std：： string& 核证机关，const std：： string& resource，const std：： string& 作用域，const std：： string& 声明)   |  构造一个新的 OAuth2Challenge 对象。
public const std：： string& GetAuthority ( # A2 const  |  获取授权字符串。
public const std：： string& GetResource ( # A2 const  |  获取资源字符串。
public const std：： string& GetScope ( # A2 const  |  获取范围字符串。
public const std：： string& GetClaims ( # A2 const  |  获取声明字符串。
  
## <a name="members"></a>成员
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge 函数
构造一个新的 OAuth2Challenge 对象。

参数：  
* **颁发机构**：需要为其生成令牌的授权机构。 


* **资源**：标记设置为的资源。 


* **作用域**：标记设置为的范围。


  
### <a name="getauthority-function"></a>GetAuthority 函数
获取授权字符串。

  
**返回**：授权字符串。
  
### <a name="getresource-function"></a>GetResource 函数
获取资源字符串。

  
**返回**：资源字符串。
  
### <a name="getscope-function"></a>GetScope 函数
获取范围字符串。

  
**返回**：范围字符串。
  
### <a name="getclaims-function"></a>GetClaims 函数
获取声明字符串。

  
**返回**：声明字符串。