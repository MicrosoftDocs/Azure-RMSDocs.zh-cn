---
title: 类 HttpOperation
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 httpoperation：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: ece0d76577747170e4328bc1d9bdabb0678e65a5
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565117"
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