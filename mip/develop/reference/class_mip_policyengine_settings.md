---
title: class mip::PolicyEngine::Settings
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p olicyengine 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: db96d00d268158b072d2052a5e98f39bf0efa425
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054321"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
定义与 [PolicyEngine](class_mip_policyengine.md) 关联的设置。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 (const std:: string & engineId, const std:: string & clientData, const std:: string & locale, bool loadSensitivityTypes)  |  用于加载现有引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。
公共设置 (常量标识 & Identity, const std:: string & clientData, const std:: string & locale, bool loadSensitivityTypes)  |  用于新建引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。
public const std::string& GetEngineId() const  |  获取引擎 ID。
public void SetEngineId(const std::string& id)  |  设置引擎 ID。
public const Identity& GetIdentity() const  |  获取[标识](class_mip_identity.md)对象。
public void SetIdentity(const Identity& identity)  |  设置[标识](class_mip_identity.md)对象。
public const std::string& GetClientData() const  |  获取设置中设置的客户端数据。
public void SetClientData(const std::string& clientData)  |  设置客户端数据字符串。
public const std::string& GetLocale() const  |  获取设置中设置的区域设置。
public void SetCustomSettings (const std:: vector\<std::p 风\<std:: string、std:: string\>\>& customSettings)  |  设置自定义设置，用于功能访问控制和测试。
public const std:: vector\<std::p air\<std:: string, std:: string\>\>& GetCustomSettings () const  |  获取用于功能访问控制和测试的自定义设置。
public void SetSessionId(const std::string& sessionId)  |  设置用于客户端定义遥测的会话 ID。
public const std::string& GetSessionId() const  |  获取唯一标识符形式的会话 ID。
public bool IsLoadSensitivityTypesEnabled () const  |  获取一个标志, 该标志指示是否启用了加载敏感度标签。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  （可选）设置云终结点基 URL。
public const std::string& GetCloudEndpointBaseUrl() const  |  获取所有服务请求使用的云基 URL（如果已指定）。
public void SetDelegatedUserEmail (const std:: string & delegatedUserEmail)  |  设置委派的用户。
public const std:: string & GetDelegatedUserEmail () const  |  获取委托的用户。
  
## <a name="members"></a>成员
  
### <a name="settings-function"></a>Settings 函数
用于加载现有引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。

参数：  
* **engineId**:将其设置为 AddEngineAsync 生成的唯一引擎 ID 或自行生成的 ID。 重新加载现有引擎时，将重用此 ID，否则将创建一个新引擎。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **可选**: 指示在加载引擎时应加载自定义敏感性类型的标志, 如果在对自定义敏感度类型的更新以及策略更改时调用配置文件上的 OnPolicyChange 观察程序, 则为。 如果为 false, 则 ListSensitivityTypes 调用将始终返回一个空列表。


  
### <a name="settings-function"></a>Settings 函数
用于新建引擎的 [PolicyEngine::Settings](class_mip_policyengine_settings.md) 构造函数。

参数：  
* **标识**:与新引擎关联的用户的[标识](class_mip_identity.md)信息。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **可选**: 指示在加载引擎时应加载自定义敏感性类型的标志, 如果在对自定义敏感度类型的更新以及策略更改时调用配置文件上的 OnPolicyChange 观察程序, 则为。 如果为 false, 则 ListSensitivityTypes 调用将始终返回一个空列表。


  
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
  
**另请参阅**: [Mip:: Identity](class_mip_identity.md)
  
### <a name="setidentity-function"></a>SetIdentity 函数
设置[标识](class_mip_identity.md)对象。

参数：  
* **identity**：用户的唯一标识。 


  
**另请参阅**: [Mip:: Identity](class_mip_identity.md)
  
### <a name="getclientdata-function"></a>GetClientData 函数
获取设置中设置的客户端数据。

  
**返回**:由客户端指定的数据字符串。
  
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
* **customSettings**:名称/值对列表。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取用于功能访问控制和测试的自定义设置。

  
**返回**:名称/值对列表。
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置用于客户端定义遥测的会话 ID。

参数：  
* **sessionId**：连接遥测事件的唯一字符串。


  
### <a name="getsessionid-function"></a>GetSessionId 函数
获取唯一标识符形式的会话 ID。

  
**返回**:会话 ID。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 函数
获取一个标志, 该标志指示是否启用了加载敏感度标签。

  
**返回**:如果启用, 则为 True; 否则为 false。
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 函数
（可选）设置云终结点基 URL。

参数：  
* **cloudEndpointBaseUrl**：所有服务请求使用的基 URL（例如，“https://dataservice.protection.outlook.com”）


  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 函数
获取所有服务请求使用的云基 URL（如果已指定）。

  
**返回**:基 URL
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 函数
设置委派的用户。

参数：  
* **delegatedUserEmail**: 委派电子邮件。


当正在进行身份验证的用户/应用程序代表其他用户时, 将指定委派的用户
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 函数
获取委托的用户。

  
**返回**:委派的用户当身份验证用户/应用程序代表其他用户操作时, 指定了委派的用户