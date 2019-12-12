---
title: 类 mip::PolicyHandler
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p olicyhandler 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 71b1a9dff879cde728e7fa1aa9e1f871d292ec4c
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560924"
---
# <a name="class-mippolicyhandler"></a>类 mip::PolicyHandler 
此类为文件上的所有策略处理程序函数提供一个接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std：： shared_ptr\<ContentLabel\> GetSensitivityLabel （const Executionstate& & 状态）  |  从现有内容获取敏感度标签。
public std：： vector\<std：： shared_ptr\<操作\>\> ComputeActions （const Executionstate& & 状态）  |  根据所提供的状态执行处理程序中的规则，并返回要执行的操作列表。
public void NotifyCommittedActions(const ExecutionState& state)  |  在应用计算操作并将数据提交到磁盘后调用。
  
## <a name="members"></a>成員
  
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