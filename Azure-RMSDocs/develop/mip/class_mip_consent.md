# <a name="class-mipconsent"></a>class mip::Consent 
表示用户对准许操作的接受/拒绝。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const mip::ConsentResult& Result() const  |  获取同意请求的结果。
public void Result(const ConsentResult& value)  |  设置同意请求的结果。
public mip::ConsentType Type() const  |  获取同意类型。
public const std::vector<std::string> Urls() const  |  获取同意请求中涉及的 URL。
public const std::string User() const  |  获取发出同意请求的用户（电子邮件地址）。
public const std::string Domain() const  |  获取与发出同意请求的用户关联的域。
  
## <a name="members"></a>成員
  
### <a name="mipconsentresult"></a>mip::ConsentResult
获取同意请求的结果。
  
#### <a name="returns"></a>Returns
同意请求的结果
  
### <a name="result"></a>结果
设置同意请求的结果。
  
#### <a name="parameters"></a>参数
* value：同意请求的结果
  
### <a name="mipconsenttype"></a>mip::ConsentType
获取同意类型。
  
#### <a name="returns"></a>Returns
同意类型
  
### <a name="urls"></a>Url
获取同意请求中涉及的 URL。
  
#### <a name="returns"></a>Returns
同意请求中涉及的 URL
  
### <a name="user"></a>用户
获取发出同意请求的用户（电子邮件地址）。
  
#### <a name="returns"></a>Returns
发出同意请求的用户
  
### <a name="domain"></a>Domain
获取与发出同意请求的用户关联的域。
  
#### <a name="returns"></a>Returns
与发出同意请求的用户关联的域