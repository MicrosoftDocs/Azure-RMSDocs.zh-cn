# <a name="class-mipprofilesettings"></a>class mip::Profile::Settings 
[Profile](class_mip_profile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_profile_settings.md)。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<Profile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  用于配置配置文件的接口。
 public const std::string& GetPath() const  |  获取存储状态的路径。
 public bool GetUseInMemoryStorage() const  |  获取“使用内存中的存储”标记。
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  获取身份验证委托。
public const std::shared_ptr<Profile::Observer>& GetObserver() const  |  获取事件观察程序。
 public const ApplicationInfo GetApplicationInfo() const  |  获取应用程序信息。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  获取应用程序提供的记录器委托（若有）。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  使用外部记录器实现。
 public void OptOutTelemetry()  |  选择退出所有遥测收集。
 public bool IsTelemetryOptedOut() const  |  获取是否应禁用遥测收集。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
用于配置配置文件的接口。

参数：  
* **path**：sdk 将在其中存储配置文件状态的目录路径。 


* **useInMemoryStorage**：指示是否应在磁盘上存储状态的标记。 


* **authDelegate**：SDK 用来获取身份验证令牌的身份验证委托。 


* **observer**：实现 [Profile::Observer](class_mip_profile_observer.md) 接口的类。 可以为 nullptr。 


* **applicationInfo**：用于访问服务的应用程序标识符。


  
### <a name="getpath"></a>GetPath
获取存储状态的路径。

  
**返回结果**：存储状态的路径。
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
获取“使用内存中的存储”标记。

  
**返回结果**：如果设置了“在内存中使用”，则为 true，否则为 false。
  
### <a name="getauthdelegate"></a>GetAuthDelegate
获取身份验证委托。

  
**返回结果**：身份验证委托。
  
### <a name="profileobserver"></a>Profile::Observer
获取事件观察程序。

  
**返回结果**：事件观察程序。
  
### <a name="applicationinfo"></a>ApplicationInfo
获取应用程序信息。

  
**返回结果**：应用程序信息。
  
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