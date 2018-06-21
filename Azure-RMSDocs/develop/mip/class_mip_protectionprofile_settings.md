# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
由 [ProtectionProfile](class_mip_protectionprofile.md) 在创建期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数。
 public const std::string& GetPath() const  |  获取在其下存储日志记录、遥测和其他保护附件的路径。
public const std::shared_ptr<ProtectionProfile::Observer>& GetObserver() const  |  获取接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关的事件通知的观察程序。
 public const ApplicationInfo& GetApplicationInfo() const  |  获取有关使用保护 SDK 的应用程序的信息。
 public bool GetSkipTelemetryInit() const  |  获取是否应跳过遥测初始化的指示。
 public void SetSkipTelemetryInit()  |  禁用遥测初始化。
 public void SetSessionId(const std::string& sessionId)  |  设置会话 ID。
 public const std::string& GetSessionId() const  |  获取会话 ID。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) 构造函数。

参数：  
* **path**：在其下存储日志记录、遥测和其他保护附件的文件路径 


* **observer**：将接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关的事件通知的 [Observer](class_mip_protectionprofile_observer.md) 实例


* **applicationInfo**：有关使用保护 SDK 的应用程序的信息


  
### <a name="getpath"></a>GetPath
获取在其下存储日志记录、遥测和其他保护附件的路径。

  
**返回结果**：在其下存储日志记录、遥测和其他保护附件的路径
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
获取接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关的事件通知的观察程序。

  
**返回结果**：接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关的事件通知的[观察程序](class_mip_protectionprofile_observer.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
获取有关使用保护 SDK 的应用程序的信息。

  
**返回结果**：有关使用保护 SDK 的应用程序的信息
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
获取是否应跳过遥测初始化的指示。

  
**返回结果**：是否应跳过遥测初始化
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
禁用遥测初始化。
这通常不应由客户端应用程序调用，而是由文件 SDK（已初始化遥测）使用，以防止重复初始化
  
### <a name="setsessionid"></a>SetSessionId
设置会话 ID。

参数：  
* **sessionId**：将用于关联日志/遥测的会话 ID


  
### <a name="getsessionid"></a>GetSessionId
获取会话 ID。

  
**返回结果**：将用于关联日志/遥测的会话 ID