# <a name="class-miprmsnotfoundexception"></a>class mip::RMSNotFoundException 
RMS 未找到异常。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public RMSNotFoundException(const std::string& message)  |  [RMSNotFoundException](class_mip_rmsnotfoundexception.md) 构造函数。
 public RMSNotFoundException(const char*const& message)  |  [RMSNotFoundException](class_mip_rmsnotfoundexception.md) 构造函数。
 public virtual const char* what() const  |  获取异常消息。
 public virtual ExceptionTypes type() const  |  获取异常类型。
 public virtual int error() const  |  获取错误代码。
  
## <a name="members"></a>成員
  
### <a name="rmsnotfoundexception"></a>RMSNotFoundException
[RMSNotFoundException](class_mip_rmsnotfoundexception.md) 构造函数。

参数：  
* **message**：异常消息


  
### <a name="rmsnotfoundexception"></a>RMSNotFoundException
[RMSNotFoundException](class_mip_rmsnotfoundexception.md) 构造函数。

参数：  
* **message**：异常消息


  
### <a name="what"></a>what
获取异常消息。

  
**返回结果**：异常消息
  
### <a name="exceptiontypes"></a>ExceptionTypes
获取异常类型。

  
**返回结果**：异常类型
  
### <a name="error"></a>错误
获取错误代码。

  
**返回结果**：[错误](class_mip_error.md)代码