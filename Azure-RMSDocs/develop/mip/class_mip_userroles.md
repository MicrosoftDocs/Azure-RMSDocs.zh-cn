# <a name="class-mipuserroles"></a>class mip::UserRoles 
表示一组用户以及与之关联的角色。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public MIP_EXPORT UserRoles(const UserList& users, const RoleList& roles)  |  [UserRoles](#classmip_1_1_user_roles) 构造函数。
public inline const UserList& Users() const  |  获取与一组角色关联的用户。
public inline const RoleList& Roles() const  |  获取与一组用户关联的角色。
  
## <a name="members"></a>成員
  
### <a name="userroles"></a>UserRoles
[UserRoles](#classmip_1_1_user_roles) 构造函数。
  
#### <a name="parameters"></a>参数
* users：共享相同角色的用户组 
* roles：由用户组共享的[角色](#classmip_1_1_roles)
  
### <a name="userlist"></a>UserList
获取与一组角色关联的用户。
  
#### <a name="returns"></a>Returns
与一组角色关联的用户
  
### <a name="rolelist"></a>RoleList
获取与一组用户关联的角色。
  
#### <a name="returns"></a>Returns
与一组用户关联的[角色](#classmip_1_1_roles)