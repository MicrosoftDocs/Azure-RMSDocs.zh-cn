---
title: 类 mip::HttpResponse
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： httpresponse.cache 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 876de8047abc4e2f13ee8e103cdfa1648738aa84
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558743"
---
# <a name="class-miphttpresponse"></a>类 mip::HttpResponse 
一个接口，该接口描述在重写 HttpDelegate 时由客户端应用程序实现的单个 HTTP 响应。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取响应 ID。
public int32_t GetStatusCode() const  |  获取响应状态代码。
public const std：： vector\<uint8_t\>& GetBody （） const  |  获取请求正文。
public const std：： map\<std：： string、std：： string、CaseInsensitiveComparator\>& GetHeaders （） const  |  获取请求标头。
  
## <a name="members"></a>成員
  
### <a name="getid-function"></a>GetId 函数
获取响应 ID。

  
**返回**：对应 HttpRequest 将具有相同 ID 的响应 ID
  
### <a name="getstatuscode-function"></a>GetStatusCode 函数
获取响应状态代码。

  
**返回结果**：状态代码
  
### <a name="getbody-function"></a>GetBody 函数
获取请求正文。

  
**返回结果**：请求正文
  
### <a name="getheaders-function"></a>GetHeaders 函数
获取请求标头。

  
**返回结果**：请求标头