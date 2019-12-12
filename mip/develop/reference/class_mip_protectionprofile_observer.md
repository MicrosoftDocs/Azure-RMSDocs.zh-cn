---
title: class mip::ProtectionProfile::Observer
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a9138e497655dfa939a9ac9b15d7ed228331e9e0
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560703"
---
# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
接收与 ProtectionProfile 相关的通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess （const std：： shared_ptr\<ProtectionProfile\>& profile，const std：： shared_ptr\<void\>& 上下文）  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess （const std：： vector\<std：： string\>& engineIds，const std：： shared_ptr\<void\>& 上下文）  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在列出引擎出错时调用。
public virtual void OnAddEngineSuccess （const std：： shared_ptr\<ProtectionEngine\>& 引擎，const std：： shared_ptr\<void\>& 上下文）  |  在成功添加新引擎时调用。
public virtual void OnAddEngineFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在添加新引擎出错时调用。
public virtual void OnDeleteEngineSuccess （const std：： shared_ptr\<void\>& 上下文）  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在删除引擎出错时调用。
  
## <a name="members"></a>成員
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 函数
在成功加载配置文件时调用。

参数：  
* **配置文件**：对新创建的 ProtectionProfile 的引用


* **context**：传递到 ProtectionProfile::LoadAsync 的相同上下文


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionProfile：： LoadAsync，并且相同的上下文将按原样转发到 ProtectionProfile：： Observer：： OnLoadSuccess 或 ProtectionProfile：： Observer：： OnLoadFailure
  
### <a name="onloadfailure-function"></a>OnLoadFailure 函数
在加载配置文件引发错误时调用。

参数：  
* **错误**：加载时出现错误 


* **context**：传递到 ProtectionProfile::LoadAsync 的相同上下文


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionProfile：： LoadAsync，并且相同的上下文将按原样转发到 ProtectionProfile：： Observer：： OnLoadSuccess 或 ProtectionProfile：： Observer：： OnLoadFailure
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 函数
在成功生成引擎列表时调用。

参数：  
* **engineIds**：可用的引擎 ID 列表。 


* **上下文**：传递到 ProtectionProfile：： ListEnginesAsync 的上下文相同


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 函数
在列出引擎出错时调用。

参数：  
* **error**：导致列出引擎操作失败的错误。 


* **上下文**：传递到 ProtectionProfile：： ListEnginesAsync 的上下文相同


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 函数
在成功添加新引擎时调用。

参数：  
* **engine**：新创建的引擎 


* **上下文**：传递到 ProtectionProfile：： AddEngineAsync 的上下文相同


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 函数
在添加新引擎出错时调用。

参数：  
* **error**：导致添加引擎操作失败的错误。 


* **上下文**：传递到 ProtectionProfile：： AddEngineAsync 的上下文相同


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 函数
在成功删除引擎时调用。

参数：  
* **上下文**：传递到 ProtectionProfile 的上下文相同：:D eleteengineasync


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 函数
在删除引擎出错时调用。

参数：  
* **error**：导致删除引擎操作失败的错误。 


* **上下文**：传递到 ProtectionProfile 的上下文相同：:D eleteengineasync

