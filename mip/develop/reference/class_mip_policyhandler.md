---
title: 类 mip::PolicyHandler
description: 记录 mip::policyhandler 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6c5979706b9868bd7d0b6b1adad5d96bd5d3e0ce
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329584"
---
# <a name="class-mippolicyhandler"></a>类 mip::PolicyHandler 
此类为文件上的所有策略处理程序函数提供一个接口。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<ContentLabel\> GetSensitivityLabel(const ExecutionState& state)  |  从现有内容获取敏感度标签。
public std::vector\<std::shared_ptr\<Action\>\> ComputeActions(const ExecutionState& state)  |  根据所提供的状态执行处理程序中的规则，并返回要执行的操作列表。
public void NotifyCommittedActions(const ExecutionState& state)  |  在应用计算操作并将数据提交到磁盘后调用。
  
## <a name="members"></a>成員
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel 函数
从现有内容获取敏感度标签。

参数：  
* **state**：内容的当前状态 



  
**返回**:当前应用于内容的标签。 如果没有标签，则返回空。
  
### <a name="computeactions-function"></a>ComputeActions 函数
根据所提供的状态执行处理程序中的规则，并返回要执行的操作列表。

参数：  
* **state**：在其中运行规则的内容的当前执行状态。 



  
**返回**:应应用于内容的操作的列表。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 函数
在应用计算操作并将数据提交到磁盘后调用。

参数：  
* **state**：提交操作后内容的当前执行状态 


：此调用将发送一个审核事件
