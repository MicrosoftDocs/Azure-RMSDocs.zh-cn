---
title: 类 mip::TaskDispatcherDelegate
description: 记录 mip::taskdispatcherdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 568a6df614370769556cd3634070e199beb4da5b
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574425"
---
# <a name="class-miptaskdispatcherdelegate"></a>类 mip::TaskDispatcherDelegate 
定义 MIP SDK 任务调度程序的接口的类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: string & taskId，std:: function\<void()\>任务)  |  在后台线程上执行的任务。
public void DispatchTask (const std:: string & taskId，std:: function\<void()\>任务，int64_t 延迟)  |  使用给定的延迟在后台线程上执行的任务。
public void ExecuteTaskOnIndependentThread (const std:: string & taskId，std:: function\<void()\>任务)  |  立即在独立线程上执行的任务。
公共 bool CancelTask (const std:: string & taskId)  |  取消后台任务。
public void CancelAllTasks()  |  取消所有后台任务。
  
## <a name="members"></a>成員
  
### <a name="dispatchtask-function"></a>DispatchTask 函数
在后台线程上执行的任务。

参数：  
* **taskId**:ID 来唯一地标识一个任务 


* **任务**:要执行的函数


  
### <a name="dispatchtask-function"></a>DispatchTask 函数
使用给定的延迟在后台线程上执行的任务。

参数：  
* **taskId**:ID 来唯一地标识一个任务 


* **任务**:要执行的函数 


* **延迟**:执行任务前延迟 （以秒为单位）


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread 函数
立即在独立线程上执行的任务。

参数：  
* **taskId**:ID 来唯一地标识一个任务 


* **任务**:要执行的函数


  
### <a name="canceltask-function"></a>CancelTask 函数
取消后台任务。

参数：  
* **taskId**:要取消的任务 ID



  
**返回**:如果任务是已成功取消，否则为 false，则返回 true
  
### <a name="cancelalltasks-function"></a>CancelAllTasks 函数
取消所有后台任务。