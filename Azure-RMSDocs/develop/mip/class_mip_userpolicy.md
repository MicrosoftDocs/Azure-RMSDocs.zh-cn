# <a name="class-mipuserpolicy"></a>class mip::UserPolicy 
表示与受保护的内容关联的策略。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public bool AccessCheck | 检查策略是否授予用户对指定权限的访问权限。
public UserPolicyType GetType | 获取策略类型。
public std::string GetName | 获取策略名称。
public std::string GetDescription | 获取策略说明。
public std::shared_ptr< TemplateDescriptor > GetTemplateDescriptor public std::shared_ptr< PolicyDescriptor > GetPolicyDescriptor public std::string GetOwner | 获取内容所有者的电子邮件地址。
public std::string GetIssuedTo | 获取与保护策略关联的用户。
public bool IsIssuedToOwner | 获取当前用户是否为内容所有者的指示。
public std::string GetContentId | 获取文档/内容的唯一标识符。
public const mip::AppDataHashMap GetEncryptedAppData | 获取已加密的应用特定数据。
public const mip::AppDataHashMap GetSignedAppData | 获取已签名的应用特定数据。
public std::chrono::time_point< std::chrono::system_clock > GetContentValidUntil | 获取策略过期时间。
public bool DoesUseDeprecatedAlgorithms | 获取策略是否使用已弃用的向后兼容性加密算法 (ECB) 的指示。
public bool IsAuditedExtractAllowed | 获取策略是否授予用户“审核提取”权限的指示。
public const std::vector< unsigned char > GetSerializedPolicy public std::shared_ptr< rmscore::core::ProtectionPolicy > GetImpl
## <a name="members"></a>成員
### <a name="accesscheck"></a>AccessCheck
检查策略是否授予用户对指定权限的访问权限。
#### <a name="parameters"></a>参数
* right：检查权限
#### <a name="returns"></a>Returns
策略是否授予用户对指定权限的访问权限
### <a name="userpolicytype"></a>UserPolicyType
获取策略类型。
#### <a name="returns"></a>Returns
策略类型
### <a name="getname"></a>GetName
获取策略名称。
#### <a name="returns"></a>Returns
策略名称
### <a name="getdescription"></a>GetDescription
获取策略说明。
#### <a name="returns"></a>Returns
策略说明
### <a name="templatedescriptor"></a>TemplateDescriptor
获取基于模板的 [UserPolicy](#classmip_1_1_user_policy) 的 [TemplateDescriptor](#classmip_1_1_template_descriptor)。
#### <a name="returns"></a>Returns
如果 [UserPolicy](#classmip_1_1_user_policy) 基于模板，则返回 [TemplateDescriptor](#classmip_1_1_template_descriptor)，否则返回 nullptr
### <a name="policydescriptor"></a>PolicyDescriptor
获取临时 [UserPolicy](#classmip_1_1_user_policy) 的 [PolicyDescriptor](#classmip_1_1_policy_descriptor)。
#### <a name="returns"></a>Returns
如果 [UserPolicy](#classmip_1_1_user_policy) 是临时策略，则返回 [PolicyDescriptor](#classmip_1_1_policy_descriptor)，否则返回 nullptr
### <a name="getowner"></a>GetOwner
获取内容所有者的电子邮件地址。
#### <a name="returns"></a>Returns
内容所有者的电子邮件地址
### <a name="getissuedto"></a>GetIssuedTo
获取与保护策略关联的用户。
#### <a name="returns"></a>Returns
与保护策略关联的用户
### <a name="isissuedtoowner"></a>IsIssuedToOwner
获取当前用户是否为内容所有者的指示。
#### <a name="returns"></a>Returns
当前用户是否为内容所有者
### <a name="getcontentid"></a>GetContentId
获取文档/内容的唯一标识符。
#### <a name="returns"></a>Returns
唯一内容标识符
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
获取已加密的应用特定数据。
[UserPolicy](#classmip_1_1_user_policy) 可能包含已由 RMS 服务进行加密的应用特定数据的字典。 此加密数据独立于可通过 [UserPolicy::GetSignedAppData](#classmip_1_1_user_policy_1a1c8a284d50adcac1a0a09316afa1d43e) 访问的签名数据
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
获取已签名的应用特定数据。
[UserPolicy](#classmip_1_1_user_policy) 可能包含已由 RMS 服务签署的应用特定数据的字典。 此签名数据独立于可通过 [UserPolicy::GetEncryptedAppData](#classmip_1_1_user_policy_1a610fbc799284ab0ce4354c0611ece0e8) 访问的加密数据
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
获取策略过期时间。
#### <a name="returns"></a>Returns
策略过期时间
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
获取策略是否使用已弃用的向后兼容性加密算法 (ECB) 的指示。
#### <a name="returns"></a>Returns
策略是否使用已弃用的加密算法
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
获取策略是否授予用户“审核提取”权限的指示。
#### <a name="returns"></a>Returns
策略是否授予用户“审核提取”权限
### <a name="getserializedpolicy"></a>GetSerializedPolicy
将 [UserPolicy](#classmip_1_1_user_policy) 序列化为发布许可证 (PL)
#### <a name="returns"></a>Returns
序列化的 [UserPolicy](#classmip_1_1_user_policy)
### <a name="getimpl"></a>GetImpl
获取 [UserPolicy](#classmip_1_1_user_policy) 的内部派生类实现。
#### <a name="returns"></a>Returns
仅限内部的 [UserPolicy](#classmip_1_1_user_policy) 的派生类实现