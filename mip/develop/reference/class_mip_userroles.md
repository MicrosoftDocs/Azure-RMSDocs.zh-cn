---
title: class mip::UserRoles
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： userroles 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d22f66c8fff22b54e5e7e30f425adc2c889e5db0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489276"
---
# <a name="class-mipuserroles"></a>class mip::UserRoles 
一组用户以及与之关联的角色。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public UserRoles （const std：： vector\<std：： string\>& users，const std：： vector\<std：： string\>& role）  |  UserRoles 构造函数。
public const std：： vector\<std：： string\>& Users （） const  |  获取与一组角色关联的用户。
public const std：： vector\<std：： string\>& Role （） const  |  获取与一组用户关联的角色。
  
## <a name="members"></a>Members
  
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