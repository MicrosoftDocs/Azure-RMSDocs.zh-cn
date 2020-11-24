---
title: 类 ProtectionProfile
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 protectionprofile：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a783a90b64d5829632e2104ff2706fd86a0d9e68
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565174"
---
# <a name="class-protectionprofile"></a>类 ProtectionProfile 
ProtectionProfile 是用于执行保护操作的根类。
在执行任何保护操作之前，应用程序都需先创建 ProtectionProfile
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取由 ProtectionProfile 在初始化期间及其整个生存期内使用的设置。
public std：： shared_ptr \<AsyncControl\> ListEnginesAsync (const std：： shared_ptr \<void\>& 上下文)   |  启动列出引擎操作。
public std：： vector \<std::string\> ListEngines ( # A1  |  列出引擎。
public std：： shared_ptr \<AsyncControl\> AddEngineAsync (Const ProtectionEngine：： settings& Settings，const std：： shared_ptr \<void\>& 上下文)   |  开始向配置文件添加新保护引擎。
public std::shared_ptr\<ProtectionEngine\> AddEngine(const ProtectionEngine::Settings& settings)  |  向配置文件添加新保护引擎。
public std：： shared_ptr \<AsyncControl\> DeleteEngineAsync (const std：： string& engineId，const std：： shared_ptr \<void\>& 上下文)   |  开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
public void DeleteEngine(const std::string& engineId)  |  删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
  
## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
获取由 ProtectionProfile 在初始化期间及其整个生存期内使用的设置。

  
**返回**： ProtectionProfile 在其初始化期间及其整个生存期内使用的设置
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

参数：  
* **context**：将以不透明形式传递回观察程序的客户端上下文



  
**返回**： Async control 对象。
ProtectionProfile::Observer 是在成功或失败时调用。
  
### <a name="listengines-function"></a>ListEngines 函数
列出引擎。

  
**返回结果**：缓存引擎 ID
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新保护引擎。

参数：  
* **settings**：指定引擎设置的 mip::ProtectionEngine::Settings 对象。 


* **context**：将以不透明形式传递回观察程序的客户端上下文



  
**返回**： Async control 对象。
ProtectionProfile::Observer 是在成功或失败时调用。
  
### <a name="addengine-function"></a>AddEngine 函数
向配置文件添加新保护引擎。

参数：  
* **settings**：指定引擎设置的 mip::ProtectionEngine::Settings 对象。



  
**返回结果**：最新创建的 ProtectionEngine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **id**：唯一的引擎 id。 


* **context**：将以不透明形式传递回观察程序的客户端上下文



  
**返回**： Async control 对象。
ProtectionProfile::Observer 是在成功或失败时调用。
  
### <a name="deleteengine-function"></a>DeleteEngine 函数
删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **id**：唯一的引擎 id。

