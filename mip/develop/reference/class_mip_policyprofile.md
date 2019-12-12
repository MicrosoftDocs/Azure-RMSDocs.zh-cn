---
title: class mip::PolicyProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p olicyprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8feb0b93982a00c4843ea914f969ef27cf8e5ca2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560914"
---
# <a name="class-mippolicyprofile"></a>class mip::PolicyProfile 
PolicyProfile 类是用于使用 Microsoft 信息保护操作的根类。 典型的应用程序只需要一个 PolicyProfile，但可以根据需要创建多个配置文件。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取配置文件上设置的设置。
public void ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public std：： vector\<std：： string\> ListEngines （）  |  引擎列表。
public void UnloadEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始卸载具有给定 ID 的策略引擎。
public void UnloadEngine （const std：： string & id）  |  开始卸载具有给定 ID 的策略引擎。
public void AddEngineAsync （const PolicyEngine：： Settings & settings，const std：： shared_ptr\<void\>& 上下文）  |  开始向配置文件添加新策略引擎。
public std：： shared_ptr\<PolicyEngine\> AddEngine （const PolicyEngine：： Settings & settings，const std：： shared_ptr\<void\>& 上下文）  |  向配置文件添加新的策略引擎。
public void DeleteEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始删除具有给定 ID 的策略引擎。 给定配置文件的所有数据都将删除。
public void DeleteEngine(const std::string& engineId)  |  删除具有给定 ID 的策略引擎。 给定引擎的所有数据都将被删除。
public static MIP_API void __CDECL MIP：:P olicyProfile：： LoadAsync | 基于提供的设置开始加载配置文件。
public static const MIP_API char * __CDECL MIP：:P olicyProfile：： GetVersion | 获取库版本

## <a name="members"></a>成員
  
### <a name="getsettings-function"></a>GetSettings 函数
获取配置文件上设置的设置。

  
**返回结果**：配置文件上设置的设置。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

参数：  
* **context**：将传递给观察程序函数的参数。 


PolicyProfile：：在成功或失败时将调用观察程序。
  
### <a name="listengines-function"></a>ListEngines 函数
引擎列表。

  
**返回结果**：缓存引擎 ID
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 函数
开始卸载具有给定 ID 的策略引擎。

参数：  
* **ID**：唯一引擎 ID。 


* context：将不透明转发给观察程序函数的参数。 


PolicyProfile：：在成功或失败时将调用观察程序。
  
### <a name="unloadengine-function"></a>UnloadEngine 函数
开始卸载具有给定 ID 的策略引擎。

参数：  
* **ID**：唯一引擎 ID。


  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新策略引擎。

参数：  
* **设置**： mip：:P olicyengine：： settings 对象，指定引擎的设置。 


* **context**：将以不透明方式 fowarded 到观察者函数和可选 HttpDelegate 的参数。 


PolicyProfile：：在成功或失败时将调用观察程序。
  
### <a name="addengine-function"></a>AddEngine 函数
向配置文件添加新的策略引擎。

参数：  
* **设置**： mip：:P olicyengine：： settings 对象，指定引擎的设置。 


* **context**：将以不透明的 HttpDelegate 转发到可选的参数



  
**返回**：新创建的 PolicyEngine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除具有给定 ID 的策略引擎。 给定配置文件的所有数据都将删除。

参数：  
* **ID**：唯一引擎 ID。 


* **context**：将传递给观察程序函数的参数。 


PolicyProfile：：在成功或失败时将调用观察程序。
  
### <a name="deleteengine-function"></a>DeleteEngine 函数
删除具有给定 ID 的策略引擎。 给定引擎的所有数据都将被删除。

参数：  
* **ID**：唯一引擎 ID。

### <a name="loadasync-function"></a>LoadAsync 函数
基于提供的设置开始加载配置文件。

参数：  
* **设置**：用于加载配置文件对象的配置文件设置。 </para>
* **context**：将传递到观察者函数的上下文参数。

### <a name="getversion-function"></a>GetVersion 函数
获取库版本

**返回**：版本字符串。