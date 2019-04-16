---
title: 类 mip::HttpDelegate
description: 记录 mip::httpdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6dedd5e52b0599a58acabd85f7bd076169b3758e
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574187"
---
# <a name="class-miphttpdelegate"></a>类 mip::HttpDelegate 
用于重写 HTTP 处理的接口。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<HttpOperation\> Send(const std::shared_ptr\<HttpRequest\>& request, const std::shared_ptr\<void\>& context)  |  发送 HTTP 请求。
public std::\<HttpOperation\> SendAsync (const std:: shared_ptr\<HttpRequest\>（& a) 请求，const std:: shared_ptr\<void\>& 上下文、 const std::函数\<void (std:: shared_ptr\<HttpOperation\>)\>& callbackFn)  |  以异步方式发送 HTTP 请求。
public void CancelOperation (const std:: string & requestId)  |  取消特定 HTTP 操作。
public void CancelAllOperations()  |  取消正在进行的 HTTP 请求。
  
## <a name="members"></a>成員
  
### <a name="send-function"></a>Send 函数
发送 HTTP 请求。

参数：  
* **请求**:HTTP 请求 


* **上下文**:传递到此 HTTP 请求会导致 API 相同的不透明的客户端上下文



  
**返回**:HTTP 操作容器
  
### <a name="sendasync-function"></a>SendAsync 函数
以异步方式发送 HTTP 请求。

参数：  
* **请求**:HTTP 请求 


* **上下文**:传递到此 HTTP 请求会导致 API 相同的不透明的客户端上下文 


* **callbackFn**:将在完成时执行的函数



  
**返回**:HTTP 操作容器
  
### <a name="canceloperation-function"></a>CancelOperation 函数
取消特定 HTTP 操作。

参数：  
* **requestId**:取消请求的 ID


  
### <a name="cancelalloperations-function"></a>CancelAllOperations 函数
取消正在进行的 HTTP 请求。