---
title: 类 mip：： AuthDelegate：： OAuth2Challenge
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： authdelegate 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 8e3119e18d465c9ad66dd1cbbece003b96d1a3b7
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489055"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>类 mip：： AuthDelegate：： OAuth2Challenge 
一个类，其中包含调用应用程序所需的所有信息，以便生成 oauth2 标记。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public OAuth2Challenge （const std：： string & 机关，const std：： string & 资源，const std：： string & 范围，const std：： string & 声明）  |  构造一个新的 OAuth2Challenge 对象。
public const std：： string & GetAuthority （） const  |  获取授权字符串。
public const std：： string & GetResource （） const  |  获取资源字符串。
public const std：： string & GetScope （） const  |  获取范围字符串。
public const std：： string & GetClaims （） const  |  获取声明字符串。
  
## <a name="members"></a>Members
  
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