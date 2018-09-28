# <a name="class-miprmsnetworkexception"></a>class mip::RMSNetworkException 
RMS 网络异常。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public RMSNetworkException(const std::string& message, Reason reason)  |  [RMSNetworkException](class_mip_rmsnetworkexception.md) 构造函数。
 public RMSNetworkException(const char*const& message, Reason reason)  |  [RMSNetworkException](class_mip_rmsnetworkexception.md) 构造函数。
 public virtual Reason reason() const  |  获取网络故障分类。
 public virtual const char* what() const  |  获取异常消息。
 public virtual ExceptionTypes type() const  |  获取异常类型。
 public virtual int error() const  |  获取错误代码。
  
## <a name="members"></a>成員
  
### <a name="rmsnetworkexception"></a>RMSNetworkException
[RMSNetworkException](class_mip_rmsnetworkexception.md) 构造函数。

参数：  
* **message**：异常消息 


* **reason**：网络故障分类


  
### <a name="rmsnetworkexception"></a>RMSNetworkException
[RMSNetworkException](class_mip_rmsnetworkexception.md) 构造函数。

参数：  
* **message**：异常消息 


* **reason**：网络故障分类


  
### <a name="reason"></a>原因
获取网络故障分类。

  
**返回结果**：网络故障分类
  
### <a name="what"></a>what
获取异常消息。

  
**返回结果**：异常消息
  
### <a name="exceptiontypes"></a>ExceptionTypes
获取异常类型。

  
**返回结果**：异常类型
  
### <a name="error"></a>错误
获取错误代码。

  
**返回结果**：[错误](class_mip_error.md)代码