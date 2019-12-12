---
title: class mip::PolicyProfile::Settings
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p olicyprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 324b31a9589cff75a758da2936a3aba242fd63c2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560869"
---
# <a name="class-mippolicyprofilesettings"></a>class mip::PolicyProfile::Settings 
PolicyProfile 在其创建期间及其整个生存期内使用的设置。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共设置（const std：： shared_ptr\<MipContext\>& mipContext，CacheStorageType cacheStorageType，const std：： shared_ptr\<AuthDelegate\>& authDelegate，const std：： shared_ptr\<PolicyProfile：： Observer\>& 观察程序）  |  用于配置配置文件的接口。
public CacheStorageType GetCacheStorageType （） const  |  获取缓存是存储在内存中还是存储在磁盘上。
public const std：： shared_ptr\<AuthDelegate\>& GetAuthDelegate （） const  |  获取身份验证委托。
public const std：： shared_ptr\<PolicyProfile：： Observer\>& GetObserver （） const  |  获取事件观察程序。
public std：： shared_ptr\<MipContext\> GetMipContext （） const  |  获取表示所有配置文件的共享状态的 MIP 上下文。
public std：： shared_ptr\<HttpDelegate\> GetHttpDelegate （） const  |  获取应用程序提供的 HTTP 委托（若有）。
public void SetHttpDelegate （const std：： shared_ptr\<HttpDelegate\>& httpDelegate）  |  使用客户端自己的替代默认 HTTP 堆栈。
public std：： shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate （） const  |  获取应用程序提供的 TaskDispatcher 委托（如果有）。
public void SetTaskDispatcherDelegate （const std：： shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate）  |  用客户端自己的 asynchonous 重写默认的任务分派处理。
public void SetSessionId(const std::string& sessionId)  | 尚未记录。
public const std::string& GetSessionId() const  | 尚未记录。
public void SetCustomSettings （const std：： vector\<std：:p air\<std：： string，std：： string\>\>& customSettings）  |  设置自定义设置，用于功能访问控制和测试。
public const std：： vector\<std：:p air\<std：： string，std：： string\>\>& GetCustomSettings （） const  |  获取用于功能访问控制和测试的自定义设置。
public ~Settings()  | 尚未记录。
  
## <a name="members"></a>成員
  
### <a name="settings-function"></a>Settings 函数
用于配置配置文件的接口。

参数：  
* **mipContext**：全局上下文设置 


* **cacheStorageType**：将任何缓存的状态存储在内存中或磁盘上 


* **authDelegate**：SDK 用来获取身份验证令牌的身份验证委托。 


* **观察**程序：一个实现 PolicyProfile：： observer 接口的类。 可以为 nullptr。


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType 函数
获取缓存是存储在内存中还是存储在磁盘上。

  
**返回**：使用的存储类型
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 函数
获取身份验证委托。

  
**返回结果**：身份验证委托。
  
### <a name="getobserver-function"></a>GetObserver 函数
获取事件观察程序。

  
**返回结果**：事件观察程序。
  
### <a name="getmipcontext-function"></a>GetMipContext 函数
获取表示所有配置文件的共享状态的 MIP 上下文。

  
**返回**： MIP 上下文
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 函数
获取应用程序提供的 HTTP 委托（若有）。

  
返回结果：要用于 HTTP 操作的 http 委托
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 函数
使用客户端自己的替代默认 HTTP 堆栈。

参数：  
* httpDelegate：客户端应用程序实现的 http 回叫接口


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate 函数
获取应用程序提供的 TaskDispatcher 委托（如果有）。

  
**返回**：用于执行异步任务的 TaskDispatcher 委托
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate 函数
用客户端自己的 asynchonous 重写默认的任务分派处理。

参数：  
* **taskDispatcherDelegate**：任务分派由客户端应用程序实现的回调接口


任务可以引用阻止其析构的配置文件对象，taskdispatcher 不应共享队列。
  
### <a name="setsessionid-function"></a>SetSessionId 函数
_尚无记录。_

  
### <a name="getsessionid-function"></a>GetSessionId 函数
_尚无记录。_

  
### <a name="setcustomsettings-function"></a>SetCustomSettings 函数
设置自定义设置，用于功能访问控制和测试。

参数：  
* **customSettings**：名称/值对列表。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取用于功能访问控制和测试的自定义设置。

  
**返回结果**：名称/值对列表。
  
### <a name="settings-function"></a>~ Settings 函数
_尚无记录。_
