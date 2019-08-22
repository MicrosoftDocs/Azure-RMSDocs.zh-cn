---
title: class mip::LoggerDelegate
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: loggerdelegate 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: effba9bc41907c477cea7e3cf6a8688187538068
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883912"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
定义 MIP SDK 记录器接口的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath, LogLevel logLevel)  |  初始化记录器。
public LogLevel GetLogLevel() const  |  获取将触发日志记录事件的最低日志级别。
public void Flush()  |  刷新记录器。
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  将日志语句写入日志文件。
  
## <a name="members"></a>成员
  
### <a name="init-function"></a>Init 函数
初始化记录器。

参数：  
* **storagePath**：指向可能存储永久性状态（包括日志）的位置的路径。 


* **logLevel**：应触发日志记录事件的最低日志级别。


  
### <a name="getloglevel-function"></a>GetLogLevel 函数
获取将触发日志记录事件的最低日志级别。

  
**返回**:触发日志记录事件的最低日志级别。
  
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

