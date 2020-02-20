---
title: 类 mip：： TaskDispatcherDelegate
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： taskdispatcherdelegate 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: dca6a5fa04b62abf23f0116f63fd4a91c6081da0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489327"
---
# <a name="class-miptaskdispatcherdelegate"></a>类 mip：： TaskDispatcherDelegate 
定义 MIP SDK 任务调度程序接口的类。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public void DispatchTask （const std：： string & taskId，std：： function\<void （）\> 任务）  |  在后台线程上执行任务。
public void DispatchTask （const std：： string & taskId，std：： function\<void （）\> 任务，int64_t delaySeconds）  |  在具有给定延迟的后台线程上执行任务。
public void ExecuteTaskOnIndependentThread （const std：： string & taskId，std：： function\<void （）\> 任务）  |  立即在独立线程上执行任务。
public bool CancelTask （const std：： string & taskId）  |  取消后台任务。
public void CancelAllTasks （）  |  取消所有后台任务。
  
## <a name="members"></a>Members
  
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