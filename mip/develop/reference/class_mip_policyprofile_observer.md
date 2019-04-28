---
title: class mip::PolicyProfile::Observer
description: 记录 mip::policyprofile 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: f9ff2448b3ae09e094189e85b15b2fabad12321e
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184546"
---
# <a name="class-mippolicyprofileobserver"></a>class mip::PolicyProfile::Observer 
[Observer](class_mip_policyprofile_observer.md) 接口，供客户端获取配置文件相关事件的通知。
所有错误都继承自 [mip::Error](class_mip_error.md)。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共虚拟 void OnLoadSuccess (const std::\<PolicyProfile\>（& a) 配置文件，const std:: shared_ptr\<void\>& 上下文)  |  在成功加载配置文件时调用。
公共虚拟 void OnLoadFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess(const std::vector\<std::string\>& engineIds, const std::shared_ptr\<void\>& context)  |  在成功生成引擎列表时调用。
公共虚拟 void OnListEnginesFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在列出引擎引发错误时调用。
public virtual void OnUnloadEngineSuccess(const std::shared_ptr\<void\>& context)  |  在成功卸载引擎时调用。
公共虚拟 void OnUnloadEngineFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在卸载引擎引发错误时调用。
public virtual void OnAddEngineSuccess(const std::shared_ptr\<PolicyEngine\>& engine, const std::shared_ptr\<void\>& context)  |  在成功添加新引擎时调用。
公共虚拟 void OnAddEngineStarting (bool requiresPolicyFetch)  |  在引擎创建，用于描述必须从服务器中提取引擎的策略数据或者它是否可以创建从本地缓存的数据之前调用。
公共虚拟 void OnAddEngineFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在添加新引擎引发错误时调用。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  在成功删除引擎时调用。
公共虚拟 void OnDeleteEngineFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在删除引擎引发错误时调用。
public virtual void OnPolicyChanged(const std::string& engineId)  |  策略已更改为具有给定 ID 的引擎时或加载自定义敏感类型已更改时调用。
  
## <a name="members"></a>成員
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 函数
在成功加载配置文件时调用。

参数：  
* **profile**：用于启动操作的当前配置文件。 


* **上下文**： 上下文传递到 LoadAsync 操作。


  
### <a name="onloadfailure-function"></a>OnLoadFailure 函数
在加载配置文件引发错误时调用。

参数：  
* error：导致负载操作失败的错误。 


* **上下文**： 上下文传递到 LoadAsync 操作。


  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 函数
在成功生成引擎列表时调用。

参数：  
* **engineIds**：可用的引擎 ID 列表。 


* **上下文**： 上下文传递到 ListEnginesAsync 操作。


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 函数
在列出引擎引发错误时调用。

参数：  
* error：导致列出引擎操作失败的错误。 


* **上下文**： 上下文传递到 ListEnginesAsync 操作。


  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess 函数
在成功卸载引擎时调用。

参数：  
* **上下文**： 上下文传递到 UnloadEngineAsync 操作。


  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure 函数
在卸载引擎引发错误时调用。

参数：  
* error：导致卸载引擎操作失败的错误。 


* **上下文**： 上下文传递到 UnloadEngineAsync 操作。


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 函数
在成功添加新引擎时调用。

参数：  
* **引擎**： 新增的引擎 


* **上下文**： 上下文传递到 AddEngineAsync 操作


  
### <a name="onaddenginestarting-function"></a>OnAddEngineStarting 函数
在引擎创建，用于描述必须从服务器中提取引擎的策略数据或者它是否可以创建从本地缓存的数据之前调用。

参数：  
* **requiresPolicyFetch**:描述是否必须通过 HTTP 提取引擎数据，或如果它将从加载缓存


此可选的回调可能会由应用程序，用于会收到通知 AddEngineAsync 操作将需要有一个 HTTP 操作 （使用其相关联的延迟） 才能完成。
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 函数
在添加新引擎引发错误时调用。

参数：  
* **error**：导致添加引擎操作失败的错误。 


* **上下文**： 上下文传递到 AddEngineAsync 操作。


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 函数
在成功删除引擎时调用。

参数：  
* **上下文**： 上下文传递到 DeleteEngineAsync 操作。


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 函数
在删除引擎引发错误时调用。

参数：  
* **error**：导致删除引擎操作失败的错误。 


* **上下文**： 上下文传递到 DeleteEngineAsync 操作。


  
### <a name="onpolicychanged-function"></a>OnPolicyChanged 函数
策略已更改为具有给定 ID 的引擎时或加载自定义敏感类型已更改时调用。

参数：  
* **engineId**：引擎 


若要加载新策略，需要再次使用指定引擎 ID 调用 AddEngineAsync。