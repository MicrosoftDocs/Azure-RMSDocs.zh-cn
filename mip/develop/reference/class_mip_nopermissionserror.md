---
title: 类 mip：： NoPermissionsError
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： nopermissionserror 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d5067dfcac8ad66464df061d6d043ae343d967cf
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487644"
---
# <a name="class-mipnopermissionserror"></a>类 mip：： NoPermissionsError 
用户无法访问内容。 例如，无权限、内容已撤销。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetReferrer() const  |  在缺少文档权限的情况下获取联系人。
public std::string GetOwner() const  |  获取文档的所有者。
  
## <a name="members"></a>Members
  
### <a name="getreferrer-function"></a>GetReferrer 函数
在缺少文档权限的情况下获取联系人。

  
**返回**：在文档缺少权限的情况下的联系人。
  
### <a name="getowner-function"></a>GetOwner 函数
获取文档的所有者。

  
**返回**：文档所有者