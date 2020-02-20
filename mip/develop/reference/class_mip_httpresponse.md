---
title: 类 mip::HttpResponse
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： httpresponse.cache 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e24eef471b11daffadb84235edbc93ff14696c25
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488052"
---
# <a name="class-miphttpresponse"></a>类 mip::HttpResponse 
一个接口，该接口描述在重写 HttpDelegate 时由客户端应用程序实现的单个 HTTP 响应。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取响应 ID。
public int32_t GetStatusCode() const  |  获取响应状态代码。
public const std：： vector\<uint8_t\>& GetBody （） const  |  获取请求正文。
public const std：： map\<std：： string、std：： string、CaseInsensitiveComparator\>& GetHeaders （） const  |  获取请求标头。
  
## <a name="members"></a>Members
  
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