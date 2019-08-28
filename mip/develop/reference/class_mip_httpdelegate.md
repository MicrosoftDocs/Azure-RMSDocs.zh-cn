---
title: 类 mip::HttpDelegate
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: httpdelegate 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: f5f5bc13f3c01e40b0034d4fae1bd698da8426c5
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054875"
---
# <a name="class-miphttpdelegate"></a>类 mip::HttpDelegate 
用于重写 HTTP 处理的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<HttpOperation\> Send (const std:: shared_ptr\<HttpRequest\>& request, const std:: shared_ptr\<void\>& context)  |  发送 HTTP 请求。
public std:: shared_ptr\<HttpOperation\> SendAsync (const std:: shared_ptr\<HttpRequest\>& request, const std:: shared_ptr\<void\>& context, const std::函数\<void (std:: shared_ptr\<HttpOperation\>)\>& callbackFn)  |  以异步方式发送 HTTP 请求。
public void CancelOperation (const std:: string & requestId)  |  取消特定的 HTTP 操作。
public void CancelAllOperations ()  |  取消正在进行的 HTTP 请求。
  
## <a name="members"></a>成员
  
### <a name="send-function"></a>Send 函数
发送 HTTP 请求。

参数：  
* **请求**:HTTP 请求 


* **上下文**:传递给导致此 HTTP 请求的 API 的同一个不透明的客户端上下文



  
**返回**:HTTP 操作容器
  
### <a name="sendasync-function"></a>SendAsync 函数
以异步方式发送 HTTP 请求。

参数：  
* **请求**:HTTP 请求 


* **上下文**:传递给导致此 HTTP 请求的 API 的同一个不透明的客户端上下文 


* **callbackFn**:完成时要执行的函数



  
**返回**:HTTP 操作容器
  
### <a name="canceloperation-function"></a>CancelOperation 函数
取消特定的 HTTP 操作。

参数：  
* **requestId**:要取消的请求的 ID


  
### <a name="cancelalloperations-function"></a>CancelAllOperations 函数
取消正在进行的 HTTP 请求。