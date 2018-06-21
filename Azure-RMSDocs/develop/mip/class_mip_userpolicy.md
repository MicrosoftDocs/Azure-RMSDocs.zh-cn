# <a name="class-mipuserpolicy"></a>class mip::UserPolicy 
表示与受保护的内容关联的策略。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public bool AccessCheck(const std::string& right) const  |  检查策略是否授予用户对指定权限的访问权限。
 public UserPolicyType GetType()  |  获取策略类型。
 public std::string GetName()  |  获取策略名称。
 public std::string GetDescription()  |  获取策略说明。
public std::shared_ptr<TemplateDescriptor> GetTemplateDescriptor()  |  获取基于模板的 [UserPolicy](class_mip_userpolicy.md) 的 [TemplateDescriptor](class_mip_templatedescriptor.md)。
public std::shared_ptr<PolicyDescriptor> GetPolicyDescriptor()  |  获取临时 [UserPolicy](class_mip_userpolicy.md) 的 [PolicyDescriptor](class_mip_policydescriptor.md)。
 public std::string GetOwner()  |  获取内容所有者的电子邮件地址。
 public std::string GetIssuedTo()  |  获取与保护策略关联的用户。
 public bool IsIssuedToOwner()  |  获取当前用户是否为内容所有者的指示。
 public std::string GetContentId()  |  获取文档/内容的唯一标识符。
 public const mip::AppDataHashMap GetEncryptedAppData()  |  获取已加密的应用特定数据。
 public const mip::AppDataHashMap GetSignedAppData()  |  获取已签名的应用特定数据。
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil()  |  获取策略过期时间。
 public bool DoesUseDeprecatedAlgorithms()  |  获取策略是否使用已弃用的向后兼容性加密算法 (ECB) 的指示。
 public bool IsAuditedExtractAllowed()  |  获取策略是否授予用户“审核提取”权限的指示。
public const std::vector<unsigned char> GetSerializedPolicy()  |  将 [UserPolicy](class_mip_userpolicy.md) 序列化为发布许可证 (PL)
public std::shared_ptr<rmscore::core::ProtectionPolicy> GetImpl()  |  获取 [UserPolicy](class_mip_userpolicy.md) 的内部派生类实现。
  
## <a name="members"></a>成員
  
### <a name="accesscheck"></a>AccessCheck
检查策略是否授予用户对指定权限的访问权限。

参数：  
* **right**：检查权限



  
**返回结果**：策略是否授予用户对指定权限的访问权限
  
### <a name="userpolicytype"></a>UserPolicyType
获取策略类型。

  
**返回结果**：策略类型
  
### <a name="getname"></a>GetName
获取策略名称。

  
**返回结果**：策略名称
  
### <a name="getdescription"></a>GetDescription
获取策略说明。

  
**返回结果**：策略说明
  
### <a name="templatedescriptor"></a>TemplateDescriptor
获取基于模板的 [UserPolicy](class_mip_userpolicy.md) 的 [TemplateDescriptor](class_mip_templatedescriptor.md)。

  
**返回结果**：如果 [UserPolicy](class_mip_userpolicy.md) 基于模板，则返回 [TemplateDescriptor](class_mip_templatedescriptor.md)，否则返回 nullptr
  
### <a name="policydescriptor"></a>PolicyDescriptor
获取临时 [UserPolicy](class_mip_userpolicy.md) 的 [PolicyDescriptor](class_mip_policydescriptor.md)。

  
**返回结果**：如果 [UserPolicy](class_mip_userpolicy.md) 是临时策略，则返回 [PolicyDescriptor](class_mip_policydescriptor.md)，否则返回 nullptr
  
### <a name="getowner"></a>GetOwner
获取内容所有者的电子邮件地址。

  
**返回结果**：内容所有者的电子邮件地址
  
### <a name="getissuedto"></a>GetIssuedTo
获取与保护策略关联的用户。

  
**返回结果**：与保护策略关联的用户
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
获取当前用户是否为内容所有者的指示。

  
**返回结果**：当前用户是否为内容所有者
  
### <a name="getcontentid"></a>GetContentId
获取文档/内容的唯一标识符。

  
**返回结果**：唯一内容标识符
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
获取已加密的应用特定数据。
[UserPolicy](class_mip_userpolicy.md) 可能包含已由 RMS 服务进行加密的应用特定数据的字典。 此加密数据独立于可通过 [UserPolicy::GetSignedAppData](class_mip_userpolicy.md#getsignedappdata) 访问的签名数据
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
获取已签名的应用特定数据。
[UserPolicy](class_mip_userpolicy.md) 可能包含已由 RMS 服务签署的应用特定数据的字典。 此签名数据独立于可通过 [UserPolicy::GetEncryptedAppData](class_mip_userpolicy.md#getencryptedappdata) 访问的加密数据
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
获取策略过期时间。

  
**返回结果**：策略过期时间
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
获取策略是否使用已弃用的向后兼容性加密算法 (ECB) 的指示。

  
**返回结果**：策略是否使用已弃用的加密算法
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
获取策略是否授予用户“审核提取”权限的指示。

  
**返回结果**：策略是否授予用户“审核提取”权限
  
### <a name="getserializedpolicy"></a>GetSerializedPolicy
将 [UserPolicy](class_mip_userpolicy.md) 序列化为发布许可证 (PL)

  
**返回结果**：序列化的 [UserPolicy](class_mip_userpolicy.md)
  
### <a name="getimpl"></a>GetImpl
获取 [UserPolicy](class_mip_userpolicy.md) 的内部派生类实现。

  
**返回结果**：[UserPolicy](class_mip_userpolicy.md) 的派生类实现。仅限内部使用