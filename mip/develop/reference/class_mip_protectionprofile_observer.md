---
title: 类 ProtectionProfile：：观察程序
description: 记录 Microsoft 信息保护（MIP） SDK 的 protectionprofile：：观察者类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 8448f75a06bfe99debcf4c1c40ab2228c46690e6
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763921"
---
# <a name="class-protectionprofileobserver"></a>类 ProtectionProfile：：观察程序 
接收与 ProtectionProfile 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess （const std：： shared_ptr\<ProtectionProfile\>& profile，const std：： shared_ptr\<void\>& 上下文）  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess （const std：： vector\<std：： String\>& engineIds，const std：： shared_ptr\<void\>& 上下文）  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在列出引擎出错时调用。
public virtual void OnAddEngineSuccess （const std：： shared_ptr\<ProtectionEngine\>& engine，const std：： shared_ptr\<void\>& 上下文）  |  在成功添加新引擎时调用。
public virtual void OnAddEngineFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在添加新引擎出错时调用。
public virtual void OnDeleteEngineSuccess （const std：： shared_ptr\<void\>& context）  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在删除引擎出错时调用。
  
## <a name="members"></a>成员
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 函数
在成功加载配置文件时调用。

参数：  
* **profile**：对新创建的 ProtectionProfile 的引用


* **上下文**：传递到 ProtectionProfile：： LoadAsync 的上下文相同。


应用程序可将任何类型的上下文（例如，std：:p romise，std：： function）传递给 ProtectionProfile：： LoadAsync，并且同一上下文将按原样转发到 ProtectionProfile：： Observer：： OnLoadSuccess 或 ProtectionProfile：： Observer：： OnLoadFailure。
  
### <a name="onloadfailure-function"></a>OnLoadFailure 函数
在加载配置文件引发错误时调用。

参数：  
* **错误**：加载时出现错误 


* **context**：传递到 ProtectionProfile::LoadAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionProfile::LoadAsync，而此相同上下文将按原样转发给 ProtectionProfile::Observer::OnLoadSuccess 或 ProtectionProfile::Observer::OnLoadFailure
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 函数
在成功生成引擎列表时调用。

参数：  
* **engineIds**：可用的引擎 id 列表。 


* **context**：传递到 [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md) 的相同上下文


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 函数
在列出引擎出错时调用。

参数：  
* **error**：导致列出引擎操作失败的错误。 


* **context**：传递到 ProtectionProfile::ListEnginesAsync 的相同上下文


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 函数
在成功添加新引擎时调用。

参数：  
* **engine**：新创建的引擎 


* **context**：传递到 [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md) 的相同上下文


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 函数
在添加新引擎出错时调用。

参数：  
* error****：导致添加引擎操作失败的错误。 


* **context**：传递到 ProtectionProfile::AddEngineAsync 的相同上下文


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 函数
在成功删除引擎时调用。

参数：  
* **context**：传递到 [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md) 的相同上下文


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 函数
在删除引擎出错时调用。

参数：  
* error****：导致删除引擎操作失败的错误。 


* **context**：传递到 ProtectionProfile::DeleteEngineAsync 的相同上下文

