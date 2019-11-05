---
title: 结构 mip：： ApplicationInfo
description: 与 Microsoft 信息保护（MIP） SDK 关联的文档结构。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6bee61bc72de35aeaefd9ef1e7639450392b70a7
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567419"
---
# <a name="struct-mipapplicationinfo"></a>结构 mip：： ApplicationInfo 
包含应用程序特定信息的结构。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  AAD 门户中设置的应用程序标识符（应为不带方括号的 GUID）。
public std::string applicationName  |  应用程序名称（应仅包含有效 ASCII 字符，不包括 ";"）
public std::string applicationVersion  |  所使用的应用程序的版本（应只包含有效的 ASCII 字符，不包括 ";"）
  
## <a name="members"></a>成員
  
### <a name="applicationid-struct-member"></a>applicationId struct 成员
AAD 门户中设置的应用程序标识符（应为不带方括号的 GUID）。
  
### <a name="applicationname-struct-member"></a>applicationName 结构成员
应用程序名称（应仅包含有效 ASCII 字符，不包括 ";"）
  
### <a name="applicationversion-struct-member"></a>applicationVersion 结构成员
所使用的应用程序的版本（应只包含有效的 ASCII 字符，不包括 ";"）