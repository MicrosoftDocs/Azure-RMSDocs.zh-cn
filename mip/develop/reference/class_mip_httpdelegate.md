---
title: 类 HttpDelegate
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 httpdelegate：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d52752538aae982f8f5b0138aaf26deefa0d98a3
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565119"
---
# <a name="class-httpdelegate"></a>类 HttpDelegate 
用于重写 HTTP 处理的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<HttpOperation\> Send(const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& context)  |  发送 HTTP 请求。
public std：： shared_ptr \<HttpOperation\> SendAsync (const std：： shared_ptr \<HttpRequest\>& request，const std：： shared_ptr \<void\>& context，const std：： function \<void(std::shared_ptr\<HttpOperation\> )   |  以异步方式发送 HTTP 请求。
公共 void CancelOperation (const std：： string& requestId)   |  取消特定的 HTTP 操作。
public void CancelAllOperations ( # A1  |  取消正在进行的 HTTP 请求。
  
## <a name="members"></a>成员
  
### <a name="send-function"></a>Send 函数
发送 HTTP 请求。

参数：  
* **request**：HTTP 请求 


* **context**：传递给导致此 HTTP 请求的 API 的相同不透明客户端上下文



  
**返回**： HTTP 操作容器
  
### <a name="sendasync-function"></a>SendAsync 函数
以异步方式发送 HTTP 请求。

参数：  
* **request**：HTTP 请求 


* **context**：传递给导致此 HTTP 请求的 API 的相同不透明客户端上下文 


* **callbackFn**：将在完成时执行的函数



  
**返回**： HTTP 操作容器
  
### <a name="canceloperation-function"></a>CancelOperation 函数
取消特定的 HTTP 操作。

参数：  
* **requestId**：要取消的请求 ID


  
### <a name="cancelalloperations-function"></a>CancelAllOperations 函数
取消正在进行的 HTTP 请求。