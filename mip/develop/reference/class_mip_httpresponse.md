---
title: 类 Httpresponse.cache
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 httpresponse.cache：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8e4a8c392c6e18197e3b9b376482f3145d1ecd3f
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211390"
---
# <a name="class-httpresponse"></a>类 Httpresponse.cache 
描述单个 HTTP 响应的接口，由客户端应用在重写 HttpDelegate 时实现。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取响应 ID。
public int32_t GetStatusCode() const  |  获取响应状态代码。
public const std：： vector \<uint8_t\>& GetBody ( # A2 const  |  获取请求正文。
public const std：： map \<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders ( # A2 const  |  获取请求标头。
  
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