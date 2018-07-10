# <a name="class-mipfileprofilesettings"></a>class mip::FileProfile::Settings 
[FileProfile](class_mip_fileprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_fileprofile_settings.md)。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, bool isLicenseCachingEnabled, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  [FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。
 public const std::string& GetPath() const  |  获取存储日志记录、遥测和其他永久性状态的路径。
 public bool GetUseInMemoryStorage() const  |  获取是否所有状态都应存储在内存中（而不是存储在磁盘上）
 public bool IsLicenseCachingEnabled() const  |  获取是否已启用缓存许可证。
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  获取用于获取身份验证令牌的身份验证委托。
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  获取用于请求用户许可连接到服务的许可委托。
public std::shared_ptr<Observer> GetObserver() const  |  获取接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的监测程序。
 public const ApplicationInfo GetApplicationInfo() const  |  获取使用 SDK 的应用程序的相关信息。
 public bool GetSkipTelemetryInit() const  |  获取是否应跳过遥测初始化的指示。
 public void SetSkipTelemetryInit()  |  禁用遥测初始化。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  获取由应用程序提供的记录器委托（如果有）。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  使用外部记录器实现。
 public void OptOutTelemetry()  |  选择退出所有遥测收集。
 public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集。
 public void SetSessionId(const std::string& sessionId)  |  设置会话 ID。
 public const std::string& GetSessionId() const  |  获取会话 ID。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
[FileProfile::Settings](class_mip_fileprofile_settings.md) 构造函数。

参数：  
* **路径**：在其下存储日志记录、遥测和其他永久性状态的文件路径 


* **useInMemoryStorage**：是否所有状态都应存储在内存中（与存储在磁盘上相反） 


* **isLicenseCachingEnabled**：启用或禁用保护许可证的缓存 


* **authDelegate**：用于获取身份验证令牌的身份验证委托 


* **observer**：将接收与 [FileProfile](class_mip_fileprofile.md) 相关的事件通知的 [Observer](class_mip_fileprofile_observer.md) 实例


* **applicationInfo**：有关使用 SDK 的应用程序的信息


  
### <a name="getpath"></a>GetPath
获取存储日志记录、遥测和其他永久性状态的路径。

  
**返回结果**：在其下存储日志记录、遥测和其他永久性状态的路径
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
获取是否所有状态都应存储在内存中（而不是存储在磁盘上）

  
**返回结果**：是否所有状态都应存储在内存中（与存储在磁盘上相反）
  
### <a name="islicensecachingenabled"></a>IsLicenseCachingEnabled
获取是否已启用缓存许可证。

  
**返回结果**：如果缓存仅存储在内存中，返回 True
  
### <a name="getauthdelegate"></a>GetAuthDelegate
获取用于获取身份验证令牌的身份验证委托。

  
**返回结果**：用于获取身份验证令牌的身份验证委托
  
### <a name="consentdelegate"></a>ConsentDelegate
获取用于请求用户许可连接到服务的许可委托。

  
**返回结果**：用户请求用户同意的同意委托
  
### <a name="observer"></a>观察者
获取接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的监测程序。

  
**返回结果**：接收 [FileProfile](class_mip_fileprofile.md) 相关事件通知的 [Observer](class_mip_fileprofile_observer.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
获取使用 SDK 的应用程序的相关信息。

  
**返回结果**：使用 SDK 的应用程序的相关信息
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
获取是否应跳过遥测初始化的指示。

  
**返回结果**：是否应跳过遥测初始化
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
禁用遥测初始化。
这通常不应由客户端应用程序调用，而是由文件 SDK（已初始化遥测）使用，以防止重复初始化
  
### <a name="loggerdelegate"></a>LoggerDelegate
获取应用程序提供的记录器委托（若有）。

  
**返回结果**：用于日志记录的记录器委托
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
使用外部记录器实现。
如果客户端应用程序要使用自己的记录器实现，其应执行此调用
  
### <a name="optouttelemetry"></a>OptOutTelemetry
选择退出所有遥测收集。
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
获取是否应禁用遥测收集。

  
**返回结果**：是否应禁用遥测收集
  
### <a name="setsessionid"></a>SetSessionId
设置会话 ID。

参数：  
* **sessionId**：将用于关联日志/遥测的会话 ID


  
### <a name="getsessionid"></a>GetSessionId
获取会话 ID。

  
**返回结果**：将用于关联日志/遥测的会话 ID