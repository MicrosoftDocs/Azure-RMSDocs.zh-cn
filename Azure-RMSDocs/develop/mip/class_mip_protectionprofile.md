# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) 是用于执行保护操作的根类。
应用程序需创建 [ProtectionProfile](class_mip_protectionprofile.md)，然后才能执行所有保护操作
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。
 public void ClearCaches()  |  删除缓存（例如，同意数据库等。）
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
获取由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的设置。

  
**返回结果**：由 [ProtectionProfile](class_mip_protectionprofile.md) 在初始化期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)
  
### <a name="clearcaches"></a>ClearCaches
删除缓存（例如，同意数据库等。）可用于调试/测试