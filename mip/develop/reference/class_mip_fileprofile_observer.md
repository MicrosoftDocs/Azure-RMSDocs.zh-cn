---
title: class mip::FileProfile::Observer
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： fileprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: fbe8b2edd8e9ee8d013134e66c39db8fbbee4dd4
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560206"
---
# <a name="class-mipfileprofileobserver"></a>class mip::FileProfile::Observer 
观察者接口，供客户端获取配置文件相关事件的通知。
所有错误都继承自 mip：： Error。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public virtual ~Observer()  | 尚未记录。
public virtual void OnLoadSuccess （const std：： shared_ptr\<mip：： FileProfile\>& profile，const std：： shared_ptr\<void\>& 上下文）  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess （const std：： vector\<std：： string\>& engineIds，const std：： shared_ptr\<void\>& 上下文）  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在列出引擎引发错误时调用。
public virtual void OnUnloadEngineSuccess （const std：： shared_ptr\<void\>& 上下文）  |  在成功卸载引擎时调用。
public virtual void OnUnloadEngineFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在卸载引擎引发错误时调用。
public virtual void OnAddEngineSuccess （const std：： shared_ptr\<mip：： FileEngine\>& 引擎，const std：： shared_ptr\<void\>& 上下文）  |  在成功添加新引擎时调用。
public virtual void OnAddEngineFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在添加新引擎引发错误时调用。
public virtual void OnDeleteEngineSuccess （const std：： shared_ptr\<void\>& 上下文）  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在删除引擎引发错误时调用。
public virtual void OnPolicyChanged(const std::string& engineId)  |  在针对具有给定 ID 的引擎的策略发生更改时调用。
public virtual void OnAddPolicyEngineStarting （bool requiresPolicyFetch）  |  在创建引擎之前调用，用于描述是否必须从服务器获取策略引擎的策略数据，或者是否可从本地缓存的数据创建策略引擎。
受保护的 Observer()  | 尚未记录。
  
## <a name="members"></a>成員
  
### <a name="observer-function"></a>~ 观察程序函数
_尚无记录。_

  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 函数
在成功加载配置文件时调用。
  
### <a name="onloadfailure-function"></a>OnLoadFailure 函数
在加载配置文件引发错误时调用。
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 函数
在成功生成引擎列表时调用。
  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 函数
在列出引擎引发错误时调用。
  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess 函数
在成功卸载引擎时调用。
  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure 函数
在卸载引擎引发错误时调用。
  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 函数
在成功添加新引擎时调用。
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 函数
在添加新引擎引发错误时调用。
  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 函数
在成功删除引擎时调用。
  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 函数
在删除引擎引发错误时调用。
  
### <a name="onpolicychanged-function"></a>OnPolicyChanged 函数
在针对具有给定 ID 的引擎的策略发生更改时调用。
  
### <a name="onaddpolicyenginestarting-function"></a>OnAddPolicyEngineStarting 函数
在创建引擎之前调用，用于描述是否必须从服务器获取策略引擎的策略数据，或者是否可从本地缓存的数据创建策略引擎。

参数：  
* **requiresPolicyFetch**：描述是否必须通过 HTTP 获取引擎数据或是否从缓存中加载引擎数据


此可选回调可由应用程序使用，通知 AddEngineAsync 操作是否需要执行 HTTP 操作（及其关联的延迟）才能完成。
  
### <a name="observer-function"></a>观察程序函数
_尚无记录。_
