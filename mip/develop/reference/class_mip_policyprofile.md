---
title: class mip::PolicyProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p olicyprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 5abcca760f89b492f26ed5fa7b46e280e1bfc8ab
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070536"
---
# <a name="class-mippolicyprofile"></a>class mip::PolicyProfile 
[PolicyProfile](class_mip_policyprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。 一个典型的应用程序只需要一个 [PolicyProfile](class_mip_policyprofile.md)，但它可以按需创建多个配置文件。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取配置文件上设置的设置。
public void ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public void UnloadEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始卸载具有给定 ID 的策略引擎。
public void AddEngineAsync （const PolicyEngine：： settings & settings，const std：： shared_ptr\<void\>& context）  |  开始向配置文件添加新策略引擎。
public void DeleteEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始删除具有给定 ID 的策略引擎。 给定配置文件的所有数据都将删除。
public static MIP_API void __CDECL MIP：:P olicyProfile：： LoadAsync | 基于提供的设置开始加载配置文件。
public static const MIP_API char * __CDECL MIP：:P olicyProfile：： GetVersion | 获取库版本


## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
获取配置文件上设置的设置。

  
**返回**：配置文件上设置的设置。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

参数：  
* **context**：将传递给观察程序函数的参数。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) 将在成功或失败时调用。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 函数
开始卸载具有给定 ID 的策略引擎。

参数：  
* **ID**：唯一引擎 ID。 


* context：将不透明转发给观察程序函数的参数。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) 将在成功或失败时调用。
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新策略引擎。

参数：  
* settings：指定引擎设置的 [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) 对象。 


* context：将不透明转发给观察程序函数的参数。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) 将在成功或失败时调用。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除具有给定 ID 的策略引擎。 给定配置文件的所有数据都将删除。

参数：  
* **ID**：唯一引擎 ID。 


* **context**：将传递给观察程序函数的参数。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) 将在成功或失败时调用。

### <a name="loadasync-function"></a>LoadAsync 函数
基于提供的设置开始加载配置文件。

参数：  
* **设置**：用于加载配置文件对象的配置文件设置。 </para>
* **context**：将传递到观察者函数的上下文参数。

### <a name="getversion-function"></a>GetVersion 函数
获取库版本

**返回**：版本字符串。

