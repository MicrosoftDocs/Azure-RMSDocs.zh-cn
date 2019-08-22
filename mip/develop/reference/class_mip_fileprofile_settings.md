---
title: class mip::FileProfile::Settings
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: fileprofile 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: f6d28ae7803834138b1e8c61270bcad3fcc1eb11
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884182"
---
# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
[FileProfile](class_mip_fileprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_fileprofile_settings.md)。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 (const std:: string & path, CacheStorageType CacheStorageType, std:: shared_ptr\<AuthDelegate\> AuthDelegate, std:: shared_ptr\<ConsentDelegate\> ConsentDelegate, std::shared_ptr\<观察\>程序观察程序, const ApplicationInfo & ApplicationInfo)  |  [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。
public Settings (const std:: shared_ptr\<MipContext\>& MipContext, CacheStorageType CacheStorageType, std:: shared_ptr\<AuthDelegate\> AuthDelegate, std:: shared_ptr\<ConsentDelegate\> ConsentDelegate, std:: shared_ptr\<观察\>程序观察程序)  |  [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。
public const std::string& GetPath() const  |  获取存储日志记录、遥测和其他永久性状态的路径。
public CacheStorageType GetCacheStorageType () const  |  获取缓存是存储在内存中还是存储在磁盘上。
public std:: shared_ptr\<AuthDelegate\> GetAuthDelegate () const  |  获取用于获取身份验证令牌的身份验证委托。
public std:: shared_ptr\<ConsentDelegate\> GetConsentDelegate () const  |  获取用于请求用户许可连接到服务的许可委托。
public std:: shared_ptr\<\> GetObserver () const  |  获取接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的观察程序。
public const ApplicationInfo& GetApplicationInfo() const  |  获取使用 SDK 的应用程序的相关信息。
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  获取表示所有配置文件的共享状态的 MIP 上下文。
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate () const  |  获取应用程序提供的记录器委托（若有）。
public void SetLoggerDelegate (const std:: shared_ptr\<LoggerDelegate\>& LoggerDelegate)  |  替代默认记录器。
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& HttpDelegate)  |  使用客户端自己的替代默认 HTTP 堆栈。
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  获取应用程序提供的 TaskDispatcher 委托 (如果有)。
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& TaskDispatcherDelegate)  |  用客户端自己的 asynchonous 重写默认的任务分派处理。
public void OptOutTelemetry()  |  选择退出所有遥测收集。
public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集的指示。
public void SetSessionId(const std::string& sessionId)  |  设置会话 ID。
public const std::string& GetSessionId() const  |  获取会话 ID。
public void SetMinimumLogLevel(LogLevel logLevel)  |  设置将触发日志记录事件的最低日志级别。
public LogLevel GetMinimumLogLevel() const  |  获取将触发日志记录事件的最低日志级别。
public void SetCanCacheLicenses (bool canCacheLicenses)  |  配置是否将以本地方式缓存最终用户许可证 (Eul)。
public bool CanCacheLicenses () const  |  获取是否在本地缓存最终用户许可证 (Eul)。
  
## <a name="members"></a>成员
  
