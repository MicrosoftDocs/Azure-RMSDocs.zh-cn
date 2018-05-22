# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  用于配置配置文件的接口。
 public ~Settings()  | _尚无记录。_
 public const std::string& GetPath() const  | _尚无记录。_
 public bool GetUseInMemoryStorage() const  | _尚无记录。_
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  | _尚无记录。_
public std::shared_ptr<Observer> GetObserver() const  | _尚无记录。_
 public const ApplicationInfo GetApplicationInfo() const  | _尚无记录。_
 public bool GetSkipTelemetryInit() const  | _尚无记录。_
 public void SetSkipTelemetryInit()  | _尚无记录。_
 public void SetSessionId(const std::string& sessionId)  |  设置配置文件会话 ID。
 public const std::string& GetSessionId() const  |  返回配置文件会话 ID。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
用于配置配置文件的接口。

参数：  
* **observer**：实现 [FileHandler::Observer](class_mip_filehandler_observer.md) 接口的类。 可以为 nullptr。


  
### <a name="settings"></a>~Settings
_尚无记录。_

  
### <a name="getpath"></a>GetPath
_尚无记录。_

  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
_尚无记录。_

  
### <a name="getauthdelegate"></a>GetAuthDelegate
_尚无记录。_

  
### <a name="observer"></a>观察者
_尚无记录。_

  
### <a name="applicationinfo"></a>ApplicationInfo
_尚无记录。_

  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
_尚无记录。_

  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
_尚无记录。_

  
### <a name="setsessionid"></a>SetSessionId
设置配置文件会话 ID。
  
### <a name="getsessionid"></a>GetSessionId
返回配置文件会话 ID。