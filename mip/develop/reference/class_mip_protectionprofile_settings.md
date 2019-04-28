---
title: class mip::ProtectionProfile::Settings
description: 记录 mip::protectionprofile 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3d3685656f8814fe495e6e29d7fe12cf54d7d7d4
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173609"
---
# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
由 [ProtectionProfile](class_mip_protectionprofile.md) 在创建期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 (const std:: string & 路径，bool useinmemorystorage: const std:: shared_ptr\<AuthDelegate\>& authDelegate，const std:: shared_ptr\<ConsentDelegate\>& consentDelegateconst std:: shared_ptr\<protectionprofile:: Observer\>& observer，const ApplicationInfo & applicationInfo)  |  [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数，指定要用于异步操作的观察程序。
公共设置 (const std:: string & 路径，bool useinmemorystorage: const std:: shared_ptr\<AuthDelegate\>& authDelegate，const std:: shared_ptr\<ConsentDelegate\>& consentDelegateconst ApplicationInfo & applicationInfo)  |  [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数，用于同步操作。
public const std::string& GetPath() const  |  获取在其下存储日志记录、遥测和其他保护附件的路径。
public bool GetUseInMemoryStorage() const  |  获取缓存是否仅存储在内存中（而不是存储在磁盘上）
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  获取用于获取身份验证令牌的身份验证委托。
public std::shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  获取用于连接到服务的许可委托。
public std::\<protectionprofile:: Observer\> GetObserver() 常量  |  获取接收 [ProtectionProfile](class_mip_protectionprofile.md) 相关事件通知的观察程序。
public const ApplicationInfo& GetApplicationInfo() const  |  获取使用保护 SDK 的应用程序的相关信息。
public void OptOutTelemetry()  |  选择退出所有遥测收集。
public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集的指示。
public std::shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  获取应用程序提供的记录器委托（若有）。
public void SetLoggerDelegate(const std::shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  替代默认记录器。
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate(const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  使用客户端自己的替代默认 HTTP 堆栈。
public std::shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate() const  |  获取应用程序提供的 TaskDispatcher 委托 （如果有）。
public void SetTaskDispatcherDelegate (const std::\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  重写默认调度处理客户端自己的异步任务。
public void SetNewFeaturesDisabled()  |  禁用新功能。
public bool AreNewFeaturesDisabled() const  |  获取是否禁用新功能的指示。
public void SetSessionId(const std::string& sessionId)  |  设置会话 ID。
public const std::string& GetSessionId() const  |  获取会话 ID。
public void SetMinimumLogLevel(LogLevel logLevel)  |  设置将触发日志记录事件的最小日志级别。
public LogLevel GetMinimumLogLevel() const  |  获取最小日志级别对象。
  
## <a name="members"></a>成員
  
### <a name="settings-function"></a>设置函数
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数，指定要用于异步操作的观察程序。

参数：  
* **路径**:文件路径下的日志记录、 遥测和其他保护附件存储 


* **useinmemorystorage:**:在内存中而不是磁盘上存储任何缓存的状态 


* **authDelegate**:要用于身份验证，由客户端应用程序实现的回调对象 


* **observer**:[观察者](class_mip_protectionprofile_observer.md)将要接收的事件通知实例与[ProtectionProfile](class_mip_protectionprofile.md)


* **applicationinfo:**:有关使用保护 SDK 的应用程序的信息


  
### <a name="settings-function"></a>设置函数
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数，用于同步操作。

参数：  
* **路径**:文件路径下的日志记录、 遥测和其他保护附件存储 


* **useinmemorystorage:**:在内存中而不是磁盘上存储任何缓存的状态 


* **authDelegate**:要用于身份验证，由客户端应用程序实现的回调对象 


* **applicationinfo:**:有关使用保护 SDK 的应用程序的信息


  
### <a name="getpath-function"></a>GetPath 函数
获取在其下存储日志记录、遥测和其他保护附件的路径。

  
**返回**:在其下存储日志记录、遥测和其他保护附件的路径
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage 函数
获取缓存是否仅存储在内存中（而不是存储在磁盘上）

  
**返回**:如果只能在内存中存储缓存，则返回 true
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate function
获取用于获取身份验证令牌的身份验证委托。

  
**返回**:用于获取身份验证令牌的身份验证委托
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate 函数
获取用于连接到服务的许可委托。

  
**返回**:使用用于连接到服务的许可委托
  
### <a name="getobserver-function"></a>GetObserver 函数
获取接收 [ProtectionProfile](class_mip_protectionprofile.md) 相关事件通知的观察程序。

  
**返回**:[观察者](class_mip_protectionprofile_observer.md)，它接收到相关的事件通知[ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo function
获取使用保护 SDK 的应用程序的相关信息。

  
**返回**:有关使用保护 SDK 的应用程序的信息
  
### <a name="optouttelemetry-function"></a>OptOutTelemetry 函数
选择退出所有遥测收集。
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut 函数
获取是否应禁用遥测收集的指示。

  
**返回**:如果应禁用遥测数据收集
  
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


  
### <a name="setnewfeaturesdisabled-function"></a>SetNewFeaturesDisabled 函数
禁用新功能。
适用于不想尝试新功能的应用程序
  
### <a name="arenewfeaturesdisabled-function"></a>AreNewFeaturesDisabled 函数
获取是否禁用新功能的指示。

  
**返回**:如果新功能将被禁用或不
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置会话 ID。

参数：  
* **sessionId**:将用于关联日志/遥测的会话 ID


  
### <a name="getsessionid-function"></a>GetSessionId 函数
获取会话 ID。

  
**返回**:将用于关联日志/遥测的会话 ID
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel 函数
设置将触发日志记录事件的最小日志级别。

参数：  
* logLevel：将触发日志记录事件的最小日志级别。 



  
**返回**:True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 函数
获取最小日志级别对象。

  
**返回**:将触发日志记录事件的最小日志级别。