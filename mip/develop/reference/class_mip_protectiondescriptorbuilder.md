# <a name="class-mipprotectiondescriptorbuilder"></a>类 mip::ProtectionDescriptorBuilder 
表示与受保护的内容关联的临时策略。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr<ProtectionDescriptor> Build()  |  创建 [ProtectionDescriptor](class_mip_protectiondescriptor.md)，它的访问权限由此 [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) 实例定义。
 public void SetName(const std::string& value)  |  设置保护策略名称。
 public void SetDescription(const std::string& value)  |  设置保护策略说明。
public void SetContentValidUntil(const std::chrono::time_point<std::chrono::system_clock>& value)  |  设置保护策略到期时间。
 public void SetAllowOfflineAccess(bool value)  |  设置保护策略是否允许脱机访问内容。
 public void SetReferrer(const std::string& uri)  |  设置保护策略引荐来源网址。
public void SetEncryptedAppData(const std::map<std::string, std::string>& value)  |  设置应加密的应用特定数据。
public void SetSignedAppData(const std::map<std::string, std::string>& value)  |  设置应签名的应用特定数据。
 public virtual ~ProtectionDescriptorBuilder()  | _尚无记录。_
  
## <a name="members"></a>成員
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
创建 [ProtectionDescriptor](class_mip_protectiondescriptor.md)，它的访问权限由此 [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) 实例定义。

  
**返回结果**：新 [ProtectionDescriptor](class_mip_protectiondescriptor.md) 实例
  
### <a name="setname"></a>SetName
设置保护策略名称。

参数：  
* **value**：保护策略名称


  
### <a name="setdescription"></a>SetDescription
设置保护策略说明。

参数：  
* **value**：策略说明


  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
设置保护策略到期时间。

参数：  
* **value**：策略过期时间


  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
设置保护策略是否允许脱机访问内容。

参数：  
* **value**：策略是否允许离线访问内容


  
### <a name="setreferrer"></a>SetReferrer
设置保护策略引荐来源网址。

参数：  
* **uri**：策略引用网址


引荐来源网址是向无法获取保护策略的用户显示的 URI，其中介绍了用户如何才能获取内容访问权限。
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
设置应加密的应用特定数据。

参数：  
* **value**：应用特定数据


应用程序可以指定保护服务加密的应用专用数据的字典。 此加密数据与 SetSignedAppData 设置的签名数据无关。
  
### <a name="setsignedappdata"></a>SetSignedAppData
设置应签名的应用特定数据。

参数：  
* **value**：应用特定数据


应用程序可以指定保护服务签名的应用专用数据的字典。 此签名数据与 SetEncryptedAppData 设置的加密数据无关。
  
### <a name="protectiondescriptorbuilder"></a>~ProtectionDescriptorBuilder
_尚无记录。_
