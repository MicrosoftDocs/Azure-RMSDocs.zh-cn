---
title: 类 mip::HttpDelegate
description: 记录 mip::httpdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 18425a807fcddc1bc1db19a35534036a6552255c
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329839"
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
