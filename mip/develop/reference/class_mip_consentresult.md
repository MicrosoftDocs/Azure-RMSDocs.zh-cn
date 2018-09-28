# <a name="class-mipconsentresult"></a>class mip::ConsentResult 
说明在用户交互后同意请求的结果。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public ConsentResult(bool accepted, bool showAgain, const std::string& userId)  |  [ConsentResult](class_mip_consentresult.md) 构造函数。
 public bool Accepted() const  |  获取用户是否同意操作的指示。
 public bool ShowAgain() const  |  获取日后请求是否需要显式同意的指示。
 public const std::string& UserId() const  |  获取发出同意请求的用户（电子邮件地址）。
  
## <a name="members"></a>成員
  
### <a name="consentresult"></a>ConsentResult
[ConsentResult](class_mip_consentresult.md) 构造函数。

参数：  
* **accepted**：用户是否同意操作 


* **showAgain**：日后操作请求是否需要显式同意 


* **userId**：发出同意请求的用户（电子邮件地址）


  
### <a name="accepted"></a>Accepted
获取用户是否同意操作的指示。

  
**返回结果**：用户是否同意操作
  
### <a name="showagain"></a>ShowAgain
获取日后请求是否需要显式同意的指示。

  
**返回结果**：日后请求是否需要显式同意，如果需要，SDK 将记住此同意结果，且将来不会提示客户端应用程序同意与否。
  
### <a name="userid"></a>UserId
获取发出同意请求的用户（电子邮件地址）。

  
**返回结果**：发出同意请求的用户