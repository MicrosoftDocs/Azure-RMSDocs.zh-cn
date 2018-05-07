# <a name="class-mipnotsupportederror"></a>class mip::NotSupportedError 
不支持操作错误。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline char const  * what | 获取 cstring 错误消息。
public std::shared_ptr< Error > Clone | 克隆错误。
public inline virtual ErrorType GetErrorType | 获取错误类型。
public inline virtual const std::string & GetErrorName | 获取错误名称。
public inline virtual const std::string & GetMessage | 获取错误消息。
public inline virtual void SetMessage | 设置错误消息。
## <a name="members"></a>成員
### <a name="what"></a>what
获取 cstring 错误消息。
#### <a name="returns"></a>Returns
cstring 错误消息
### <a name="error"></a>错误
克隆错误。
#### <a name="returns"></a>Returns
错误副本。
### <a name="errortype"></a>ErrorType
获取错误类型。
#### <a name="returns"></a>Returns
错误类型。
### <a name="geterrorname"></a>GetErrorName
获取错误名称。
#### <a name="returns"></a>Returns
错误名称。
### <a name="getmessage"></a>GetMessage
获取错误消息。
#### <a name="returns"></a>Returns
错误消息。
### <a name="setmessage"></a>SetMessage
设置错误消息。
#### <a name="parameters"></a>参数
* msg：错误消息。