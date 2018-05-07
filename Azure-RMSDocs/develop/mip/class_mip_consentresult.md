# <a name="class-mipconsentresult"></a>class mip::ConsentResult 
说明在用户交互后同意请求的结果。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline  ConsentResult public inline bool Accepted | 获取用户是否同意操作的指示。
public inline bool ShowAgain | 获取日后请求是否需要显式同意的指示。
public inline const std::string & UserId | 获取发出同意请求的用户（电子邮件地址）。
## <a name="members"></a>成員
### <a name="consentresult"></a>ConsentResult
[ConsentResult](#classmip_1_1_consent_result) 构造函数。
#### <a name="parameters"></a>参数
* accepted：用户是否同意操作 
* showAgain：日后操作请求是否需要显式同意 
* userId：发出同意请求的用户（电子邮件地址）
### <a name="accepted"></a>Accepted
获取用户是否同意操作的指示。
#### <a name="returns"></a>Returns
用户是否同意操作
### <a name="showagain"></a>ShowAgain
获取日后请求是否需要显式同意的指示。
#### <a name="returns"></a>Returns
日后请求是否需要显式同意，如果需要，SDK 将记住此同意结果，且将来不会提示客户端应用程序同意与否。
### <a name="userid"></a>UserId
获取发出同意请求的用户（电子邮件地址）。
#### <a name="returns"></a>Returns
发出同意请求的用户