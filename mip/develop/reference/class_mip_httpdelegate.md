---
title: 类 mip::HttpDelegate
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： httpdelegate 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a29673c71aaa0357ebb52bc4cab3b3fef74a21d1
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560200"
---
# <a name="class-miphttpdelegate"></a>类 mip::HttpDelegate 
用于重写 HTTP 处理的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std：： shared_ptr\<HttpOperation\> Send （const std：： shared_ptr\<HttpRequest\>& request，const std：： shared_ptr\<void\>& 上下文）  |  发送 HTTP 请求。
public std：： shared_ptr\<HttpOperation\> SendAsync （const std：： shared_ptr\<HttpRequest\>& request，const std：： shared_ptr\<void\>& context，const std：： function\<void （std：： shared_ptr\<HttpOperation\>）  |  以异步方式发送 HTTP 请求。
public void CancelOperation （const std：： string & requestId）  |  取消特定的 HTTP 操作。
public void CancelAllOperations （）  |  取消正在进行的 HTTP 请求。
  
## <a name="members"></a>成員
  
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