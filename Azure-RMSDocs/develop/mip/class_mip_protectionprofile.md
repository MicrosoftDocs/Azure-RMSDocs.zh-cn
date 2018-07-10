# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) 是用于执行保护操作的根类。
应用程序需创建 [ProtectionProfile](class_mip_protectionprofile.md)，然后才能执行所有保护操作
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  启动列出引擎操作。
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr<void>& context)  |  开始向配置文件添加新保护引擎。
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr<void>& context)  |  开始删除给定 ID 的保护引擎。将完全删除给定引擎的所有数据。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。

  
**返回结果**：由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)
  
### <a name="listenginesasync"></a>ListEnginesAsync
启动列出引擎操作。

参数：  
* **context**：将传递给观察程序函数的参数。 


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="addengineasync"></a>AddEngineAsync
开始向配置文件添加新保护引擎。

参数：  
* **settings**：指定引擎参数的 [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) 对象。 


* **context**：将传递给观察程序函数的参数。 


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
开始删除给定 ID 的保护引擎。将完全删除给定引擎的所有数据。

参数：  
* **ID**：唯一引擎 ID。 


* **context**：将传递给观察程序函数的参数。 


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) 是在成功或失败时调用。