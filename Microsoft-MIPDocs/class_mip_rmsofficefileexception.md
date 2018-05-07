# <a name="class-miprmsofficefileexception"></a>class mip::RMSOfficeFileException 
RMS Office 文件异常。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline  RMSOfficeFileExceptionReason reason) public inline  RMSOfficeFileExceptionReason reason) public inline virtual Reason reason | 获取 Office 文件失败分类。
public inline virtual const char * what | 获取异常消息。
public inline virtual ExceptionTypes type | 获取异常类型。
public inline virtual int error | 获取错误代码。
## <a name="members"></a>成員
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
[RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception) 构造函数。
#### <a name="parameters"></a>参数
* message：异常消息 
* reason：Office 文件失败分类
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
[RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception) 构造函数。
#### <a name="parameters"></a>参数
* message：异常消息 
* reason：Office 文件失败分类
### <a name="reason"></a>原因
获取 Office 文件失败分类。
#### <a name="returns"></a>Returns
Office 文件失败分类
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