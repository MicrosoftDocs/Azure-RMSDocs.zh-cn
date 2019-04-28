---
title: class mip::LoggerDelegate
description: 记录 mip::loggerdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 511c8dabc8ff31c70c8343a80d423b76c43fa946
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184614"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
定义 MIP SDK 记录器接口的类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath, LogLevel logLevel)  |  初始化记录器。
public LogLevel GetLogLevel() const  |  获取将触发日志记录事件的最低日志级别。
public void Flush()  |  刷新记录器。
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  将日志语句写入日志文件。
  
## <a name="members"></a>成員
  
### <a name="init-function"></a>Init 函数
初始化记录器。

参数：  
* **storagePath**：指向可能存储永久性状态（包括日志）的位置的路径。 


* **logLevel**：应触发日志记录事件的最低日志级别。


  
### <a name="getloglevel-function"></a>GetLogLevel 函数
获取将触发日志记录事件的最低日志级别。

  
**返回**:最低日志级别触发日志记录事件。
  
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

