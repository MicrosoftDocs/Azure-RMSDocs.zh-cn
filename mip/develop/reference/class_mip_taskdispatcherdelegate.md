---
title: 类 TaskDispatcherDelegate
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 taskdispatcherdelegate：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: f8f84b51200ff630b6158f7b02ca88e2a3d21e25
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212869"
---
# <a name="class-taskdispatcherdelegate"></a>类 TaskDispatcherDelegate 
定义 MIP SDK 任务调度程序接口的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std：： string& taskId，std：： function \<void()\> task)   |  在后台线程上执行任务。
public void DispatchTask (const std：： string& taskId，std：： function \<void()\> task，Int64_t delaySeconds)   |  在具有给定延迟的后台线程上执行任务。
public void ExecuteTaskOnIndependentThread (const std：： string& taskId，std：： function \<void()\> task)   |  立即在独立线程上执行任务。
public bool CancelTask (const std：： string& taskId)   |  取消后台任务。
public void CancelAllTasks ( # A1  |  取消所有后台任务。
  
## <a name="members"></a>成员
  
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


* **delaySeconds**：执行任务之前延迟 (秒) 


  
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