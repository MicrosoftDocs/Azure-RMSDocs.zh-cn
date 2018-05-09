# <a name="class-mipprofileobserver"></a>class mip::Profile::Observer 
[Observer](#classmip_1_1_profile_1_1_observer) 接口，供客户端获取配置文件相关事件的通知。
如果发生 *Error 事件，错误对象将保存在 [mip::Error](#classmip_1_1_error) 类中。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline virtual void OnLoadSuccess(const std::shared_ptr<Profile>& profile, const std::shared_ptr<void>& context)  |  在成功加载配置文件时调用。
public inline virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在加载配置文件引发错误时调用。
public inline virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  在成功生成引擎列表时调用。
public inline virtual void OnListEnginesError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在列出引擎引发错误时调用。
public inline virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  在成功卸载引擎时调用。
public inline virtual void OnUnloadEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在卸载引擎引发错误时调用。
public inline virtual void OnAddEngineSuccess(const std::shared_ptr<PolicyEngine>& engine, const std::shared_ptr<void>& context)  |  在成功添加新引擎时调用。
public inline virtual void OnAddEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在添加新引擎引发错误时调用。
public inline virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  在成功删除引擎时调用。
public inline virtual void OnDeleteEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在删除引擎引发错误时调用。
public inline virtual void OnPolicyChanged(const std::string& engineId)  |  在针对具有给定 ID 的引擎的策略发生更改时调用。
  
## <a name="members"></a>成員
  
### <a name="onloadsuccess"></a>OnLoadSuccess
在成功加载配置文件时调用。
  
#### <a name="parameters"></a>参数
* profile：用于启动操作的当前配置文件。 
* context：传递给操作的上下文。
  
### <a name="onloadfailure"></a>OnLoadFailure
在加载配置文件引发错误时调用。
  
#### <a name="parameters"></a>参数
* error：导致负载操作失败的错误。 
* context：传递给操作的上下文。
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
在成功生成引擎列表时调用。
  
#### <a name="parameters"></a>参数
* engineIds：可用的引擎 ID 列表。 
* context：传递给操作的上下文。
  
### <a name="onlistengineserror"></a>OnListEnginesError
在列出引擎引发错误时调用。
  
#### <a name="parameters"></a>参数
* error：导致列出引擎操作失败的错误。 
* context：传递给操作的上下文。
  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
在成功卸载引擎时调用。
  
#### <a name="parameters"></a>参数
* context：传递给操作的上下文。
  
### <a name="onunloadengineerror"></a>OnUnloadEngineError
在卸载引擎引发错误时调用。
  
#### <a name="parameters"></a>参数
* error：导致卸载引擎操作失败的错误。 
* context：传递给操作的上下文。
  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
在成功添加新引擎时调用。
  
### <a name="onaddengineerror"></a>OnAddEngineError
在添加新引擎引发错误时调用。
  
#### <a name="parameters"></a>参数
* error：导致添加引擎操作失败的错误。 
* context：传递给操作的上下文。
  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
在成功删除引擎时调用。
  
#### <a name="parameters"></a>参数
* context：传递给操作的上下文。
  
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
在删除引擎引发错误时调用。
  
#### <a name="parameters"></a>参数
* error：导致删除引擎操作失败的错误。 
* context：传递给操作的上下文。
  
### <a name="onpolicychanged"></a>OnPolicyChanged
在针对具有给定 ID 的引擎的策略发生更改时调用。
  
#### <a name="parameters"></a>参数
* engineId the engine：若要加载新策略，需要再次调用 AddEngineAsync，同时给定引擎 ID。