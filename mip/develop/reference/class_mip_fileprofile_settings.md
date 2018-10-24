---
title: 类 mip FileProfile Settings
description: 类 mip FileProfile Settings 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 4b79d8eb75a54a56f1b3e48645bdd5eec0afaa19
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446373"
---
# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
[FileProfile](class_mip_fileprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_fileprofile_settings.md)。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。
 public const std::string& GetPath() const  |  获取存储日志记录、遥测和其他永久性状态的路径。
 public bool GetUseInMemoryStorage() const  |  获取是否所有状态都应存储在内存中（而不是存储在磁盘上）的指示
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  获取用于获取身份验证令牌的身份验证委托。
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  获取用于请求用户许可连接到服务的许可委托。
public std::shared_ptr<Observer> GetObserver() const  |  获取接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的观察程序。
 public const ApplicationInfo GetApplicationInfo() const  |  获取使用 SDK 的应用程序的相关信息。
 public bool GetSkipTelemetryInit() const  |  获取是否应跳过遥测初始化的指示。
 public void SetSkipTelemetryInit()  |  禁用遥测初始化。
 public void SetNewFeaturesDisabled()  |  禁用新功能。
 public bool AreNewFeaturesDisabled() const  |  获取是否禁用新功能的指示。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  获取应用程序提供的记录器委托（若有）。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  替代默认记录器。
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  使用客户端自己的替代默认 HTTP 堆栈。
 public void OptOutTelemetry()  |  选择退出所有遥测收集。
 public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集的指示。
 public void SetSessionId(const std::string& sessionId)  |  设置会话 ID。
 public const std::string& GetSessionId() const  |  获取会话 ID。
 public void SetMinimumLogLevel(LogLevel logLevel)  |  设置将触发日志记录事件的最低日志级别。
 public LogLevel GetMinimumLogLevel() const  |  获取将触发日志记录事件的最低日志级别。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
[FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。

参数：  
* **路径**：在其下存储日志记录、遥测和其他永久性状态的文件路径 


* **useInMemoryStorage**：如果所有状态都应存储在内存中，则为 true；如果状态可以缓存到磁盘，则为 false 


* **authDelegate**：用于获取身份验证令牌的身份验证委托 


* **observer**：将接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的[观察程序](class_mip_fileprofile_observer.md)实例


* **applicationInfo**：使用 SDK 的应用程序的相关信息


  
### <a name="getpath"></a>GetPath
获取存储日志记录、遥测和其他永久性状态的路径。

  
**返回结果**：在其下存储日志记录、遥测和其他永久性状态的路径
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
获取是否所有状态都应存储在内存中（而不是存储在磁盘上）的指示

  
**返回结果**：指示是否所有状态都应存储在内存中（而不是存储在磁盘上）
  
### <a name="getauthdelegate"></a>GetAuthDelegate
获取用于获取身份验证令牌的身份验证委托。

  
**返回结果**：用于获取身份验证令牌的身份验证委托
  
### <a name="consentdelegate"></a>ConsentDelegate
获取用于请求用户许可连接到服务的许可委托。

  
**返回结果**：用户请求用户同意的同意委托
  
### <a name="observer"></a>观察者
获取接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的观察程序。

  
**返回结果**：接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的[观察程序](class_mip_fileprofile_observer.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
获取使用 SDK 的应用程序的相关信息。

  
**返回结果**：使用 SDK 的应用程序的相关信息
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
获取是否应跳过遥测初始化的指示。

  
**返回结果**：指示是否应跳过遥测初始化
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
禁用遥测初始化。
此方法通常不会被客户端应用程序调用，而是由文件 SDK 用于防止重复初始化
  
### <a name="setnewfeaturesdisabled"></a>SetNewFeaturesDisabled
禁用新功能。
适用于不想尝试新功能的应用程序
  
### <a name="arenewfeaturesdisabled"></a>AreNewFeaturesDisabled
获取是否禁用新功能的指示。

  
**返回结果**：指示是否禁用新功能
  
### <a name="loggerdelegate"></a>LoggerDelegate
获取应用程序提供的记录器委托（若有）。

  
**返回结果**：记录器
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
替代默认记录器。

参数：  
* loggerDelegate：客户端应用程序实现的日志记录回叫接口


客户端应用程序应调用此方法以使用自己的记录器实现
  
### <a name="httpdelegate"></a>HttpDelegate
获取应用程序提供的 HTTP 委托（若有）。

  
**返回结果**：要用于 HTTP 操作的 HTTP 委托
  
### <a name="sethttpdelegate"></a>SetHttpDelegate
使用客户端自己的替代默认 HTTP 堆栈。

参数：  
* **httpDelegate**：客户端应用程序实现的 HTTP 回叫接口


  
### <a name="optouttelemetry"></a>OptOutTelemetry
选择退出所有遥测收集。
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
获取是否应禁用遥测收集的指示。

  
**返回结果**：指示是否应禁用遥测收集
  
### <a name="setsessionid"></a>SetSessionId
设置会话 ID。

参数：  
* **sessionId**：将用于关联日志/遥测的会话 ID


  
### <a name="getsessionid"></a>GetSessionId
获取会话 ID。

  
**返回结果**：将用于关联日志/遥测的会话 ID
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
设置将触发日志记录事件的最低日志级别。

参数：  
* **logLevel**：将触发日志记录事件的最低日志级别。 



  
**返回结果**：True
  
### <a name="loglevel"></a>日志级别
获取将触发日志记录事件的最低日志级别。

  
**返回结果**：将触发日志记录事件的最低日志级别。