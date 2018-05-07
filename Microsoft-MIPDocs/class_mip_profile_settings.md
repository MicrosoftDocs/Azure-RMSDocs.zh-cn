# <a name="class-mipprofilesettings"></a>class mip::Profile::Settings 
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline  SettingsProfile::Observer > & observer,const ApplicationInfo & applicationInfo) | 用于配置配置文件的接口。
public inline const std::string & GetPath | 获取存储状态的路径。
public inline bool GetUseInMemoryStorage | 获取“使用内存中的存储”标记。
public inline const std::shared_ptr< AuthDelegate > & GetAuthDelegate | 获取身份验证委托。
public inline const std::shared_ptr< Profile::Observer > & GetObserver | 获取事件观察程序。
public inline const ApplicationInfo GetApplicationInfo | 获取应用程序信息。
## <a name="members"></a>成員
### <a name="settings"></a>设置
用于配置配置文件的接口。
#### <a name="parameters"></a>参数
* path：sdk 将在其中存储配置文件状态的目录路径。 
* useInMemoryStorage：指示是否应在磁盘上存储状态的标记。 
* authDelegate：由 SDK 用于获取身份验证令牌的身份验证委托。 
* observer：实现 [Profile::Observer](#classmip_1_1_profile_1_1_observer) 接口的类。 可以为 nullptr。 
* applicationInfo：用于访问服务的应用程序标识符。
### <a name="getpath"></a>GetPath
获取存储状态的路径。
#### <a name="returns"></a>Returns
存储状态的路径。
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
获取“使用内存中的存储”标记。
#### <a name="returns"></a>Returns
如果在内存中使用，则为 true，否则为 false。
### <a name="getauthdelegate"></a>GetAuthDelegate
获取身份验证委托。
#### <a name="returns"></a>Returns
身份验证委托。
### <a name="profileobserver"></a>Profile::Observer
获取事件观察程序。
#### <a name="returns"></a>Returns
事件观察程序。
### <a name="applicationinfo"></a>ApplicationInfo
获取应用程序信息。
#### <a name="returns"></a>Returns
应用程序信息。