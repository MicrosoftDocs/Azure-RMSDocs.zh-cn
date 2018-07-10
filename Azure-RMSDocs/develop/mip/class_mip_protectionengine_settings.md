# <a name="class-mipprotectionenginesettings"></a>类 mip::ProtectionEngine::Settings 
[ProtectionEngine](class_mip_protectionengine.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_protectionengine_settings.md)。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  用于新建引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  用于加载现有引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。
 public const std::string& GetEngineId() const  |  获取引擎 ID。
 public void SetEngineId(const std::string& engineId)  |  设置引擎 ID。
 public const Identity& GetIdentity() const  |  获取与引擎关联的用户标识。
 public void SetIdentity(const Identity& identity)  |  设置与引擎关联的用户标识。
 public const std::string& GetClientData() const  |  获取客户端指定的自定义数据。
 public const std::string& GetLocale() const  |  获取写入引擎数据所用的区域设置。
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  设置用于测试和试验的名称/值对。
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  获取用于测试和试验的名称/值对。
 public void SetSessionId(const std::string& sessionId)  |  设置用于日志记录/遥测相关性的引擎会话 ID。
 public const std::string& GetSessionId() const  |  获取引擎会话 ID。
 public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  设置用于指定云边界的云终结点基 URL。
 public const std::string& GetCloudEndpointBaseUrl() const  |  获取 cloudEndpointBaseUrl。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
用于新建引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。

参数：  
* **identity**：与 [ProtectionEngine](class_mip_protectionengine.md) 关联的标识


* **clientData**：可自定义客户端数据，不仅卸载时可存储在引擎中，而且还能从加载的引擎中检索。 


* **locale**：引擎输出所用的区域设置，默认为“zh-CN”。


  
### <a name="settings"></a>设置
用于加载现有引擎的 [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 构造函数。

参数：  
* **engineId**：将加载的引擎的唯一标识符 


* **clientData**：可自定义客户端数据，不仅卸载时可存储在引擎中，而且还能从加载的引擎中检索。 


* **locale**：引擎输出所用的区域设置，默认为“zh-CN”。


  
### <a name="getengineid"></a>GetEngineId
获取引擎 ID。

  
**返回结果**：引擎 ID
  
### <a name="setengineid"></a>SetEngineId
设置引擎 ID。

参数：  
* **engineId**：引擎 ID。


  
### <a name="getidentity"></a>GetIdentity
获取与引擎关联的用户标识。

  
**返回结果**：与引擎关联的用户标识
  
### <a name="setidentity"></a>SetIdentity
设置与引擎关联的用户标识。

参数：  
* **identity**：与引擎关联的用户标识


  
### <a name="getclientdata"></a>GetClientData
获取客户端指定的自定义数据。

  
**返回结果**：客户端指定的自定义数据
  
### <a name="getlocale"></a>GetLocale
获取写入引擎数据所用的区域设置。

  
**返回结果**：写入引擎数据所用的区域设置
  
### <a name="setcustomsettings"></a>SetCustomSettings
设置用于测试和试验的名称/值对。

参数：  
* **customSettings**：用于测试和试验的名称/值对


  
### <a name="getcustomsettings"></a>GetCustomSettings
获取用于测试和试验的名称/值对。

  
**返回结果**：用于测试和试验的名称/值对
  
### <a name="setsessionid"></a>SetSessionId
设置用于日志记录/遥测相关性的引擎会话 ID。

参数：  
* **sessionId**：用于日志记录/遥测相关性的引擎会话 ID


  
### <a name="getsessionid"></a>GetSessionId
获取引擎会话 ID。

  
**返回结果**：引擎会话 ID
  
### <a name="setcloudendpointbaseurl"></a>SetCloudEndpointBaseUrl
设置用于指定云边界的云终结点基 URL。

参数：  
* **cloudEndpointBaseUrl**：与保护终结点关联的基 URL


  
### <a name="getcloudendpointbaseurl"></a>GetCloudEndpointBaseUrl
获取 cloudEndpointBaseUrl。

  
**返回结果**：与保护终结点关联的基 URL