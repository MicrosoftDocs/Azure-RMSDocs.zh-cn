---
title: 类 LoggerDelegate
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 loggerdelegate：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: d7869035af314c2328b49380567f4259d69c961a
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215198"
---
# <a name="class-loggerdelegate"></a>类 LoggerDelegate 
定义 MIP SDK 记录器接口的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath)  |  初始化记录器。
public void Flush()  |  刷新记录器。
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  将日志语句写入日志文件。
  
## <a name="members"></a>成员
  
### <a name="init-function"></a>Init 函数
初始化记录器。

参数：  
* **storagePath**：指向可能存储永久性状态（包括日志）的位置的路径。


  
### <a name="flush-function"></a>Flush 函数
刷新记录器。
  
### <a name="writetolog-function"></a>WriteToLog 函数
将日志语句写入日志文件。

参数：  
* **level**：日志语句的日志级别。 


* **message**：日志语句的消息。 


* **function**：日志语句的函数名称。 


* **file**：生成的日志语句所在的文件名。 


* **line**：生成的日志语句所在的行号。

