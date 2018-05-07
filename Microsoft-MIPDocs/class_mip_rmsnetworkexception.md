# <a name="class-miprmsnetworkexception"></a>class mip::RMSNetworkException 
RMS 网络异常。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline  RMSNetworkExceptionReason reason) public inline  RMSNetworkExceptionReason reason) public inline virtual Reason reason | 获取网络故障分类。
public inline virtual const char * what | 获取异常消息。
public inline virtual ExceptionTypes type | 获取异常类型。
public inline virtual int error | 获取错误代码。
## <a name="members"></a>成員
### <a name="rmsnetworkexception"></a>RMSNetworkException
[RMSNetworkException](#classmip_1_1_r_m_s_network_exception) 构造函数。
#### <a name="parameters"></a>参数
* message：异常消息 
* reason：网络故障分类
### <a name="rmsnetworkexception"></a>RMSNetworkException
[RMSNetworkException](#classmip_1_1_r_m_s_network_exception) 构造函数。
#### <a name="parameters"></a>参数
* message：异常消息 
* reason：网络故障分类
### <a name="reason"></a>原因
获取网络故障分类。
#### <a name="returns"></a>Returns
网络故障分类
### <a name="what"></a>what
获取异常消息。
#### <a name="returns"></a>Returns
异常消息
### <a name="exceptiontypes"></a>ExceptionTypes
获取异常类型。
#### <a name="returns"></a>Returns
例外类型
### <a name="error"></a>错误
获取错误代码。
#### <a name="returns"></a>Returns
[错误](#classmip_1_1_error)代码