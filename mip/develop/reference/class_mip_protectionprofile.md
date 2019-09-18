---
title: class mip::ProtectionProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: dcd50c403f20486e479fc00016ed6c0ef8885efa
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070496"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) 是用于执行保护操作的根类。
在执行任何保护操作之前，应用程序都需先创建 [ProtectionProfile](class_mip_protectionprofile.md)
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。
public void ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public std：： vector\<std：： string\> ListEngines （）  |  列出引擎。
public void AddEngineAsync （const ProtectionEngine：： settings & settings，const std：： shared_ptr\<void\>& context）  |  开始向配置文件添加新保护引擎。
public std：： shared_ptr\<ProtectionEngine\> AddEngine （const ProtectionEngine：： settings & 设置）  |  向配置文件添加新保护引擎。
public void DeleteEngineAsync （const std：： string & engineId，const std：： shared_ptr\<void\>& context）  |  开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
public void DeleteEngine(const std::string& engineId)  |  删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
public static MIP_API void __CDECL MIP：:P rotectionProfile：： LoadAsync | ProtectionProfile 在初始化期间及其整个生存期内使用的设置
public static MIP_API std：： shared_ptr&lt;ProtectionProfile&gt; __CDECL MIP：:P rotectionprofile：： Load | 基于提供的设置加载配置文件。
public static const MIP_API char * __CDECL MIP：:P rotectionProfile：： GetVersion | 获取库版本。
public static MIP_API std：： shared_ptr&lt;PublishingLicenseInfo&gt; __CDECL MIP：:P rotectionprofile：： GetPublishingLicenseInfo | 创建一个持有者，以获取发布许可证的详细信息，并可用于创建保护处理程序。 


## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。

  
**返回**：由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

参数：  
* **上下文**：将以不透明形式传递回观察器的客户端上下文


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="listengines-function"></a>ListEngines 函数
列出引擎。

  
**返回**：缓存引擎 Id
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新保护引擎。

参数：  
* **settings**：指定引擎设置的 [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 对象。 


* **上下文**：将以不透明形式传递回观察器的客户端上下文


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="addengine-function"></a>AddEngine 函数
向配置文件添加新保护引擎。

参数：  
* **settings**：指定引擎设置的 [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 对象。



  
**返回**：新创建的[ProtectionEngine](class_mip_protectionengine.md)
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **ID**：唯一引擎 ID。 


* **上下文**：将以不透明形式传递回观察器的客户端上下文


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="deleteengine-function"></a>DeleteEngine 函数
删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **ID**：唯一引擎 ID。

### <a name="loadasync-function"></a>LoadAsync 函数
ProtectionProfile 在初始化期间及其整个生存期内使用的设置 

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。

参数：
* **设置**：ProtectionProfile 在初始化期间及其整个生存期内使用的设置。
* **上下文**：此相同的上下文将被转发到 ProtectionProfile：： Observer：： OnLoadSuccess 或 ProtectionProfile：： Observer：： OnLoadFailure。

### <a name="load-function"></a>Load 函数
基于提供的设置加载配置文件。

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。

参数：
* **设置**：ProtectionProfile 在初始化期间及其整个生存期内使用的设置。

**返回**：新创建的配置文件。

### <a name="getversion-function"></a>GetVersion 函数
获取库版本。 

**返回**：库版本。

### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo 函数
创建一个持有者，以获取发布许可证的详细信息，并可用于创建保护处理程序。 

参数：
* **serializedPublishingLicense**：序列化发布许可证。

**返回**：用于发布许可证详细信息的持有人 
