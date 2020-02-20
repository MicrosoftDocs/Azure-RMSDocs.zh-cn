---
title: 类 mip::ProtectionEngine::Settings
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionengine 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 71f428667bf485d0abd4f953aa2d94181b1bd8f1
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486879"
---
# <a name="class-mipprotectionenginesettings"></a>类 mip::ProtectionEngine::Settings 
ProtectionEngine 在其创建期间及其整个生存期内使用的设置。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  用于创建新引擎的 ProtectionEngine：： Settings 构造函数。
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  用于加载现有引擎的 ProtectionEngine：： Settings 构造函数。
public const std::string& GetEngineId() const  |  获取引擎 ID。
public void SetEngineId(const std::string& engineId)  |  设置引擎 ID。
public const Identity& GetIdentity() const  |  获取与引擎关联的用户标识。
public void SetIdentity(const Identity& identity)  |  设置与引擎关联的用户标识。
public const std::string& GetClientData() const  |  获取客户端指定的自定义数据。
public void SetClientData(const std::string& clientData)  |  设置客户端指定的自定义数据。
public const std::string& GetLocale() const  |  获取写入引擎数据所用的区域设置。
public void SetCustomSettings （const std：： vector\<std：:p 空中\<std：： string，std：： string\>\>& 值）  |  设置用于测试和试验的名称/值对。
public const std：： vector\<std：:p air\<std：： string，std：： string\>\>& GetCustomSettings （） const  |  获取用于测试和试验的名称/值对。
public void SetSessionId(const std::string& sessionId)  |  设置用于关联日志记录/遥测的引擎会话 ID。
public const std::string& GetSessionId() const  |  获取引擎会话 ID。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  （可选）设置云终结点基 URL。
public const std::string& GetCloudEndpointBaseUrl() const  |  获取所有服务请求使用的云基 URL（如果已指定）。
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Settings 函数
用于创建新引擎的 ProtectionEngine：： Settings 构造函数。

参数：  
* **标识**：将与 ProtectionEngine 关联的标识


* **clientData**：可自定义客户端数据，不仅卸载时可存储在引擎中，而且还能从加载的引擎中检索。 


* **locale**：将在此区域设置中提供引擎输出。


  
### <a name="settings-function"></a>Settings 函数
用于加载现有引擎的 ProtectionEngine：： Settings 构造函数。

参数：  
* **engineId**：将加载的引擎的唯一标识符 


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
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 函数
（可选）设置云终结点基 URL。

参数：  
* **cloudEndpointBaseUrl**：所有服务请求使用的基 URL（例如，“https://api.aadrm.com”）


如果未指定基 URL，则将通过 DNS 查找引擎标识的域来确定它。
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 函数
获取所有服务请求使用的云基 URL（如果已指定）。

  
**返回结果**：基 URL