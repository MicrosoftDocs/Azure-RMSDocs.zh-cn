---
title: 类 mip::HttpDelegate
description: 记录 mip::httpdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 8dd81508766c65d6232c278d56f3720a98aaa9eb
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256288"
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
