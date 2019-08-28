---
title: class mip::LoggerDelegate
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: loggerdelegate 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 6339accaa94d00a95faf9ab047e148d61671422c
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054592"
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

