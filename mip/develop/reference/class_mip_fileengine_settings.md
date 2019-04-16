---
title: class mip::FileEngine::Settings
description: 记录 mip::fileengine 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2481ee7d42f00ce5b33529b15e17b22ba6556b0e
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574034"
---
# <a name="class-mipfileenginesettings"></a>class mip::FileEngine::Settings 
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 （const std:: string & engineId，const std:: string & clientData，const std:: string 和区域设置，bool loadSensitivityTypes）  |  用于加载现有引擎的 [FileEngine::Settings](class_mip_fileengine_settings.md) 构造函数。
公共设置 (const Identity & 标识、 const std:: string & clientData、 const std:: string 和区域设置、 bool loadSensitivityTypes)  |  用于新建引擎的 [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。
public const std::string& GetEngineId() const  |  返回引擎 ID。
public void SetEngineId(const std::string& id)  |  设置引擎 ID。
public const Identity& GetIdentity() const  |  返回引擎[标识](class_mip_identity.md)。
public void SetIdentity(const Identity& identity)  |  设置引擎标识。
public const std::string& GetClientData() const  |  返回引擎客户端数据。
public const std::string& GetLocale() const  |  返回引擎区域设置。
public void SetCustomSettings (const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& 值)  |  设置用于测试和试验的名称/值对列表。
public const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& GetCustomSettings() 常量  |  获取用于测试和试验的名称/值对列表。
public void SetSessionId(const std::string& sessionId)  |  设置引擎会话 ID。
public const std::string& GetSessionId() const  |  返回引擎会话 ID。
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  设置用于指定云边界的保护云终结点基 URL。
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  获取保护云终结点基 url。
public void SetPolicyCloudEndpointBaseUrl(const std::string& policyCloudEndpointBaseUrl)  |  设置的策略云终结点基 url，用于指定云边界。
public const std:: string & GetPolicyCloudEndpointBaseUrl() 常量  |  获取策略的云终结点基 url。
public void SetProtectionOnlyEngine(const bool protectionOnly)  |  设置仅保护引擎指示器 - 无策略/标签。
public const bool IsProtectionOnlyEngine() const  |  返回仅保护引擎指示器 - 无策略/标签。
公共 bool IsLoadSensitivityTypesEnabled() 常量  |  获取指示是否启用了负载敏感度标签的标志。
  
## <a name="members"></a>成員
  
### <a name="settings-function"></a>设置函数
用于加载现有引擎的 [FileEngine::Settings](class_mip_fileengine_settings.md) 构造函数。

参数：  
* **engineId**:将其设置为 AddEngineAsync 生成的唯一引擎 ID。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **loadSensitivityTypes**:可选标志，指示引擎加载时应加载还自定义敏感类型，当将自定义敏感类型，以及策略更改的更新上调用，则返回 true OnPolicyChange 观察者的配置文件。 如果 false ListSensitivityTypes 调用将始终返回空列表。


  
### <a name="settings-function"></a>设置函数
用于新建引擎的 [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。

参数：  
* **标识**:[标识](class_mip_identity.md)与新的引擎关联的用户的信息。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **loadSensitivityTypes**:可选标志，指示引擎加载时应加载还自定义敏感类型，当将自定义敏感类型，以及策略更改的更新上调用，则返回 true OnPolicyChange 观察者的配置文件。 如果 false ListSensitivityTypes 调用将始终返回空列表。


  
### <a name="getengineid-function"></a>GetEngineId 函数
返回引擎 ID。
  
### <a name="setengineid-function"></a>SetEngineId 函数
设置引擎 ID。

参数：  
* **ID**：引擎 ID。


  
### <a name="getidentity-function"></a>GetIdentity 函数
返回引擎[标识](class_mip_identity.md)。
  
### <a name="setidentity-function"></a>SetIdentity 函数
设置引擎标识。
  
### <a name="getclientdata-function"></a>GetClientData 函数
返回引擎客户端数据。
  
### <a name="getlocale-function"></a>GetLocale 函数
返回引擎区域设置。
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 函数
设置用于测试和试验的名称/值对列表。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取用于测试和试验的名称/值对列表。
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置引擎会话 ID。
  
### <a name="getsessionid-function"></a>GetSessionId 函数
返回引擎会话 ID。
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl function
设置用于指定云边界的保护云终结点基 URL。

参数：  
* **protectionCloudEndpointBaseUrl**:与保护终结点相关联的基 url


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl function
获取保护云终结点基 url。

  
**返回**:与保护终结点相关联的基 url
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl 函数
设置的策略云终结点基 url，用于指定云边界。

参数：  
* **policyCloudEndpointBaseUrl**:与策略终结点相关联的基 url


  
### <a name="getpolicycloudendpointbaseurl-function"></a>GetPolicyCloudEndpointBaseUrl 函数
获取策略的云终结点基 url。

  
**返回**:与策略终结点相关联的基 url
  
### <a name="setprotectiononlyengine-function"></a>SetProtectionOnlyEngine 函数
设置仅保护引擎指示器 - 无策略/标签。
  
### <a name="isprotectiononlyengine-function"></a>IsProtectionOnlyEngine 函数
返回仅保护引擎指示器 - 无策略/标签。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 函数
获取指示是否启用了负载敏感度标签的标志。

  
**返回**:如果启用，否则返回 false，则为 true。