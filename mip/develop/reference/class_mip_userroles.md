---
title: class mip::UserRoles
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： userroles 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e77ed6ae4d4b5467964f855a081cc22780d9869c
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560465"
---
# <a name="class-mipuserroles"></a>class mip::UserRoles 
一组用户以及与之关联的角色。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public UserRoles （const std：： vector\<std：： string\>& users，const std：： vector\<std：： string\>& role）  |  UserRoles 构造函数。
public const std：： vector\<std：： string\>& Users （） const  |  获取与一组角色关联的用户。
public const std：： vector\<std：： string\>& Role （） const  |  获取与一组用户关联的角色。
  
## <a name="members"></a>成員
  
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