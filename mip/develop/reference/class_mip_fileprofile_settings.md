---
title: class mip::FileProfile::Settings
description: 记录 mip::fileprofile 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d85fe9f4b3de485ab966a38b2c41358a6ba091e0
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173281"
---
# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
[FileProfile](class_mip_fileprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_fileprofile_settings.md)。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 (const std:: string & 路径，bool useinmemorystorage: std:: shared_ptr\<AuthDelegate\> authDelegate，std:: shared_ptr\<ConsentDelegate\> consentDelegate，std:: shared_ptr\<观察者\>observer，const ApplicationInfo & applicationInfo)  |  [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。
public const std::string& GetPath() const  |  获取存储日志记录、遥测和其他永久性状态的路径。
public bool GetUseInMemoryStorage() const  |  获取是否所有状态都应存储在内存中（而不是存储在磁盘上）的指示
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  获取用于获取身份验证令牌的身份验证委托。
public std::shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  获取用于请求用户许可连接到服务的许可委托。
public std::shared_ptr\<Observer\> GetObserver() const  |  获取接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的观察程序。
public const ApplicationInfo GetApplicationInfo() const  |  获取使用 SDK 的应用程序的相关信息。
public void SetNewFeaturesDisabled()  |  禁用新功能。
public bool AreNewFeaturesDisabled() const  |  获取是否禁用新功能的指示。
public std::shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  获取应用程序提供的记录器委托（若有）。
public void SetLoggerDelegate(const std::shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  替代默认记录器。
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate(const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  使用客户端自己的替代默认 HTTP 堆栈。
public std::shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate() const  |  获取应用程序提供的 TaskDispatcher 委托 （如果有）。
public void SetTaskDispatcherDelegate (const std::\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  重写默认调度处理客户端自己的异步任务。
public void OptOutTelemetry()  |  选择退出所有遥测收集。
public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集的指示。
public void SetSessionId(const std::string& sessionId)  |  设置会话 ID。
public const std::string& GetSessionId() const  |  获取会话 ID。
public void SetMinimumLogLevel(LogLevel logLevel)  |  设置将触发日志记录事件的最低日志级别。
public LogLevel GetMinimumLogLevel() const  |  获取将触发日志记录事件的最低日志级别。
  
## <a name="members"></a>成員
  
### <a name="settings-function"></a>设置函数
[FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。

参数：  
* **路径**:文件路径下的日志记录、 遥测和其他持久状态存储 


* **useInMemoryStorage**：如果所有状态都应存储在内存中，则为 true；如果状态可以缓存到磁盘，则为 false 


* **authDelegate**:用于获取身份验证令牌的身份验证委托 


* **observer**:[观察者](class_mip_fileprofile_observer.md)将要接收的事件通知实例与[FileProfile](class_mip_fileprofile.md)


* **applicationinfo:**:有关使用 SDK 的应用程序的信息


  
### <a name="getpath-function"></a>GetPath 函数
获取存储日志记录、遥测和其他永久性状态的路径。

  
**返回**:路径下的日志记录、 遥测和其他持久状态存储
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage 函数
获取是否所有状态都应存储在内存中（而不是存储在磁盘上）的指示

  
**返回**:（与用于在磁盘上），如果应在内存中存储的所有状态
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate function
获取用于获取身份验证令牌的身份验证委托。

  
**返回**:用于获取身份验证令牌的身份验证委托
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate 函数
获取用于请求用户许可连接到服务的许可委托。

  
**返回**:用于请求用户同意的同意委托
  
### <a name="getobserver-function"></a>GetObserver 函数
获取接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的观察程序。

  
**返回**:[观察者](class_mip_fileprofile_observer.md)，它接收到相关的事件通知[FileProfile](class_mip_fileprofile.md)
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo function
获取使用 SDK 的应用程序的相关信息。

  
**返回**:有关使用 SDK 的应用程序的信息
  
### <a name="setnewfeaturesdisabled-function"></a>SetNewFeaturesDisabled 函数
禁用新功能。
适用于不想尝试新功能的应用程序
  
### <a name="arenewfeaturesdisabled-function"></a>AreNewFeaturesDisabled 函数
获取是否禁用新功能的指示。

  
**返回**:如果新功能将被禁用或不
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 函数
获取应用程序提供的记录器委托（若有）。

  
**返回**:记录器
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate 函数
替代默认记录器。

参数：  
* **loggerDelegate**:日志记录由客户端应用程序实现的回调接口


客户端应用程序应调用此方法以使用自己的记录器实现
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 函数
获取应用程序提供的 HTTP 委托（若有）。

  
**返回**:要用于 HTTP 操作的 HTTP 委托
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 函数
使用客户端自己的替代默认 HTTP 堆栈。

参数：  
* **httpDelegate**:由客户端应用程序实现 HTTP 回调接口


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 函数
获取应用程序提供的 TaskDispatcher 委托 （如果有）。

  
**返回**:要用于执行异步任务的 TaskDispatcher 委托
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 函数
重写默认调度处理客户端自己的异步任务。

参数：  
* **taskDispatcherDelegate**:任务调度回调由客户端应用程序实现的接口


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry 函数
选择退出所有遥测收集。
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut 函数
获取是否应禁用遥测收集的指示。

  
**返回**:如果应禁用遥测数据收集
  
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



  
**返回**:True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 函数
获取将触发日志记录事件的最低日志级别。

  
**返回**:将触发日志记录事件的最低日志级别。