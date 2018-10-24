---
title: 类 mip PolicyHandler
description: 类 mip PolicyHandler 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 23de5616558a298189cb885727d69a20373a3609
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445931"
---
# <a name="class-mippolicyhandler"></a>类 mip::PolicyHandler 
此类为文件上的所有策略处理程序函数提供一个接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state)  |  从现有内容获取敏感度标签。
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  根据所提供的状态执行处理程序中的规则，并返回要执行的操作列表。
 public void NotifyCommittedActions(const ExecutionState& state)  |  在应用计算操作并将数据提交到磁盘后调用。
  
## <a name="members"></a>成員
  
### <a name="contentlabel"></a>ContentLabel
从现有内容获取敏感度标签。

参数：  
* **state**：内容的当前状态 



  
**返回结果**：当前应用于内容的标签。 如果没有标签，则返回空。
  
### <a name="action"></a>操作
根据所提供的状态执行处理程序中的规则，并返回要执行的操作列表。

参数：  
* **state**：在其中运行规则的内容的当前执行状态。 



  
**返回结果**：应该应用于内容的操作列表。
  
### <a name="notifycommittedactions"></a>NotifyCommittedActions
在应用计算操作并将数据提交到磁盘后调用。

参数：  
* **state**：提交操作后内容的当前执行状态 


：此调用发送审核事件