---
title: class mip::ProtectionProfile::Observer
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: e7e260f879fb1e48b19d43f13a451a3a91ee1a39
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057460"
---
# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess (const std:: shared_ptr\<ProtectionProfile\>& profile, const std:: shared_ptr\<void\>& context)  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess (const std:: vector\<std:: string\>& engineIds, const std:: shared_ptr\<void\>& context)  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在列出引擎出错时调用。
public virtual void OnAddEngineSuccess (const std:: shared_ptr\<ProtectionEngine\>& engine, const std:: shared_ptr\<void\>& context)  |  在成功添加新引擎时调用。
public virtual void OnAddEngineFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在添加新引擎出错时调用。
public virtual void OnDeleteEngineSuccess (const std:: shared_ptr\<void\>& 上下文)  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在删除引擎出错时调用。
  
## <a name="members"></a>成员
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 函数
在成功加载配置文件时调用。

参数：  
* **配置文件**:对新创建的[ProtectionProfile](class_mip_protectionprofile.md)的引用


* **上下文**:传递给[ProtectionProfile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)的上下文相同


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) 或 [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onloadfailure-function"></a>OnLoadFailure 函数
在加载配置文件引发错误时调用。

参数：  
* **错误**:加载时发生的[错误](class_mip_error.md) 


* **上下文**:传递给[ProtectionProfile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)的上下文相同


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) 或 [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 函数
在成功生成引擎列表时调用。

参数：  
* **engineIds**：可用的引擎 ID 列表。 


* **上下文**:传递给[ProtectionProfile:: ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)的上下文相同


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 函数
在列出引擎出错时调用。

参数：  
* **error**：导致列出引擎操作失败的错误。 


* **上下文**:传递给[ProtectionProfile:: ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)的上下文相同


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 函数
在成功添加新引擎时调用。

参数：  
* **引擎**:新创建的引擎 


* **上下文**:传递给[ProtectionProfile:: AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)的上下文相同


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 函数
在添加新引擎出错时调用。

参数：  
* **error**：导致添加引擎操作失败的错误。 


* **上下文**:传递给[ProtectionProfile:: AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)的上下文相同


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 函数
在成功删除引擎时调用。

参数：  
* **上下文**:传递给 ProtectionProfile 的同一上下文[::D eleteengineasync](class_mip_protectionprofile.md#deleteengineasync-function)


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 函数
在删除引擎出错时调用。

参数：  
* **error**：导致删除引擎操作失败的错误。 


* **上下文**:传递给 ProtectionProfile 的同一上下文[::D eleteengineasync](class_mip_protectionprofile.md#deleteengineasync-function)

