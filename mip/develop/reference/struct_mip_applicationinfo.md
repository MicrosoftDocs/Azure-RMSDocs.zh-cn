---
title: 结构 ApplicationInfo
description: 记录 ApplicationInfo 结构
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d56fdcaccf67f46b2d6632ec6586e2b140717696
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535580"
---
# <a name="struct-applicationinfo"></a>结构 ApplicationInfo 
包含应用程序特定信息的结构。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  在 AAD 门户中设置的应用程序标识符， (应为不带方括号) 的 GUID。
public std::string applicationName  |  应用程序名称、 (应该只包含有效的 ASCII 字符，不包括 ";") 
public std::string applicationVersion  |  所使用的应用程序的版本 (应该只包含有效的 ASCII 字符，不包括 ";") 
  
## <a name="members"></a>成员
  
### <a name="applicationid-struct-member"></a>applicationId struct 成员
在 AAD 门户中设置的应用程序标识符， (应为不带方括号) 的 GUID。
  
### <a name="applicationname-struct-member"></a>applicationName 结构成员
应用程序名称、 (应该只包含有效的 ASCII 字符，不包括 ";") 
  
### <a name="applicationversion-struct-member"></a>applicationVersion 结构成员
所使用的应用程序的版本 (应该只包含有效的 ASCII 字符，不包括 ";") 