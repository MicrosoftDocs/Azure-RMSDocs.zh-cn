# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
由 [ProtectionProfile](#classmip_1_1_protection_profile) 在创建期间及其整个生存期内使用的[设置](#classmip_1_1_protection_profile_1_1_settings)。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline  SettingsProtectionProfile::Observer > & observer,const ApplicationInfo & applicationInfo) public inline const std::string & GetPath | 获取在其下存储日志记录、遥测和其他保护附件的路径。
public inline const std::shared_ptr< ProtectionProfile::Observer > & GetObserver public inline const ApplicationInfo & GetApplicationInfo | 获取有关使用保护 SDK 的应用程序的信息。
public inline bool GetSkipTelemetryInit | 获取是否应跳过遥测初始化的指示。
public inline void SetSkipTelemetryInit | 禁用遥测初始化。
public inline void SetSessionId | Sets the session id. public inline const std::string & GetSessionId | 获取会话 ID。
## <a name="members"></a>成員
### <a name="settings"></a>设置
[ProtectionProfile::Settings](#classmip_1_1_protection_profile_1_1_settings) 构造函数。
#### <a name="parameters"></a>参数
* path：在其下存储日志记录、遥测和其他保护附件的文件路径 
* observer：[Observer](#classmip_1_1_protection_profile_1_1_observer) 实例，将接收与 [ProtectionProfile](#classmip_1_1_protection_profile) 相关的事件通知
* applicationInfo：有关使用保护 SDK 的应用程序的信息
### <a name="getpath"></a>GetPath
获取在其下存储日志记录、遥测和其他保护附件的路径。
#### <a name="returns"></a>Returns
在其下存储日志记录、遥测和其他保护附件的路径
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
获取接收与 [ProtectionProfile](#classmip_1_1_protection_profile) 相关的事件通知的观察程序。
#### <a name="returns"></a>Returns
接收与 [ProtectionProfile](#classmip_1_1_protection_profile) 相关的事件通知的[观察程序](#classmip_1_1_protection_profile_1_1_observer)
### <a name="applicationinfo"></a>ApplicationInfo
获取有关使用保护 SDK 的应用程序的信息。
#### <a name="returns"></a>Returns
有关使用保护 SDK 的应用程序的信息
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
获取是否应跳过遥测初始化的指示。
#### <a name="returns"></a>Returns
是否应跳过遥测初始化
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
禁用遥测初始化。
这通常不应由客户端应用程序调用，而是由文件 SDK（已初始化遥测）使用，以防止重复初始化
### <a name="setsessionid"></a>SetSessionId
设置会话 ID。
#### <a name="parameters"></a>参数
* sessionId：将用于关联日志/遥测的会话 ID
### <a name="getsessionid"></a>GetSessionId
获取会话 ID。
#### <a name="returns"></a>Returns
将用于关联日志/遥测的会话 ID