# <a name="class-mipfileprofile"></a>class mip::FileProfile 
[FileProfile](#classmip_1_1_file_profile) 类是用于使用 Microsoft 信息保护操作的根类。
一个典型的应用程序只需要一个[配置文件](#classmip_1_1_profile)，但它可以按需创建多个配置文件。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline virtual  ~FileProfile | 
public const Settings & GetSettings | 返回配置文件的设置。
public void ListEnginesAsync | 启动列出引擎操作。
public void UnloadEngineAsync | 开始卸载具有给定 ID 的文件引擎。
public void AddEngineAsyncFileEngine::Settings & settings,const std::shared_ptr< void > & context) | 开始向配置文件添加新文件引擎。
public void DeleteEngineAsync | 开始删除具有给定 ID 的文件引擎。给定配置文件的所有数据都将彻底删除。
protected inline  FileProfile | 
## <a name="members"></a>成員
### <a name="fileprofile"></a>~FileProfile
### <a name="settings"></a>设置
返回配置文件的设置。
### <a name="listenginesasync"></a>ListEnginesAsync
启动列出引擎操作。
[FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) 将在成功或失败时调用。
### <a name="unloadengineasync"></a>UnloadEngineAsync
开始卸载具有给定 ID 的文件引擎。[FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) 将在成功或失败时调用。
### <a name="addengineasync"></a>AddEngineAsync
开始向配置文件添加新文件引擎。
[FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) 将在成功或失败时调用。
### <a name="deleteengineasync"></a>DeleteEngineAsync
开始删除具有给定 ID 的文件引擎。给定配置文件的所有数据都将彻底删除。
[FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) 将在成功或失败时调用。
### <a name="fileprofile"></a>FileProfile