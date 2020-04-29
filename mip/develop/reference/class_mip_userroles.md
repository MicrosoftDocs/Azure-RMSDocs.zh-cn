---
title: 类 UserRoles
description: 记录 Microsoft 信息保护（MIP） SDK 的 userroles：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: bbff817578bb5ba1fe143c850632e25df8f78708
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764201"
---
# <a name="class-userroles"></a>类 UserRoles 
一组用户以及与之关联的角色。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public UserRoles （const std：： vector\<std：： string\>& users，const std：： vector\<std：： string\>& role）  |  UserRoles 构造函数。
public const std：： vector\<std：： String\>& Users （） const  |  获取与一组角色关联的用户。
public const std：： vector\<std：： String\>& role （） const  |  获取与一组用户关联的角色。
  
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