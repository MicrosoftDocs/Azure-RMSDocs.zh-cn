---
title: class mip::UserRights
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: userrights 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: c26c7d1aa31cf8fb2ea562582a2ebaad8417615d
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884974"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
一组用户以及与之关联的权限。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public UserRights (const std:: vector\<std:: string\>& users, const std:: vector\<std:: string\>& 权限)  |  [UserRights](class_mip_userrights.md) 构造函数。
public const std:: vector\<std:: string\>& Users () const  |  获取与一组权限关联的用户。
public const std:: vector\<std:: string\>& 权限 () const  |  获取与一组用户关联的权限。
  
## <a name="members"></a>成员
  
### <a name="userrights-function"></a>UserRights 函数
[UserRights](class_mip_userrights.md) 构造函数。

参数：  
* **用户**:共享相同权限的用户组 


* **权限**:用户组共享的权限


  
### <a name="users-function"></a>用户函数
获取与一组权限关联的用户。

  
**返回**:与一组权限关联的用户
  
### <a name="rights-function"></a>权限函数
获取与一组用户关联的权限。

  
**返回**:与一组用户关联的权限