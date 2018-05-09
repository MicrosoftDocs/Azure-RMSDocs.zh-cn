# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
此类的一个实例带有适当的参数，应提供以启动引擎。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
`public inline Settings(const std::string& id, const std::string& clientData, const std::string& locale)`  |  使用给定参数构造实例。 用于创建[设置](#classmip_1_1_policy_engine_1_1_settings)来调用 LoadEngineAsync 以加载现有引擎。
`public inline Settings(const Identity& identity, const std::string& clientData, const std::string& locale)`  |  用于创建[设置](#classmip_1_1_policy_engine_1_1_settings)来调用 AddEngineAsync 以添加新引擎。
`public inline const std::string& GetId() const`  |  获取引擎 ID。
`public inline void SetId(const std::string& id)`  |  设置引擎 ID。
`public inline const Identity& GetIdentity() const`  |  获取标识对象。
`public inline void SetIdentity(const Identity& identity)`  |  设置标识对象。
`public inline const std::string& GetClientData() const`  |  获取设置中设置的客户端数据。
`public inline void SetClientData(const std::string& clientData)`  |  设置客户端数据字符串。
`public inline const std::string& GetLocale() const`  |  获取设置中设置的区域设置。
`public inline void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)`  |  设置自定义设置，用于功能访问控制和测试。
`public inline const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const`  |  设置自定义设置，用于功能访问控制和测试。
`public inline void SetSessionId(const std::string& sessionId)`  |  设置用于客户端定义遥测的会话 ID。
`public inline const std::string& GetSessionId() const`  |  获取唯一标识符形式的会话 ID。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
使用给定参数构造实例。 用于创建[设置](#classmip_1_1_policy_engine_1_1_settings)来调用 LoadEngineAsync 以加载现有引擎。
  
#### <a name="parameters"></a>参数
* ID：将其设置为 AddEngineAsync 生成或自生成的唯一引擎 ID。 重新加载现有引擎时，将重用此 ID，否则将创建一个新引擎。 
* clientData：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 
* locale：将在此区域设置中提供引擎可本地化输出，默认为“zh-CN”。
  
### <a name="settings"></a>设置
用于创建[设置](#classmip_1_1_policy_engine_1_1_settings)来调用 AddEngineAsync 以添加新引擎。
  
#### <a name="parameters"></a>参数
* identity：需要为其添加引擎的用户的唯一标识符。 
* clientData：卸载时可存储在引擎中的可自定义的客户端数据，可以从已加载的引擎中检索该数据。 
* locale：将在此区域设置中提供引擎可本地化输出，默认为 `en-US`。
  
### <a name="getid"></a>GetId
获取引擎 ID。
  
#### <a name="returns"></a>Returns
标识引擎的唯一字符串。
  
### <a name="setid"></a>SetId
设置引擎 ID。
  
#### <a name="parameters"></a>参数
* ID：引擎 ID。
  
### <a name="getidentity"></a>GetIdentity
获取标识对象。
  
#### <a name="returns"></a>Returns
对设置对象中的标识的引用。 
另请参阅：mip::Identity
  
### <a name="setidentity"></a>SetIdentity
设置标识对象。
  
#### <a name="parameters"></a>参数
* identity：用户的唯一标识。 
另请参阅：mip::Identity
  
### <a name="getclientdata"></a>GetClientData
获取设置中设置的客户端数据。
  
#### <a name="returns"></a>Returns
客户端指定数据的字符串。
  
### <a name="setclientdata"></a>SetClientData
设置客户端数据字符串。
  
#### <a name="parameters"></a>参数
* clientData：用户指定的数据。
  
### <a name="getlocale"></a>GetLocale
获取设置中设置的区域设置。
  
#### <a name="returns"></a>Returns
区域设置。
  
### <a name="setcustomsettings"></a>SetCustomSettings
设置自定义设置，用于功能访问控制和测试。
  
#### <a name="parameters"></a>参数
* customSettings：名称/值对列表。
  
### <a name="getcustomsettings"></a>GetCustomSettings
设置自定义设置，用于功能访问控制和测试。
  
#### <a name="parameters"></a>参数
* 名称/值对列表。
  
### <a name="setsessionid"></a>SetSessionId
设置用于客户端定义遥测的会话 ID。
  
#### <a name="parameters"></a>参数
* sessionId：连接遥测事件的唯一字符串。
  
### <a name="getsessionid"></a>GetSessionId
获取唯一标识符形式的会话 ID。
  
#### <a name="returns"></a>Returns
会话 ID。