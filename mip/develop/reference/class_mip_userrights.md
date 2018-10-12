---
title: class mip UserRights
description: class mip UserRights 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c1ef7aaba00bf595d80f07f318aa5808f3a56409
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445115"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
一组用户和与之关联的权限。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public UserRights(const std::vector<std::string>& users, const std::vector<std::string>& rights)  |  [UserRights](class_mip_userrights.md) 构造函数。
public const std::vector<std::string>& Users() const  |  获取与一组权限关联的用户。
public const std::vector<std::string>& Rights() const  |  获取与一组用户关联的权限。
  
## <a name="members"></a>成員
  
### <a name="userrights"></a>UserRights
[UserRights](class_mip_userrights.md) 构造函数。

参数：  
* **users**：共享相同权限的用户组 


* **rights**：由用户组共享的权限


  
### <a name="users"></a>Users
获取与一组权限关联的用户。

  
**返回结果**：与一组权限关联的用户
  
### <a name="rights"></a>权限
获取与一组用户关联的权限。

  
**返回结果**：与一组用户关联的权限