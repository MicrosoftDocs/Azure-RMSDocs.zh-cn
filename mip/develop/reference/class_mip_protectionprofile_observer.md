---
title: class mip ProtectionProfile Observer
description: class mip ProtectionProfile Observer 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3678e6c1e1659f28b2f1dcc36f61295a8d29393e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446424"
---
# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesFailure(const std::exception_ptr& error、const std::shared_ptr<void>& context)  |  在列出引擎出错时调用。
public virtual void OnAddEngineSuccess(const std::shared_ptr<ProtectionEngine>& engine, const std::shared_ptr<void>& context)  |  在成功添加新引擎时调用。
public virtual void OnAddEngineFailure(const std::exception_ptr& error、const std::shared_ptr<void>& context)  |  在添加新引擎出错时调用。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在删除引擎出错时调用。
  
## <a name="members"></a>成員
  
### <a name="onloadsuccess"></a>OnLoadSuccess
在成功加载配置文件时调用。

参数：  
* **profile**：对新创建的 [ProtectionProfile](class_mip_protectionprofile.md) 的引用


* **context**：传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) 或 [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
在加载配置文件引发错误时调用。

参数：  
* **error**：加载时发生的 [Error](class_mip_error.md) 


* **context**：传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) 或 [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
在成功生成引擎列表时调用。

参数：  
* **engineIds**：可用的引擎 ID 列表。 


* **context**：传递到 [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync) 的相同上下文


  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
在列出引擎出错时调用。

参数：  
* **error**：导致列出引擎操作失败的错误。 


* **context**：传递到 [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync) 的相同上下文


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
在成功添加新引擎时调用。

参数：  
* **engine**：新创建的引擎 


* **context**：传递到 [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync) 的相同上下文


  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
在添加新引擎出错时调用。

参数：  
* **error**：导致添加引擎操作失败的错误。 


* **context**：传递到 [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync) 的相同上下文


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
在成功删除引擎时调用。

参数：  
* **context**：传递到 [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync) 的相同上下文


  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
在删除引擎出错时调用。

参数：  
* **error**：导致删除引擎操作失败的错误。 


* **context**：传递到 [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync) 的相同上下文

