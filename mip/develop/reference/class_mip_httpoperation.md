---
title: 类 HttpOperation
description: 记录 Microsoft 信息保护（MIP） SDK 的 httpoperation：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 09fac96f16bf18e72d6217842728d48244b9c412
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762799"
---
# <a name="class-httpoperation"></a>类 HttpOperation 
一个接口，该接口描述在重写 HttpDelegate 时由客户端应用程序实现的单个 HTTP 操作。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取操作 ID。
public std：： shared_ptr\<httpresponse.cache\> GetResponse （）  |  获取响应（如果有）。
public bool IsCancelled （）  |  获取操作的取消状态。
  
## <a name="members"></a>成员
  
### <a name="getid-function"></a>GetId 函数
获取操作 ID。

  
**返回**：操作 ID 相应的[HttpRequest](class_mip_httprequest.md)和[HTTPRESPONSE.CACHE](class_mip_httpresponse.md)将具有相同的 id
  
### <a name="getresponse-function"></a>GetResponse 函数
获取响应（如果有）。

  
**返回**：响应
  
### <a name="iscancelled-function"></a>IsCancelled 函数
获取操作的取消状态。

  
**返回**：取消状态