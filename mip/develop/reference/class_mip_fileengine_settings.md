---
title: class mip::FileEngine::Settings
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: fileengine 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 00ad6058b146f428a65a0697b722e6d3adb5c07d
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884296"
---
# <a name="class-mipfileenginesettings"></a>class mip::FileEngine::Settings 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共设置 (const std:: string & engineId, const std:: string & clientData, const std:: string & locale, bool loadSensitivityTypes)  |  用于加载现有引擎的 [FileEngine::Settings](class_mip_fileengine_settings.md) 构造函数。
公共设置 (常量标识 & Identity, const std:: string & clientData, const std:: string & locale, bool loadSensitivityTypes)  |  用于新建引擎的 [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。
public const std::string& GetEngineId() const  |  返回引擎 ID。
public void SetEngineId(const std::string& id)  |  设置引擎 ID。
public const Identity& GetIdentity() const  |  返回引擎[标识](class_mip_identity.md)。
public void SetIdentity(const Identity& identity)  |  设置引擎标识。
public const std::string& GetClientData() const  |  返回引擎客户端数据。
public const std::string& GetLocale() const  |  返回引擎区域设置。
public void SetCustomSettings (const std:: vector\<std::p 风\<std:: string、std:: string\>\>& 值)  |  设置用于测试和试验的名称/值对列表。
public const std:: vector\<std::p air\<std:: string, std:: string\>\>& GetCustomSettings () const  |  获取用于测试和试验的名称/值对列表。
public void SetSessionId(const std::string& sessionId)  |  设置引擎会话 ID。
public const std::string& GetSessionId() const  |  返回引擎会话 ID。
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  设置用于指定云边界的保护云终结点基 URL。
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  获取保护云终结点基 url。
public void SetPolicyCloudEndpointBaseUrl (const std:: string & policyCloudEndpointBaseUrl)  |  设置用于指定云边界的策略云终结点基 url。
public const std:: string & GetPolicyCloudEndpointBaseUrl () const  |  获取策略云终结点基 url。
public void SetProtectionOnlyEngine (bool protectionOnly)  |  设置仅保护引擎指示器 - 无策略/标签。
public const bool IsProtectionOnlyEngine() const  |  返回仅保护引擎指示器 - 无策略/标签。
public bool IsLoadSensitivityTypesEnabled () const  |  获取一个标志, 该标志指示是否启用了加载敏感度标签。
public void EnablePFile (布尔值)  |  设置指示是否生成 Pfile 的标志。
public const bool IsPFileEnabled ()  |  获取一个标志, 该标志指示是否生成 Pfile。
public void SetDelegatedUserEmail (const std:: string & delegatedUserEmail)  |  设置委派的用户。
public const std:: string & GetDelegatedUserEmail () const  |  获取委托的用户。
  
## <a name="members"></a>成员
  
### <a name="settings-function"></a>Settings 函数
用于加载现有引擎的 [FileEngine::Settings](class_mip_fileengine_settings.md) 构造函数。

参数：  
* **engineId**:将其设置为 AddEngineAsync 生成的唯一引擎 ID。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **loadSensitivityTypes**:可选标志, 指示在加载引擎时应加载自定义敏感性类型, 如果在对自定义敏感度类型的更新以及策略更改时调用配置文件上的 OnPolicyChange 观察程序, 则为。 如果为 false, 则 ListSensitivityTypes 调用将始终返回一个空列表。


  
### <a name="settings-function"></a>Settings 函数
用于新建引擎的 [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。

参数：  
* **标识**:与新引擎关联的用户的[标识](class_mip_identity.md)信息。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。 


* **loadSensitivityTypes**:可选标志, 指示在加载引擎时应加载自定义敏感性类型, 如果在对自定义敏感度类型的更新以及策略更改时调用配置文件上的 OnPolicyChange 观察程序, 则为。 如果为 false, 则 ListSensitivityTypes 调用将始终返回一个空列表。


  
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
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl 函数
设置用于指定云边界的保护云终结点基 URL。

参数：  
* **protectionCloudEndpointBaseUrl**:与保护终结点关联的基 url


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl 函数
获取保护云终结点基 url。

  
**返回**:与保护终结点关联的基 url
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl 函数
设置用于指定云边界的策略云终结点基 url。

参数：  
* **policyCloudEndpointBaseUrl**:与策略终结点关联的基 url


  
### <a name="getpolicycloudendpointbaseurl-function"></a>GetPolicyCloudEndpointBaseUrl 函数
获取策略云终结点基 url。

  
**返回**:与策略终结点关联的基 url
  
### <a name="setprotectiononlyengine-function"></a>SetProtectionOnlyEngine 函数
设置仅保护引擎指示器 - 无策略/标签。
  
### <a name="isprotectiononlyengine-function"></a>IsProtectionOnlyEngine 函数
返回仅保护引擎指示器 - 无策略/标签。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 函数
获取一个标志, 该标志指示是否启用了加载敏感度标签。

  
**返回**:如果启用, 则为 True; 否则为 false。
  
### <a name="enablepfile-function"></a>EnablePFile 函数
设置指示是否生成 Pfile 的标志。
  
### <a name="ispfileenabled-function"></a>IsPFileEnabled 函数
获取一个标志, 该标志指示是否生成 Pfile。

  
**返回**:如果启用, 则为 True; 否则为 false。
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 函数
设置委派的用户。

参数：  
* **delegatedUserEmail**: 委派电子邮件。


当正在进行身份验证的用户/应用程序代表其他用户时, 将指定委派的用户
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 函数
获取委托的用户。

  
**返回**:委派的用户当身份验证用户/应用程序代表其他用户操作时, 指定了委派的用户