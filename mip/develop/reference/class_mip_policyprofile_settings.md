---
title: class mip::PolicyProfile::Settings
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p olicyprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2edec96a34b6885aa6c38477d36e401ebc49242a
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055654"
---
# <a name="class-mippolicyprofilesettings"></a>class mip::PolicyProfile::Settings 
[PolicyProfile](class_mip_policyprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_policyprofile_settings.md)。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 (const std:: string & path, CacheStorageType CacheStorageType, const std:: shared_ptr\<AuthDelegate\>& AuthDelegate, const std:: shared_ptr\<PolicyProfile:: Observer\>& 观察程序, const ApplicationInfo & applicationInfo)  |  用于配置配置文件的接口。
public Settings (const std:: shared_ptr\<MipContext\>& MipContext, CacheStorageType CacheStorageType, const std:: shared_ptr\<AuthDelegate\>& AuthDelegate, const std:: shared_ptr\<PolicyProfile:: observer\>& 观察程序)  |  用于配置配置文件的接口。
public const std::string& GetPath() const  |  获取存储状态的路径。
public CacheStorageType GetCacheStorageType () const  |  获取缓存是存储在内存中还是存储在磁盘上。
public const std:: shared_ptr\<AuthDelegate\>& GetAuthDelegate () const  |  获取身份验证委托。
public const std:: shared_ptr\<PolicyProfile:: Observer\>& GetObserver () const  |  获取事件观察程序。
public const ApplicationInfo& GetApplicationInfo() const  |  获取应用程序信息。
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  获取表示所有配置文件的共享状态的 MIP 上下文。
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate () const  |  获取应用程序提供的记录器委托（若有）。
public void SetLoggerDelegate (const std:: shared_ptr\<LoggerDelegate\>& LoggerDelegate)  |  替代默认记录器。
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& HttpDelegate)  |  使用客户端自己的替代默认 HTTP 堆栈。
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  获取应用程序提供的 TaskDispatcher 委托 (如果有)。
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& TaskDispatcherDelegate)  |  用客户端自己的 asynchonous 重写默认的任务分派处理。
public void OptOutTelemetry()  |  选择退出所有遥测收集。
public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集的指示。
public void SetMinimumLogLevel(LogLevel logLevel)  |  设置将触发日志记录事件的最小日志级别。
public LogLevel GetMinimumLogLevel() const  |  获取最小日志级别对象。
public void SetSessionId(const std::string& sessionId)  | _尚无记录。_
public const std::string& GetSessionId() const  | _尚无记录。_
public ~Settings()  | _尚无记录。_
  
## <a name="members"></a>成员
  
### <a name="settings-function"></a>Settings 函数
用于配置配置文件的接口。

参数：  
* **路径**:SDK 将在其中存储配置文件状态的目录的路径。 


* **cacheStorageType**:将任何缓存的状态存储在内存中或磁盘上 


* **authDelegate**:SDK 用于获取身份验证令牌的身份验证委托。 


* **观察**程序:实现[PolicyProfile:: Observer](class_mip_policyprofile_observer.md)接口的类。 可以为 nullptr。 


* **applicationInfo**:用于服务访问的应用程序标识符。


> 弃用此构造函数即将弃用, 以支持一个需要 mip:: MipContext 参数
  
### <a name="settings-function"></a>Settings 函数
用于配置配置文件的接口。

参数：  
* **mipContext**:全局上下文设置 


* **cacheStorageType**:将任何缓存的状态存储在内存中或磁盘上 


* **authDelegate**:SDK 用于获取身份验证令牌的身份验证委托。 


* **观察**程序:实现[PolicyProfile:: Observer](class_mip_policyprofile_observer.md)接口的类。 可以为 nullptr。


  
### <a name="getpath-function"></a>GetPath 函数
获取存储状态的路径。

  
**返回**:存储状态的路径。
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公共上下文数据。
  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType 函数
获取缓存是存储在内存中还是存储在磁盘上。

  
**返回**:使用的存储类型
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 函数
获取身份验证委托。

  
**返回**:身份验证委托。
  
### <a name="getobserver-function"></a>GetObserver 函数
获取事件观察程序。

  
**返回**:事件观察程序。
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 函数
获取应用程序信息。

  
**返回**:应用程序信息。
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公共上下文数据。
  
### <a name="getmipcontext-function"></a>GetMipContext 函数
获取表示所有配置文件的共享状态的 MIP 上下文。

  
**返回**:MIP 上下文
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 函数
获取应用程序提供的记录器委托（若有）。

  
**返回**:记录器
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公共上下文数据。
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate 函数
替代默认记录器。

参数：  
* **loggerDelegate**:记录由客户端应用程序实现的回调接口


客户端应用程序应调用此方法以使用自己的记录器实现 
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公共上下文数据。
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 函数
获取应用程序提供的 HTTP 委托（若有）。

  
**返回**:要用于 HTTP 操作的 http 委托
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 函数
使用客户端自己的替代默认 HTTP 堆栈。

参数：  
* **httpDelegate**:由客户端应用程序实现的 Http 回调接口


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 函数
获取应用程序提供的 TaskDispatcher 委托 (如果有)。

  
**返回**:用于执行异步任务的 TaskDispatcher 委托
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 函数
用客户端自己的 asynchonous 重写默认的任务分派处理。

参数：  
* **taskDispatcherDelegate**:任务分派由客户端应用程序实现的回调接口


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry 函数
选择退出所有遥测收集。
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公共上下文数据。
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut 函数
获取是否应禁用遥测收集的指示。

  
**返回**:如果应禁用遥测收集, 则为 True; 否则为 false
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公共上下文数据。
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel 函数
设置将触发日志记录事件的最小日志级别。

参数：  
* logLevel：将触发日志记录事件的最小日志级别。


> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公共上下文数据。
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 函数
获取最小日志级别对象。

  
**返回**:将触发日志记录事件的最小日志级别。
> 弃用此方法将很快被弃用, 以通过 mip:: MipContext 获取/设置公共上下文数据。
  
### <a name="setsessionid-function"></a>SetSessionId 函数
_尚无记录。_

  
### <a name="getsessionid-function"></a>GetSessionId 函数
_尚无记录。_

  
### <a name="settings-function"></a>~ Settings 函数
_尚无记录。_
