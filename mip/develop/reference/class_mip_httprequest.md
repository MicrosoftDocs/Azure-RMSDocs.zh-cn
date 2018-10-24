---
title: class mip HttpRequest
description: class mip HttpRequest 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e838eb247bc00d43da72db1de03304e89a1b1da5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445234"
---
# <a name="class-miphttprequest"></a>class mip::HttpRequest 
描述单个 HTTP 请求的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public HttpRequestType GetRequestType() const  |  获取请求类型。
 public const std::string& GetUrl() const  |  获取请求 URL。
 public const std::string& GetBody() const  |  获取请求正文。
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  获取请求标头。
  
## <a name="members"></a>成員
  
### <a name="httprequesttype"></a>HttpRequestType
获取请求类型。

  
**返回结果**：请求类型
  
### <a name="geturl"></a>GetUrl
获取请求 URL。

  
**返回结果**：请求 URL
  
### <a name="getbody"></a>GetBody
获取请求正文。

  
**返回结果**：请求正文
  
### <a name="getheaders"></a>GetHeaders
获取请求标头。

  
**返回结果**：请求标头