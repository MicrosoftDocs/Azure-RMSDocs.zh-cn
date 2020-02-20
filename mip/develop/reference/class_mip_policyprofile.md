---
title: class mip::PolicyProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p olicyprofile 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 515f780c269025175e99caed72e8da381ef88104
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489769"
---
# <a name="class-mippolicyprofile"></a>class mip::PolicyProfile 
PolicyProfile 类是用于使用 Microsoft 信息保护操作的根类。 典型的应用程序只需要一个 PolicyProfile，但可以根据需要创建多个配置文件。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取配置文件上设置的设置。
public std：： shared_ptr\<AsyncControl\> ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public std：： vector\<std：： string\> ListEngines （）  |  引擎列表。
public std：： shared_ptr\<AsyncControl\> UnloadEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始卸载具有给定 ID 的策略引擎。
public void UnloadEngine （const std：： string & id）  |  开始卸载具有给定 ID 的策略引擎。
public std：： shared_ptr\<AsyncControl\> AddEngineAsync （const PolicyEngine：： Settings & settings，const std：： shared_ptr\<void\>& 上下文）  |  开始向配置文件添加新策略引擎。
public std：： shared_ptr\<PolicyEngine\> AddEngine （const PolicyEngine：： Settings & settings，const std：： shared_ptr\<void\>& 上下文）  |  向配置文件添加新的策略引擎。
public std：： shared_ptr\<AsyncControl\> DeleteEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始删除具有给定 ID 的策略引擎。 给定配置文件的所有数据都将删除。
public void DeleteEngine(const std::string& engineId)  |  删除具有给定 ID 的策略引擎。 给定引擎的所有数据都将被删除。
  
## <a name="members"></a>Members
  
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
* ID：唯一引擎 ID。 


* context：将不透明转发给观察程序函数的参数。 


PolicyProfile：：在成功或失败时将调用观察程序。
  
### <a name="unloadengine-function"></a>UnloadEngine 函数
开始卸载具有给定 ID 的策略引擎。

参数：  
* ID：唯一引擎 ID。


  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新策略引擎。

参数：  
* **设置**： mip：:P olicyengine：： settings 对象，指定引擎的设置。 


* **context**：将以不透明方式转发给观察者函数和可选 HttpDelegate 的参数。 


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
* ID：唯一引擎 ID。 


* **context**：将传递给观察程序函数的参数。 


PolicyProfile：：在成功或失败时将调用观察程序。
  
### <a name="deleteengine-function"></a>DeleteEngine 函数
删除具有给定 ID 的策略引擎。 给定引擎的所有数据都将被删除。

参数：  
* ID：唯一引擎 ID。

