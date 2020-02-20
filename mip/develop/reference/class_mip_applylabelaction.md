---
title: class mip::ApplyLabelAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： applylabelaction 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e1551adddec611c6f9a0982c5a267fad39c436c4
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490670"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
应用标签操作要求，必须调用应用程序，才能应用特定标签。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： shared_ptr\<Label\>& GetLabel （） const  |  获取所需的标签。
public const std：： vector\<std：： string\>& GetClassificationIds （） const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>Members
  
### <a name="getlabel-function"></a>GetLabel 函数
获取所需的标签。

  
**返回**：标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**： Const std：： vector < std：： string > & 导致此标签出现的分类 id 的列表。