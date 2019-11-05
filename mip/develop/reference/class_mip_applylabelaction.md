---
title: class mip::ApplyLabelAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： applylabelaction 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: cb3ff8c247ad4dbcf4d85ba31608b07f3aaceddf
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559042"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
应用标签操作要求，必须调用应用程序，才能应用特定标签。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： shared_ptr\<标签\>& GetLabel （） const  |  获取所需的标签。
public const std：： vector\<std：： string\>& GetClassificationIds （） const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>成員
  
### <a name="getlabel-function"></a>GetLabel 函数
获取所需的标签。

  
**返回**：标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**： Const std：： vector < std：： string > & 导致此标签出现的分类 id 的列表。