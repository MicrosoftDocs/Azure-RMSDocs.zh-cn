---
title: 类 mip HttpResponse
description: 类 mip HttpResponse 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a19ea78b048cafe94501d452bb9c7409237f6ffd
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445338"
---
# <a name="class-miphttpresponse"></a>类 mip::HttpResponse 
描述单个 HTTP 响应的接口，由客户端应用在重写 [HttpDelegate](class_mip_httpdelegate.md) 时实现。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public int32_t GetStatusCode() const  |  获取响应状态代码。
 public const std::string& GetBody() const  |  获取请求正文。
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  获取请求标头。
  
## <a name="members"></a>成員
  
### <a name="getstatuscode"></a>GetStatusCode
获取响应状态代码。

  
**返回结果**：状态代码
  
### <a name="getbody"></a>GetBody
获取请求正文。

  
**返回结果**：请求正文
  
### <a name="getheaders"></a>GetHeaders
获取请求标头。

  
**返回结果**：请求标头