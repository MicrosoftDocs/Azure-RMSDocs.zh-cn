---
title: 类 mip::HttpResponse
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: httpresponse.cache 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 4d7711f755f4ffde923eb7d913abdb5bd2a905db
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884135"
---
# <a name="class-miphttpresponse"></a>类 mip::HttpResponse 
描述单个 HTTP 响应的接口，由客户端应用在重写 [HttpDelegate](class_mip_httpdelegate.md) 时实现。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取响应 ID。
public int32_t GetStatusCode() const  |  获取响应状态代码。
public const std:: vector\<uint8_t\>& GetBody () const  |  获取请求正文。
public const std:: map\<std:: string, std:: string, CaseInsensitiveComparator\>& GetHeaders () const  |  获取请求标头。
  
## <a name="members"></a>成员
  
### <a name="getid-function"></a>GetId 函数
获取响应 ID。

  
**返回**:对应 HttpRequest 将具有相同 ID 的响应 ID
  
### <a name="getstatuscode-function"></a>GetStatusCode 函数
获取响应状态代码。

  
**返回**:状态代码
  
### <a name="getbody-function"></a>GetBody 函数
获取请求正文。

  
**返回**:请求正文
  
### <a name="getheaders-function"></a>GetHeaders 函数
获取请求标头。

  
**返回**:请求标头