---
title: 类 FileProfile：：观察程序
description: 记录 Microsoft 信息保护（MIP） SDK 的 fileprofile：：观察者类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 4dd3ff426e92fdd28cac211eb6953b8d30eb5ae5
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762763"
---
# <a name="class-fileprofileobserver"></a>类 FileProfile：：观察程序 
Observer 接口，供客户端获取配置文件相关事件的通知。
所有错误都继承自 mip::Error。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual ~Observer()  | _尚无记录。_
public virtual void OnLoadSuccess （const std：： shared_ptr\<mip：： FileProfile\>& profile，const std：： shared_ptr\<void\>& 上下文）  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess （const std：： vector\<std：： String\>& engineIds，const std：： shared_ptr\<void\>& 上下文）  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在列出引擎引发错误时调用。
public virtual void OnUnloadEngineSuccess （const std：： shared_ptr\<void\>& context）  |  在成功卸载引擎时调用。
public virtual void OnUnloadEngineFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在卸载引擎引发错误时调用。
public virtual void OnAddEngineSuccess （const std：： shared_ptr\<mip：： FileEngine\>& engine，const std：： shared_ptr\<void\>& 上下文）  |  在成功添加新引擎时调用。
public virtual void OnAddEngineFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在添加新引擎引发错误时调用。
public virtual void OnDeleteEngineSuccess （const std：： shared_ptr\<void\>& context）  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在删除引擎引发错误时调用。
public virtual void OnPolicyChanged(const std::string& engineId)  |  在针对具有给定 ID 的引擎的策略发生更改时调用。
public virtual void OnAddPolicyEngineStarting （bool requiresPolicyFetch）  |  在创建引擎之前调用，用于描述是否必须从服务器获取策略引擎的策略数据，或者是否可从本地缓存的数据创建策略引擎。
受保护的 Observer()  | _尚无记录。_
  
## <a name="members"></a>成员
  
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
