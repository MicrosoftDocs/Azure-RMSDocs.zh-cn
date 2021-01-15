---
title: 类 ProtectionEngine：： Settings
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 protectionengine：： settings 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 015c806c8830fd932354a1cc6afa33e15b9c1256
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224903"
---
# <a name="class-protectionenginesettings"></a>类 ProtectionEngine：： Settings 
ProtectionEngine 在其创建期间及其整个生存期内使用的 Settings。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 (const Identity& Identity，const std：： shared_ptr \<AuthDelegate\>& authDelegate，const std：： string& clientData，const std：： string& 区域设置)   |  用于新建引擎的 ProtectionEngine::Settings 构造函数。
公共设置 (const std：： string& engineId，const std：： shared_ptr \<AuthDelegate\>& authDelegate，const std：： string& clientData，const std：： string& locale)   |  用于加载现有引擎的 ProtectionEngine::Settings 构造函数。
public const std::string& GetEngineId() const  |  获取引擎 ID。
public void SetEngineId(const std::string& engineId)  |  设置引擎 ID。
public const Identity& GetIdentity() const  |  获取与引擎关联的用户标识。
public void SetIdentity(const Identity& identity)  |  设置与引擎关联的用户标识。
public const std::string& GetClientData() const  |  获取客户端指定的自定义数据。
public void SetClientData(const std::string& clientData)  |  设置客户端指定的自定义数据。
public const std::string& GetLocale() const  |  获取写入引擎数据所用的区域设置。
public void SetCustomSettings (const std：： vector \<std::pair\<std::string, std::string\> \>& 值)   |  设置用于测试和试验的名称/值对。
public const std：： vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings ( # A2 const  |  获取用于测试和试验的名称/值对。
public void SetSessionId(const std::string& sessionId)  |  设置用于关联日志记录/遥测的引擎会话 ID。
public const std::string& GetSessionId() const  |  获取引擎会话 ID。
公有 void SetCloud (云云)   |  选择性地设置目标云。
公有 Cloud GetCloud ( # A1 const  |  获取所有服务请求使用的目标云。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  为自定义云设置云终结点基 URL。
public const std::string& GetCloudEndpointBaseUrl() const  |  获取所有服务请求使用的云基 URL（如果已指定）。
public void SetAuthDelegate (const std：： shared_ptr \<AuthDelegate\>& authDelegate)   |  设置引擎身份验证委托。
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  获取引擎身份验证委托。
public const std：： string& GetUnderlyingApplicationId ( # A2 const  |  获取基础应用程序 ID。
public void SetUnderlyingApplicationId (const std：： string& underlyingApplicationId)   |  设置基础应用程序 ID。
public bool GetAllowCloudServiceOnly ( # A1 const  |  获取是否只允许使用云服务。
public void SetAllowCloudServiceOnly (bool allowCloudServiceOnly)   |  设置是否只允许使用云服务。
  
## <a name="members"></a>成员
  
### <a name="settings-function"></a>Settings 函数
用于新建引擎的 ProtectionEngine::Settings 构造函数。

参数：  
* **identity**：与 ProtectionEngine 关联的标识


* **authDelegate**： SDK 用于获取身份验证令牌的身份验证委托，将重写 PolicyProfile：： Settings：： authDelegate （如果两者都提供） 


* **clientData**：可自定义客户端数据，不仅卸载时可存储在引擎中，而且还能从加载的引擎中检索。 


* **locale**：将在此区域设置中提供引擎输出。


  
### <a name="settings-function"></a>Settings 函数
用于加载现有引擎的 ProtectionEngine::Settings 构造函数。

参数：  
* **engineId**：将加载的引擎的唯一标识符 


* **authDelegate**： SDK 用于获取身份验证令牌的身份验证委托，将重写 PolicyProfile：： Settings：： authDelegate （如果两者都提供） 


* **clientData**：可自定义客户端数据，不仅卸载时可存储在引擎中，而且还能从加载的引擎中检索。 


* **locale**：将在此区域设置中提供引擎输出。


  
### <a name="getengineid-function"></a>GetEngineId 函数
获取引擎 ID。

  
**返回结果**：引擎 ID
  
### <a name="setengineid-function"></a>SetEngineId 函数
设置引擎 ID。

参数：  
* **engineId**：引擎 ID。


  
### <a name="getidentity-function"></a>GetIdentity 函数
获取与引擎关联的用户标识。

  
**返回结果**：与引擎关联的用户标识
  
### <a name="setidentity-function"></a>SetIdentity 函数
设置与引擎关联的用户标识。

参数：  
* **identity**：与引擎关联的用户标识


  
### <a name="getclientdata-function"></a>GetClientData 函数
获取客户端指定的自定义数据。

  
**返回结果**：客户端指定的自定义数据
  
### <a name="setclientdata-function"></a>SetClientData 函数
设置客户端指定的自定义数据。

参数：  
* **Custom**：客户端指定的数据


  
### <a name="getlocale-function"></a>GetLocale 函数
获取写入引擎数据所用的区域设置。

  
**返回结果**：写入引擎数据所用的区域设置
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 函数
设置用于测试和试验的名称/值对。

参数：  
* **customSettings**：用于测试和试验的名称/值对


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取用于测试和试验的名称/值对。

  
**返回结果**：用于测试和试验的名称/值对
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置用于关联日志记录/遥测的引擎会话 ID。

参数：  
* **sessionId**：用于关联日志记录/遥测的引擎会话 ID


  
### <a name="getsessionid-function"></a>GetSessionId 函数
获取引擎会话 ID。

  
**返回结果**：引擎会话 ID
  
### <a name="setcloud-function"></a>SetCloud 函数
选择性地设置目标云。

参数：  
* **云**：云


如果未指定 cloud，则它将由引擎的标识域的 DNS 查找确定（如果可能），否则将回退到全局云。
  
### <a name="getcloud-function"></a>GetCloud 函数
获取所有服务请求使用的目标云。

  
**返回**： Cloud
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 函数
为自定义云设置云终结点基 URL。

参数：  
* **cloudEndpointBaseUrl**：所有服务请求使用的基 URL（例如，“https://api.aadrm.com”）


此值将仅被读取，并且必须设置为 Cloud = Custom
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 函数
获取所有服务请求使用的云基 URL（如果已指定）。

  
**返回结果**：基 URL
  
### <a name="setauthdelegate-function"></a>SetAuthDelegate 函数
设置引擎身份验证委托。

参数：  
* **authDelegate**：身份验证委托


  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 函数
获取引擎身份验证委托。

  
**返回**：引擎身份验证委托。
  
### <a name="getunderlyingapplicationid-function"></a>GetUnderlyingApplicationId 函数
获取基础应用程序 ID。

  
**返回**：基础应用程序 ID
  
### <a name="setunderlyingapplicationid-function"></a>SetUnderlyingApplicationId 函数
设置基础应用程序 ID。

参数：  
* **UnderlyingApplicationId**：基础应用程序 ID。


  
### <a name="getallowcloudserviceonly-function"></a>GetAllowCloudServiceOnly 函数
获取是否只允许使用云服务。

  
**返回**：一个布尔值，指示是否只允许使用云服务
  
### <a name="setallowcloudserviceonly-function"></a>SetAllowCloudServiceOnly 函数
设置是否只允许使用云服务。

参数：  
* **allowCloudServiceOnly**：一个布尔值，指示是否只允许使用云服务

