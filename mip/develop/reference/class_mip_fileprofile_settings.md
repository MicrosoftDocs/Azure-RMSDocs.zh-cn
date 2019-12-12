---
title: class mip::FileProfile::Settings
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： fileprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 21bbda3424f5c436324ce97137082200ee8d9837
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73561105"
---
# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
FileProfile 在其创建期间及其整个生存期内使用的设置。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共设置（const std：： shared_ptr\<MipContext\>& mipContext，CacheStorageType cacheStorageType，std：： shared_ptr\<AuthDelegate\> authDelegate，std：： shared_ptr\<ConsentDelegate\> consentDelegate，std：： shared_ptr\<观察程序\> 观察程序）  |  FileProfile：： Settings 构造函数。
public CacheStorageType GetCacheStorageType （） const  |  获取缓存是存储在内存中还是存储在磁盘上。
public std：： shared_ptr\<AuthDelegate\> GetAuthDelegate （） const  |  获取用于获取身份验证令牌的身份验证委托。
public std：： shared_ptr\<ConsentDelegate\> GetConsentDelegate （） const  |  获取用于请求用户许可连接到服务的许可委托。
public std：： shared_ptr\<观察程序\> GetObserver （） const  |  获取接收与 FileProfile 相关的事件通知的观察程序。
public std：： shared_ptr\<MipContext\> GetMipContext （） const  |  获取表示所有配置文件的共享状态的 MIP 上下文。
public std：： shared_ptr\<HttpDelegate\> GetHttpDelegate （） const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate （const std：： shared_ptr\<HttpDelegate\>& httpDelegate）  |  使用客户端自己的替代默认 HTTP 堆栈。
public std：： shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate （） const  |  获取应用程序提供的 TaskDispatcher 委托（如果有）。
public void SetTaskDispatcherDelegate （const std：： shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate）  |  用客户端自己的 asynchonous 重写默认的任务分派处理。
public void SetSessionId(const std::string& sessionId)  |  设置会话 ID。
public const std::string& GetSessionId() const  |  获取会话 ID。
public void SetCanCacheLicenses （bool canCacheLicenses）  |  配置是否将以本地方式缓存最终用户许可证（Eul）。
public bool CanCacheLicenses （） const  |  获取是否在本地缓存最终用户许可证（Eul）。
  
## <a name="members"></a>成員
  
### <a name="settings-function"></a>Settings 函数
FileProfile：： Settings 构造函数。

参数：  
* **mipContext**：全局上下文设置 


* **cacheStorageType**：将任何缓存的状态存储在内存中或磁盘上 


* **authDelegate**：用于获取身份验证令牌的身份验证委托 


* **consentDelegate**：用于获取访问外部资源的用户权限的委托 


* **观察**者：将接收与 FileProfile 相关的事件通知的观察程序实例


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType 函数
获取缓存是存储在内存中还是存储在磁盘上。

  
**返回**：使用的存储类型
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 函数
获取用于获取身份验证令牌的身份验证委托。

  
**返回结果**：用于获取身份验证令牌的身份验证委托
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate 函数
获取用于请求用户许可连接到服务的许可委托。

  
**返回结果**：用户请求用户同意的同意委托
  
### <a name="getobserver-function"></a>GetObserver 函数
获取接收与 FileProfile 相关的事件通知的观察程序。

  
**返回**：接收与 FileProfile 相关的事件通知的观察程序
  
### <a name="getmipcontext-function"></a>GetMipContext 函数
获取表示所有配置文件的共享状态的 MIP 上下文。

  
**返回**： MIP 上下文
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 函数
获取应用程序提供的 HTTP 委托（若有）。

  
**返回结果**：要用于 HTTP 操作的 HTTP 委托
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 函数
使用客户端自己的替代默认 HTTP 堆栈。

参数：  
* **httpDelegate**：客户端应用程序实现的 HTTP 回叫接口


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 函数
获取应用程序提供的 TaskDispatcher 委托（如果有）。

  
**返回**：用于执行异步任务的 TaskDispatcher 委托
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 函数
用客户端自己的 asynchonous 重写默认的任务分派处理。

参数：  
* **taskDispatcherDelegate**：任务分派由客户端应用程序实现的回调接口


任务可以引用阻止其析构的配置文件对象，taskdispatcher 不应共享队列。
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置会话 ID。

参数：  
* **sessionId**：将用于关联日志/遥测的会话 ID


  
### <a name="getsessionid-function"></a>GetSessionId 函数
获取会话 ID。

  
**返回结果**：将用于关联日志/遥测的会话 ID
  
### <a name="setcancachelicenses-function"></a>SetCanCacheLicenses 函数
配置是否将以本地方式缓存最终用户许可证（Eul）。

参数：  
* **canCacheLicenses**：打开受保护的内容时，引擎是否应缓存许可证


如果为 true，则打开受保护的内容将在本地缓存关联的许可证。 如果为 false，则打开受保护的内容将始终执行 HTTP 操作以从 RMS 服务获取许可证。
  
### <a name="cancachelicenses-function"></a>CanCacheLicenses 函数
获取是否在本地缓存最终用户许可证（Eul）。

  
**返回**：许可证缓存配置