# <a name="class-mipuserroles"></a>class mip::UserRoles 
表示一组用户以及与之关联的角色。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public UserRoles(const std::vector<std::string>& users, const std::vector<std::string>& roles)  |  [UserRoles](class_mip_userroles.md) 构造函数。
public const std::vector<std::string>& Users() const  |  获取与一组角色关联的用户。
public const std::vector<std::string>& Roles() const  |  获取与一组用户关联的角色。
  
## <a name="members"></a>成員
  
### <a name="userroles"></a>UserRoles
[UserRoles](class_mip_userroles.md) 构造函数。

参数：  
* **users**：共享相同角色的用户组 


* **roles**：用户组共同拥有的角色


  
### <a name="users"></a>Users
获取与一组角色关联的用户。

  
**返回结果**：与一组角色关联的用户
  
### <a name="roles"></a>角色
获取与一组用户关联的角色。

  
**返回结果**：与一组用户关联的角色