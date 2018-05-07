# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline  SettingsObserver > observer,const ApplicationInfo & applicationInfo) | 用于配置配置文件的接口。
public inline  ~Settings | 
public inline const std::string & GetPath | 
public inline bool GetUseInMemoryStorage | 
public inline std::shared_ptr< AuthDelegate > GetAuthDelegate | 
public inline std::shared_ptr< Observer > GetObserver | 
public inline const ApplicationInfo GetApplicationInfo | 
public inline bool GetSkipTelemetryInit | 
public inline void SetSkipTelemetryInit | 
public inline void SetSessionId | 设置配置文件会话 ID。
public inline const std::string & GetSessionId | 返回配置文件会话 ID。
## <a name="members"></a>成員
### <a name="settings"></a>设置
用于配置配置文件的接口。
#### <a name="parameters"></a>参数
* observer：实现 [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) 接口的类。 可以为 nullptr。
### <a name="settings"></a>~Settings
### <a name="getpath"></a>GetPath
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
### <a name="getauthdelegate"></a>GetAuthDelegate
### <a name="observer"></a>观察者
### <a name="applicationinfo"></a>ApplicationInfo
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
### <a name="setsessionid"></a>SetSessionId
设置配置文件会话 ID。
### <a name="getsessionid"></a>GetSessionId
返回配置文件会话 ID。