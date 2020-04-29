---
title: 类 FileProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 fileprofile：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: cf5950b37953dc32100e8ae2700b6111783cb612
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762931"
---
# <a name="class-fileprofile"></a>类 FileProfile 
FileProfile 类是用于使用 Microsoft 信息保护操作的根类。
典型的应用程序将仅需要一个配置文件。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  返回配置文件的设置。
public std：： shared_ptr\<AsyncControl\> ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public std：： shared_ptr\<AsyncControl\> UnloadEngineAsync （const std：： string& id，const std：： shared_ptr\<void\>& 上下文）  |  开始卸载具有给定 ID 的文件引擎。
public std：： shared_ptr\<AsyncControl\> AddEngineAsync （Const FileEngine：： settings& settings，const std：： shared_ptr\<void\>& 上下文）  |  开始向配置文件添加新文件引擎。
public std：： shared_ptr\<AsyncControl\> DeleteEngineAsync （const std：： string& id，const std：： shared_ptr\<void\>& 上下文）  |  开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。
public void AcquirePolicyAuthToken （Cloud cloud，const std：： shared_ptr\<authDelegate\>& AuthDelegate） const  |  触发策略的身份验证回叫。
  
## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
返回配置文件的设置。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

  
**返回**： Async control 对象。
FileProfile::Observer 将在成功或失败时调用。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 函数
开始卸载具有给定 ID 的文件引擎。

  
**返回**： Async control 对象。
FileProfile::Observer 将在成功或失败时调用。
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新文件引擎。

  
**返回**： Async control 对象。
FileProfile::Observer 将在成功或失败时调用。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。

  
**返回**： Async control 对象。
FileProfile::Observer 将在成功或失败时调用。
  
### <a name="acquirepolicyauthtoken-function"></a>AcquirePolicyAuthToken 函数
触发策略的身份验证回叫。

参数：  
* **云**： Azure 云 


* **authDelegate**：将调用的身份验证回调


MIP 将不会缓存或使用 auth 委托返回的值执行任何其他操作。 对于在 MIP 请求身份验证令牌之前未 "登录" 的应用程序，建议使用此函数。 它允许应用程序在 MIP 实际需要一个令牌之前提取令牌。