---
title: class mip FileProfile Observer
description: class mip FileProfile Observer 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 105380ef63f6533839190e4c9e3f3ee5379781f1
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446390"
---
# <a name="class-mipfileprofileobserver"></a>class mip::FileProfile::Observer 
[Observer](class_mip_fileprofile_observer.md) 接口，供客户端获取配置文件相关事件的通知。
所有错误都继承自 [mip::Error](class_mip_error.md)。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public virtual ~Observer()  | _尚无记录。_
public virtual void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context)  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在列出引擎引发错误时调用。
public virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  在成功卸载引擎时调用。
public virtual void OnUnloadEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在卸载引擎引发错误时调用。
public virtual void OnAddEngineSuccess(const std::shared_ptr<mip::FileEngine>& engine, const std::shared_ptr<void>& context)  |  在成功添加新引擎时调用。
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在添加新引擎引发错误时调用。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在删除引擎引发错误时调用。
 public virtual void OnPolicyChanged(const std::string& engineId)  |  在针对具有给定 ID 的引擎的策略发生更改时调用。
 受保护的 Observer()  | _尚无记录。_
  
## <a name="members"></a>成員
  
### <a name="observer"></a>~Observer
_尚无记录。_

  
### <a name="onloadsuccess"></a>OnLoadSuccess
在成功加载配置文件时调用。
  
### <a name="onloadfailure"></a>OnLoadFailure
在加载配置文件引发错误时调用。
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
在成功生成引擎列表时调用。
  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
在列出引擎引发错误时调用。
  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
在成功卸载引擎时调用。
  
### <a name="onunloadenginefailure"></a>OnUnloadEngineFailure
在卸载引擎引发错误时调用。
  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
在成功添加新引擎时调用。
  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
在添加新引擎引发错误时调用。
  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
在成功删除引擎时调用。
  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
在删除引擎引发错误时调用。
  
### <a name="onpolicychanged"></a>OnPolicyChanged
在针对具有给定 ID 的引擎的策略发生更改时调用。
  
### <a name="observer"></a>观察者
_尚无记录。_