---
title: 类 HttpOperation
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 httpoperation：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 7ceb76ff61ce13fd47b764fa336ffcf5e167608e
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211509"
---
# <a name="class-httpoperation"></a>类 HttpOperation 
一个接口，该接口描述在重写 HttpDelegate 时由客户端应用程序实现的单个 HTTP 操作。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取操作 ID。
public std：： shared_ptr \<HttpResponse\> GetResponse ( # A1  |  获取响应（如果有）。
public bool IsCancelled ( # A1  |  获取操作的取消状态。
  
## <a name="members"></a>成员
  
### <a name="getid-function"></a>GetId 函数
获取操作 ID。

  
**返回**：操作 ID 相应的 HttpRequest 和 httpresponse.cache 将具有相同的 id
  
### <a name="getresponse-function"></a>GetResponse 函数
获取响应（如果有）。

  
**返回**：响应
  
### <a name="iscancelled-function"></a>IsCancelled 函数
获取操作的取消状态。

  
**返回**：取消状态