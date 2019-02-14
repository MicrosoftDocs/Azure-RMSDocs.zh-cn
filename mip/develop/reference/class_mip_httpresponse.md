---
title: 类 mip::HttpResponse
description: 记录 mip::httpresponse 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 00a6d7dd3728edbf6fb1dbb4e59c537d7b6cf911
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252990"
---
# <a name="class-miphttpresponse"></a>类 mip::HttpResponse 
描述单个 HTTP 响应的接口，由客户端应用在重写 [HttpDelegate](class_mip_httpdelegate.md) 时实现。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public int32_t GetStatusCode() const  |  获取响应状态代码。
public const std::string& GetBody() const  |  获取请求正文。
public const std:: map\<std:: string、 std:: string，CaseInsensitiveComparator\>& GetHeaders() 常量  |  获取请求标头。
  
## <a name="members"></a>成員
  
### <a name="getstatuscode-function"></a>GetStatusCode 函数
获取响应状态代码。

  
**返回**:状态代码
  
### <a name="getbody-function"></a>GetBody 函数
获取请求正文。

  
**返回**:请求正文
  
### <a name="getheaders-function"></a>GetHeaders 函数
获取请求标头。

  
**返回**:请求标头
