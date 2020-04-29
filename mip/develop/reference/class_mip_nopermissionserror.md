---
title: 类 NoPermissionsError
description: 记录 Microsoft 信息保护（MIP） SDK 的 nopermissionserror：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 18c3c66fe10ce9291a936a3e754923d36f3d1df0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761411"
---
# <a name="class-nopermissionserror"></a>类 NoPermissionsError 
用户无法访问内容。 例如，无权限、内容已撤销。
  
## <a name="summary"></a>“摘要”
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