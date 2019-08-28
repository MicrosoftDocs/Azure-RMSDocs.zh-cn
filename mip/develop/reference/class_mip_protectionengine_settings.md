---
title: 类 mip::ProtectionEngine::Settings
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionengine 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: a083d037fcfb48ae9eee5df67fb78d53fcb5490a
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057603"
---
# <a name="class-mipprotectionenginesettings"></a>类 mip::ProtectionEngine::Settings 
[ProtectionEngine](class_mip_protectionengine.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_protectionengine_settings.md)。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  用于新建引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  用于加载现有引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。
public const std::string& GetEngineId() const  |  获取引擎 ID。
public void SetEngineId(const std::string& engineId)  |  设置引擎 ID。
public const Identity& GetIdentity() const  |  获取与引擎关联的用户[标识](class_mip_identity.md)。
public void SetIdentity(const Identity& identity)  |  设置与引擎关联的用户[标识](class_mip_identity.md)。
public const std::string& GetClientData() const  |  获取客户端指定的自定义数据。
public void SetClientData(const std::string& clientData)  |  设置客户端指定的自定义数据。
public const std::string& GetLocale() const  |  获取写入引擎数据所用的区域设置。
public void SetCustomSettings (const std:: vector\<std::p 风\<std:: string、std:: string\>\>& 值)  |  设置用于测试和试验的名称/值对。
public const std:: vector\<std::p air\<std:: string, std:: string\>\>& GetCustomSettings () const  |  获取用于测试和试验的名称/值对。
public void SetSessionId(const std::string& sessionId)  |  设置用于关联日志记录/遥测的引擎会话 ID。
public const std::string& GetSessionId() const  |  获取引擎会话 ID。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  （可选）设置云终结点基 URL。
public const std::string& GetCloudEndpointBaseUrl() const  |  获取所有服务请求使用的云基 URL（如果已指定）。
  
## <a name="members"></a>成员
  
### <a name="settings-function"></a>Settings 函数
用于新建引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。

参数：  
* **标识**:将与[ProtectionEngine](class_mip_protectionengine.md)关联的[标识](class_mip_identity.md)


* **clientData**：可自定义客户端数据，不仅卸载时可存储在引擎中，而且还能从加载的引擎中检索。 


* **区域设置**:将在此区域设置中提供引擎输出。


  
### <a name="settings-function"></a>Settings 函数
用于加载现有引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。

参数：  
* **engineId**:将加载的引擎的唯一标识符 


* **clientData**：可自定义客户端数据，不仅卸载时可存储在引擎中，而且还能从加载的引擎中检索。 


* **区域设置**:将在此区域设置中提供引擎输出。


  
### <a name="getengineid-function"></a>GetEngineId 函数
获取引擎 ID。

  
**返回**:引擎 ID
  
### <a name="setengineid-function"></a>SetEngineId 函数
设置引擎 ID。

参数：  
* **engineId**：引擎 ID。


  
### <a name="getidentity-function"></a>GetIdentity 函数
获取与引擎关联的用户[标识](class_mip_identity.md)。

  
**返回**:与引擎关联的用户[标识](class_mip_identity.md)
  
### <a name="setidentity-function"></a>SetIdentity 函数
设置与引擎关联的用户[标识](class_mip_identity.md)。

参数：  
* **标识**:与引擎关联的用户[标识](class_mip_identity.md)


  
### <a name="getclientdata-function"></a>GetClientData 函数
获取客户端指定的自定义数据。

  
**返回**:客户端指定的自定义数据
  
### <a name="setclientdata-function"></a>SetClientData 函数
设置客户端指定的自定义数据。

参数：  
* **Custom**：客户端指定的数据


  
### <a name="getlocale-function"></a>GetLocale 函数
获取写入引擎数据所用的区域设置。

  
**返回**:将写入引擎数据的区域设置
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 函数
设置用于测试和试验的名称/值对。

参数：  
* **customSettings**:用于测试和试验的名称/值对


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取用于测试和试验的名称/值对。

  
**返回**:用于测试和试验的名称/值对
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置用于关联日志记录/遥测的引擎会话 ID。

参数：  
* **sessionId**:用于关联日志记录/遥测数据的引擎会话 ID


  
### <a name="getsessionid-function"></a>GetSessionId 函数
获取引擎会话 ID。

  
**返回**:引擎会话 ID
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 函数
（可选）设置云终结点基 URL。

参数：  
* **cloudEndpointBaseUrl**：所有服务请求使用的基 URL（例如，“https://api.aadrm.com”）


如果未指定基 URL，则将通过 DNS 查找引擎标识的域来确定它。
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 函数
获取所有服务请求使用的云基 URL（如果已指定）。

  
**返回**:基 URL