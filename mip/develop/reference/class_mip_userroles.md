---
title: class mip::UserRoles
description: 记录 mip::userroles 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 45b2b5170fac04364af1a0418da5d6e1f5e488a3
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56260045"
---
# <a name="class-mipuserroles"></a>class mip::UserRoles 
一组用户以及与之关联的角色。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共 UserRoles (const std:: vector\<std:: string\>& users，const std:: vector\<std:: string\>（& a) 角色)  |  [UserRoles](class_mip_userroles.md) 构造函数。
public const std:: vector\<std:: string\>& Users() 常量  |  获取与一组角色关联的用户。
public const std:: vector\<std:: string\>& Roles() 常量  |  获取与一组用户关联的角色。
  
## <a name="members"></a>成員
  
### <a name="userroles-function"></a>UserRoles 函数
[UserRoles](class_mip_userroles.md) 构造函数。

参数：  
* **用户**:共享相同角色的用户组 


* **角色**:由用户组共享的角色


  
### <a name="users-function"></a>用户函数
获取与一组角色关联的用户。

  
**返回**:与一组角色关联的用户
  
### <a name="roles-function"></a>角色函数
获取与一组用户关联的角色。

  
**返回**:与一组用户关联的角色
