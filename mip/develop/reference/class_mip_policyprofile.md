---
title: 类 PolicyProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 policyprofile：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 9f70b8bfa1eee6e994b67c668b5144d6cb74ecad
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760909"
---
# <a name="class-policyprofile"></a>类 PolicyProfile 
PolicyProfile 类是用于使用 Microsoft 信息保护操作的根类。 一个典型的应用程序只需要一个 PolicyProfile，但它可以按需创建多个配置文件。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取配置文件上设置的设置。
public std：： shared_ptr\<AsyncControl\> ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public std：： vector\<std：： string\> ListEngines （）  |  引擎列表。
public std：： shared_ptr\<AsyncControl\> UnloadEngineAsync （const std：： string& id，const std：： shared_ptr\<void\>& 上下文）  |  开始卸载具有给定 ID 的策略引擎。
public void UnloadEngine （const std：： string& id）  |  开始卸载具有给定 ID 的策略引擎。
public std：： shared_ptr\<AsyncControl\> AddEngineAsync （Const PolicyEngine：： settings& settings，const std：： shared_ptr\<void\>& 上下文）  |  开始向配置文件添加新策略引擎。
public std：： shared_ptr\<PolicyEngine\> AddEngine （Const PolicyEngine：： settings& settings，const std：： shared_ptr\<void\>& 上下文）  |  向配置文件添加新的策略引擎。
public std：： shared_ptr\<AsyncControl\> DeleteEngineAsync （const std：： string& id，const std：： shared_ptr\<void\>& 上下文）  |  开始删除具有给定 ID 的策略引擎。 给定配置文件的所有数据都将删除。
public void DeleteEngine(const std::string& engineId)  |  删除具有给定 ID 的策略引擎。 给定引擎的所有数据都将被删除。
public void AcquireAuthToken （Cloud cloud，const std：： shared_ptr\<authDelegate\>& AuthDelegate） const  |  触发身份验证回叫。
  
## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
获取配置文件上设置的设置。

  
**返回结果**：配置文件上设置的设置。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

参数：  
* **context**：将传递给观察程序函数的参数。 


PolicyProfile::Observer 将在成功或失败时调用。
  
### <a name="listengines-function"></a>ListEngines 函数
引擎列表。

  
**返回结果**：缓存引擎 ID
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 函数
开始卸载具有给定 ID 的策略引擎。

参数：  
* **id**：唯一的引擎 id。 


* context****：将不透明转发给观察程序函数的参数。 


PolicyProfile::Observer 将在成功或失败时调用。
  
### <a name="unloadengine-function"></a>UnloadEngine 函数
开始卸载具有给定 ID 的策略引擎。

参数：  
* **id**：唯一的引擎 id。


  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新策略引擎。

参数：  
* settings****：指定引擎设置的 mip::PolicyEngine::Settings 对象。 


* **context**：将以不透明方式转发给观察者函数和可选 HttpDelegate 的参数。 


PolicyProfile::Observer 将在成功或失败时调用。
  
### <a name="addengine-function"></a>AddEngine 函数
向配置文件添加新的策略引擎。

参数：  
* settings****：指定引擎设置的 mip::PolicyEngine::Settings 对象。 


* **context**：将以不透明的 HttpDelegate 转发到可选的参数



  
**返回**：新创建的 PolicyEngine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除具有给定 ID 的策略引擎。 给定配置文件的所有数据都将删除。

参数：  
* **id**：唯一的引擎 id。 


* **context**：将传递给观察程序函数的参数。 


PolicyProfile::Observer 将在成功或失败时调用。
  
### <a name="deleteengine-function"></a>DeleteEngine 函数
删除具有给定 ID 的策略引擎。 给定引擎的所有数据都将被删除。

参数：  
* **id**：唯一的引擎 id。


  
### <a name="acquireauthtoken-function"></a>AcquireAuthToken 函数
触发身份验证回叫。

参数：  
* **云**： Azure 云 


* **authDelegate**：将调用的身份验证回调


MIP 将不会缓存或使用 auth 委托返回的值执行任何其他操作。 对于在 MIP 请求身份验证令牌之前未 "登录" 的应用程序，建议使用此函数。 它允许应用程序在 MIP 实际需要一个令牌之前提取令牌。