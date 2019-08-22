---
title: '类 mip:: TaskDispatcherDelegate'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: taskdispatcherdelegate 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 0455f446cddd7db1c05f0f7e7b76b33496810cf1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883007"
---
# <a name="class-miptaskdispatcherdelegate"></a>类 mip:: TaskDispatcherDelegate 
定义 MIP SDK 任务调度程序接口的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: string & taskId, std:: function\<void ()\>任务)  |  在后台线程上执行任务。
public void DispatchTask (const std:: string & taskId, std:: function\<void ()\>任务, int64_t 延迟)  |  在具有给定延迟的后台线程上执行任务。
public void ExecuteTaskOnIndependentThread (const std:: string & taskId, std:: function\<void ()\>任务)  |  立即在独立线程上执行任务。
public bool CancelTask (const std:: string & taskId)  |  取消后台任务。
public void CancelAllTasks ()  |  取消所有后台任务。
  
## <a name="members"></a>成员
  
### <a name="dispatchtask-function"></a>DispatchTask 函数
在后台线程上执行任务。

参数：  
* **taskId**:用于唯一标识任务的 ID 


* **任务**:要执行的函数


  
### <a name="dispatchtask-function"></a>DispatchTask 函数
在具有给定延迟的后台线程上执行任务。

参数：  
* **taskId**:用于唯一标识任务的 ID 


* **任务**:要执行的函数 


* **延迟**:执行任务之前的延迟 (以秒为单位)


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread 函数
立即在独立线程上执行任务。

参数：  
* **taskId**:用于唯一标识任务的 ID 


* **任务**:要执行的函数


  
### <a name="canceltask-function"></a>CancelTask 函数
取消后台任务。

参数：  
* **taskId**:要取消的任务的 ID



  
**返回**:如果任务已成功取消, 则为 True; 否则为 false
  
### <a name="cancelalltasks-function"></a>CancelAllTasks 函数
取消所有后台任务。