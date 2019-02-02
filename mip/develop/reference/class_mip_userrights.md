---
title: class mip::UserRights
description: 记录 mip::userrights 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 3e3abd2045b0e66ee8c2b307d555bf860e489625
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650606"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
一组用户以及与之关联的权限。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共 UserRights (const std:: vector\<std:: string\>& users，const std:: vector\<std:: string\>& rights)  |  [UserRights](class_mip_userrights.md) 构造函数。
public const std:: vector\<std:: string\>& Users() 常量  |  获取与一组权限关联的用户。
public const std:: vector\<std:: string\>& Rights() 常量  |  获取与一组用户关联的权限。
  
## <a name="members"></a>成員
  
### <a name="userrights-function"></a>UserRights 函数
[UserRights](class_mip_userrights.md) 构造函数。

参数：  
* **用户**:共享相同的权限的用户组 


* **权限**:由用户组共享的权限


  
### <a name="users-function"></a>用户函数
获取与一组权限关联的用户。

  
**返回**:与一组权限关联的用户
  
### <a name="rights-function"></a>权限函数
获取与一组用户关联的权限。

  
**返回**:与一组用户关联的权限