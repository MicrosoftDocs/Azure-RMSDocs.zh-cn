---
title: 类 TaskDispatcherDelegate
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 taskdispatcherdelegate：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 057ba0d4de58ab4dedf8d3e2f8b2a42b0e5f969a
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565155"
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