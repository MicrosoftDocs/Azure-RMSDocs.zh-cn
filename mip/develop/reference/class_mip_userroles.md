---
title: class mip::UserRoles
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: userroles 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: cda40d4b3a118ff065dc2e3899b39cf8f405dd68
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056699"
---
# <a name="class-mipuserroles"></a>class mip::UserRoles 
一组用户以及与之关联的角色。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: vector\<std:: string\>& users, const std:: vector\<std:: string\>& role)  |  [UserRoles](class_mip_userroles.md) 构造函数。
public const std:: vector\<std:: string\>& Users () const  |  获取与一组角色关联的用户。
public const std:: vector\<std:: string\>& role () const  |  获取与一组用户关联的角色。
  
## <a name="members"></a>成员
  
### <a name="userroles-function"></a>UserRoles 函数
[UserRoles](class_mip_userroles.md) 构造函数。

参数：  
* **用户**:共享相同角色的用户组 


* **角色**:用户组共享的角色


  
### <a name="users-function"></a>用户函数
获取与一组角色关联的用户。

  
**返回**:与一组角色关联的用户
  
### <a name="roles-function"></a>Role 函数
获取与一组用户关联的角色。

  
**返回**:与一组用户关联的角色