### <a name="settings-function"></a>Settings 函数
[FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。

参数：  
* **路径**:用于存储日志记录、遥测和其他持久状态的文件路径 


* **cacheStorageType**:将任何缓存的状态存储在内存中或磁盘上 


* **authDelegate**:用于获取身份验证令牌的身份验证委托 


* **consentDelegate**:用于获取访问外部资源的用户权限的委托 


* **观察**程序:将接收与[FileProfile](class_mip_fileprofile.md)相关的事件通知的[观察](class_mip_fileprofile_observer.md)程序实例


* **applicationInfo**:有关使用 SDK 的应用程序的信息


> 弃用此构造函数即将弃用, 以支持一个需要 mip:: MipContext 参数
  
### <a name="settings-function"></a>Settings 函数
[FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。

参数：  
* **mipContext**:全局上下文设置 


* **cacheStorageType**:将任何缓存的状态存储在内存中或磁盘上 


* **authDelegate**:用于获取身份验证令牌的身份验证委托 


* **consentDelegate**:用于获取访问外部资源的用户权限的委托 


* **观察**程序:将接收与[FileProfile](class_mip_fileprofile.md)相关的事件通知的[观察](class_mip_fileprofile_observer.md)程序实例


  
### <a name="getpath-function"></a>GetPath 函数
获取存储日志记录、遥测和其他永久性状态的路径。

  
**返回**:存储日志记录、遥测和其他持久状态的路径
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公用上下文数据
  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType 函数
获取缓存是存储在内存中还是存储在磁盘上。

  
**返回**:使用的存储类型
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 函数
获取用于获取身份验证令牌的身份验证委托。

  
**返回**:用于获取身份验证令牌的身份验证委托
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate 函数
获取用于请求用户许可连接到服务的许可委托。

  
**返回**:用于请求用户同意的许可委托
  
### <a name="getobserver-function"></a>GetObserver 函数
获取接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的观察程序。

  
**返回**:接收与[FileProfile](class_mip_fileprofile.md)相关的事件通知的[观察](class_mip_fileprofile_observer.md)程序
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 函数
获取使用 SDK 的应用程序的相关信息。

  
**返回**:有关使用 SDK 的应用程序的信息
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公用上下文数据
  
### <a name="getmipcontext-function"></a>GetMipContext 函数
获取表示所有配置文件的共享状态的 MIP 上下文。

  
**返回**:MIP 上下文
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 函数
获取应用程序提供的记录器委托（若有）。

  
**返回**:记录器
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公用上下文数据
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate 函数
替代默认记录器。

参数：  
* **loggerDelegate**:记录由客户端应用程序实现的回调接口


客户端应用程序应调用此方法以使用自己的记录器实现 
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公用上下文数据
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 函数
获取应用程序提供的 HTTP 委托（若有）。

  
**返回**:要用于 HTTP 操作的 HTTP 委托
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 函数
使用客户端自己的替代默认 HTTP 堆栈。

参数：  
* **httpDelegate**:由客户端应用程序实现的 HTTP 回调接口


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 函数
获取应用程序提供的 TaskDispatcher 委托 (如果有)。

  
**返回**:用于执行异步任务的 TaskDispatcher 委托
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 函数
用客户端自己的 asynchonous 重写默认的任务分派处理。

参数：  
* **taskDispatcherDelegate**:任务分派由客户端应用程序实现的回调接口


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry 函数
选择退出所有遥测收集。
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公用上下文数据
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut 函数
获取是否应禁用遥测收集的指示。

  
**返回**:如果应禁用遥测收集
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公用上下文数据
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置会话 ID。

参数：  
* **sessionId**:将用于关联日志/遥测的会话 ID


  
### <a name="getsessionid-function"></a>GetSessionId 函数
获取会话 ID。

  
**返回**:将用于关联日志/遥测的会话 ID
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel 函数
设置将触发日志记录事件的最低日志级别。

参数：  
* **logLevel**：将触发日志记录事件的最低日志级别。


> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公用上下文数据
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 函数
获取将触发日志记录事件的最低日志级别。

  
**返回**:将触发日志记录事件的最低日志级别。
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公用上下文数据
  
### <a name="setcancachelicenses-function"></a>SetCanCacheLicenses 函数
配置是否将以本地方式缓存最终用户许可证 (Eul)。

参数：  
* **canCacheLicenses**:打开受保护的内容时, 引擎是否应缓存许可证


如果为 true, 则打开受保护的内容将在本地缓存关联的许可证。 如果为 false, 则打开受保护的内容将始终执行 HTTP 操作以从 RMS 服务获取许可证。
  
### <a name="cancachelicenses-function"></a>CanCacheLicenses 函数
获取是否在本地缓存最终用户许可证 (Eul)。

  
**返回**:许可证缓存配置