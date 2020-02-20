---
title: 类 mip：： HttpOperation
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： httpoperation 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 4be7b54dd5df255c488043d84ebcfebbce7e6ac2
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489990"
---
# <a name="class-miphttpoperation"></a>类 mip：： HttpOperation 
一个接口，该接口描述在重写 HttpDelegate 时由客户端应用程序实现的单个 HTTP 操作。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取操作 ID。
public std：： shared_ptr\<Httpresponse.cache\> GetResponse （）  |  获取响应（如果有）。
public bool IsCancelled （）  |  获取操作的取消状态。
  
## <a name="members"></a>Members
  
### <a name="getid-function"></a>GetId 函数
获取操作 ID。

  
**返回**：操作 ID 相应的 HttpRequest 和 httpresponse.cache 将具有相同的 id
  
### <a name="getresponse-function"></a>GetResponse 函数
获取响应（如果有）。

  
**返回**：响应
  
### <a name="iscancelled-function"></a>IsCancelled 函数
获取操作的取消状态。

  
**返回**：取消状态