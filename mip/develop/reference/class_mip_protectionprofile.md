---
title: class mip::ProtectionProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionprofile 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 14d52de8ff87a75aaf2c777eb55c427bbde72a12
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486726"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
ProtectionProfile 是用于执行保护操作的根类。
在执行任何保护操作之前，应用程序需要创建 ProtectionProfile
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取 ProtectionProfile 在其初始化期间及其整个生存期内使用的设置。
public std：： shared_ptr\<AsyncControl\> ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public std：： vector\<std：： string\> ListEngines （）  |  列出引擎。
public std：： shared_ptr\<AsyncControl\> AddEngineAsync （const ProtectionEngine：： Settings & settings，const std：： shared_ptr\<void\>& 上下文）  |  开始向配置文件添加新保护引擎。
public std：： shared_ptr\<ProtectionEngine\> AddEngine （const ProtectionEngine：： Settings & settings）  |  向配置文件添加新保护引擎。
public std：： shared_ptr\<AsyncControl\> DeleteEngineAsync （const std：： string & engineId，const std：： shared_ptr\<void\>& 上下文）  |  开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
public void DeleteEngine(const std::string& engineId)  |  删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings 函数
获取 ProtectionProfile 在其初始化期间及其整个生存期内使用的设置。

  
**返回**： ProtectionProfile 在其初始化期间及其整个生存期内使用的设置
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

参数：  
* **context**：将以不透明形式传递回观察程序的客户端上下文



  
**返回**： Async control 对象。
ProtectionProfile：：在成功或失败时将调用观察程序。
  
### <a name="listengines-function"></a>ListEngines 函数
列出引擎。

  
**返回结果**：缓存引擎 ID
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新保护引擎。

参数：  
* **设置**： mip：:P rotectionengine：： settings 对象，指定引擎的设置。 


* **context**：将以不透明形式传递回观察程序的客户端上下文



  
**返回**： Async control 对象。
ProtectionProfile：：在成功或失败时将调用观察程序。
  
### <a name="addengine-function"></a>AddEngine 函数
向配置文件添加新保护引擎。

参数：  
* **设置**： mip：:P rotectionengine：： settings 对象，指定引擎的设置。



  
**返回**：新创建的 ProtectionEngine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* ID：唯一引擎 ID。 


* **context**：将以不透明形式传递回观察程序的客户端上下文



  
**返回**： Async control 对象。
ProtectionProfile：：在成功或失败时将调用观察程序。
  
### <a name="deleteengine-function"></a>DeleteEngine 函数
删除给定 ID 的保护引擎。 给定引擎的所有数据都将被删除。

参数：  
* ID：唯一引擎 ID。

