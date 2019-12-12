---
title: class mip::UserRights
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： userrights 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 1df26089f37b1e89be8749aa1bc862f0d3a729ba
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558396"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
一组用户以及与之关联的权限。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public UserRights （const std：： vector\<std：： string\>& users，const std：： vector\<std：： string\>& 权限）  |  UserRights 构造函数。
public const std：： vector\<std：： string\>& Users （） const  |  获取与一组权限关联的用户。
public const std：： vector\<std：： string\>& 权限（） const  |  获取与一组用户关联的权限。
  
## <a name="members"></a>成員
  
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