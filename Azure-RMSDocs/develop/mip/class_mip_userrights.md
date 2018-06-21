# <a name="class-mipuserrights"></a>class mip::UserRights 
表示一组用户和与之关联的权限。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public UserRights(const UserList& users, const RightList& rights)  |  [UserRights](class_mip_userrights.md) 构造函数。
 public const UserList& Users() const  |  获取与一组权限关联的用户。
 public const RightList& Rights() const  |  获取与一组用户关联的权限。
  
## <a name="members"></a>成員
  
### <a name="userrights"></a>UserRights
[UserRights](class_mip_userrights.md) 构造函数。

参数：  
* **users**：共享相同权限的用户组 


* **rights**：由用户组共享的权限


  
### <a name="userlist"></a>UserList
获取与一组权限关联的用户。

  
**返回结果**：与一组权限关联的用户
  
### <a name="rightlist"></a>RightList
获取与一组用户关联的权限。

  
**返回结果**：与一组用户关联的权限