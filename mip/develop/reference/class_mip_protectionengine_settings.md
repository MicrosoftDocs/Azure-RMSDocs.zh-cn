---
title: 类 mip::ProtectionEngine::Settings
description: 记录 mip::protectionengine 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d874e57806ecf2ee98fa41eb3b655e9525ed8362
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333748"
---
# <a name="class-mipprotectionenginesettings"></a>类 mip::ProtectionEngine::Settings 
[ProtectionEngine](class_mip_protectionengine.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_protectionengine_settings.md)。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  用于新建引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  用于加载现有引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。
public const std::string& GetEngineId() const  |  获取引擎 ID。
public void SetEngineId(const std::string& engineId)  |  设置引擎 ID。
public const Identity& GetIdentity() const  |  获取用户[标识](class_mip_identity.md)与引擎相关联。
public void SetIdentity(const Identity& identity)  |  设置的用户[标识](class_mip_identity.md)与引擎相关联。
public const std::string& GetClientData() const  |  获取客户端指定的自定义数据。
public void SetClientData(const std::string& clientData)  |  设置客户端指定的自定义数据。
public const std::string& GetLocale() const  |  获取写入引擎数据所用的区域设置。
public void SetCustomSettings (const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& 值)  |  设置用于测试和试验的名称/值对。
public const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& GetCustomSettings() 常量  |  获取用于测试和试验的名称/值对。
public void SetSessionId(const std::string& sessionId)  |  设置用于关联日志记录/遥测的引擎会话 ID。
public const std::string& GetSessionId() const  |  获取引擎会话 ID。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  （可选）设置云终结点基 URL。
public const std::string& GetCloudEndpointBaseUrl() const  |  获取所有服务请求使用的云基 URL（如果已指定）。
  
## <a name="members"></a>成員
  
### <a name="settings-function"></a>设置函数
用于新建引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。

参数：  
* **标识**:[标识](class_mip_identity.md)，将关联的[ProtectionEngine](class_mip_protectionengine.md)


* **clientData**：可自定义客户端数据，不仅卸载时可存储在引擎中，而且还能从加载的引擎中检索。 


* **区域设置**:将在此区域设置中提供引擎输出。


  
### <a name="settings-function"></a>设置函数
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
获取用户[标识](class_mip_identity.md)与引擎相关联。

  
**返回**:用户[标识](class_mip_identity.md)与引擎关联
  
### <a name="setidentity-function"></a>SetIdentity 函数
设置的用户[标识](class_mip_identity.md)与引擎相关联。

参数：  
* **标识**:用户[标识](class_mip_identity.md)与引擎关联


  
### <a name="getclientdata-function"></a>GetClientData 函数
获取客户端指定的自定义数据。

  
**返回**:指定的客户端的自定义数据
  
### <a name="setclientdata-function"></a>SetClientData 函数
设置客户端指定的自定义数据。

参数：  
* **Custom**：客户端指定的数据


  
### <a name="getlocale-function"></a>GetLocale 函数
获取写入引擎数据所用的区域设置。

  
**返回**:数据将写入哪个引擎中的区域设置
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 函数
设置用于测试和试验的名称/值对。

参数：  
* **customsettings:**:名称/值对用于测试和试验


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取用于测试和试验的名称/值对。

  
**返回**:名称/值对用于测试和试验
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置用于关联日志记录/遥测的引擎会话 ID。

参数：  
* **sessionId**:引擎会话 ID，以便进行日志记录/遥测关联


  
### <a name="getsessionid-function"></a>GetSessionId 函数
获取引擎会话 ID。

  
**返回**:引擎会话 ID
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl function
（可选）设置云终结点基 URL。

参数：  
* **cloudEndpointBaseUrl**：所有服务请求使用的基 URL（例如，“https://api.aadrm.com”）


如果未指定基 URL，则将通过 DNS 查找引擎标识的域来确定它。
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl function
获取所有服务请求使用的云基 URL（如果已指定）。

  
**返回**:基 URL
