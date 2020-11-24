---
title: 结构 ApplicationInfo
description: 与 Microsoft 信息保护 (MIP) SDK 关联的文档结构。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 4971d7cf0891308733dafd0dc64d58c02343f1e4
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565015"
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