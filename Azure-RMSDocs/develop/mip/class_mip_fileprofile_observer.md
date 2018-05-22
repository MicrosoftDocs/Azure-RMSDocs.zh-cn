# <a name="class-mipfileprofileobserver"></a>class mip::FileProfile::Observer 
[Observer](class_mip_fileprofile_observer.md) 接口，供客户端获取配置文件相关事件的通知。
如果发生 *Error 事件，错误对象将保存在 [mip::Error](class_mip_error.md) 类中。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public virtual ~Observer()  | _尚无记录。_
public virtual void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context)  |  在成功加载配置文件时调用。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在加载配置文件引发错误时调用。
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  在成功生成引擎列表时调用。
public virtual void OnListEnginesError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在列出引擎引发错误时调用。
public virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  在成功卸载引擎时调用。
public virtual void OnUnloadEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在卸载引擎引发错误时调用。
public virtual void OnAddEngineSuccess(const std::shared_ptr<mip::FileEngine>& engine, const std::shared_ptr<void>& context)  |  在成功添加新引擎时调用。
public virtual void OnAddEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在添加新引擎引发错误时调用。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  在成功删除引擎时调用。
public virtual void OnDeleteEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在删除引擎引发错误时调用。
 public virtual void OnPolicyChanged(const std::string& engineId)  |  在针对具有给定 ID 的引擎的策略发生更改时调用。
 受保护的 Observer()  | _尚无记录。_
  
## <a name="members"></a>成員
  
### <a name="observer"></a>~Observer
_尚无记录。_

  
### <a name="onloadsuccess"></a>OnLoadSuccess
在成功加载配置文件时调用。
  
### <a name="onloadfailure"></a>OnLoadFailure
在加载配置文件引发错误时调用。
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
在成功生成引擎列表时调用。
  
### <a name="onlistengineserror"></a>OnListEnginesError
在列出引擎引发错误时调用。
  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
在成功卸载引擎时调用。
  
### <a name="onunloadengineerror"></a>OnUnloadEngineError
在卸载引擎引发错误时调用。
  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
在成功添加新引擎时调用。
  
### <a name="onaddengineerror"></a>OnAddEngineError
在添加新引擎引发错误时调用。
  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
在成功删除引擎时调用。
  
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
在删除引擎引发错误时调用。
  
### <a name="onpolicychanged"></a>OnPolicyChanged
在针对具有给定 ID 的引擎的策略发生更改时调用。
  
### <a name="observer"></a>观察者
_尚无记录。_
