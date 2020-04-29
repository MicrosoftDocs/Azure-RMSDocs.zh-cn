---
title: 类 HttpRequest
description: 记录 Microsoft 信息保护（MIP） SDK 的 httprequest：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: af302a760ee6b8f24b077b2c45bfe86ab0a80dac
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762708"
---
# <a name="class-httprequest"></a>类 HttpRequest 
描述单个 HTTP 请求的接口。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取请求 ID。
public HttpRequestType GetRequestType() const  |  获取请求类型。
public const std::string& GetUrl() const  |  获取请求 URL。
public const std：： vector\<Uint8_t\>& GetBody （） const  |  获取请求正文。
public const std：： map\<std：： string，std：： String，CaseInsensitiveComparator\>& GetHeaders （） const  |  获取请求标头。
  
## <a name="members"></a>成员
  
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