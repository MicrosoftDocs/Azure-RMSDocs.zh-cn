---
title: 类 mip HttpDelegate
description: 类 mip HttpDelegate 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3e55f9aff5a9ebd97731ec21e408a33f22905648
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445340"
---
# <a name="class-miphttpdelegate"></a>类 mip::HttpDelegate 
用于重写 HTTP 处理的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public std::shared_ptr<HttpResponse> Send(const std::shared_ptr<HttpRequest>& request, const std::shared_ptr<void>& context)  |  发送 HTTP 请求。
  
## <a name="members"></a>成員
  
### <a name="httpresponse"></a>HttpResponse
发送 HTTP 请求。

参数：  
* **request**：HTTP 请求 


* **context**：传递给导致此 HTTP 请求的 API 的相同不透明客户端上下文



  
**返回结果**：HTTP 响应