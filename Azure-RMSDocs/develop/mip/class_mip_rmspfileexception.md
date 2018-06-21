# <a name="class-miprmspfileexception"></a>class mip::RMSPFileException 
RMS PFile 异常。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public RMSPFileException(const std::string& message, Reason reason)  |  [RMSPFileException](class_mip_rmspfileexception.md) 构造函数。
 public RMSPFileException(const char*const& message, Reason reason)  |  [RMSPFileException](class_mip_rmspfileexception.md) 构造函数。
 public virtual Reason reason() const  |  获取 PFile 错误分类。
 public virtual const char* what() const  |  获取异常消息。
 public virtual ExceptionTypes type() const  |  获取异常类型。
 public virtual int error() const  |  获取错误代码。
  
## <a name="members"></a>成員
  
### <a name="rmspfileexception"></a>RMSPFileException
[RMSPFileException](class_mip_rmspfileexception.md) 构造函数。

参数：  
* **message**：异常消息 


* **reason**：PFile 错误分类


  
### <a name="rmspfileexception"></a>RMSPFileException
[RMSPFileException](class_mip_rmspfileexception.md) 构造函数。

参数：  
* **message**：异常消息 


* **reason**：PFile 错误分类


  
### <a name="reason"></a>原因
获取 PFile 错误分类。

  
**返回结果**：PFile 错误分类
  
### <a name="what"></a>what
获取异常消息。

  
**返回结果**：异常消息
  
### <a name="exceptiontypes"></a>ExceptionTypes
获取异常类型。

  
**返回结果**：异常类型
  
### <a name="error"></a>错误
获取错误代码。

  
**返回结果**：[错误](class_mip_error.md)代码