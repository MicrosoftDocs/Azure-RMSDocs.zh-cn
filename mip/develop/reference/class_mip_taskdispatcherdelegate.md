---
title: 类 mip：： TaskDispatcherDelegate
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： taskdispatcherdelegate 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e73a03b842b1216bcc4ef71941ca4bc0b0233945
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559953"
---
# <a name="class-miptaskdispatcherdelegate"></a>类 mip：： TaskDispatcherDelegate 
定义 MIP SDK 任务调度程序接口的类。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public void DispatchTask （const std：： string & taskId，std：： function\<void （）\> 任务）  |  在后台线程上执行任务。
public void DispatchTask （const std：： string & taskId，std：： function\<void （）\> 任务，int64_t delaySeconds）  |  在具有给定延迟的后台线程上执行任务。
public void ExecuteTaskOnIndependentThread （const std：： string & taskId，std：： function\<void （）\> 任务）  |  立即在独立线程上执行任务。
public bool CancelTask （const std：： string & taskId）  |  取消后台任务。
public void CancelAllTasks （）  |  取消所有后台任务。
  
## <a name="members"></a>成員
  
### <a name="dispatchtask-function"></a>DispatchTask 函数
在后台线程上执行任务。

参数：  
* **taskId**：唯一标识任务的 ID 


* **task**：要执行的函数


  
### <a name="dispatchtask-function"></a>DispatchTask 函数
在具有给定延迟的后台线程上执行任务。

参数：  
* **taskId**：唯一标识任务的 ID 


* **task**：要执行的函数 


* **delaySeconds**：执行任务之前的延迟（以秒为单位）


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread 函数
立即在独立线程上执行任务。

参数：  
* **taskId**：唯一标识任务的 ID 


* **task**：要执行的函数


  
### <a name="canceltask-function"></a>CancelTask 函数
取消后台任务。

参数：  
* **taskId**：要取消的任务的 ID



  
**返回**：如果已成功取消任务，则返回 True; 否则返回 false
  
### <a name="cancelalltasks-function"></a>CancelAllTasks 函数
取消所有后台任务。