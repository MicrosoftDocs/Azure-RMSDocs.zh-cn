---
title: '类 mip:: HttpOperation'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: httpoperation 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 8503a5466fe180fc6831e85e1b53954ba99f55c7
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884112"
---
# <a name="class-miphttpoperation"></a>类 mip:: HttpOperation 
一个接口, 该接口描述在重写[HttpDelegate](class_mip_httpdelegate.md)时由客户端应用程序实现的单个 HTTP 操作。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取操作 ID。
public std:: shared_ptr\<httpresponse.cache\> GetResponse ()  |  获取响应 (如果有)。
public bool IsCancelled ()  |  获取操作的取消状态。
  
## <a name="members"></a>成员
  
### <a name="getid-function"></a>GetId 函数
获取操作 ID。

  
**返回**:操作 ID 相应的 HttpRequest 和 Httpresponse.cache 将具有相同的 ID
  
### <a name="getresponse-function"></a>GetResponse 函数
获取响应 (如果有)。

  
**返回**:响应
  
### <a name="iscancelled-function"></a>IsCancelled 函数
获取操作的取消状态。

  
**返回**:取消状态