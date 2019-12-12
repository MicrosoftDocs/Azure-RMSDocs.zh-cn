---
title: 类 mip：： AuthDelegate：： OAuth2Token
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： authdelegate 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d8bce56e02778d48e6e3c0cfdb02f1c3f1f4054a
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560352"
---
# <a name="class-mipauthdelegateoauth2token"></a>类 mip：： AuthDelegate：： OAuth2Token 
定义 MIP SDK 期望将 oauth2 标记传回 SDK 的方式的类。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public OAuth2Token （）  |  构造一个新的 OAuth2Token 对象。
public OAuth2Token （const std：： string & accessToken）  |  从 accessToken 构造新的 OAuth2Token 对象。
public const std：： string & GetAccessToken （） const  |  获取访问令牌字符串。
public void SetAccessToken （const std：： string & accessToken）  |  设置访问令牌字符串。
  
## <a name="members"></a>成員
  
### <a name="oauth2token-function"></a>OAuth2Token 函数
构造一个新的 OAuth2Token 对象。
  
### <a name="oauth2token-function"></a>OAuth2Token 函数
从 accessToken 构造新的 OAuth2Token 对象。

参数：  
* **accessToken**：传入 SDK 的实际访问令牌。


  
### <a name="getaccesstoken-function"></a>GetAccessToken 函数
获取访问令牌字符串。

  
**返回**：访问令牌字符串。
  
### <a name="setaccesstoken-function"></a>SetAccessToken 函数
设置访问令牌字符串。

参数：  
* **accessToken**：访问令牌字符串。

