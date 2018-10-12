---
title: class mip PolicyProfile Observer
description: class mip PolicyProfile Observer 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5de2156f4906c14e4ebc1418df8acb092c089d7d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446839"
---
# <a name="class-mippolicyprofileobserver"></a>class mip::PolicyProfile::Observer 
[Observer](class_mip_policyprofile_observer.md) 接口，供客户端获取配置文件相关事件的通知。
所有错误都继承自 [mip::Error](class_mip_error.md)。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<PolicyProfile>& profile, const std::shared_ptr<void>& context)  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在列出引擎引发错误时调用。
public virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  在成功卸载引擎时调用。
public virtual void OnUnloadEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在卸载引擎引发错误时调用。
public virtual void OnAddEngineSuccess(const std::shared_ptr<PolicyEngine>& engine, const std::shared_ptr<void>& context)  |  在成功添加新引擎时调用。
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在添加新引擎引发错误时调用。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在删除引擎引发错误时调用。
 public virtual void OnPolicyChanged(const std::string& engineId)  |  在针对具有给定 ID 的引擎的策略发生更改时调用。
  
## <a name="members"></a>成員
  
### <a name="onloadsuccess"></a>OnLoadSuccess
在成功加载配置文件时调用。

参数：  
* **profile**：用于启动操作的当前配置文件。 


* **context**：传递给操作的上下文。


  
### <a name="onloadfailure"></a>OnLoadFailure
在加载配置文件引发错误时调用。

参数：  
* error：导致负载操作失败的错误。 


* **context**：传递给操作的上下文。


  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
在成功生成引擎列表时调用。

参数：  
* engineIds：可用的引擎 ID 列表。 


* **context**：传递给操作的上下文。


  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
在列出引擎引发错误时调用。

参数：  
* error：导致列出引擎操作失败的错误。 


* **context**：传递给操作的上下文。


  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
在成功卸载引擎时调用。

参数：  
* **context**：传递给操作的上下文。


  
### <a name="onunloadenginefailure"></a>OnUnloadEngineFailure
在卸载引擎引发错误时调用。

参数：  
* error：导致卸载引擎操作失败的错误。 


* **context**：传递给操作的上下文。


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
在成功添加新引擎时调用。
  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
在添加新引擎引发错误时调用。

参数：  
* error：导致添加引擎操作失败的错误。 


* **context**：传递给操作的上下文。


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
在成功删除引擎时调用。

参数：  
* **context**：传递给操作的上下文。


  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
在删除引擎引发错误时调用。

参数：  
* error：导致删除引擎操作失败的错误。 


* **context**：传递给操作的上下文。


  
### <a name="onpolicychanged"></a>OnPolicyChanged
在针对具有给定 ID 的引擎的策略发生更改时调用。

参数：  
* **engineId**：引擎 


若要加载新策略，需要再次使用指定引擎 ID 调用 AddEngineAsync。