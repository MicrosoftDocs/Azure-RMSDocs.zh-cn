---
title: 类 mip FileEngine Settings
description: 类 mip FileEngine Settings 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 656ad1cf21a2d761dfb4c857b278b7421ee2b790
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446475"
---
# <a name="class-mipfileenginesettings"></a>class mip::FileEngine::Settings 
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  用于加载现有引擎的 [FileEngine::Settings](class_mip_fileengine_settings.md) 构造函数。
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  用于新建引擎的 [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。
 public const std::string& GetEngineId() const  |  返回引擎 ID。
 public const Identity& GetIdentity() const  |  返回引擎标识。
 public void SetIdentity(const Identity& identity)  |  设置引擎标识。
 public const std::string& GetClientData() const  |  返回引擎客户端数据。
 public const std::string& GetLocale() const  |  返回引擎区域设置。
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  设置用于测试和试验的名称/值对列表。
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  获取用于测试和试验的名称/值对列表。
 public void SetSessionId(const std::string& sessionId)  |  设置引擎会话 ID。
 public const std::string& GetSessionId() const  |  返回引擎会话 ID。
 public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  设置用于指定云边界的保护云终结点基 URL。
 public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  获取 cloudEndpointBaseUrl。
 public void SetProtectionOnlyEngine(const bool protectionOnly)  |  设置仅保护引擎指示器 - 无策略/标签。
 public const bool IsProtectionOnlyEngine() const  |  返回仅保护引擎指示器 - 无策略/标签。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
用于加载现有引擎的 [FileEngine::Settings](class_mip_fileengine_settings.md) 构造函数。

参数：  
* **engineId**：将它设置为 AddEngineAsync 生成的唯一引擎 ID。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。


  
### <a name="settings"></a>设置
用于新建引擎的 [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。

参数：  
* **identity**：与新引擎关联的用户的标识信息。 


* **clientData**：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 


* **locale**：将在此区域设置中提供引擎可本地化输出。


  
### <a name="getengineid"></a>GetEngineId
返回引擎 ID。
  
### <a name="getidentity"></a>GetIdentity
返回引擎标识。
  
### <a name="setidentity"></a>SetIdentity
设置引擎标识。
  
### <a name="getclientdata"></a>GetClientData
返回引擎客户端数据。
  
### <a name="getlocale"></a>GetLocale
返回引擎区域设置。
  
### <a name="setcustomsettings"></a>SetCustomSettings
设置用于测试和试验的名称/值对列表。
  
### <a name="getcustomsettings"></a>GetCustomSettings
获取用于测试和试验的名称/值对列表。
  
### <a name="setsessionid"></a>SetSessionId
设置引擎会话 ID。
  
### <a name="getsessionid"></a>GetSessionId
返回引擎会话 ID。
  
### <a name="setprotectioncloudendpointbaseurl"></a>SetProtectionCloudEndpointBaseUrl
设置用于指定云边界的保护云终结点基 URL。

参数：  
* **protectionCloudEndpointBaseUrl**：与保护终结点关联的基 URL


  
### <a name="getprotectioncloudendpointbaseurl"></a>GetProtectionCloudEndpointBaseUrl
获取 cloudEndpointBaseUrl。

  
**返回结果**：与保护终结点关联的基 URL
  
### <a name="setprotectiononlyengine"></a>SetProtectionOnlyEngine
设置仅保护引擎指示器 - 无策略/标签。
  
### <a name="isprotectiononlyengine"></a>IsProtectionOnlyEngine
返回仅保护引擎指示器 - 无策略/标签。