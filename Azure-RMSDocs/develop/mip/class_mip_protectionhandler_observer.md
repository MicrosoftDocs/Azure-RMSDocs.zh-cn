# <a name="class-mipprotectionhandlerobserver"></a>类 mip::ProtectionHandler::Observer 
接收 [ProtectionHandler](class_mip_protectionhandler.md) 相关通知的接口。
此接口必须由应用程序通过使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  在成功创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。
public virtual void OnCreateProtectionHandlerError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在无法创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。
  
## <a name="members"></a>成員
  
### <a name="oncreateprotectionhandlersuccess"></a>OnCreateProtectionHandlerSuccess
在成功创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。

参数：  
* **protectionHandler**：新建的 [ProtectionHandler](class_mip_protectionhandler.md)


* **context**：传递到 [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) 或 [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function 等）传递到 [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) 或 [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlererror"></a>OnCreateProtectionHandlerError
在无法创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。

参数：  
* **error**：创建期间发生的 [Error](class_mip_error.md) 


* **context**：传递到 [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) 或 [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function 等）传递到 [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) 或 [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure