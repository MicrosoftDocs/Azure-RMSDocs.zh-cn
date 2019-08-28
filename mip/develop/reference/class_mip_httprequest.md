---
title: class mip::HttpRequest
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: httprequest 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 92cf2bc3840e3cb38210c42c1e1b2d43db1e8bd4
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054828"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
描述单个 HTTP 请求的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取请求 ID。
public HttpRequestType GetRequestType() const  |  获取请求类型。
public const std::string& GetUrl() const  |  获取请求 URL。
public const std:: vector\<uint8_t\>& GetBody () const  |  获取请求正文。
public const std:: map\<std:: string, std:: string, CaseInsensitiveComparator\>& GetHeaders () const  |  获取请求标头。
  
## <a name="members"></a>成员
  
### <a name="getid-function"></a>GetId 函数
获取请求 ID。

  
**返回**:请求 ID 相应的 Httpresponse.cache 将具有相同的 ID
  
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