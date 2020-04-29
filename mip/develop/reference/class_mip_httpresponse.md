---
title: 类 Httpresponse.cache
description: 记录 Microsoft 信息保护（MIP） SDK 的 httpresponse.cache：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 6e37613adce0397ed543c4df793a59e74795fb26
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762469"
---
# <a name="class-httpresponse"></a>类 Httpresponse.cache 
描述单个 HTTP 响应的接口，由客户端应用在重写 HttpDelegate 时实现。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取响应 ID。
public int32_t GetStatusCode() const  |  获取响应状态代码。
public const std：： vector\<Uint8_t\>& GetBody （） const  |  获取请求正文。
public const std：： map\<std：： string，std：： String，CaseInsensitiveComparator\>& GetHeaders （） const  |  获取请求标头。
  
## <a name="members"></a>成员
  
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