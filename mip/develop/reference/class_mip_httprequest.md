---
title: 类 HttpRequest
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 httprequest：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: c613729664141eb96e2cd1844107fcc1d9a4fa18
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215215"
---
# <a name="class-httprequest"></a>类 HttpRequest 
描述单个 HTTP 请求的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取请求 ID。
public HttpRequestType GetRequestType() const  |  获取请求类型。
public const std::string& GetUrl() const  |  获取请求 URL。
public const std：： vector \<uint8_t\>& GetBody ( # A2 const  |  获取请求正文。
public const std：： map \<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders ( # A2 const  |  获取请求标头。
  
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