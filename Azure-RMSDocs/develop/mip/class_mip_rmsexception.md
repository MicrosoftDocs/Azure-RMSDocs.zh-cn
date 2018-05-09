# <a name="class-miprmsexception"></a>class mip::RMSException 
基本 RMS 异常。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline RMSException(const ExceptionTypes type, const int error, const std::string& message)  |  [RMSException](#classmip_1_1_r_m_s_exception) 构造函数。
public inline RMSException(const ExceptionTypes type, const int error, const char*const& message)  |  [RMSException](#classmip_1_1_r_m_s_exception) 构造函数。
public inline virtual const char* what() const  |  获取异常消息。
public inline virtual ExceptionTypes type() const  |  获取异常类型。
public inline virtual int error() const  |  获取错误代码。
  
## <a name="members"></a>成員
  
### <a name="rmsexception"></a>RMSException
[RMSException](#classmip_1_1_r_m_s_exception) 构造函数。
  
#### <a name="parameters"></a>参数
* type：异常类型 
* error：[错误](#classmip_1_1_error)代码 
* message：异常消息
  
### <a name="rmsexception"></a>RMSException
[RMSException](#classmip_1_1_r_m_s_exception) 构造函数。
  
#### <a name="parameters"></a>参数
* type：异常类型 
* error：[错误](#classmip_1_1_error)代码 
* message：异常消息
  
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