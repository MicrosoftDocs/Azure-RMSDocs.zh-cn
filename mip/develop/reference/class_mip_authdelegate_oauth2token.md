---
title: 类 AuthDelegate：： OAuth2Token
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 authdelegate：： oauth2token 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 4db3d2fbb2299b30b85516047ec237d2f23d7cd9
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212036"
---
# <a name="class-authdelegateoauth2token"></a>类 AuthDelegate：： OAuth2Token 
一个类，其中包含应用程序提供的访问令牌信息。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public OAuth2Token ( # A1  |  构造一个新的 OAuth2Token 对象。
public OAuth2Token (const std：： string& accessToken)   |  从 JWT 访问令牌构造一个新的 OAuth2Token 对象。
public const std：： string& GetAccessToken ( # A2 const  |  获取访问令牌字符串。
public void SetAccessToken (const std：： string& accessToken)   |  设置访问令牌字符串。
public const std：： string& GetErrorMessage ( # A2 const  |  获取错误消息（如果有）。
public void SetErrorMessage (const std：： string& errorMessage)   |  设置错误消息。
  
## <a name="members"></a>成员
  
### <a name="oauth2token-function"></a>OAuth2Token 函数
构造一个新的 OAuth2Token 对象。
  
### <a name="oauth2token-function"></a>OAuth2Token 函数
从 JWT 访问令牌构造一个新的 OAuth2Token 对象。

参数：  
* **accessToken**： JWT 访问令牌。


  
### <a name="getaccesstoken-function"></a>GetAccessToken 函数
获取访问令牌字符串。

  
**返回**：访问令牌字符串。
  
### <a name="setaccesstoken-function"></a>SetAccessToken 函数
设置访问令牌字符串。

参数：  
* **accessToken**：访问令牌字符串。


  
### <a name="geterrormessage-function"></a>GetErrorMessage 函数
获取错误消息（如果有）。

  
**返回**：错误消息。
  
### <a name="seterrormessage-function"></a>SetErrorMessage 函数
设置错误消息。

参数：  
* **errorMessage**：错误消息。

