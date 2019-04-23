---
title: 类 mip::HttpResponse
description: 记录 mip::httpresponse 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 06bc3f52bdecd85412dc0c35df46c7847167aa1b
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173977"
---
# <a name="class-miphttpresponse"></a>类 mip::HttpResponse 
描述单个 HTTP 响应的接口，由客户端应用在重写 [HttpDelegate](class_mip_httpdelegate.md) 时实现。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取响应 id。
public int32_t GetStatusCode() const  |  获取响应状态代码。
public const std:: vector\<uint8_t\>& GetBody() 常量  |  获取请求正文。
public const std:: map\<std:: string、 std:: string，CaseInsensitiveComparator\>& GetHeaders() 常量  |  获取请求标头。
  
## <a name="members"></a>成員
  
### <a name="getid-function"></a>GetId 函数
获取响应 id。

  
**返回**:响应 ID 对应[HttpRequest](class_mip_httprequest.md)将有相同的 ID
  
### <a name="getstatuscode-function"></a>GetStatusCode 函数
获取响应状态代码。

  
**返回**:状态代码
  
### <a name="getbody-function"></a>GetBody 函数
获取请求正文。

  
**返回**:请求正文
  
### <a name="getheaders-function"></a>GetHeaders 函数
获取请求标头。

  
**返回**:请求标头