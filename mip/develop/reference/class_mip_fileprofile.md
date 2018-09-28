# <a name="class-mipfileprofile"></a>class mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。
一个典型的应用程序只需要一个[配置文件](class_mip_profile.md)，但它可以按需创建多个配置文件。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  返回配置文件的设置。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  启动列出引擎操作。
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  开始卸载具有给定 ID 的文件引擎。
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr<void>& context)  |  开始向配置文件添加新文件引擎。
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  开始删除具有给定 ID 的文件引擎。给定配置文件的所有数据都将彻底删除。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
返回配置文件的设置。
  
### <a name="listenginesasync"></a>ListEnginesAsync
启动列出引擎操作。
[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
开始卸载具有给定 ID 的文件引擎。[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。
  
### <a name="addengineasync"></a>AddEngineAsync
开始向配置文件添加新文件引擎。
[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
开始删除具有给定 ID 的文件引擎。给定配置文件的所有数据都将彻底删除。
[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。