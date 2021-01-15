---
title: 类 NoPermissionsError
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 nopermissionserror：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 0e9c13e1609b6ea5fa2033d5d27c47d76a1acb43
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213566"
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