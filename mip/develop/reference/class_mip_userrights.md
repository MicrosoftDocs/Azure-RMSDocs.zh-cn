---
title: class mip::UserRights
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： userrights 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f44ff30c890a5a8ab3dbce2426a6c1898df1f0e5
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489293"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
一组用户和与之关联的权限。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public UserRights （const std：： vector\<std：： string\>& users，const std：： vector\<std：： string\>& 权限）  |  UserRights 构造函数。
public const std：： vector\<std：： string\>& Users （） const  |  获取与一组权限关联的用户。
public const std：： vector\<std：： string\>& 权限（） const  |  获取与一组用户关联的权限。
  
## <a name="members"></a>Members
  
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