---
title: 类 UserRights
description: 记录 Microsoft 信息保护（MIP） SDK 的 userrights：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 1a3bf2c6c8f417d30fac24263f672f2603347960
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764247"
---
# <a name="class-userrights"></a>类 UserRights 
一组用户以及与之关联的权限。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public UserRights （const std：： vector\<std：： string\>& users，const std：： vector\<std：： string\>& 权限）  |  UserRights 构造函数。
public const std：： vector\<std：： String\>& Users （） const  |  获取与一组权限关联的用户。
public const std：： vector\<std：： String\>& 权限（） const  |  获取与一组用户关联的权限。
  
## <a name="members"></a>成员
  
### <a name="userrights-function"></a>UserRights 函数
UserRights 构造函数。

参数：  
* **users**：共享相同权限的用户组 


* **rights**：由用户组共享的权限


  
### <a name="users-function"></a>用户函数
获取与一组权限关联的用户。

  
**返回结果**：与一组权限关联的用户
  
### <a name="rights-function"></a>权限函数
获取与一组用户关联的权限。

  
**返回结果**：与一组用户关联的权限