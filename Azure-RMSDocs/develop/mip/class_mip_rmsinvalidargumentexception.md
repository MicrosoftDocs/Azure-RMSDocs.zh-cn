# <a name="class-miprmsinvalidargumentexception"></a>class mip::RMSInvalidArgumentException 
RMS 无效参数异常。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public RMSInvalidArgumentException(const std::string& message)  |  [RMSInvalidArgumentException](class_mip_rmsinvalidargumentexception.md) 构造函数。
 public RMSInvalidArgumentException(const char*const& message)  |  [RMSInvalidArgumentException](class_mip_rmsinvalidargumentexception.md) 构造函数。
 public virtual const char* what() const  |  获取异常消息。
 public virtual ExceptionTypes type() const  |  获取异常类型。
 public virtual int error() const  |  获取错误代码。
  
## <a name="members"></a>成員
  
### <a name="rmsinvalidargumentexception"></a>RMSInvalidArgumentException
[RMSInvalidArgumentException](class_mip_rmsinvalidargumentexception.md) 构造函数。

参数：  
* **message**：异常消息


  
### <a name="rmsinvalidargumentexception"></a>RMSInvalidArgumentException
[RMSInvalidArgumentException](class_mip_rmsinvalidargumentexception.md) 构造函数。

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