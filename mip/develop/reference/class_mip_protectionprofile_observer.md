---
title: class mip::ProtectionProfile::Observer
description: 记录 mip::protectionprofile 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d6d376e5b6e1ba65394e575b2e257a3b15c19f14
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251036"
---
# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共虚拟 void OnLoadSuccess (const std::\<ProtectionProfile\>（& a) 配置文件，const std:: shared_ptr\<void\>& 上下文)  |  在成功加载配置文件时调用。
公共虚拟 void OnLoadFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess(const std::vector\<std::string\>& engineIds, const std::shared_ptr\<void\>& context)  |  在成功生成引擎列表时调用。
公共虚拟 void OnListEnginesFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在列出引擎出错时调用。
公共虚拟 void OnAddEngineSuccess (const std::\<ProtectionEngine\>& 引擎，const std:: shared_ptr\<void\>& 上下文)  |  在成功添加新引擎时调用。
公共虚拟 void OnAddEngineFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在添加新引擎出错时调用。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  在成功删除引擎时调用。
公共虚拟 void OnDeleteEngineFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在删除引擎出错时调用。
  
## <a name="members"></a>成員
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 函数
在成功加载配置文件时调用。

参数：  
* **配置文件**:对新创建的引用[ProtectionProfile](class_mip_protectionprofile.md)


* **上下文**:传递给同一上下文[protectionprofile:: Loadasync](class_mip_protectionprofile.md#addengineasync-function)


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) 或 [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onloadfailure-function"></a>OnLoadFailure 函数
在加载配置文件引发错误时调用。

参数：  
* **错误**:[错误](class_mip_error.md)加载时发生 


* **上下文**:传递给同一上下文[protectionprofile:: Loadasync](class_mip_protectionprofile.md#addengineasync-function)


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) 或 [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 函数
在成功生成引擎列表时调用。

参数：  
* **engineIds**：可用的引擎 ID 列表。 


* **上下文**:传递给同一上下文[ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 函数
在列出引擎出错时调用。

参数：  
* **error**：导致列出引擎操作失败的错误。 


* **上下文**:传递给同一上下文[ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 函数
在成功添加新引擎时调用。

参数：  
* **引擎**:新创建的引擎 


* **上下文**:传递给同一上下文[ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 函数
在添加新引擎出错时调用。

参数：  
* **error**：导致添加引擎操作失败的错误。 


* **上下文**:传递给同一上下文[ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 函数
在成功删除引擎时调用。

参数：  
* **上下文**:传递给同一上下文[ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync-function)


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 函数
在删除引擎出错时调用。

参数：  
* **error**：导致删除引擎操作失败的错误。 


* **上下文**:传递给同一上下文[ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync-function)

