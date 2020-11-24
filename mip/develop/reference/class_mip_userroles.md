---
title: 类 UserRoles
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 userroles：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: fc6e5f77c68ecde2582cfd622624c0c6b986500b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565038"
---
# <a name="class-userroles"></a>类 UserRoles 
一组用户以及与之关联的角色。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public UserRoles (const std：： vector \<std::string\>& users，const std：： vector \<std::string\>& role)   |  UserRoles 构造函数。
public const std：： vector \<std::string\>& 用户 ( # A2 const  |  获取与一组角色关联的用户。
public const std：： vector \<std::string\>& role ( # A2 const  |  获取与一组用户关联的角色。
  
## <a name="members"></a>成员
  
### <a name="userroles-function"></a>UserRoles 函数
UserRoles 构造函数。

参数：  
* **users**：共享相同角色的用户组 


* **roles**：用户组共同拥有的角色


  
### <a name="users-function"></a>用户函数
获取与一组角色关联的用户。

  
**返回结果**：与一组角色关联的用户
  
### <a name="roles-function"></a>Role 函数
获取与一组用户关联的角色。

  
**返回结果**：与一组用户关联的角色