---
title: 类 mip::HttpOperation
description: 记录 mip::httpoperation 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: e3eaedbf508f116b19521286b686bc955d108efe
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574476"
---
# <a name="class-miphttpoperation"></a>类 mip::HttpOperation 
描述单个 HTTP 操作，重写时，由客户端应用程序实现的接口[HttpDelegate](class_mip_httpdelegate.md)。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取操作 id。
public std::shared_ptr\<HttpResponse\> GetResponse()  |  获取响应，如果有。
public bool IsCancelled()  |  获取操作的取消状态。
  
## <a name="members"></a>成員
  
### <a name="getid-function"></a>GetId 函数
获取操作 id。

  
**返回**:操作 ID 的相应[HttpRequest](class_mip_httprequest.md)并[HttpResponse](class_mip_httpresponse.md)将具有相同的 ID
  
### <a name="getresponse-function"></a>GetResponse 函数
获取响应，如果有。

  
**返回**:响应
  
### <a name="iscancelled-function"></a>IsCancelled 函数
获取操作的取消状态。

  
**返回**:取消状态