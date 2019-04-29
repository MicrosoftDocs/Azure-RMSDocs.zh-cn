---
title: class mip::PolicyEngine::Settings
description: 记录 mip::policyengine 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3ffd4b3e86192786309739add907a724acdaffa5
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60174181"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
定义与 [PolicyEngine](class_mip_policyengine.md) 关联的设置。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 （const std:: string & engineId，const std:: string & clientData，const std:: string 和区域设置，bool loadSensitivityTypes）  |  用于加载现有引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。
公共设置 (const Identity & 标识、 const std:: string & clientData、 const std:: string 和区域设置、 bool loadSensitivityTypes)  |  用于新建引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。
public const std::string& GetEngineId() const  |  获取引擎 ID。
public void SetEngineId(const std::string& id)  |  设置引擎 ID。
public const Identity& GetIdentity() const  |  获取[标识](class_mip_identity.md)对象。
public void SetIdentity(const Identity& identity)  |  设置[标识](class_mip_identity.md)对象。
public const std::string& GetClientData() const  |  获取设置中设置的客户端数据。
public void SetClientData(const std::string& clientData)  |  设置客户端数据字符串。
public const std::string& GetLocale() const  |  获取设置中设置的区域设置。
public void SetCustomSettings (const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& customsettings:)  |  设置自定义设置，用于功能访问控制和测试。
public const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& GetCustomSettings() 常量  |  获取用于功能访问控制和测试的自定义设置。
public void SetSessionId(const std::string& sessionId)  |  设置用于客户端定义遥测的会话 ID。
public const std::string& GetSessionId() const  |  获取唯一标识符形式的会话 ID。
公共 bool IsLoadSensitivityTypesEnabled() 常量  |  获取指示是否启用了负载敏感度标签的标志。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  （可选）设置云终结点基 URL。
public const std::string& GetCloudEndpointBaseUrl() const  |  获取所有服务请求使用的云基 URL（如果已指定）。
  
## <a name="members"></a>成員
  
### <a name="settings-function"></a>设置函数
用于加载现有引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。

参数：  
* **engineId**:将其设置为 AddEngineAsync 生成或自生成的唯一引擎 ID。 重新加载现有引擎时，将重用此 ID，否则将创建一个新引擎。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **可选**： 标志，指示引擎加载时应加载还自定义敏感类型，当将自定义敏感类型，以及策略更改的更新上调用，则返回 true OnPolicyChange 观察者的配置文件。 如果 false ListSensitivityTypes 调用将始终返回空列表。


  
### <a name="settings-function"></a>设置函数
用于新建引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。

参数：  
* **标识**:[标识](class_mip_identity.md)与新的引擎关联的用户的信息。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **可选**： 标志，指示引擎加载时应加载还自定义敏感类型，当将自定义敏感类型，以及策略更改的更新上调用，则返回 true OnPolicyChange 观察者的配置文件。 如果 false ListSensitivityTypes 调用将始终返回空列表。


  
### <a name="getengineid-function"></a>GetEngineId 函数
获取引擎 ID。

  
**返回**:标识引擎的唯一字符串。
  
### <a name="setengineid-function"></a>SetEngineId 函数
设置引擎 ID。

参数：  
* **ID**：引擎 ID。


  
### <a name="getidentity-function"></a>GetIdentity 函数
获取[标识](class_mip_identity.md)对象。

  
**返回**:对设置对象中的标识的引用。 
  
**另请参阅**: [mip::Identity](class_mip_identity.md)
  
### <a name="setidentity-function"></a>SetIdentity 函数
设置[标识](class_mip_identity.md)对象。

参数：  
* **identity**：用户的唯一标识。 


  
**另请参阅**: [mip::Identity](class_mip_identity.md)
  
### <a name="getclientdata-function"></a>GetClientData 函数
获取设置中设置的客户端数据。

  
**返回**:一个指定客户端的数据的字符串。
  
### <a name="setclientdata-function"></a>SetClientData 函数
设置客户端数据字符串。

参数：  
* **clientData**：用户指定的数据。


  
### <a name="getlocale-function"></a>GetLocale 函数
获取设置中设置的区域设置。

  
**返回**:区域设置。
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 函数
设置自定义设置，用于功能访问控制和测试。

参数：  
* **customsettings:**:名称/值对列表。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取用于功能访问控制和测试的自定义设置。

  
**返回**:名称/值对列表。
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置用于客户端定义遥测的会话 ID。

参数：  
* **sessionId**：连接遥测事件的唯一字符串。


  
### <a name="getsessionid-function"></a>GetSessionId 函数
获取唯一标识符形式的会话 ID。

  
**返回**:会话 id。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 函数
获取指示是否启用了负载敏感度标签的标志。

  
**返回**:如果启用，否则返回 false，则为 true。
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl function
（可选）设置云终结点基 URL。

参数：  
* **cloudEndpointBaseUrl**：所有服务请求使用的基 URL（例如，“https://dataservice.protection.outlook.com”）


  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl function
获取所有服务请求使用的云基 URL（如果已指定）。

  
**返回**:基 URL