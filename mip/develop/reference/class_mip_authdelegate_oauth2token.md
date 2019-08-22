---
title: '类 mip:: AuthDelegate:: OAuth2Token'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: authdelegate 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: b7b9b73d9f1f3952af1d6a9bdea94c75a8032fb7
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885889"
---
# <a name="class-mipauthdelegateoauth2token"></a>类 mip:: AuthDelegate:: OAuth2Token 
定义 MIP SDK 期望将 oauth2 标记传回 SDK 的方式的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public OAuth2Token ()  |  构造一个新的[OAuth2Token](class_mip_authdelegate_oauth2token.md)对象。
public OAuth2Token (const std:: string & accessToken)  |  从 accessToken 构造新的[OAuth2Token](class_mip_authdelegate_oauth2token.md)对象。
public const std:: string & GetAccessToken () const  |  获取访问令牌字符串。
public void SetAccessToken (const std:: string & accessToken)  |  设置访问令牌字符串。
  
## <a name="members"></a>成员
  
### <a name="oauth2token-function"></a>OAuth2Token 函数
构造一个新的[OAuth2Token](class_mip_authdelegate_oauth2token.md)对象。
  
### <a name="oauth2token-function"></a>OAuth2Token 函数
从 accessToken 构造新的[OAuth2Token](class_mip_authdelegate_oauth2token.md)对象。

参数：  
* **accessToken**:传入 SDK 的实际访问令牌。


  
### <a name="getaccesstoken-function"></a>GetAccessToken 函数
获取访问令牌字符串。

  
**返回**:访问令牌字符串。
  
### <a name="setaccesstoken-function"></a>SetAccessToken 函数
设置访问令牌字符串。

参数：  
* **accessToken**: 访问令牌字符串。

