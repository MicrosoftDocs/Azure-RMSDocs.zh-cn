---
title: 类 mip：： AuthDelegate：： OAuth2Challenge
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： authdelegate 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8205d207a48d90832b5961b14d37c7a7226293a2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73559020"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>类 mip：： AuthDelegate：： OAuth2Challenge 
一个类，其中包含调用应用程序所需的所有信息，以便生成 oauth2 标记。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public OAuth2Challenge （const std：： string & 机关，const std：： string & 资源，const std：： string & 范围，const std：： string & 声明）  |  构造一个新的 OAuth2Challenge 对象。
public const std：： string & GetAuthority （） const  |  获取授权字符串。
public const std：： string & GetResource （） const  |  获取资源字符串。
public const std：： string & GetScope （） const  |  获取范围字符串。
public const std：： string & GetClaims （） const  |  获取声明字符串。
  
## <a name="members"></a>成員
  
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