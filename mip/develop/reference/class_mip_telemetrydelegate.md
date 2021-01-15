---
title: 类 TelemetryDelegate
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 telemetrydelegate：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 40e9c3a695f70af8051ef2a6e89ad232a7c09f54
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224913"
---
# <a name="class-telemetrydelegate"></a>类 TelemetryDelegate 
一个类，用于定义 MIP SDK 审核/遥测通知的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public void WriteEvent (const std：： shared_ptr \<TelemetryEvent\>& 事件)   |  记录诊断事件。
public void Flush()  |  刷新任何排队事件 (例如由于关机) 
  
## <a name="members"></a>成员
  
### <a name="writeevent-function"></a>WriteEvent 函数
记录诊断事件。

参数：  
* **event**：要记录的事件


  
### <a name="flush-function"></a>Flush 函数
刷新任何排队事件 (例如由于关机) 