---
title: 类 LoggerDelegate
description: 记录 Microsoft 信息保护（MIP） SDK 的 loggerdelegate：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: e213f243a0e46bb804b224c7a0752a0b9b270103
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761831"
---
# <a name="class-loggerdelegate"></a>类 LoggerDelegate 
定义 MIP SDK 记录器接口的类。
  
## <a name="summary"></a>“摘要”
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

