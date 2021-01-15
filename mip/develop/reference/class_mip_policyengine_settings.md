---
title: 类 PolicyEngine：： Settings
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 policyengine：： settings 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 4e40bccefa523e18dfdb99a8ef0adacad9f9d4cf
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215096"
---
# <a name="class-policyenginesettings"></a>类 PolicyEngine：： Settings 
定义与 PolicyEngine 关联的设置。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 (const std：： string& engineId，const std：： shared_ptr \<AuthDelegate\>& authDelegate，const std：： string& clientData，const std：： string& locale，Bool loadSensitivityTypes)   |  用于加载现有引擎的 PolicyEngine::Settings 构造函数。
公共设置 (const Identity& Identity，const std：： shared_ptr \<AuthDelegate\>& authDelegate，const std：： string& clientData，const std：： string& locale，Bool loadSensitivityTypes)   |  用于新建引擎的 PolicyEngine::Settings 构造函数。
public const std::string& GetEngineId() const  |  获取引擎 ID。
public void SetEngineId(const std::string& id)  |  设置引擎 ID。
public const Identity& GetIdentity() const  |  获取标识对象。
public void SetIdentity(const Identity& identity)  |  设置标识对象。
public const std::string& GetClientData() const  |  获取设置中设置的客户端数据。
public void SetClientData(const std::string& clientData)  |  设置客户端数据字符串。
public const std::string& GetLocale() const  |  获取设置中设置的区域设置。
public void SetCustomSettings (const std：： vector \<std::pair\<std::string, std::string\> \>& customSettings)   |  设置自定义设置，用于功能访问控制和测试。
public const std：： vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings ( # A2 const  |  获取用于功能访问控制和测试的自定义设置。
public void SetSessionId(const std::string& sessionId)  |  设置用于客户端定义遥测的会话 ID。
public const std::string& GetSessionId() const  |  获取唯一标识符形式的会话 ID。
public bool IsLoadSensitivityTypesEnabled ( # A1 const  |  获取一个标志，该标志指示是否启用了加载敏感度标签。
公有 void SetCloud (云云)   |  选择性地设置目标云。
公有 Cloud GetCloud ( # A1 const  |  获取所有服务请求使用的目标云。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  为自定义云设置云终结点基 URL。
public const std::string& GetCloudEndpointBaseUrl() const  |  获取所有服务请求使用的云基 URL（如果已指定）。
public void SetDelegatedUserEmail (const std：： string& delegatedUserEmail)   |  设置委派的用户。
public const std：： string& GetDelegatedUserEmail ( # A2 const  |  获取委托的用户。
public void SetLabelFilter (const std：： vector \<LabelFilterType\>& deprecatedLabelFilters)   |  设置标签筛选器。
public const std：： vector \<LabelFilterType\>& GetLabelFilter ( # A2 const  |  获取通过弃用的函数 SetLabelFilter 设置的标签筛选器。
public void ConfigureFunctionality (FunctionalityFilterType functionalityFilterType，bool 已启用)   |  启用或禁用功能。
public const std：： map \<FunctionalityFilterType, bool\>& GetConfiguredFunctionality ( # A2 const  |  获取已配置的功能。
public void SetVariableTextMarkingType (VariableTextMarkingType variableTextMarkingType)   |  设置变量文本标记类型。
public VariableTextMarkingType GetVariableTextMarkingType ( # A1 const  |  获取变量文本标记类型。
public void SetAuthDelegate (const std：： shared_ptr \<AuthDelegate\>& authDelegate)   |  设置引擎身份验证委托。
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  获取引擎身份验证委托。
  
## <a name="members"></a>成员
  
### <a name="settings-function"></a>Settings 函数
用于加载现有引擎的 PolicyEngine::Settings 构造函数。

参数：  
* **engineId**：将它设置为 AddEngineAsync 生成或自生成的唯一引擎 ID。 重新加载现有引擎时，将重用此 ID，否则将创建一个新引擎。 


* **authDelegate**： SDK 用于获取身份验证令牌的身份验证委托，将重写 PolicyProfile：： Settings：： authDelegate （如果两者都提供） 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **可选**：指示在加载引擎时应加载自定义敏感性类型的标志，如果在对自定义敏感度类型的更新以及策略更改时调用配置文件上的 OnPolicyChange 观察程序，则为。 如果为 false，则 ListSensitivityTypes 调用将始终返回一个空列表。


  
### <a name="settings-function"></a>Settings 函数
用于新建引擎的 PolicyEngine::Settings 构造函数。

参数：  
* **identity**：与新引擎关联的用户的标识信息。 


* **authDelegate**： SDK 用于获取身份验证令牌的身份验证委托，将重写 PolicyProfile：： Settings：： authDelegate （如果两者都提供） 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **可选**：指示在加载引擎时应加载自定义敏感性类型的标志，如果在对自定义敏感度类型的更新以及策略更改时调用配置文件上的 OnPolicyChange 观察程序，则为。 如果为 false，则 ListSensitivityTypes 调用将始终返回一个空列表。


  
### <a name="getengineid-function"></a>GetEngineId 函数
获取引擎 ID。

  
**返回结果**：标识引擎的唯一字符串。
  
### <a name="setengineid-function"></a>SetEngineId 函数
设置引擎 ID。

参数：  
* **ID**：引擎 ID。


  
### <a name="getidentity-function"></a>GetIdentity 函数
获取标识对象。

  
**返回结果**：对设置对象中的标识的引用。 
  
另请参阅：mip::Identity
  
### <a name="setidentity-function"></a>SetIdentity 函数
设置标识对象。

参数：  
* **标识**：用户的唯一标识。 


  
另请参阅：mip::Identity
  
### <a name="getclientdata-function"></a>GetClientData 函数
获取设置中设置的客户端数据。

  
**返回结果**：客户端指定的数据的字符串。
  
### <a name="setclientdata-function"></a>SetClientData 函数
设置客户端数据字符串。

参数：  
* **clientData**：用户指定的数据。


  
### <a name="getlocale-function"></a>GetLocale 函数
获取设置中设置的区域设置。

  
**返回结果**：区域设置。
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 函数
设置自定义设置，用于功能访问控制和测试。

参数：  
* **customSettings**：名称/值对列表。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取用于功能访问控制和测试的自定义设置。

  
**返回结果**：名称/值对列表。
  
### <a name="setsessionid-function"></a>SetSessionId 函数
设置用于客户端定义遥测的会话 ID。

参数：  
* **sessionId**：连接遥测事件的唯一字符串。


  
### <a name="getsessionid-function"></a>GetSessionId 函数
获取唯一标识符形式的会话 ID。

  
**返回结果**：会话 ID。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 函数
获取一个标志，该标志指示是否启用了加载敏感度标签。

  
**返回**：如果启用，则为 True; 否则为 false。
  
### <a name="setcloud-function"></a>SetCloud 函数
选择性地设置目标云。

参数：  
* **云**：云


如果未指定 cloud，则默认为 "商用云"。
  
### <a name="getcloud-function"></a>GetCloud 函数
获取所有服务请求使用的目标云。

  
**返回**： Cloud
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 函数
为自定义云设置云终结点基 URL。

参数：  
* **cloudEndpointBaseUrl**：所有服务请求使用的基 URL（例如，“https://dataservice.protection.outlook.com”）


此值将仅被读取，并且必须设置为 Cloud = Custom
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 函数
获取所有服务请求使用的云基 URL（如果已指定）。

  
**返回结果**：基 URL
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 函数
设置委派的用户。

参数：  
* **delegatedUserEmail**：委派电子邮件。


当正在进行身份验证的用户/应用程序代表其他用户时，将指定委派的用户
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 函数
获取委托的用户。

  
**返回**：已委派的用户在进行身份验证的用户/应用程序代表其他用户时指定了委派的用户
  
### <a name="setlabelfilter-function"></a>SetLabelFilter 函数
设置标签筛选器。

参数：  
* **labelFilter**：标签筛选器。


标签默认为 "筛选范围"，此 api 允许按可能的操作进行筛选。 如果未设置 HyokProtection 和 DoubleKeyProtection，则进行筛选。
  
### <a name="getlabelfilter-function"></a>GetLabelFilter 函数
获取通过弃用的函数 SetLabelFilter 设置的标签筛选器。

  
**返回**：标签筛选器。
标签默认为 "筛选范围"，此 api 允许按可能的操作进行筛选。
  
### <a name="configurefunctionality-function"></a>ConfigureFunctionality 函数
启用或禁用功能。

参数：  
* **functionalityFilterType**：功能的类型。 


* **enabled**：若要启用，则为 True，禁用 false


默认情况下，HyokProtection、DoubleKeyProtection、DoubleKeyUserDefinedProtection 处于禁用状态，并且必须启用
  
### <a name="getconfiguredfunctionality-function"></a>GetConfiguredFunctionality 函数
获取已配置的功能。

  
**返回**：将类型映射到布尔值，指示是否已启用该类型
  
### <a name="setvariabletextmarkingtype-function"></a>SetVariableTextMarkingType 函数
设置变量文本标记类型。

参数：  
* **variableTextMarkingType**：标记类型的变量文本。


  
### <a name="getvariabletextmarkingtype-function"></a>GetVariableTextMarkingType 函数
获取变量文本标记类型。

  
**返回**：变量文本标记类型。
  
### <a name="setauthdelegate-function"></a>SetAuthDelegate 函数
设置引擎身份验证委托。

参数：  
* **authDelegate**：身份验证委托


  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 函数
获取引擎身份验证委托。

  
**返回**：引擎身份验证委托。