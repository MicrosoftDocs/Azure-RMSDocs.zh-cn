---
title: 类 mip：： AuthDelegate：： OAuth2Token
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： authdelegate 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 6053a282d162dc2b0f316b265fe6878a4c535a7f
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490432"
---
# <a name="class-mipauthdelegateoauth2token"></a>类 mip：： AuthDelegate：： OAuth2Token 
一个类，其中包含应用程序提供的访问令牌信息。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public OAuth2Token （）  |  构造一个新的 OAuth2Token 对象。
public OAuth2Token （const std：： string & accessToken）  |  从 JWT 访问令牌构造一个新的 OAuth2Token 对象。
public const std：： string & GetAccessToken （） const  |  获取访问令牌字符串。
public void SetAccessToken （const std：： string & accessToken）  |  设置访问令牌字符串。
public const std：： string & GetErrorMessage （） const  |  获取错误消息（如果有）。
public void SetErrorMessage （const std：： string & errorMessage）  |  设置错误消息。
  
## <a name="members"></a>Members
  
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

