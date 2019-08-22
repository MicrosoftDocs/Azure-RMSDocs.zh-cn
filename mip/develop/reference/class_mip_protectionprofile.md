---
title: class mip::ProtectionProfile
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionprofile 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: cc69e167a5b5a8dc46157443c13d70732ace62c0
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883330"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) 是用于执行保护操作的根类。
在执行任何保护操作之前，应用程序都需先创建 [ProtectionProfile](class_mip_protectionprofile.md)
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。
public void ListEnginesAsync (const std:: shared_ptr\<void\>& 上下文)  |  启动列出引擎操作。
public std:: vector\<std:: string\> ListEngines ()  |  列出引擎。
public void AddEngineAsync (const ProtectionEngine:: settings & settings, const std:: shared_ptr\<void\>& context)  |  开始向配置文件添加新保护引擎。
public std:: shared_ptr\<ProtectionEngine\> AddEngine (const ProtectionEngine:: settings & 设置)  |  向配置文件添加新保护引擎。
public void DeleteEngineAsync (const std:: string & engineId, const std:: shared_ptr\<void\>& context)  |  开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
public void DeleteEngine(const std::string& engineId)  |  删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
  
## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。

  
**返回**:由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

参数：  
* **上下文**:将以不透明形式传递回观察器的客户端上下文


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="listengines-function"></a>ListEngines 函数
列出引擎。

  
**返回**:缓存引擎 Id
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新保护引擎。

参数：  
* **settings**：指定引擎设置的 [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 对象。 


* **上下文**:将以不透明形式传递回观察器的客户端上下文


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="addengine-function"></a>AddEngine 函数
向配置文件添加新保护引擎。

参数：  
* **settings**：指定引擎设置的 [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 对象。



  
**返回**:新创建的[ProtectionEngine](class_mip_protectionengine.md)
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **ID**：唯一引擎 ID。 


* **上下文**:将以不透明形式传递回观察器的客户端上下文


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="deleteengine-function"></a>DeleteEngine 函数
删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **ID**：唯一引擎 ID。

