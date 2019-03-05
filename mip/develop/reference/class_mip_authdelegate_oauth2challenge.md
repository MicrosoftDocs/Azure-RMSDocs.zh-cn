---
title: 类 mip::AuthDelegate::OAuth2Challenge
description: 记录 mip::authdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2e4a107a0a967f4d3ff58ebf269bb701f5834fb0
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57331811"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>类 mip::AuthDelegate::OAuth2Challenge 
包含从调用应用程序，以便生成 oauth2 令牌所需的所有信息的类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共 OAuth2Challenge （const std:: string & 颁发机构，const std:: string 和资源、 const std:: string 和作用域）  |  构造一个新[OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)对象。
public const std:: string & GetAuthority() 常量  |  获取颁发机构字符串。
public const std:: string & GetResource() 常量  |  获取资源字符串。
public const std:: string & GetScope() 常量  |  获取范围字符串。
  
## <a name="members"></a>成員
  
### <a name="oauth2challenge-function"></a>OAuth2Challenge 函数
构造一个新[OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)对象。

参数：  
* **颁发机构**： 需要对生成令牌的颁发机构。 


* **资源**: 令牌设置为该资源。 


* **作用域**: 令牌设置为的作用域。


  
### <a name="getauthority-function"></a>GetAuthority 函数
获取颁发机构字符串。

  
**返回**:颁发机构的字符串。
  
### <a name="getresource-function"></a>GetResource 函数
获取资源字符串。

  
**返回**:资源字符串中。
  
### <a name="getscope-function"></a>GetScope 函数
获取范围字符串。

  
**返回**:作用域字符串中。
