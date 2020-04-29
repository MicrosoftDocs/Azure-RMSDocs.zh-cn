---
title: 类 PolicyHandler
description: 记录 Microsoft 信息保护（MIP） SDK 的 policyhandler：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: c46b72f3a040204b4485da14f00f38ca69fa8222
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760949"
---
# <a name="class-policyhandler"></a>类 PolicyHandler 
此类为文件上的所有策略处理程序函数提供一个接口。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std：： shared_ptr\<ContentLabel\> GetSensitivityLabel （const executionstate&& state）  |  从现有内容获取敏感度标签。
public std：： vector\<std：： shared_ptr\<Action\> \> ComputeActions （const executionstate&& state）  |  根据所提供的状态执行处理程序中的规则，并返回要执行的操作列表。
public void NotifyCommittedActions(const ExecutionState& state)  |  在应用计算操作并将数据提交到磁盘后调用。
  
## <a name="members"></a>成员
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel 函数
从现有内容获取敏感度标签。

参数：  
* **状态**：内容的当前状态。 



  
**返回结果**：当前应用于内容的标签。 如果没有标签，则返回空。
  
### <a name="computeactions-function"></a>ComputeActions 函数
根据所提供的状态执行处理程序中的规则，并返回要执行的操作列表。

参数：  
* **state**：在其中运行规则的内容的当前执行状态。 



  
**返回结果**：应该应用于内容的操作列表。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 函数
在应用计算操作并将数据提交到磁盘后调用。

参数：  
* **状态**：提交操作后内容的当前执行状态。 


：此调用发送审核事件。