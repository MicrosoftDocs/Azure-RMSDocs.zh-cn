---
title: 类 ProtectionProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 protectionprofile：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: d3a2f02a0dab5bba9b74b264348bcfd7e073f783
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764409"
---
# <a name="class-protectionprofile"></a>类 ProtectionProfile 
ProtectionProfile 是用于执行保护操作的根类。
在执行任何保护操作之前，应用程序都需先创建 ProtectionProfile
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取由 ProtectionProfile 在初始化期间及其整个生存期内使用的设置。
public std：： shared_ptr\<AsyncControl\> ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public std：： vector\<std：： string\> ListEngines （）  |  列出引擎。
public std：： shared_ptr\<AsyncControl\> AddEngineAsync （Const ProtectionEngine：： settings& settings，const std：： shared_ptr\<void\>& 上下文）  |  开始向配置文件添加新保护引擎。
public std：： shared_ptr\<ProtectionEngine\> AddEngine （Const ProtectionEngine：： settings& settings）  |  向配置文件添加新保护引擎。
public std：： shared_ptr\<AsyncControl\> DeleteEngineAsync （const std：： string& engineId，const std：： shared_ptr\<void\>& 上下文）  |  开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
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
[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
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

