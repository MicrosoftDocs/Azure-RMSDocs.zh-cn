---
title: '类 mip:: TaskDispatcherDelegate'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: taskdispatcherdelegate 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d5237bf999f7ad704fd303783a9fbdc506b58ed2
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056773"
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