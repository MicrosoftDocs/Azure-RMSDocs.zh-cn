---
title: class mip::HttpRequest
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： httprequest 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: bfe55f09caaa20687750b055e10828f8cc6df2bd
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560176"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
描述单个 HTTP 请求的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取请求 ID。
public HttpRequestType GetRequestType() const  |  获取请求类型。
public const std::string& GetUrl() const  |  获取请求 URL。
public const std：： vector\<uint8_t\>& GetBody （） const  |  获取请求正文。
public const std：： map\<std：： string、std：： string、CaseInsensitiveComparator\>& GetHeaders （） const  |  获取请求标头。
  
## <a name="members"></a>成員
  
### <a name="getid-function"></a>GetId 函数
获取请求 ID。

  
**返回**：请求 ID 相应的 httpresponse.cache 将具有相同的 id
  
### <a name="getrequesttype-function"></a>GetRequestType 函数
获取请求类型。

  
**返回结果**：请求类型
  
### <a name="geturl-function"></a>GetUrl 函数
获取请求 URL。

  
**返回结果**：请求 URL
  
### <a name="getbody-function"></a>GetBody 函数
获取请求正文。

  
**返回结果**：请求正文
  
### <a name="getheaders-function"></a>GetHeaders 函数
获取请求标头。

  
**返回结果**：请求标头