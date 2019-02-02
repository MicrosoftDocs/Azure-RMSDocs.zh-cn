---
title: 类 mip::HttpDelegate
description: 记录 mip::httpdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 68d26b23c1e3ea2e29c22316f80e18937ab78d5c
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651014"
---
# <a name="class-miphttpdelegate"></a>类 mip::HttpDelegate 
用于重写 HTTP 处理的接口。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::\<HttpResponse\>发送 (const std:: shared_ptr\<HttpRequest\>（& a) 请求，const std:: shared_ptr\<void\>& 上下文)  |  发送 HTTP 请求。
public void SendAsync(const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& context, const std::function\<void(std::shared_ptr\<HttpResponse\>)\>& fnCallback)  | _尚无记录。_
  
## <a name="members"></a>成員
  
### <a name="send-function"></a>Send 函数
发送 HTTP 请求。

参数：  
* **请求**:HTTP 请求 


* **上下文**:传递到此 HTTP 请求会导致 API 相同的不透明的客户端上下文



  
**返回**:HTTP 响应
  
### <a name="sendasync-function"></a>SendAsync 函数
_尚无记录。_
