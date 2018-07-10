# <a name="class-mipprotectionengineobserver"></a>类 mip::ProtectionEngine::Observer 
接收 [ProtectionEngine](class_mip_protectionengine.md) 相关通知的接口。
此接口必须由应用程序通过使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  在成功检索模板时调用。
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在检索模板出错时调用。
  
## <a name="members"></a>成員
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
在成功检索模板时调用。

参数：  
* **templateIds**：对已检索模板的列表的引用 


* **context**：传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function 等）传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) 或 [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
在检索模板出错时调用。

参数：  
* **error**：检索模板时发生的[错误](class_mip_error.md) 


* **context**：传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function 等）传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) 或 [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)