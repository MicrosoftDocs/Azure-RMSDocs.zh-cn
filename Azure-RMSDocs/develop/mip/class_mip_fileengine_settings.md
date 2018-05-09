# <a name="class-mipfileenginesettings"></a>class mip::FileEngine::Settings 
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline Settings(const std::string& id, const std::string& clientData, const std::string& locale)  |  使用给定参数创建实例。
public inline Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  使用给定参数创建实例。
public inline const std::string& GetId() const  |  返回引擎 ID。
public inline const Identity& GetIdentity() const  |  返回引擎标识。
public inline void SetIdentity(const Identity& identity)  |  设置引擎标识。
public inline const std::string& GetClientData() const  |  返回引擎客户端数据。
public inline const std::string& GetLocale() const  |  返回引擎区域设置。
public inline void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  设置用于测试和试验的名称/值对列表。
public inline const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  获取用于测试和试验的名称/值对列表。
public inline void SetSessionId(const std::string& sessionId)  |  设置引擎会话 ID。
public inline const std::string& GetSessionId() const  |  返回引擎会话 ID。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
使用给定参数创建实例。
用于创建[设置](#classmip_1_1_file_engine_1_1_settings)来调用 LoadEngineAsync 以加载现有引擎（以前通过 AddEngineAsync 添加）。
  
#### <a name="parameters"></a>参数
* ID：将其设置为 AddEngineAsync 生成的唯一引擎 ID。
  
### <a name="settings"></a>设置
使用给定参数创建实例。
用于创建[设置](#classmip_1_1_file_engine_1_1_settings)来调用 AddEngineAsync 以添加新引擎。
  
#### <a name="parameters"></a>参数
* identity：需要为其添加引擎的用户的标识信息。
  
### <a name="getid"></a>GetId
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