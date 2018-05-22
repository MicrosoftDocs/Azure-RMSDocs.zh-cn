# <a name="class-mipgetuserpolicyresult"></a>class mip::GetUserPolicyResult 
描述用户策略获取请求的结果。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public GetUserPolicyResultStatus GetResultStatus()  |  获取策略获取请求的状态。
public std::shared_ptr<std::string> GetReferrer()  |  获取策略的引用网址。
public std::shared_ptr<UserPolicy> GetPolicy()  |  获取 [UserPolicy](class_mip_userpolicy.md) 实例。
  
## <a name="members"></a>成員
  
### <a name="getuserpolicyresultstatus"></a>GetUserPolicyResultStatus
获取策略获取请求的状态。

  
**返回结果**：策略获取请求的状态
  
### <a name="getreferrer"></a>GetReferrer
获取策略的引用网址。

  
**返回结果**：策略的引用网址：该引用网站是一个 URI，它会在获取策略失败时显示给用户，其中包含有关用户如何获取内容访问权限的信息。
  
### <a name="userpolicy"></a>UserPolicy
获取 [UserPolicy](class_mip_userpolicy.md) 实例。

  
**返回结果**：如果获取成功，则返回 [UserPolicy](class_mip_userpolicy.md) 实例，否则返回 nullptr