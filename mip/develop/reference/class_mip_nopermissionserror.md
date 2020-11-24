---
title: 类 NoPermissionsError
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 nopermissionserror：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: aaa26e640c59ffaf80bec182042b86a7b8e90d3f
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565067"
---
# <a name="class-nopermissionserror"></a>类 NoPermissionsError 
用户无法访问内容。 例如，无权限、内容已撤销。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetReferrer() const  |  在缺少文档权限的情况下获取联系人。
public std::string GetOwner() const  |  获取文档的所有者。
  
## <a name="members"></a>成员
  
### <a name="getreferrer-function"></a>GetReferrer 函数
在缺少文档权限的情况下获取联系人。

  
**返回**：在文档缺少权限的情况下的联系人。
  
### <a name="getowner-function"></a>GetOwner 函数
获取文档的所有者。

  
**返回**：文档所有者