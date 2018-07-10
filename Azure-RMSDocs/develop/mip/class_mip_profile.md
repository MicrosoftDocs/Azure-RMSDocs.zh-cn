# <a name="class-mipprofile"></a>class mip::Profile 
[Profile](class_mip_profile.md) 类是用于使用 Microsoft 信息保护操作的根类。 一个典型的应用程序只需要一个[配置文件](class_mip_profile.md)，但它可以按需创建多个配置文件。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  获取配置文件上设置的设置。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  启动列出引擎操作。
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  开始卸载具有给定 ID 的策略引擎。
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr<void>& context)  |  开始向配置文件添加新策略引擎。
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  开始删除具有给定 ID 的策略引擎。给定配置文件的所有数据都将彻底删除。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
获取配置文件上设置的设置。

  
**返回结果**：配置文件上设置的设置。
  
### <a name="listenginesasync"></a>ListEnginesAsync
启动列出引擎操作。

参数：  
* **context**：将传递给观察程序函数的参数。 


[Profile::Observer](class_mip_profile_observer.md) 将在成功或失败时调用。
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
开始卸载具有给定 ID 的策略引擎。

参数：  
* **ID**：唯一引擎 ID。 


* **context**：将传递给观察程序函数的参数。 


[Profile::Observer](class_mip_profile_observer.md) 将在成功或失败时调用。
  
### <a name="addengineasync"></a>AddEngineAsync
开始向配置文件添加新策略引擎。

参数：  
* **settings**：指定引擎参数的 [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) 对象。 


* **context**：将传递给观察程序函数的参数。 


[Profile::Observer](class_mip_profile_observer.md) 将在成功或失败时调用。
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
开始删除具有给定 ID 的策略引擎。给定配置文件的所有数据都将彻底删除。

参数：  
* **ID**：唯一引擎 ID。 


* **context**：将传递给观察程序函数的参数。 


[Profile::Observer](class_mip_profile_observer.md) 将在成功或失败时调用。