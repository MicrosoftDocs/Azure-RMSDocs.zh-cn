---
title: class mip::HttpRequest
description: 记录 mip::httprequest 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 56c736d985e7c8bd258fcb7c1f7e42b5db3801fd
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256934"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
描述单个 HTTP 请求的接口。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public HttpRequestType GetRequestType() const  |  获取请求类型。
public const std::string& GetUrl() const  |  获取请求 URL。
public const std::string& GetBody() const  |  获取请求正文。
public const std:: map\<std:: string、 std:: string，CaseInsensitiveComparator\>& GetHeaders() 常量  |  获取请求标头。
  
## <a name="members"></a>成員
  
### <a name="getrequesttype-function"></a>GetRequestType 函数
获取请求类型。

  
**返回**:请求类型
  
### <a name="geturl-function"></a>GetUrl 函数
获取请求 URL。

  
**返回**:请求 url
  
### <a name="getbody-function"></a>GetBody 函数
获取请求正文。

  
**返回**:请求正文
  
### <a name="getheaders-function"></a>GetHeaders 函数
获取请求标头。

  
**返回**:请求标头
