---
title: 类 mip ProtectionProfile Settings
description: 类 mip ProtectionProfile Settings 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: fe2413b2265cf4994dce0e57a7c472d59336902a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446662"
---
# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
由 [ProtectionProfile](class_mip_protectionprofile.md) 在创建期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数，指定要用于异步操作的观察程序。
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const ApplicationInfo& applicationInfo)  |  [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数，用于同步操作。
 public const std::string& GetPath() const  |  获取在其下存储日志记录、遥测和其他保护附件的路径。
 public bool GetUseInMemoryStorage() const  |  获取缓存是否仅存储在内存中（而不是存储在磁盘上）
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  获取用于获取身份验证令牌的身份验证委托。
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  获取用于连接到服务的许可委托。
public std::shared_ptr<ProtectionProfile::Observer> GetObserver() const  |  获取接收 [ProtectionProfile](class_mip_protectionprofile.md) 相关事件通知的观察程序。
 public const ApplicationInfo& GetApplicationInfo() const  |  获取使用保护 SDK 的应用程序的相关信息。
 public void OptOutTelemetry()  |  选择退出所有遥测收集。
 public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集的指示。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  获取应用程序提供的记录器委托（若有）。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  替代默认记录器。
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  使用客户端自己的替代默认 HTTP 堆栈。
 public bool GetSkipTelemetryInit() const  |  获取是否应跳过遥测初始化的指示。
 public void SetSkipTelemetryInit()  |  禁用遥测初始化。
 public void SetNewFeaturesDisabled()  |  禁用新功能。
 public bool AreNewFeaturesDisabled() const  |  获取是否禁用新功能的指示。
 public void SetSessionId(const std::string& sessionId)  |  设置会话 ID。
 public const std::string& GetSessionId() const  |  获取会话 ID。
 public void SetMinimumLogLevel(LogLevel logLevel)  |  设置将触发日志记录事件的最小日志级别。
 public LogLevel GetMinimumLogLevel() const  |  获取最小日志级别对象。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数，指定要用于异步操作的观察程序。

参数：  
* **path**：在其下存储日志记录、遥测和其他保护附件的文件路径 


* **useInMemoryStorage**：将任意缓存状态存储到内存中，而不是存储在磁盘上 


* **authDelegate**：客户端应用程序实现的用于身份验证的回叫对象 


* **observer**：将接收 [ProtectionProfile](class_mip_protectionprofile.md) 相关事件通知的[观察程序](class_mip_protectionprofile_observer.md)实例


* **applicationInfo**：使用保护 SDK 的应用程序的相关信息


  
### <a name="settings"></a>设置
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数，用于同步操作。

参数：  
* **path**：在其下存储日志记录、遥测和其他保护附件的文件路径 


* **useInMemoryStorage**：将任意缓存状态存储到内存中，而不是存储在磁盘上 


* **authDelegate**：客户端应用程序实现的用于身份验证的回叫对象 


* **applicationInfo**：使用保护 SDK 的应用程序的相关信息


  
### <a name="getpath"></a>GetPath
获取在其下存储日志记录、遥测和其他保护附件的路径。

  
**返回结果**：在其下存储日志记录、遥测和其他保护附件的路径
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
获取缓存是否仅存储在内存中（而不是存储在磁盘上）

  
**返回结果**：如果缓存仅存储在内存中，返回 True
  
### <a name="getauthdelegate"></a>GetAuthDelegate
获取用于获取身份验证令牌的身份验证委托。

  
**返回结果**：用于获取身份验证令牌的身份验证委托
  
### <a name="consentdelegate"></a>ConsentDelegate
获取用于连接到服务的许可委托。

  
**返回结果**：用于连接到服务的许可委托
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
获取接收 [ProtectionProfile](class_mip_protectionprofile.md) 相关事件通知的观察程序。

  
**返回结果**：接收 [ProtectionProfile](class_mip_protectionprofile.md) 相关事件通知的[观察程序](class_mip_protectionprofile_observer.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
获取使用保护 SDK 的应用程序的相关信息。

  
**返回结果**：使用保护 SDK 的应用程序的相关信息
  
### <a name="optouttelemetry"></a>OptOutTelemetry
选择退出所有遥测收集。
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
获取是否应禁用遥测收集的指示。

  
**返回结果**：指示是否应禁用遥测收集
  
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
  
### <a name="setsessionid"></a>SetSessionId
设置会话 ID。

参数：  
* **sessionId**：将用于关联日志/遥测的会话 ID


  
### <a name="getsessionid"></a>GetSessionId
获取会话 ID。

  
**返回结果**：将用于关联日志/遥测的会话 ID
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
设置将触发日志记录事件的最小日志级别。

参数：  
* logLevel：将触发日志记录事件的最小日志级别。 



  
返回结果：True
  
### <a name="loglevel"></a>日志级别
获取最小日志级别对象。

  
返回结果：将触发日志记录事件的最小日志级别。