# <a name="class-mipprotectiondescriptor"></a>类 mip::ProtectionDescriptor 
表示与受保护的内容关联的临时策略。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public ProtectionType GetProtectionType() const  |  获取保护类型，无论是否源自保护 SDK 模板。
 public const std::string& GetName() const  |  获取策略名称。
 public const std::string& GetDescription() const  |  获取策略说明。
 public const std::string& GetTemplateId() const  |  获取保护模板 ID。
public const std::vector<UserRights>& GetUserRights() const  |  获取用户到权限映射的集合。
public const std::vector<UserRoles>& GetUserRoles() const  |  获取用户到角色映射的集合。
public const std::chrono::time_point<std::chrono::system_clock>& GetContentValidUntil() const  |  获取策略过期时间。
 public bool DoesAllowOfflineAccess() const  |  获取策略是否允许离线访问内容。
 public const std::string& GetReferrer() const  |  获取策略引用网址。
public const std::map<std::string, std::string>& GetEncryptedAppData() const  |  获取已加密的应用特定数据。
public const std::map<std::string, std::string>& GetSignedAppData() const  |  获取已签名的应用特定数据。
  
## <a name="members"></a>成員
  
### <a name="protectiontype"></a>ProtectionType
获取保护类型，无论是否源自保护 SDK 模板。

  
**返回结果**：保护类型
  
### <a name="getname"></a>GetName
获取策略名称。

  
**返回结果**：策略名称
  
### <a name="getdescription"></a>GetDescription
获取策略说明。

  
**返回结果**：策略说明
  
### <a name="gettemplateid"></a>GetTemplateId
获取保护模板 ID。

  
**返回结果**：模板 ID
  
### <a name="userrights"></a>UserRights
获取用户到权限映射的集合。

  
**返回结果**：用户映射到权限的集合。如果当前用户无权访问用户权限信息（即不是所有者，没有 VIEWRIGHTSDATA 权限），[UserRights](class_mip_userrights.md) 属性值为空。
  
### <a name="userroles"></a>UserRoles
获取用户到角色映射的集合。

  
**返回结果**：用户到角色映射的集合
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
获取策略过期时间。

  
**返回结果**：策略过期时间
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
获取策略是否允许离线访问内容。

  
**返回结果**：策略是否允许离线访问内容（默认值 = true）
  
### <a name="getreferrer"></a>GetReferrer
获取策略引用网址。

  
**返回结果**：策略引用网址：该引用网站是一个 URI，它会在获取策略失败时显示给用户，其中包含有关用户如何获取内容访问权限的信息。
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
获取已加密的应用特定数据。

  
**返回结果**：应用专用数据。[ProtectionHandler](class_mip_protectionhandler.md) 可能包含保护服务加密的应用专用数据的字典。此加密数据与可通过 [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata) 访问的签名数据无关
  
### <a name="getsignedappdata"></a>GetSignedAppData
获取已签名的应用特定数据。

  
**返回结果**：应用专用数据。[ProtectionHandler](class_mip_protectionhandler.md) 可能包含保护服务签名的应用专用数据的字典。 此签名数据与可通过 [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata) 访问的加密数据无关