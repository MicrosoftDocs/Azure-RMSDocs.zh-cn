---
title: class mip::HttpRequest
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： httprequest 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f3b26ad07b8b3bfc556646cfd96a71aa9188bbb0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488086"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
描述单个 HTTP 请求的接口。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取请求 ID。
public HttpRequestType GetRequestType() const  |  获取请求类型。
public const std::string& GetUrl() const  |  获取请求 URL。
public const std：： vector\<uint8_t\>& GetBody （） const  |  获取请求正文。
public const std：： map\<std：： string、std：： string、CaseInsensitiveComparator\>& GetHeaders （） const  |  获取请求标头。
  
## <a name="members"></a>Members
  
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