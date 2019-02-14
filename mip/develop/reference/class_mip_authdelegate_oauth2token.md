---
title: 类 mip::AuthDelegate::OAuth2Token
description: 记录 mip::authdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: bef28489d16b040ff910103d9e0bf5a4719c66ff
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255965"
---
# <a name="class-mipauthdelegateoauth2token"></a>类 mip::AuthDelegate::OAuth2Token 
定义 MIP SDK 如何要求要传递到 SDK 的 oauth2 令牌的类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public OAuth2Token()  |  构造一个新[OAuth2Token](class_mip_authdelegate_oauth2token.md)对象。
公共 OAuth2Token (const std:: string & accessToken)  |  构造一个新[OAuth2Token](class_mip_authdelegate_oauth2token.md) accessToken 中的对象。
public const std:: string & const getaccesstoken （)  |  获取访问令牌字符串。
public void SetAccessToken (const std:: string & accessToken)  |  设置访问令牌的字符串。
  
## <a name="members"></a>成員
  
### <a name="oauth2token-function"></a>OAuth2Token 函数
构造一个新[OAuth2Token](class_mip_authdelegate_oauth2token.md)对象。
  
### <a name="oauth2token-function"></a>OAuth2Token 函数
构造一个新[OAuth2Token](class_mip_authdelegate_oauth2token.md) accessToken 中的对象。

参数：  
* **accessToken**:实际访问令牌传递到 SDK。


  
### <a name="getaccesstoken-function"></a>GetAccessToken 函数
获取访问令牌字符串。

  
**返回**:访问令牌字符串。
  
### <a name="setaccesstoken-function"></a>SetAccessToken 函数
设置访问令牌的字符串。

参数：  
* **accessToken**： 访问令牌字符串。

