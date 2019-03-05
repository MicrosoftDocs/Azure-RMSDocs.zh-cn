---
title: class mip::PolicyProfile::Settings
description: 记录 mip::policyprofile 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: a48f22af3f699412a2976683695467ee7ed71cdb
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57331182"
---
# <a name="class-mippolicyprofilesettings"></a>class mip::PolicyProfile::Settings 
[PolicyProfile](class_mip_policyprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_policyprofile_settings.md)。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 (const std:: string & 路径，bool useinmemorystorage: const std:: shared_ptr\<AuthDelegate\>& authDelegate，const std:: shared_ptr\<PolicyProfile::Observer\>（& a)observer，const ApplicationInfo & applicationInfo)  |  用于配置配置文件的接口。
public const std::string& GetPath() const  |  获取存储状态的路径。
public bool GetUseInMemoryStorage() const  |  获取“使用内存中的存储”标记。
public const std::\<AuthDelegate\>& GetAuthDelegate() 常量  |  获取身份验证委托。
public const std::\<PolicyProfile::Observer\>& GetObserver() 常量  |  获取事件观察程序。
public const ApplicationInfo GetApplicationInfo() const  |  获取应用程序信息。
public std::shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  获取应用程序提供的记录器委托（若有）。
public void SetLoggerDelegate(const std::shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  替代默认记录器。
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate(const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  使用客户端自己的替代默认 HTTP 堆栈。
public void OptOutTelemetry()  |  选择退出所有遥测收集。
public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集的指示。
public void SetMinimumLogLevel(LogLevel logLevel)  |  设置将触发日志记录事件的最小日志级别。
public LogLevel GetMinimumLogLevel() const  |  获取最小日志级别对象。
  
## <a name="members"></a>成員
  
### <a name="settings-function"></a>设置函数
用于配置配置文件的接口。

参数：  
* **路径**:SDK 将在其中存储配置文件状态目录的路径。 


* **useinmemorystorage:**:在内存中而不是磁盘上存储任何缓存的状态。 


* **authDelegate**:由 SDK 用于获取身份验证令牌的身份验证委托。 


* **observer**:类实现[PolicyProfile::Observer](class_mip_policyprofile_observer.md)接口。 可以为 nullptr。 


* **applicationinfo:**:用于访问服务应用程序标识符。


  
### <a name="getpath-function"></a>GetPath 函数
获取存储状态的路径。

  
**返回**:存储状态的路径。
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage 函数
获取“使用内存中的存储”标记。

  
**返回**:如果在内存中的使用设置否则为 false，则为 true。
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate function
获取身份验证委托。

  
**返回**:身份验证委托。
  
### <a name="getobserver-function"></a>GetObserver 函数
获取事件观察程序。

  
**返回**:事件观察程序。
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo function
获取应用程序信息。

  
**返回**:应用程序信息。
  
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

  
**返回**:要用于 HTTP 操作的 http 委托
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 函数
使用客户端自己的替代默认 HTTP 堆栈。

参数：  
* **httpDelegate**:由客户端应用程序实现 http 回调接口


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry 函数
选择退出所有遥测收集。
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut 函数
获取是否应禁用遥测收集的指示。

  
**返回**:如果应禁用收集的遥测则为 true，否则返回 false
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel 函数
设置将触发日志记录事件的最小日志级别。

参数：  
* logLevel：将触发日志记录事件的最小日志级别。 



  
**返回**:True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 函数
获取最小日志级别对象。

  
**返回**:将触发日志记录事件的最小日志级别。
