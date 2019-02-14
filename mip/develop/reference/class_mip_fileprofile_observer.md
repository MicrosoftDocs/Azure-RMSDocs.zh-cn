---
title: class mip::FileProfile::Observer
description: 记录 mip::fileprofile 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: e1eb3a91b4acb1687563fb10d26e9f7c6b873e94
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254724"
---
# <a name="class-mipfileprofileobserver"></a>class mip::FileProfile::Observer 
[Observer](class_mip_fileprofile_observer.md) 接口，供客户端获取配置文件相关事件的通知。
所有错误都继承自 [mip::Error](class_mip_error.md)。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public virtual ~Observer()  | _尚无记录。_
公共虚拟 void OnLoadSuccess (const std::\<mip::FileProfile\>（& a) 配置文件，const std:: shared_ptr\<void\>& 上下文)  |  在成功加载配置文件时调用。
公共虚拟 void OnLoadFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess(const std::vector\<std::string\>& engineIds, const std::shared_ptr\<void\>& context)  |  在成功生成引擎列表时调用。
公共虚拟 void OnListEnginesFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在列出引擎引发错误时调用。
public virtual void OnUnloadEngineSuccess(const std::shared_ptr\<void\>& context)  |  在成功卸载引擎时调用。
公共虚拟 void OnUnloadEngineFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在卸载引擎引发错误时调用。
public virtual void OnAddEngineSuccess(const std::shared_ptr\<mip::FileEngine\>& engine, const std::shared_ptr\<void\>& context)  |  在成功添加新引擎时调用。
公共虚拟 void OnAddEngineFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在添加新引擎引发错误时调用。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  在成功删除引擎时调用。
公共虚拟 void OnDeleteEngineFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在删除引擎引发错误时调用。
public virtual void OnPolicyChanged(const std::string& engineId)  |  在针对具有给定 ID 的引擎的策略发生更改时调用。
公共虚拟 void OnAddPolicyEngineStarting (bool requiresPolicyFetch)  |  在引擎创建，用于描述必须从服务器获取策略引擎的策略数据或者它是否可以创建从本地缓存的数据之前调用。
受保护的 Observer()  | _尚无记录。_
  
## <a name="members"></a>成員
  
### <a name="observer-function"></a>~ 观察者函数
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
在引擎创建，用于描述必须从服务器获取策略引擎的策略数据或者它是否可以创建从本地缓存的数据之前调用。

参数：  
* **requiresPolicyFetch**:描述是否必须通过 HTTP 提取引擎数据，或如果它将从加载缓存


此可选的回调可能会由应用程序，用于会收到通知 AddEngineAsync 操作将需要有一个 HTTP 操作 （使用其相关联的延迟） 才能完成。
  
### <a name="observer-function"></a>观察者函数
_尚无记录。_
