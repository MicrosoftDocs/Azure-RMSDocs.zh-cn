# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
[Observer](class_mip_filehandler_observer.md) 接口，供客户端获取文件处理程序相关事件的通知。
如果发生 *Error 事件，错误对象将保存在 [mip::Error](class_mip_error.md) 类中。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public virtual ~Observer()  | _尚无记录。_
public void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  在成功检索到标签（从文件中）时调用。
public void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在检索标签（从文件中）因错误而失败时调用。
public void OnGetProtectionSuccess(const std::shared_ptr<UserPolicy>& userPolicy, const std::shared_ptr<void>& context)  |  在成功检索到保护策略（从文件中）时调用。
public void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在检索保护策略（从文件中）因错误而失败时调用。
public void OnCommitSuccess(bool commited, const std::shared_ptr<void>& context)  |  在将更改成功提交至文件时调用。
public void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在将更改提交至文件因错误而失败时调用。
 受保护的 Observer()  | _尚无记录。_
  
## <a name="members"></a>成員
  
### <a name="observer"></a>~Observer
_尚无记录。_

  
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
在成功检索到标签（从文件中）时调用。
  
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
在检索标签（从文件中）因错误而失败时调用。
  
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
在成功检索到保护策略（从文件中）时调用。
  
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
在检索保护策略（从文件中）因错误而失败时调用。
  
### <a name="oncommitsuccess"></a>OnCommitSuccess
在将更改成功提交至文件时调用。
  
### <a name="oncommitfailure"></a>OnCommitFailure
在将更改提交至文件因错误而失败时调用。
  
### <a name="observer"></a>观察者
_尚无记录。_
