---
title: class mip ProtectionProfile
description: class mip ProtectionProfile 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7dffb4a6b1490ef185eb9a5062f394f4509f00a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446679"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) 是用于执行保护操作的根类。
在执行任何保护操作之前，应用程序都需先创建 [ProtectionProfile](class_mip_protectionprofile.md)
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  启动列出引擎操作。
public std::vector<std::string> ListEngines()  |  列出引擎。
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr<void>& context)  |  开始向配置文件添加新保护引擎。
public std::shared_ptr<ProtectionEngine> AddEngine(const ProtectionEngine::Settings& settings)  |  向配置文件添加新保护引擎。
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr<void>& context)  |  开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
 public void DeleteEngine(const std::string& engineId)  |  删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。

  
**返回结果**：由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)
  
### <a name="listenginesasync"></a>ListEnginesAsync
启动列出引擎操作。

参数：  
* **context**：将以不透明形式传递回观察程序的客户端上下文


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="listengines"></a>ListEngines
列出引擎。

  
**返回结果**：缓存引擎 ID
  
### <a name="addengineasync"></a>AddEngineAsync
开始向配置文件添加新保护引擎。

参数：  
* **settings**：指定引擎设置的 [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 对象。 


* **context**：将以不透明形式传递回观察程序的客户端上下文


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="protectionengine"></a>ProtectionEngine
向配置文件添加新保护引擎。

参数：  
* **settings**：指定引擎设置的 [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 对象。



  
**返回结果**：最新创建的 [ProtectionEngine](class_mip_protectionengine.md)
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **ID**：唯一引擎 ID。 


* **context**：将以不透明形式传递回观察程序的客户端上下文


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="deleteengine"></a>DeleteEngine
删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **ID**：唯一引擎 ID。

