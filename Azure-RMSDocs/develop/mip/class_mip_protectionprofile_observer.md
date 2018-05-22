# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关通知的接口。
此接口必须由应用程序通过使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在加载配置文件引发错误时调用。
  
## <a name="members"></a>成員
  
### <a name="onloadsuccess"></a>OnLoadSuccess
在成功加载配置文件时调用。

参数：  
* **profile**：对新创建的 [ProtectionProfile](class_mip_protectionprofile.md) 的引用


* **context**：传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) 的相同上下文


应用程序可以将任何类型的上下文（例如 std::promise、std::function 等）传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) 或 [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
在加载配置文件引发错误时调用。

参数：  
* **error**：加载时发生的[错误](class_mip_error.md) 


* **context**：传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) 的相同上下文


应用程序可以将任何类型的上下文（例如 std::promise、std::function 等）传递到 [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) 或 [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)