---
title: 类 mip LoggerDelegate
description: 类 mip LoggerDelegate 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: b25cdb177735feccfa5c4d344613e4747d18b77f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445846"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
定义 MIP SDK 记录器接口的类。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public void Init(const std::string& storagePath, LogLevel logLevel)  |  初始化记录器。
 public LogLevel GetLogLevel() const  |  获取将触发日志记录事件的最低日志级别。
 public void Flush()  |  刷新记录器。
 public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  将日志语句写入日志文件。
  
## <a name="members"></a>成員
  
### <a name="init"></a>初始化
初始化记录器。

参数：  
* **storagePath**：指向可能存储永久性状态（包括日志）的位置的路径。 


* **logLevel**：应触发日志记录事件的最低日志级别。


  
### <a name="loglevel"></a>日志级别
获取将触发日志记录事件的最低日志级别。

  
**返回结果**：将触发日志记录事件的最低日志级别。
  
### <a name="flush"></a>刷新
刷新记录器。
  
### <a name="writetolog"></a>WriteToLog
将日志语句写入日志文件。

参数：  
* **level**：日志语句的日志级别。 


* **message**：日志语句的消息。 


* **function**：日志语句的函数名称。 


* **file**：生成的日志语句所在的文件名。 


* **line**：生成的日志语句所在的行号。

