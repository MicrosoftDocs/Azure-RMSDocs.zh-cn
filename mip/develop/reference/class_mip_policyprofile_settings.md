---
title: class mip PolicyProfile Settings
description: 类 mip PolicyProfile Settings 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 07cbcbc022c02a43f751e1cf55b5b0efdfb816d1
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446850"
---
# <a name="class-mippolicyprofilesettings"></a>class mip::PolicyProfile::Settings 
[PolicyProfile](class_mip_policyprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_policyprofile_settings.md)。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<PolicyProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  用于配置配置文件的接口。
 public const std::string& GetPath() const  |  获取存储状态的路径。
 public bool GetUseInMemoryStorage() const  |  获取“使用内存中的存储”标记。
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  获取身份验证委托。
public const std::shared_ptr<PolicyProfile::Observer>& GetObserver() const  |  获取事件观察程序。
 public const ApplicationInfo GetApplicationInfo() const  |  获取应用程序信息。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  获取应用程序提供的记录器委托（若有）。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  替代默认记录器。
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  使用客户端自己的替代默认 HTTP 堆栈。
 public void OptOutTelemetry()  |  选择退出所有遥测收集。
 public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集。
 public void SetMinimumLogLevel(LogLevel logLevel)  |  设置将触发日志记录事件的最小日志级别。
 public LogLevel GetMinimumLogLevel() const  |  获取最小日志级别对象。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
用于配置配置文件的接口。

参数：  
* path：SDK 将在其中存储配置文件状态的目录路径。 


* useInMemoryStorage：将任意缓存状态存储到内存中，而不是存储在磁盘上。 


* **authDelegate**：SDK 用来获取身份验证令牌的身份验证委托。 


* observer：实现 [PolicyProfile::Observer](class_mip_policyprofile_observer.md) 接口的类。 可以为 nullptr。 


* **applicationInfo**：用于访问服务的应用程序标识符。


  
### <a name="getpath"></a>GetPath
获取存储状态的路径。

  
**返回结果**：存储状态的路径。
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
获取“使用内存中的存储”标记。

  
**返回结果**：如果设置了“在内存中使用”，则为 true，否则为 false。
  
### <a name="getauthdelegate"></a>GetAuthDelegate
获取身份验证委托。

  
**返回结果**：身份验证委托。
  
### <a name="policyprofileobserver"></a>PolicyProfile::Observer
获取事件观察程序。

  
**返回结果**：事件观察程序。
  
### <a name="applicationinfo"></a>ApplicationInfo
获取应用程序信息。

  
**返回结果**：应用程序信息。
  
### <a name="loggerdelegate"></a>LoggerDelegate
获取应用程序提供的记录器委托（若有）。

  
返回结果：记录器
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
替代默认记录器。

参数：  
* loggerDelegate：客户端应用程序实现的日志记录回叫接口


客户端应用程序应调用此方法以使用自己的记录器实现
  
### <a name="httpdelegate"></a>HttpDelegate
获取应用程序提供的 HTTP 委托（若有）。

  
返回结果：要用于 HTTP 操作的 http 委托
  
### <a name="sethttpdelegate"></a>SetHttpDelegate
使用客户端自己的替代默认 HTTP 堆栈。

参数：  
* httpDelegate：客户端应用程序实现的 http 回叫接口


  
### <a name="optouttelemetry"></a>OptOutTelemetry
选择退出所有遥测收集。
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
获取是否应禁用遥测收集。

  
返回结果：是否应禁用遥测收集
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
设置将触发日志记录事件的最小日志级别。

参数：  
* logLevel：将触发日志记录事件的最小日志级别。 



  
返回结果：True
  
### <a name="loglevel"></a>日志级别
获取最小日志级别对象。

  
返回结果：将触发日志记录事件的最小日志级别。