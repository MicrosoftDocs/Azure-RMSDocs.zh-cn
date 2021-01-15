---
title: 类 UserRights
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 userrights：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 13c9da9ef9cd8b5e1c9c42f48b7f249f69bd7b30
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212801"
---
# <a name="class-userrights"></a>类 UserRights 
一组用户以及与之关联的权限。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public UserRights (const std：： vector \<std::string\>& users，const std：： vector \<std::string\>& 权限)   |  UserRights 构造函数。
public const std：： vector \<std::string\>& 用户 ( # A2 const  |  获取与一组权限关联的用户。
public const std：： vector \<std::string\>& 权限 ( # A2 const  |  获取与一组用户关联的权限。
  
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