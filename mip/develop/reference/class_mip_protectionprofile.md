---
title: class mip::ProtectionProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a6c78e7311f3af3920df19d7a3a6ca92bb09e819
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560057"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
ProtectionProfile 是用于执行保护操作的根类。
在执行任何保护操作之前，应用程序需要创建 ProtectionProfile
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取 ProtectionProfile 在其初始化期间及其整个生存期内使用的设置。
public void ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public std：： vector\<std：： string\> ListEngines （）  |  列出引擎。
public void AddEngineAsync （const ProtectionEngine：： Settings & settings，const std：： shared_ptr\<void\>& 上下文）  |  开始向配置文件添加新保护引擎。
public std：： shared_ptr\<ProtectionEngine\> AddEngine （const ProtectionEngine：： Settings & settings）  |  向配置文件添加新保护引擎。
public void DeleteEngineAsync （const std：： string & engineId，const std：： shared_ptr\<void\>& 上下文）  |  开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
public void DeleteEngine(const std::string& engineId)  |  删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
public static MIP_API void __CDECL MIP：:P rotectionProfile：： LoadAsync | ProtectionProfile 在初始化期间及其整个生存期内使用的设置
public static MIP_API std：： shared_ptr&lt;ProtectionProfile&gt; __CDECL MIP：:P rotectionProfile：： Load | 基于提供的设置加载配置文件。
public static const MIP_API char * __CDECL MIP：:P rotectionProfile：： GetVersion | 获取库版本。
public static MIP_API std：： shared_ptr&lt;PublishingLicenseInfo&gt; __CDECL MIP：:P rotectionProfile：： GetPublishingLicenseInfo | 创建一个持有者，以获取发布许可证的详细信息，并可用于创建保护处理程序。 

## <a name="members"></a>成員
  
### <a name="getsettings-function"></a>GetSettings 函数
获取 ProtectionProfile 在其初始化期间及其整个生存期内使用的设置。

  
**返回**： ProtectionProfile 在其初始化期间及其整个生存期内使用的设置
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

参数：  
* **context**：将以不透明形式传递回观察程序的客户端上下文


ProtectionProfile：：在成功或失败时将调用观察程序。
  
### <a name="listengines-function"></a>ListEngines 函数
列出引擎。

  
**返回结果**：缓存引擎 ID
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新保护引擎。

参数：  
* **设置**： mip：:P rotectionengine：： settings 对象，指定引擎的设置。 


* **context**：将以不透明形式传递回观察程序的客户端上下文


ProtectionProfile：：在成功或失败时将调用观察程序。
  
### <a name="addengine-function"></a>AddEngine 函数
向配置文件添加新保护引擎。

参数：  
* **设置**： mip：:P rotectionengine：： settings 对象，指定引擎的设置。



  
**返回**：新创建的 ProtectionEngine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **ID**：唯一引擎 ID。 


* **context**：将以不透明形式传递回观察程序的客户端上下文


ProtectionProfile：：在成功或失败时将调用观察程序。
  
### <a name="deleteengine-function"></a>DeleteEngine 函数
删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* **ID**：唯一引擎 ID。

### <a name="loadasync-function"></a>LoadAsync 函数
ProtectionProfile 在初始化期间及其整个生存期内使用的设置 

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。

参数：
* **设置**： ProtectionProfile 在其初始化期间及其整个生存期内使用的设置。
* **上下文**：此相同的上下文将转发到 ProtectionProfile：： observer：： OnLoadSuccess 或 ProtectionProfile：： observer：： OnLoadFailure。

### <a name="load-function"></a>Load 函数
基于提供的设置加载配置文件。

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。

参数：
* **设置**： ProtectionProfile 在其初始化期间及其整个生存期内使用的设置。

**返回**：新创建的配置文件。

### <a name="getversion-function"></a>GetVersion 函数
获取库版本。 

**返回**：库版本。

### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo 函数
创建一个持有者，以获取发布许可证的详细信息，并可用于创建保护处理程序。 

参数：
* **serializedPublishingLicense**：序列化发布许可证。

**返回**：持有者提供发布许可证的详细信息 