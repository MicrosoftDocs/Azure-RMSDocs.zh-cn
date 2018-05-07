# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
[Observer](#classmip_1_1_file_handler_1_1_observer) 接口，供客户端获取文件处理程序相关事件的通知。
如果发生 *Error 事件，错误对象将保存在 [mip::Error](#classmip_1_1_error) 类中。 客户端不应在调用观察程序的线程上回调引擎。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline virtual  ~Observer | 
public void OnGetLabelSuccessContentLabel > & label,const std::shared_ptr< void > & context) | 在成功检索到标签（从文件中）时调用。
public void OnGetLabelFailure | 在检索标签（从文件中）因错误而失败时调用。
public void OnGetProtectionSuccessUserPolicy > & userPolicy,const std::shared_ptr< void > & context) | 在成功检索到保护策略（从文件中）时调用。
public void OnGetProtectionFailure | 在检索保护策略（从文件中）因错误而失败时调用。
public void OnCommitSuccess | 在将更改成功提交至文件时调用。
public void OnCommitFailure | 在将更改提交至文件因错误而失败时调用。
protected inline  Observer | 
## <a name="members"></a>成員
### <a name="observer"></a>~Observer
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