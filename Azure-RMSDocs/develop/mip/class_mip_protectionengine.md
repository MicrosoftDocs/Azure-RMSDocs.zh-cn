# <a name="class-mipprotectionengine"></a>类 mip::ProtectionEngine 
执行与特定标识有关的保护相关操作。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  获取引擎设置。
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  获取用户可用模板的集合。
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  创建将权限/角色分配给特定用户的保护处理程序。
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  从序列化形式创建保护处理程序。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
获取引擎设置。

  
**返回结果**：引擎设置
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
获取用户可用模板的集合。

参数：  
* **observer**：实现 [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 接口的类 


* **context**：这是转发给 [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) 或 [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure) 的相同上下文


  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **descriptor**：描述保护配置的 [ProtectionDescriptor](class_mip_protectiondescriptor.md) 


* **options**：“创建”选项 


* **observer**：实现 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 接口的类 


* **context**：这是转发给 [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) 或 ProtectionHandler::Observer::OnCreateProtectionHandlerFailure 的相同上下文


  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
从序列化形式创建保护处理程序。

参数：  
* **serializedPublishingLicense**：序列化的发布许可证 


* **options**：“创建”选项 


* **observer**：实现 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 接口的类 


* **context**：这是转发给 [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) 或 ProtectionHandler::Observer::OnCreateProtectionHandlerFailure 的相同上下文

