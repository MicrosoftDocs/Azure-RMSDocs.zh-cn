---
title: 类 mip::HttpDelegate
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： httpdelegate 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e629e15ed3a4754123f8ca71adee04d32bc3785f
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488103"
---
# <a name="class-miphttpdelegate"></a>类 mip::HttpDelegate 
用于重写 HTTP 处理的接口。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
公共 std：： shared_ptr\<HttpOperation\> Send （const std：： shared_ptr\<HttpRequest\>& request，const std：： shared_ptr\<void\>& 上下文）  |  发送 HTTP 请求。
public std：： shared_ptr\<HttpOperation\> SendAsync （const std：： shared_ptr\<HttpRequest\>& request，const std：： shared_ptr\<void\>& context，const std：： function\<void （std：： shared_ptr\<HttpOperation\>）  |  以异步方式发送 HTTP 请求。
public void CancelOperation （const std：： string & requestId）  |  取消特定的 HTTP 操作。
public void CancelAllOperations （）  |  取消正在进行的 HTTP 请求。
  
## <a name="members"></a>Members
  
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