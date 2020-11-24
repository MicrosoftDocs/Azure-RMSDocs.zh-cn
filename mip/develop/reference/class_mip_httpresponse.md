---
title: 类 Httpresponse.cache
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 httpresponse.cache：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 0a08b2bea4834375a01897b3d657772112463b89
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565116"
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