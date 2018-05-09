# <a name="class-mippolicydescriptor"></a>class mip::PolicyDescriptor 
表示与受保护的内容关联的临时策略。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const std::string& GetName()  |  获取策略名称。
public void SetName(const std::string& value)  |  设置策略名称。
public const std::string& GetDescription()  |  获取策略说明。
public void SetDescription(const std::string& value)  |  设置策略说明。
public const std::vector<UserRights>& GetUserRightsList() const  |  获取用户到权限映射的集合。
public const std::vector<mip::UserRoles>& GetUserRolesList()  |  获取用户到角色映射的集合。
public const std::chrono::time_point<std::chrono::system_clock>& GetContentValidUntil()  |  获取策略过期时间。
public void SetContentValidUntil(const std::chrono::time_point<std::chrono::system_clock>& value)  |  设置策略过期时间。
public bool DoesAllowOfflineAccess()  |  获取策略是否允许离线访问内容。
public void SetAllowOfflineAccess(bool value)  |  设置策略是否允许离线访问内容。
public const std::string& GetReferrer() const  |  获取策略引用网址。
public void SetReferrer(const std::string& uri)  |  设置策略引用网址。
public const AppDataHashMap& GetEncryptedAppData()  |  获取已加密的应用特定数据。
public void SetEncryptedAppData(const AppDataHashMap& value)  |  设置应加密的应用特定数据。
public const AppDataHashMap& GetSignedAppData()  |  获取已签名的应用特定数据。
public void SetSignedAppData(const AppDataHashMap& value)  |  设置应签名的应用特定数据。
  
## <a name="members"></a>成員
  
### <a name="getname"></a>GetName
获取策略名称。
  
#### <a name="returns"></a>Returns
策略名称
  
### <a name="setname"></a>SetName
设置策略名称。
  
#### <a name="parameters"></a>参数
* value：策略名称
  
### <a name="getdescription"></a>GetDescription
获取策略说明。
  
#### <a name="returns"></a>Returns
策略说明
  
### <a name="setdescription"></a>SetDescription
设置策略说明。
  
#### <a name="parameters"></a>参数
* value：策略说明
  
### <a name="userrights"></a>UserRights
获取用户到权限映射的集合。
  
#### <a name="returns"></a>Returns
用户到权限映射集合：如果当前用户无权访问用户权限信息（即不是所有者，且没有 VIEWRIGHTSDATA 权限），UserRightsList 属性值将为空。
  
### <a name="mipuserroles"></a>mip::UserRoles
获取用户到角色映射的集合。
  
#### <a name="returns"></a>Returns
用户到角色映射的集合
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
获取策略过期时间。
  
#### <a name="returns"></a>Returns
策略过期时间
  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
设置策略过期时间。
  
#### <a name="parameters"></a>参数
* value：策略过期时间
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
获取策略是否允许离线访问内容。
  
#### <a name="returns"></a>Returns
策略是否允许离线访问内容（默认值 = true）
  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
设置策略是否允许离线访问内容。
  
#### <a name="parameters"></a>参数
* value：策略是否允许离线访问内容
  
### <a name="getreferrer"></a>GetReferrer
获取策略引用网址。
  
#### <a name="returns"></a>Returns
策略引用网址：该引用网站是一个 URI，它会在获取策略失败时显示给用户，其中包含有关用户如何获取访问内容权限的信息。
  
### <a name="setreferrer"></a>SetReferrer
设置策略引用网址。
  
#### <a name="parameters"></a>参数
* uri Policy referrer address：该引用网站是一个 URI，它会在获取策略失败时显示给用户，其中包含有关用户如何获取访问内容权限的信息。
  
### <a name="appdatahashmap"></a>AppDataHashMap
获取已加密的应用特定数据。
  
#### <a name="returns"></a>Returns
应用特定数据：[UserPolicy](#classmip_1_1_user_policy) 可能包含已由 RMS 服务进行加密的应用特定数据的字典。 此加密数据独立于可通过 [PolicyDescriptor::GetSignedAppData](#classmip_1_1_policy_descriptor_1ad523870efc92f9f81c82121a054d74d4) 访问的签名数据
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
设置应加密的应用特定数据。
  
#### <a name="parameters"></a>参数
* value App-specific data：应用程序可以指定将由 RMS 服务进行加密的应用特定数据的字典。 此加密数据独立于通过 [PolicyDescriptor::SetSignedAppData](#classmip_1_1_policy_descriptor_1a00f35c0b91e48ccdcc6387466a61f362) 设置的签名数据。
  
### <a name="appdatahashmap"></a>AppDataHashMap
获取已签名的应用特定数据。
  
#### <a name="returns"></a>Returns
应用特定数据：[UserPolicy](#classmip_1_1_user_policy) 可能包含已由 RMS 服务签署的应用特定数据的字典。 此签名数据独立于可通过 [PolicyDescriptor::GetEncryptedAppData](#classmip_1_1_policy_descriptor_1a9a5bcf9d1bf7357de549429179197ab6) 访问的加密数据
  
### <a name="setsignedappdata"></a>SetSignedAppData
设置应签名的应用特定数据。
  
#### <a name="parameters"></a>参数
* value App-specific data：应用程序可以指定将由 RMS 服务签署的应用特定数据的字典。 此签名数据独立于通过 [PolicyDescriptor::SetEncryptedAppData](#classmip_1_1_policy_descriptor_1a5275224932dc17319092304497e59eb2) 设置的加密数据。